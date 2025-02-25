Here’s a cleaned-up version of your notes in bullet-point format:

- **Inference & k-fold cross-validation:**
    
    - What happens at the end of all k-fold iterations?
    - Do all k-fold splits collect errors?
    - Retrain the best model after evaluation.
- **Training & validation:**
    
    - Perform internal training and validation.
    - Compute errors for each test set and parameter combination.
- **Coefficient calculation:**
    
    - Analyze how coefficients are computed within k-fold iterations.
- **Model training & validation:**
    
    - Train and validate the model.
    - Compute validation errors and store them in an error buffer.
- **Inference process:**
    
    - Input data into the model and obtain predictions.
- **Raw data handling:**
    
    - Retrieve raw data buffer.
    - Convert MAGMA buffers into standard arrays.
- **MAGMA engine initialization:**
    
    - Handle `init_magma_engine`.
    - Modify `dalalscode -> sbm.c` to create a struct storing any MAGMA queue or device.
    - Save the struct as a void pointer in the handle.

