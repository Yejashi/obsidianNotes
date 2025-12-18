**Sources**:
- Video: https://vimeo.com/742349001
- PDF: https://www.olcf.ornl.gov/wp-content/uploads/Intro_Register_pressure_ORNL_20220812_2083.pdf

The performance of GPU kernels is highly dependent on "occupancy", where there are various wavefronts (warps) running in parallel.
- **Occupancy** is the fraction of the GPU’s maximum hardware execution capacity that is actively utilized by resident wavefronts (warps) on a compute unit