`OptimizationRemarkEmitter` (ORE), is key LLVM utility used to emit diagnostic remarks related to optimization passes in LLVM's compilation pipeline.
### Purpose
- Reports optimization-related diagnostics, including when optimizations succeed or fail.
- Includes "hotness" information (derived from block frequency) if enabled via `DiagnosticsHotnessRequested` in the LLVM context.
- 