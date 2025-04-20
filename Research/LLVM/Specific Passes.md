## -O0
```bash
(base) [bogale2@dane7:build]$ llvm-as < /dev/null   | opt -enable-new-pm=0 -O0 -disable-out
put -debug-pass=Arguments
Pass Arguments:  -tti -verify
Pass Arguments:  -targetlibinfo -tti -assumption-cache-tracker -profile-summary-info -annotation2metadata -forceattrs -basiccg -always-inline -barrier -annotation-remarks -verify
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


## -O2