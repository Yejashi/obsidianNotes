## -O0
```bash
(base) [bogale2@dane7:build]$ llvm-as < /dev/null   | opt -enable-new-pm=0 -O0 -disable-out
put -debug-pass=Arguments
Pass Arguments:  -tti -verify
Pass Arguments:  -targetlibinfo -tti -assumption-cache-tracker -profile-summary-info -annotation2metadata -forceattrs -basiccg -always-inline -barrier -annotation-remarks -verify
```

```bash
(base) [bogale2@dane7:build]$ opt -O0 -disable-output -print-pipeline-passes junk.cpp 
verify,always-inline,function(coro-early),cgscc(coro-split),function(coro-cleanup),function(annotation-remarks),verify
```


## -O1
```bash
(base) [bogale2@dane7:build]$ llvm-as < /dev/null   | opt -enable-new-pm=0 -O1 -disable-output -debug-pass=Arguments
Pass Arguments:  -tti -tbaa -scoped-noalias-aa -assumption-cache-tracker -targetlibinfo -verify -lower-expect -simplifycfg -domtree -sroa -early-cse
Pass Arguments:  -targetlibinfo -tti -tbaa -scoped-noalias-aa -assumption-cache-tracker -profile-summary-info -annotation2metadata -forceattrs -inferattrs -ipsccp -called-value-propagation -globalopt -domtree -mem2reg -deadargelim -domtree -basic-aa -aa -loops -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instcombine -simplifycfg -basiccg -globals-aa -prune-eh -always-inline -function-attrs -domtree -sroa -basic-aa -aa -memoryssa -early-cse-memssa -simplifycfg -domtree -basic-aa -aa -loops -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instcombine -libcalls-shrinkwrap -loops -postdomtree -branch-prob -block-freq -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -pgo-memop-opt -simplifycfg -reassociate -domtree -basic-aa -aa -memoryssa -loops -loop-simplify -lcssa-verification -lcssa -scalar-evolution -lazy-branch-prob -lazy-block-freq -licm -loop-rotate -licm -loop-unswitch -simplifycfg -domtree -basic-aa -aa -loops -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instcombine -loop-simplify -lcssa-verification -lcssa -scalar-evolution -loop-idiom -indvars -loop-deletion -loop-unroll -sroa -sccp -demanded-bits -bdce -aa -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instcombine -postdomtree -adce -basic-aa -aa -memoryssa -memcpyopt -simplifycfg -domtree -basic-aa -aa -loops -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instcombine -barrier -basiccg -rpo-function-attrs -globalopt -globaldce -basiccg -globals-aa -domtree -float2int -lower-constant-intrinsics -loops -loop-simplify -lcssa-verification -lcssa -basic-aa -aa -scalar-evolution -loop-rotate -loop-accesses -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -loop-distribute -postdomtree -branch-prob -block-freq -scalar-evolution -basic-aa -aa -loop-accesses -demanded-bits -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -inject-tli-mappings -loop-vectorize -loop-simplify -scalar-evolution -aa -loop-accesses -lazy-branch-prob -lazy-block-freq -loop-load-elim -basic-aa -aa -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instcombine -simplifycfg -domtree -basic-aa -aa -vector-combine -loops -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instcombine -loop-simplify -lcssa-verification -lcssa -scalar-evolution -loop-unroll -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instcombine -memoryssa -loop-simplify -lcssa-verification -lcssa -scalar-evolution -lazy-branch-prob -lazy-block-freq -licm -opt-remark-emitter -transform-warning -alignment-from-assumptions -strip-dead-prototypes -cg-profile -domtree -loops -postdomtree -branch-prob -block-freq -loop-simplify -lcssa-verification -lcssa -basic-aa -aa -scalar-evolution -block-freq -loop-sink -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instsimplify -div-rem-pairs -simplifycfg -annotation-remarks -verify
Pass Arguments:  -domtree
Pass Arguments:  -targetlibinfo -domtree -loops -postdomtree -branch-prob -block-freq
Pass Arguments:  -targetlibinfo -domtree -loops -postdomtree -branch-prob -block-freq
Pass Arguments:  -targetlibinfo -domtree -loops -lazy-branch-prob -lazy-block-freq
```

