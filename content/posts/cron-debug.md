---
title: "Configure cron with debug logging"
date: 2020-09-15T11:30:03+00:00
# weight: 1
# aliases: ["/first"]
# tags: ["first"]
author: "Me"
# author: ["Me", "You"] # multiple authors
showToc: false
TocOpen: false
draft: false
hidemeta: false
comments: false
summary: If a cron job is failing or more information is needed, how can crond be configured....
---

If a cron job is failing or more information is needed, how can cron be configured
to run in debug mode for more detailed logging?

### Environment

* Red Hat Enterprise Linux

### Resolution

* The `crond` daemon has an `-x` option that allows you to set debug flags.

* `crond -x [ext,sch,proc,pars,load,misc,test,bit]`

~~~
ext   print extended debugging information
sch   scheduling
proc  process control
pars  parsing
load  database loading
misc  miscellaneous
test  test mode - do not actually execute any commands
bit   show how various bits are set (long)
~~~

* Add the following line to the `/etc/sysconfig/crond` file to enable debugging.

~~~
CRONDARGS="-x ext,sch,proc,pars,load,misc,bit"
~~~

* Restart `crond` to make the change active.

**Red Hat Enterprise Linux 6**

~~~
service crond restart > /dev/null 2>&1 &
~~~

**Red Hat Enterprise Linux 7 or later**
~~~
systemctl restart crond
~~~

## Root Cause

Debug flags are not configured by default for the `crond` daemon. They must be configured in order to use them.
