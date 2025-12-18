**Sources**:
- Video: https://vimeo.com/742349001
- PDF: https://www.olcf.ornl.gov/wp-content/uploads/Intro_Register_pressure_ORNL_20220812_2083.pdf

The performance of GPU kernels is highly dependent on "occupancy", where there are various wavefronts (warps) running in parallel.
- **Occupancy** is the fraction of the GPU’s maximum hardware execution capacity that is actively utilized by  wavefronts (warps) on a compute unit.
- Basically, the ratio of active wavefronts per SM/CU to the maximum wavefronts the hardware can support simultaneously.

GPUs execute many wavefronts (warps) in parallel on each compute unit and occupancy determines how many of these wavefronts can be resident and ready to run at the same time.

Occupancy depends on the amount of resources (e.g. registers, LDS, etc) used by a wavefront.