```bash
(base) [bogale2@dane7:build]$ opt -O1 -disable-output -print-pipeline-passes junk.cpp 
verify,annotation2metadata,forceattrs,inferattrs,function<eager-inv>(lower-expect,simplifycfg<bonus-inst-threshold=1;no-forward-switch-cond;no-switch-range-to-icmp;no-switch-to-lookup;keep-loops;no-hoist-common-insts;no-sink-common-insts>,sroa,early-cse<>,coro-early),openmp-opt,ipsccp,called-value-propagation,globalopt,function(mem2reg),deadargelim,function<eager-inv>(instcombine,simplifycfg<bonus-inst-threshold=1;no-forward-switch-cond;switch-range-to-icmp;no-switch-to-lookup;keep-loops;no-hoist-common-insts;no-sink-common-insts>),require<globals-aa>,function(invalidate<aa>),require<profile-summary>,cgscc(devirt<4>(inline<only-mandatory>,inline,function-attrs,function<eager-inv>(sroa,early-cse<memssa>,simplifycfg<bonus-inst-threshold=1;no-forward-switch-cond;switch-range-to-icmp;no-switch-to-lookup;keep-loops;no-hoist-common-insts;no-sink-common-insts>,instcombine,libcalls-shrinkwrap,simplifycfg<bonus-inst-threshold=1;no-forward-switch-cond;switch-range-to-icmp;no-switch-to-lookup;keep-loops;no-hoist-common-insts;no-sink-common-insts>,reassociate,require<opt-remark-emit>,loop-mssa(loop-instsimplify,loop-simplifycfg,licm,loop-rotate,licm,simple-loop-unswitch<no-nontrivial;trivial>),simplifycfg<bonus-inst-threshold=1;no-forward-switch-cond;switch-range-to-icmp;no-switch-to-lookup;keep-loops;no-hoist-common-insts;no-sink-common-insts>,instcombine,loop(loop-idiom,indvars,loop-deletion,loop-unroll-full),sroa,memcpyopt,sccp,bdce,instcombine,coro-elide,adce,simplifycfg<bonus-inst-threshold=1;no-forward-switch-cond;switch-range-to-icmp;no-switch-to-lookup;keep-loops;no-hoist-common-insts;no-sink-common-insts>,instcombine),coro-split)),globalopt,globaldce,elim-avail-extern,rpo-function-attrs,require<globals-aa>,function<eager-inv>(float2int,lower-constant-intrinsics,loop(loop-rotate,loop-deletion),loop-distribute,inject-tli-mappings,loop-vectorize<no-interleave-forced-only;vectorize-forced-only;>,loop-load-elim,instcombine,simplifycfg<bonus-inst-threshold=1;forward-switch-cond;switch-range-to-icmp;switch-to-lookup;no-keep-loops;hoist-common-insts;sink-common-insts>,vector-combine,instcombine,loop-unroll<O1>,transform-warning,instcombine,require<opt-remark-emit>,loop-mssa(licm),alignment-from-assumptions,loop-sink,instsimplify,div-rem-pairs,simplifycfg<bonus-inst-threshold=1;no-forward-switch-cond;switch-range-to-icmp;no-switch-to-lookup;keep-loops;no-hoist-common-insts;no-sink-common-insts>,coro-cleanup),cg-profile,globaldce,constmerge,rel-lookup-table-converter,function(annotation-remarks),verify
```

## -O2

