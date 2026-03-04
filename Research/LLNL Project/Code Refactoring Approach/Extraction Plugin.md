### What Currently Exists
Three Plugins
- Function Extraction
- Remark Diag Handler
- IR Metric Extraction

**Function Extraction**
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
			
		}
	}
}	
```

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
			"numInsts": 17,
			"numBasicBlocks": 3,
			...,
			"maxLiveSSAValues"
		}
	}
}
```
