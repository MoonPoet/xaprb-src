---
title: MySQL Table Checksum 1.1.6 released
date: "2007-06-03"
url: /blog/2007/06/03/mysql-table-checksum-116-released/
categories:
  - Databases
---

MySQL Table Checksum 1.1.6 enhances chunking, adds features and fixes bugs. The chunking functionality is where I continue to put most of my effort. **This release's behavior is incompatible with the last release**, and it will probably change again in the future.

Thanks to everyone who has been helping me chase down bugs, including one user who sent me a major patch! It's a great feeling to get a patch.

### Changes

Incompatible changes:

*   The chunking functionality no longer guarantees chunks will be no larger than the specified size. Use `--chunksize-exact` for that. Note that the chunking functionality is still experimental and likely to change further.

Changes:

*   Chunking now works with multiple-column indexes.
*   Added `--quiet` option, useful for cron jobs with `--replicate.`
*   Added `--float-precision` option; works around different floating-point formats.
*   Added `--sleep-coef` option; sleeps a multiple of the time the last checksum took.
*   Added error handling for tables that are dropped during checksumming.
*   Added documentation on the finer points of `--replicate-do` and `--binlog-do.`

Bugs fixed:

*   There was a race condition between listing and checksumming tables.
*   Perl's auto-vivify hashes could cause all tables to be skipped after the first VIEW.
*   Some DBIs did not consider ? inside a comment to be a placeholder.
*   Systems that return nothing from CHECKSUM TABLE crashed mysql-table-checksum.
*   `--askpass` did not print a newline after reading password.
*   Different TIMESTAMP display formatting could cause spurious checksum differences.
*   Checksumming by chunks did not work when the chunk column contained NULL.
*   `--replicate` did not always work correctly with `binlog_do_db`.

### About MySQL Toolkit

[MySQL Toolkit](http://code.google.com/p/maatkit) is a set of essential tools for MySQL users, developers and administrators. The project's goal is to make high-quality command-line tools that follow the UNIX philosophy of doing one thing and doing it well. They are designed for scriptability and ease of processing with standard command-line utilities such as `awk` and `sed`.