```bash
(base) [bogale2@dane7:build]$ llvm-as < /dev/null   | opt -enable-new-pm=0 -O2 -disable-out
put -debug-pass=Arguments
Pass Arguments:  -tti -tbaa -scoped-noalias-aa -assumption-cache-tracker -targetlibinfo -verify -lower-expect -simplifycfg -domtree -sroa -early-cse
Pass Arguments:  -targetlibinfo -tti -tbaa -scoped-noalias-aa -assumption-cache-tracker -profile-summary-info -annotation2metadata -forceattrs -inferattrs -ipsccp -called-value-propagation -globalopt -domtree -mem2reg -deadargelim -domtree -basic-aa -aa -loops -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instcombine -simplifycfg -basiccg -globals-aa -prune-eh -inline -openmp-opt-cgscc -function-attrs -domtree -sroa -basic-aa -aa -memoryssa -early-cse-memssa -speculative-execution -aa -lazy-value-info -jump-threading -correlated-propagation -simplifycfg -domtree -basic-aa -aa -loops -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instcombine -libcalls-shrinkwrap -loops -postdomtree -branch-prob -block-freq -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -pgo-memop-opt -basic-aa -aa -loops -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -tailcallelim -simplifycfg -reassociate -domtree -basic-aa -aa -memoryssa -loops -loop-simplify -lcssa-verification -lcssa -scalar-evolution -lazy-branch-prob -lazy-block-freq -licm -loop-rotate -licm -loop-unswitch -simplifycfg -domtree -basic-aa -aa -loops -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instcombine -loop-simplify -lcssa-verification -lcssa -scalar-evolution -loop-idiom -indvars -loop-deletion -loop-unroll -sroa -aa -mldst-motion -phi-values -aa -memdep -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -gvn -sccp -demanded-bits -bdce -basic-aa -aa -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instcombine -lazy-value-info -jump-threading -correlated-propagation -postdomtree -adce -basic-aa -aa -memoryssa -memcpyopt -loops -dse -loop-simplify -lcssa-verification -lcssa -aa -scalar-evolution -lazy-branch-prob -lazy-block-freq -licm -simplifycfg -domtree -basic-aa -aa -loops -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instcombine -barrier -elim-avail-extern -basiccg -rpo-function-attrs -globalopt -globaldce -basiccg -globals-aa -domtree -float2int -lower-constant-intrinsics -loops -loop-simplify -lcssa-verification -lcssa -basic-aa -aa -scalar-evolution -loop-rotate -loop-accesses -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -loop-distribute -postdomtree -branch-prob -block-freq -scalar-evolution -basic-aa -aa -loop-accesses -demanded-bits -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -inject-tli-mappings -loop-vectorize -loop-simplify -scalar-evolution -aa -loop-accesses -lazy-branch-prob -lazy-block-freq -loop-load-elim -basic-aa -aa -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instcombine -simplifycfg -domtree -loops -scalar-evolution -basic-aa -aa -demanded-bits -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -inject-tli-mappings -slp-vectorizer -vector-combine -opt-remark-emitter -instcombine -loop-simplify -lcssa-verification -lcssa -scalar-evolution -loop-unroll -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instcombine -memoryssa -loop-simplify -lcssa-verification -lcssa -scalar-evolution -lazy-branch-prob -lazy-block-freq -licm -opt-remark-emitter -transform-warning -alignment-from-assumptions -strip-dead-prototypes -globaldce -constmerge -cg-profile -domtree -loops -postdomtree -branch-prob -block-freq -loop-simplify -lcssa-verification -lcssa -basic-aa -aa -scalar-evolution -block-freq -loop-sink -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instsimplify -div-rem-pairs -simplifycfg -annotation-remarks -verify
Pass Arguments:  -domtree
Pass Arguments:  -targetlibinfo -domtree -loops -postdomtree -branch-prob -block-freq
Pass Arguments:  -targetlibinfo -domtree -loops -postdomtree -branch-prob -block-freq
Pass Arguments:  -targetlibinfo -domtree -loops -lazy-branch-prob -lazy-block-freq
```

