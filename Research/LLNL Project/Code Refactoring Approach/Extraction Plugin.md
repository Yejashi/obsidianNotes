### What Currently Exists
Three Plugins
- Function Extraction
- Remark Diag Handler
- IR Metric Extraction

Note: None of these passess mutate the IR

**Function Extraction**
Registered at beginning of pipeline
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
			"beginLine": 128,
			"endLine": 129,
			"externallyVisible": true,
			"isHipStub: false,
			"scopeLine": -1
		},
		...
	}
}	
```

**Remark Diag Handler**
Registered at beginning of pipeline, used at end of each pass
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
		...
	}

}
```

**IR Metric Extraction**
End of Pipeline
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
			"numInsts": 17,
			"numBasicBlocks": 3,
			...,
			"maxLiveSSAValues"
		}
	}
}
```

### What Should Be After Refactor
Single Plugin

**Extraction Plugin**
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
			"ExternallyVisible": true,
			"FunctionsCalled": [
				"bar()",
				...
			],
			"IRStatistics": {
				"numInsts": 17,
				"numBasicBlocks": 3,
				...
			},
			"RemarkInformation": {
				"RemarkStatistics": {
					"inline_attempted": 5,
					"inline_passed": 3,
					"inline_missed": 1,
					"inline_unknown": 1,
					...
				},
				"Remarks": [
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
				...
			]
		},
		...
	}
}	
```
