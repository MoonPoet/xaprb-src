---
title: Status versus configuration variables
date: "2012-10-30"
url: /blog/2012/10/30/status-versus-configuration-variables/
categories:
  - Databases
---
MySQL's SHOW STATUS and SHOW VARIABLES commands (or queries against the corresponding `INFORMATION_SCHEMA` tables) don't always show what they say. In particular, SHOW STATUS contains several rows that aren't status-related, but are really configuration variables in my opinion (and it is an opinion---sometimes the difference isn't black and white).

Here's a short list of some status counters that I think are really better off as configuration variables:

*   `Innodb_page_size`
*   `Replica_heartbeat_period`
*   `Ssl_cipher`
*   `Ssl_cipher_list`
*   `Ssl_ctx_verify_depth`
*   `Ssl_ctx_verify_mode`
*   `Ssl_default_timeout`
*   `Ssl_session_cache_mode`
*   `Ssl_verify_depth`
*   `Ssl_verify_mode`
*   `Ssl_version`

Most of those are legacy, but `Replica_heartbeat_period` is a recent addition.

Can you think of others? What are your favorite oddities of SHOW STATUS and SHOW VARIABLES?