```bash
(base) [bogale2@dane7:build]$ opt -O2 -disable-output -print-pipeline-passes junk.cpp 
verify,annotation2metadata,forceattrs,inferattrs,function<eager-inv>(lower-expect,simplifycfg<bonus-inst-threshold=1;no-forward-switch-cond;no-switch-range-to-icmp;no-switch-to-lookup;keep-loops;no-hoist-common-insts;no-sink-common-insts>,sroa,early-cse<>,coro-early),openmp-opt,ipsccp,called-value-propagation,globalopt,function(mem2reg),deadargelim,function<eager-inv>(instcombine,simplifycfg<bonus-inst-threshold=1;no-forward-switch-cond;switch-range-to-icmp;no-switch-to-lookup;keep-loops;no-hoist-common-insts;no-sink-common-insts>),require<globals-aa>,function(invalidate<aa>),require<profile-summary>,cgscc(devirt<4>(inline<only-mandatory>,inline,function-attrs,openmp-opt-cgscc,function<eager-inv>(sroa,early-cse<memssa>,speculative-execution,jump-threading,correlated-propagation,simplifycfg<bonus-inst-threshold=1;no-forward-switch-cond;switch-range-to-icmp;no-switch-to-lookup;keep-loops;no-hoist-common-insts;no-sink-common-insts>,instcombine,libcalls-shrinkwrap,tailcallelim,simplifycfg<bonus-inst-threshold=1;no-forward-switch-cond;switch-range-to-icmp;no-switch-to-lookup;keep-loops;no-hoist-common-insts;no-sink-common-insts>,reassociate,require<opt-remark-emit>,loop-mssa(loop-instsimplify,loop-simplifycfg,licm,loop-rotate,licm,simple-loop-unswitch<no-nontrivial;trivial>),simplifycfg<bonus-inst-threshold=1;no-forward-switch-cond;switch-range-to-icmp;no-switch-to-lookup;keep-loops;no-hoist-common-insts;no-sink-common-insts>,instcombine,loop(loop-idiom,indvars,loop-deletion,loop-unroll-full),sroa,mldst-motion<no-split-footer-bb>,gvn<>,sccp,bdce,instcombine,jump-threading,correlated-propagation,adce,memcpyopt,dse,loop-mssa(licm),coro-elide,simplifycfg<bonus-inst-threshold=1;no-forward-switch-cond;switch-range-to-icmp;no-switch-to-lookup;keep-loops;hoist-common-insts;sink-common-insts>,instcombine),coro-split)),globalopt,globaldce,elim-avail-extern,rpo-function-attrs,require<globals-aa>,function<eager-inv>(float2int,lower-constant-intrinsics,loop(loop-rotate,loop-deletion),loop-distribute,inject-tli-mappings,loop-vectorize<no-interleave-forced-only;no-vectorize-forced-only;>,loop-load-elim,instcombine,simplifycfg<bonus-inst-threshold=1;forward-switch-cond;switch-range-to-icmp;switch-to-lookup;no-keep-loops;hoist-common-insts;sink-common-insts>,slp-vectorizer,vector-combine,instcombine,loop-unroll<O2>,transform-warning,instcombine,require<opt-remark-emit>,loop-mssa(licm),alignment-from-assumptions,loop-sink,instsimplify,div-rem-pairs,simplifycfg<bonus-inst-threshold=1;no-forward-switch-cond;switch-range-to-icmp;no-switch-to-lookup;keep-loops;no-hoist-common-insts;no-sink-common-insts>,coro-cleanup),cg-profile,globaldce,constmerge,rel-lookup-table-converter,function(annotation-remarks),verify
```
## -O3

