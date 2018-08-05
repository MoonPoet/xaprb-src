---
title: "ASP.NET's Profile DB schema"
date: "2006-01-08"
url: /blog/2006/01/08/aspnet-profile-schema/
categories:
  - Programming
  - Databases
---
ASP.NET has built-in functionality to store profile information about a user. The DB table schema has several design trade-offs that make it somewhat inflexible for certain uses.

ASP.NET will write a custom class, given the properties you want, such as name and birthdate. It will also take care of hooking the plumbing up in the database (there is a little script to create the profile tables in the database). It then stores and retrieves the data on subsequent requests. The feature can handle both text and binary data, but for simplicity's sake, I'll just ignore the binary. Since the profile could contain arbitrary information, the table has to be designed to accommodate any type of data---essentially name/value pairs. Here's the table schema:

```sql
CREATE TABLE dbo.aspnet_Profile (
    UserId uniqueidentifier NOT NULL PRIMARY KEY CLUSTERED,
    PropertyNames ntext NOT NULL,
    PropertyValuesString ntext NOT NULL,
    PropertyValuesBinary image NOT NULL,
    LastUpdatedDate datetime NOT NULL
)
```

Hmmm, that's an interesting schema. How do you store name/value pairs in that? I'd expect to see a `UserID` column and a `Name` column, with the primary key on `UserID` and `Name`, but it looks like they must be storing the data another way. For one thing, there can't be multiple rows per user---all the values have to be in one row. I could see someone arguing that's a good idea, because it would keep the data all on one page---but the columns are `ntext` and `image` so they're not stored in-page anyway. That results in a compact table, with a small clustered index to seek for the user's row, but then the DB has to seek to other pages and find the data stored in those three columns. So how is the data stored?

```sql
select top 1 UserId, PropertyNames, PropertyValuesString from aspnet_Profile;
```

Results:

| UserId           | PropertyNames                      | PropertyValuesString |
|------------------|------------------------------------|----------------------|
| 017D...[snip]... | User.LName:S:0:5:User.FName:S:5:4: | SmithJohn            |
