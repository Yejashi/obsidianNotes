### What Currently Exists
Three Plugins
- Remark Diag Handler
- Function Extraction
- IR Metric Extraction


Remark Diag Handler
```
{
	"Metadata": {
		"Module Name": "src/foo.cpp",
		"Target Triple": {
			"Arch": "x86_64",
			"OS": "linux",
			"Vendor": "unknown"
		}
	},
	"Remark Data": {
		"foo()": [
			{
				"location" : {
					"AbsolutePath": "/g/.../src/foo.cpp",
					"Column": 5,
					"Line": 360,
					"RelativePath": "src/foo.cpp"
				},
				"Message": "Yo, what uppppp!!",
				"Pass Name": "inline",
				"Remark Name": "AlwaysInline",
				"RemarkType": "Transformation",
				"Status": "Passed"
			},
			{
				...
			}
		],
		"bar()": [
			...
		]
	}

}
```

IR Metric Extraction:

```
{
	"Metadata": {
		"Module Name": "src/foo.cpp",
		"Target Triple": {
			"Arch": "x86_64",
			"OS": "linux",
			"Vendor": "unknown"
		}
	},
	"Functions": {
		"foo()": {
"maxLiveSSAValues": 17,

"maxLoopDepth": 0,

"numAllocaInsts": 0,

"numArithmeticInsts": 94,

"numAtomicInsts": 0,

"numBasicBlocks": 51,

"numBranchEdges": 75,

"numBranchInsts": 50,

"numCastInsts": 11,

"numCompareInsts": 17,

"numDirectFuncCalls": 0,

"numFenceInsts": 14,

"numFloatArithmeticInsts": 78,

"numGEPInsts": 86,

"numIndirectFuncCalls": 0,

"numInsts": 393,

"numIntegerArithmeticInsts": 16,

"numLoads": 75,

"numLogicInsts": 11,

"numLoopInvInsts": 0,

"numLoops": 0,

"numMemAccessInsts": 88,

"numMemRelatedInsts": 102,

"numPHIInsts": 1,

"numSelectInsts": 0,

"numSmallConstTripLoops": 0,

"numStores": 13	
		}
	}
}
```