```bash
(base) [bogale2@dane7:build]$ llvm-as < /dev/null   | opt -enable-new-pm=0 -O3 -disable-out
put -debug-pass=Arguments
Pass Arguments:  -tti -tbaa -scoped-noalias-aa -assumption-cache-tracker -targetlibinfo -verify -lower-expect -simplifycfg -domtree -sroa -early-cse
Pass Arguments:  -targetlibinfo -tti -tbaa -scoped-noalias-aa -assumption-cache-tracker -profile-summary-info -annotation2metadata -forceattrs -inferattrs -domtree -callsite-splitting -ipsccp -called-value-propagation -globalopt -domtree -mem2reg -deadargelim -domtree -basic-aa -aa -loops -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instcombine -simplifycfg -basiccg -globals-aa -prune-eh -inline -openmp-opt-cgscc -function-attrs -argpromotion -domtree -sroa -basic-aa -aa -memoryssa -early-cse-memssa -speculative-execution -aa -lazy-value-info -jump-threading -correlated-propagation -simplifycfg -domtree -aggressive-instcombine -basic-aa -aa -loops -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instcombine -libcalls-shrinkwrap -loops -postdomtree -branch-prob -block-freq -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -pgo-memop-opt -basic-aa -aa -loops -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -tailcallelim -simplifycfg -reassociate -domtree -basic-aa -aa -memoryssa -loops -loop-simplify -lcssa-verification -lcssa -scalar-evolution -lazy-branch-prob -lazy-block-freq -licm -loop-rotate -licm -loop-unswitch -simplifycfg -domtree -basic-aa -aa -loops -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instcombine -loop-simplify -lcssa-verification -lcssa -scalar-evolution -loop-idiom -indvars -loop-deletion -loop-unroll -sroa -aa -mldst-motion -phi-values -aa -memdep -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -gvn -sccp -demanded-bits -bdce -basic-aa -aa -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instcombine -lazy-value-info -jump-threading -correlated-propagation -postdomtree -adce -basic-aa -aa -memoryssa -memcpyopt -loops -dse -loop-simplify -lcssa-verification -lcssa -aa -scalar-evolution -lazy-branch-prob -lazy-block-freq -licm -simplifycfg -domtree -basic-aa -aa -loops -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instcombine -barrier -elim-avail-extern -basiccg -rpo-function-attrs -globalopt -globaldce -basiccg -globals-aa -domtree -float2int -lower-constant-intrinsics -loops -loop-simplify -lcssa-verification -lcssa -basic-aa -aa -scalar-evolution -loop-rotate -loop-accesses -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -loop-distribute -postdomtree -branch-prob -block-freq -scalar-evolution -basic-aa -aa -loop-accesses -demanded-bits -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -inject-tli-mappings -loop-vectorize -loop-simplify -scalar-evolution -aa -loop-accesses -lazy-branch-prob -lazy-block-freq -loop-load-elim -basic-aa -aa -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instcombine -simplifycfg -domtree -loops -scalar-evolution -basic-aa -aa -demanded-bits -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -inject-tli-mappings -slp-vectorizer -vector-combine -opt-remark-emitter -instcombine -loop-simplify -lcssa-verification -lcssa -scalar-evolution -loop-unroll -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instcombine -memoryssa -loop-simplify -lcssa-verification -lcssa -scalar-evolution -lazy-branch-prob -lazy-block-freq -licm -opt-remark-emitter -transform-warning -alignment-from-assumptions -strip-dead-prototypes -globaldce -constmerge -cg-profile -domtree -loops -postdomtree -branch-prob -block-freq -loop-simplify -lcssa-verification -lcssa -basic-aa -aa -scalar-evolution -block-freq -loop-sink -lazy-branch-prob -lazy-block-freq -opt-remark-emitter -instsimplify -div-rem-pairs -simplifycfg -annotation-remarks -verify
Pass Arguments:  -domtree
Pass Arguments:  -targetlibinfo -domtree -loops -postdomtree -branch-prob -block-freq
Pass Arguments:  -targetlibinfo -domtree -loops -postdomtree -branch-prob -block-freq
Pass Arguments:  -targetlibinfo -domtree -loops -lazy-branch-prob -lazy-block-freq
```

