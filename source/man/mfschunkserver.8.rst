.. _mfschunkserver.8:

*****************
mfschunkserver(8)
*****************

NAME
====

mfschunkserver - start, restart or stop Lizard File System chunkserver process

SYNOPSIS
========

::

  mfschunkserver* [-f] [-c CFGFILE] [-u] [-d] [-t LOCKTIMEOUT] [-p PIDFILE] [ACTION]

  mfschunkserver -s [-c CFGFILE]

  mfschunkserver -v

  mfschunkserver -h


DESCRIPTION
===========

**mfschunkserver** is the data server of Lizard File System. Depending on
parameters it can start, restart or stop the LizardFS chunkserver process.
Without any options it starts the LizardFS chunkserver, killing previously run
process if lock file exists.

SIGHUP (or *reload* ACTION) forces *mfschunkserver* to reload all
configuration files.

Chunkserver periodically tests stored chunks (see *HDD_TEST_FREQ* option
in *mfschunkserver.cfg* manual).

LizardFS master doesn't send metadata change logs to chunkserver and
expects at least one *mfsmetalogger* daemon to connect.

Chunkserver scans attached disks in background.

OPTIONS
=======

-v
  print version information and exit

-h
  print usage information and exit

-f
  (deprecated, use *start* action instead)
  forcily run LizardFS chunkserver process, without trying to kill previous
  instance (this option allows to run LizardFS chunkserver if stale PID file
  exists)

-s
  (deprecated, use *stop* action instead)
  stop the LizardFS chunkserver process

-c CFGFILE
  specify alternative path of configuration file (default is
  *mfschunkserver.cfg* in system configuration directory)

-u
  log undefined configuration values (when default is assumed)

-d
  run in foreground, don't daemonize

-t LOCKTIMEOUT
  how long to wait for lockfile (default is 60 seconds)

-p PIDFILE
  write pid to given file

ACTION
is one of *start*, *stop*, *restart*, *reload*, *test*, *isalive* or *kill*.
Default action is *restart*.

FILES
=====

mfschunkserver.cfg
  configuration file for LizardFS chunkserver process; refer to
  *mfschunkserver.cfg(5)* manual for details.

mfshdd.cfg
  list of directories (mountpoints) used for LizardFS storage (one per line;
  directory prefixed by **\*** character causes given directory to be freed by
  replicating all data already stored there to another locations)

mfschunkserver.lock
  PID file of running LizardFS chunkserver process

.mfschunkserver.lock
  lock file of running LizardFS chunkserver process
  (created in data directory)

data.csstats
  Chunkserver charts state

REPORTING BUGS
==============

Report bugs to <contact@lizardfs.org>.

COPYRIGHT
=========

Copyright 2008-2009 Gemius SA, 2013-2017 Skytechnology sp. z o.o.

LizardFS is free software: you can redistribute it and/or modify it under the
terms of the GNU General Public License as published by the Free Software
Foundation, version 3.

LizardFS is distributed in the hope that it will be useful, but WITHOUT ANY
WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR
A PARTICULAR PURPOSE. See the GNU General Public License for more details.

You should have received a copy of the GNU General Public License along with
LizardFS. If not, see <http://www.gnu.org/licenses/>.

SEE ALSO
========

mfsmaster(8), mfsmount(1), mfschunkserver.cfg(5), mfshdd.cfg(5), lizardfs(7)
