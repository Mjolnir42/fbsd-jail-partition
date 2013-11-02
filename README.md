FreeBSD partitioned jails patch
===============================

Trivial patch for the FreeBSD's `/etc/rc.d/jail` to add support
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
  layer
* you can use `kldstat -q -m mac_partition; echo $?` to check if the
  mac partition module is loaded / compiled into your kernel
* this patch was originally made against FreeBSD 8.3 but should apply
  to newer versions as well with trivial modifications
