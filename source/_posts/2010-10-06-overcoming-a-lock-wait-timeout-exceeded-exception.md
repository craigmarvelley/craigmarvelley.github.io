---
title: 'Overcoming a &#8216;lock wait timeout exceeded&#8217; exception.'
author: Craig
layout: post
permalink: /2010/10/06/overcoming-a-lock-wait-timeout-exceeded-exception/
categories:
  - MySQL
  - PHP
---
This exception was being thrown by [Doctrine][1] during a long-running process:

` exception 'Doctrine_Connection_Mysql_Exception' with message 'SQLSTATE[HY000]: General error: 1205 Lock wait timeout exceeded; try restarting transaction'<br />
`

The code in question was performing a lot of queries within a transaction &#8211; it seems that innodb will only hold a lock for so long, and this limit was being reached before the transaction could commit and release the lock. The solution (other than refactoring the code to be a little quicker!) was to increase innodb&#8217;s `innodb_lock_wait_timeout` setting in `my.cnf` to accommodate the transaction.

 [1]: http://doctrine-project.org