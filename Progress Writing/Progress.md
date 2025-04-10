### What Have you done so far?

I have successfully created a custom diagnostic handler to intercept the remark information generated by LLVM. This enables me to access all the details contained within the optimization records, providing a comprehensive view of the optimization process.

In addition, I have started developing a proxy application. The base code for the application is ready, and I have tested it to ensure its functionality. Currently, I am in the process of integrating Caliper annotations into the proxy application to facilitate detailed performance analysis.

I have also begun contemplating the user perspective for the final product. This involves considering how the tool will be run, its usability, and how the results will be presented to end-users for maximum effectiveness.


### What is your contribution with you project?

My contribution enables users to easily access LLVM's remark information and output it in any format they choose. By compiling my work into a plugin and pairing it with a compiler, it allows for the custom output of remark information for every translation unit. This approach differs from the default optimization record output, which limits users to a predefined set of data. With my solution, users have complete control over how the data is formatted and presented, offering greater flexibility and customization.

### What is still needed?

For the plugin, I still need to determine the file format that will be most suitable for outputting data in a way that is easily digestible for Caliper. Currently, I have access to line numbers through the remark data, which could potentially be used for mapping with Caliper's Calling Context Tree (CCT). However, I aim to use additional attributes available within the LLVM infrastructure to develop a more comprehensive and holistic mapping approach.

To achieve this, I need to explore how tools like Dyninst could assist in enhancing the mapping process. I can experiment with these ideas using my proxy application as a testing ground. Additionally, I’ve learned that libdw is accessible from Caliper, which could provide symbol information for regions, further enriching the mapping and analysis capabilities.


### What is the goal of your project?

Compiler optimization analysis can be significantly enhanced using compiler remarks, which often contain invaluable information. Meanwhile, Caliper provides detailed runtime data for applications across various compiler optimizations, leveraging fine-grained annotations. Compilers can output remarks detailing which optimization passes were executed, succeeded, or failed, while Caliper offers runtime context. This raises an intriguing possibility: combining compiler remark information with Caliper's calling context tree (CCT) to better explain runtime performance.

The final deliverable for this project would enable users to examine, for every Caliper region, the optimization passes that were executed, their statuses, and the accompanying remark information. This integration would provide a comprehensive view of how compiler optimizations influence runtime performance, bridging the gap between static and dynamic analysis.