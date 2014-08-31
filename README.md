FreeBSD partitioned jails patch and more!
=========================================

Trivial patch for FreeBSD's `/etc/rc.d/jail` to add support
for `mac_partition(4)` partitions.

It introduces a new per-jail variable in `rc.conf(5)`, similar
to the `_fib` variable used by `setfib(1)`.

```
/etc/rc.conf:

jail_enable="YES"
jail_list="foobar"
...
jail_foobar_partition="42"
...
```

This will prepend the call to `jail(8)` with `setpmac partition/42`.

Note:
* this does not add any restrictions to the jail that the jail
  system does not already impose on its own. It only adds another
  layer and maybe a warm fuzzy feeling
* since you can not set partitions inside a jail, setting a partition
  for the entire jail is no loss in functionality
* you can use `kldstat -q -m mac_partition; echo $?` to check if the
  mac partition module is loaded / compiled into your kernel
* this patch was originally made against FreeBSD 8.3, it can easily be
  adopted to FreeBSD 9.x if you use the "old" jail configuration style
* FreeBSD 10 jail.conf(5) configuration is not supported. If you know
  a way, let me know

Assorted FreeBSD10 patches
==========================

Various patches against FreeBSD 10.0-RELEASE-p7 to accomplish stuff
can be found in the fbsd10/ directory.
Check to commitlog of the files for descriptions etc.
