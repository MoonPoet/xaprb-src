---
title: Maatkit in RHEL and CentOS
date: "2008-05-13"
url: /blog/2008/05/13/maatkit-in-rhel-and-centos/
categories:
  - Databases
  - Open Source
---
**Update:** Karanbir says "Just one thing to keep in mind is that we dont want too many people using it from the Testing repository – we only need enough feedback to move it from testing to stable ( and to be honest, there are already 8 people who have said yes it works – so move to stable should happen within the next 24 – 48 hrs ). Once the package is in stable, users on CentOS4 and 5 wont need to do anything more than just 'yum install maatkit' and it will install for them."

At least one person (Karanbir Singh) is working to get [Maatkit](http://www.maatkit.org/) into the [CentOS](http://www.centos.org/) repositories, and I believe there might be movement towards [RHEL](http://www.redhat.com/rhel/) also. From an email to the Maatkit discussion list a little while ago,

> I am in the process of getting maatkit into the CentOS-Extras repositories. The first step for that is that every package needs to go into a CentOS-Testing repo and feedback is required from the project and users on its stability / usability and packaging quality.  

> maatkit-1887 is now available in the CentOS-Testing[*] repo's and as soon as we can get some feedback ( needs to be 5 different people, none of whom can be CentOS Developers ) – the packages will move into the main repository so that all users can get access.  

> I'd appreciate it if people on this were able to give those packages a go and let me know if there are any issues. You can leave feedback :  

* via the maatkit-discuss mailing list (http://sourceforge.net/mailarchive/forum.php?forum_name=maatkit-discuss)
* on the centos-devel list ( http://lists.centos.org ) or
* http://bugs.centos.org/ against category 'maatkit'
> [*] : Info about the Testing repo and howto set it up on your machine : http://wiki.centos.org/Repositories  

If you're interested in getting Maatkit into these repositories, please take a moment and give the requested feedback. I can't do it because it would be a conflict of interest for the main developer to assert that the code is stable and usable.