```bash
(base) [bogale2@dane7:build]$ opt -O3 -disable-output -print-pipeline-passes junk.cpp 
verify,annotation2metadata,forceattrs,inferattrs,function<eager-inv>(lower-expect,simplifycfg<bonus-inst-threshold=1;no-forward-switch-cond;no-switch-range-to-icmp;no-switch-to-lookup;keep-loops;no-hoist-common-insts;no-sink-common-insts>,sroa,early-cse<>,coro-early,callsite-splitting),openmp-opt,ipsccp,called-value-propagation,globalopt,function(mem2reg),deadargelim,function<eager-inv>(instcombine,simplifycfg<bonus-inst-threshold=1;no-forward-switch-cond;switch-range-to-icmp;no-switch-to-lookup;keep-loops;no-hoist-common-insts;no-sink-common-insts>),require<globals-aa>,function(invalidate<aa>),require<profile-summary>,cgscc(devirt<4>(inline<only-mandatory>,inline,function-attrs,argpromotion,openmp-opt-cgscc,function<eager-inv>(sroa,early-cse<memssa>,speculative-execution,jump-threading,correlated-propagation,simplifycfg<bonus-inst-threshold=1;no-forward-switch-cond;switch-range-to-icmp;no-switch-to-lookup;keep-loops;no-hoist-common-insts;no-sink-common-insts>,instcombine,aggressive-instcombine,libcalls-shrinkwrap,tailcallelim,simplifycfg<bonus-inst-threshold=1;no-forward-switch-cond;switch-range-to-icmp;no-switch-to-lookup;keep-loops;no-hoist-common-insts;no-sink-common-insts>,reassociate,require<opt-remark-emit>,loop-mssa(loop-instsimplify,loop-simplifycfg,licm,loop-rotate,licm,simple-loop-unswitch<nontrivial;trivial>),simplifycfg<bonus-inst-threshold=1;no-forward-switch-cond;switch-range-to-icmp;no-switch-to-lookup;keep-loops;no-hoist-common-insts;no-sink-common-insts>,instcombine,loop(loop-idiom,indvars,loop-deletion,loop-unroll-full),sroa,mldst-motion<no-split-footer-bb>,gvn<>,sccp,bdce,instcombine,jump-threading,correlated-propagation,adce,memcpyopt,dse,loop-mssa(licm),coro-elide,simplifycfg<bonus-inst-threshold=1;no-forward-switch-cond;switch-range-to-icmp;no-switch-to-lookup;keep-loops;hoist-common-insts;sink-common-insts>,instcombine),coro-split)),globalopt,globaldce,elim-avail-extern,rpo-function-attrs,require<globals-aa>,function<eager-inv>(float2int,lower-constant-intrinsics,loop(loop-rotate,loop-deletion),loop-distribute,inject-tli-mappings,loop-vectorize<no-interleave-forced-only;no-vectorize-forced-only;>,loop-load-elim,instcombine,simplifycfg<bonus-inst-threshold=1;forward-switch-cond;switch-range-to-icmp;switch-to-lookup;no-keep-loops;hoist-common-insts;sink-common-insts>,slp-vectorizer,vector-combine,instcombine,loop-unroll<O3>,transform-warning,instcombine,require<opt-remark-emit>,loop-mssa(licm),alignment-from-assumptions,loop-sink,instsimplify,div-rem-pairs,simplifycfg<bonus-inst-threshold=1;no-forward-switch-cond;switch-range-to-icmp;no-switch-to-lookup;keep-loops;no-hoist-common-insts;no-sink-common-insts>,coro-cleanup),cg-profile,globaldce,constmerge,rel-lookup-table-converter,function(annotation-remarks),verify
```

***

