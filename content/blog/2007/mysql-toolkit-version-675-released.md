---
title: MySQL Toolkit version 675 released
date: "2007-07-20"
url: /blog/2007/07/20/mysql-toolkit-version-675-released/
categories:
  - Databases
  - Open Source
---

I've just released changes to two of the tools in MySQL Toolkit. MySQL Table Checksum got some convenient functionality to help you recursively check replicas for bad replicated checksum chunks. MySQL Archiver got statistics-gathering functionality to help you optimize your archiving and purging jobs, plus a few important bug fixes.

Changes in MySQL Archiver:

*   Made `--time` suffix optional.
*   Added `--statistics` option to gather and print timing statistics.
*   Added signal handling so mysql-archiver exits cleanly when it can.
*   Changed exit status to 0 when `--help` is given.
*   Out-of-column-order primary keys were not ascended correctly.

Changes in MySQL Table Checksum:

*   Added `--replcheck` option to check `--replicate` results on replicas.
*   Added `--recursecheck` option to do `--replcheck` recursively.


