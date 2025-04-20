## -O0
```bash
(base) [bogale2@dane7:build]$ llvm-as < /dev/null   | opt -enable-new-pm=0 -O0 -disable-out
put -debug-pass=Arguments
Pass Arguments:  -tti -verify
Pass Arguments:  -targetlibinfo -tti -assumption-cache-tracker -profile-summary-info -annotation2metadata -forceattrs -basiccg -always-inline -barrier -annotation-remarks -verify
```


## -O1