```
[bogale2@dane4:dane_junk]$ opt --print-passes
Module passes:
  always-inline
  attributor
  annotation2metadata
  openmp-opt
  called-value-propagation
  canonicalize-aliases
  cg-profile
  check-debugify
  constmerge
  cross-dso-cfi
  deadargelim
  debugify
  elim-avail-extern
  extract-blocks
  forceattrs
  function-import
  function-specialization
  globaldce
  globalopt
  globalsplit
  hotcoldsplit
  inferattrs
  inliner-wrapper
  print<inline-advisor>
  inliner-wrapper-no-mandatory-first
  insert-gcov-profiling
  instrorderfile
  instrprof
  internalize
  invalidate<all>
  ipsccp
  iroutliner
  print-ir-similarity
  lowertypetests
  metarenamer
  mergefunc
  name-anon-globals
  no-op-module
  objc-arc-apelim
  partial-inliner
  pgo-icall-prom
  pgo-instr-gen
  pgo-instr-use
  print-profile-summary
  print-callgraph
  print
  print-lcg
  print-lcg-dot
  print-must-be-executed-contexts
  print-stack-safety
  print<module-debuginfo>
  rel-lookup-table-converter
  rewrite-statepoints-for-gc
  rewrite-symbols
  rpo-function-attrs
  sample-profile
  scc-oz-module-inliner
  strip
  strip-dead-debug-info
  pseudo-probe
  strip-dead-prototypes
  strip-debug-declare
  strip-nondebug
  strip-nonlinetable-debuginfo
  synthetic-counts-propagation
  verify
  wholeprogramdevirt
  dfsan
  msan-module
  module-inline
  tsan-module
  sancov-module
  memprof-module
  poison-checking
  pseudo-probe-update
Module passes with params:
  loop-extract<single>
  hwasan<kernel;recover>
  asan-module<kernel>
Module analyses:
  callgraph
  lcg
  module-summary
  no-op-module
  profile-summary
  stack-safety
  verify
  pass-instrumentation
  asan-globals-md
  inline-advisor
  ir-similarity
  globals-aa
Module alias analyses:
  globals-aa
CGSCC passes:
  argpromotion
  invalidate<all>
  function-attrs
  attributor-cgscc
  openmp-opt-cgscc
  coro-split
  no-op-cgscc
CGSCC passes with params:
  inline<only-mandatory>
CGSCC analyses:
  no-op-cgscc
  fam-proxy
  pass-instrumentation
Function passes:
  aa-eval
  adce
  add-discriminators
  aggressive-instcombine
  assume-builder
  assume-simplify
  alignment-from-assumptions
  annotation-remarks
  bdce
  bounds-checking
  break-crit-edges
  callsite-splitting
  consthoist
  constraint-elimination
  chr
  coro-early
  coro-elide
  coro-cleanup
  correlated-propagation
  dce
  dfa-jump-threading
  div-rem-pairs
  dse
  dot-cfg
  dot-cfg-only
  dot-dom
  dot-dom-only
  fix-irreducible
  flattencfg
  make-guards-explicit
  gvn-hoist
  gvn-sink
  helloworld
  infer-address-spaces
  instcombine
  instcount
  instsimplify
  invalidate<all>
  irce
  float2int
  no-op-function
  libcalls-shrinkwrap
  lint
  inject-tli-mappings
  instnamer
  loweratomic
  lower-expect
  lower-guard-intrinsic
  lower-constant-intrinsics
  lower-widenable-condition
  guard-widening
  load-store-vectorizer
  loop-simplify
  loop-sink
  lowerinvoke
  lowerswitch
  mem2reg
  memcpyopt
  mergeicmps
  mergereturn
  nary-reassociate
  newgvn
  jump-threading
  partially-inline-libcalls
  lcssa
  loop-data-prefetch
  loop-load-elim
  loop-fusion
  loop-distribute
  loop-versioning
  objc-arc
  objc-arc-contract
  objc-arc-expand
  pgo-memop-opt
  print
  print<assumptions>
  print<block-freq>
  print<branch-prob>
  print<cost-model>
  print<cycles>
  print<da>
  print<divergence>
  print<domtree>
  print<postdomtree>
  print<delinearization>
  print<demanded-bits>
  print<domfrontier>
  print<func-properties>
  print<inline-cost>
  print<inliner-size-estimator>
  print<loops>
  print<memoryssa>
  print<memoryssa-walker>
  print<phi-values>
  print<regions>
  print<scalar-evolution>
  print<stack-safety-local>
  print-alias-sets
  print-predicateinfo
  print-mustexecute
  print-memderefs
  reassociate
  redundant-dbg-inst-elim
  reg2mem
  scalarize-masked-mem-intrin
  scalarizer
  separate-const-offset-from-gep
  sccp
  sink
  slp-vectorizer
  slsr
  speculative-execution
  sroa
  strip-gc-relocates
  structurizecfg
  tailcallelim
  unify-loop-exits
  vector-combine
  verify
  verify<domtree>
  verify<loops>
  verify<memoryssa>
  verify<regions>
  verify<safepoint-ir>
  verify<scalar-evolution>
  view-cfg
  view-cfg-only
  transform-warning
  tsan
  memprof
Function passes with params:
  early-cse<memssa>
  ee-instrument<post-inline>
  lower-matrix-intrinsics<minimal>
  loop-unroll<O0;O1;O2;O3;full-unroll-max=N;no-partial;partial;no-peeling;peeling;no-profile-peeling;profile-peeling;no-runtime;runtime;no-upperbound;upperbound>
  asan<kernel>
  msan<recover;kernel;eager-checks;track-origins=N>
  simplifycfg<no-forward-switch-cond;forward-switch-cond;no-switch-range-to-icmp;switch-range-to-icmp;no-switch-to-lookup;switch-to-lookup;no-keep-loops;keep-loops;no-hoist-common-insts;hoist-common-insts;no-sink-common-insts;sink-common-insts;bonus-inst-threshold=N>
  loop-vectorize<no-interleave-forced-only;interleave-forced-only;no-vectorize-forced-only;vectorize-forced-only>
  mldst-motion<no-split-footer-bb;split-footer-bb>
  gvn<no-pre;pre;no-load-pre;load-pre;no-split-backedge-load-pre;split-backedge-load-pre;no-memdep;memdep>
  print<stack-lifetime><may;must>
Function analyses:
  aa
  assumptions
  block-freq
  branch-prob
  cycles
  domtree
  postdomtree
  demanded-bits
  domfrontier
  func-properties
  loops
  lazy-value-info
  da
  inliner-size-estimator
  memdep
  memoryssa
  phi-values
  regions
  no-op-function
  opt-remark-emit
  scalar-evolution
  should-not-run-function-passes
  should-run-extra-vector-passes
  stack-safety-local
  targetlibinfo
  targetir
  verify
  pass-instrumentation
  divergence
  basic-aa
  cfl-anders-aa
  cfl-steens-aa
  objc-arc-aa
  scev-aa
  scoped-noalias-aa
  tbaa
Function alias analyses:
  basic-aa
  cfl-anders-aa
  cfl-steens-aa
  objc-arc-aa
  scev-aa
  scoped-noalias-aa
  tbaa
LoopNest passes:
  lnicm
  loop-flatten
  loop-interchange
  loop-unroll-and-jam
  no-op-loopnest
Loop passes:
  canon-freeze
  dot-ddg
  invalidate<all>
  licm
  loop-idiom
  loop-instsimplify
  loop-rotate
  no-op-loop
  print
  loop-deletion
  loop-simplifycfg
  loop-reduce
  indvars
  loop-unroll-full
  print-access-info
  print<ddg>
  print<iv-users>
  print<loopnest>
  print<loop-cache-cost>
  loop-predication
  guard-widening
  loop-bound-split
  loop-reroll
  loop-versioning-licm
Loop passes with params:
  simple-loop-unswitch<nontrivial;no-nontrivial;trivial;no-trivial>
Loop analyses:
  no-op-loop
  access-info
  ddg
  iv-users
  pass-instrumentation
```