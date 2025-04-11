# **Building Polynomial Regression Models Using Linear Algebra**

## Slide 1: Title Slide

- **Talk Title:** _Building Polynomial Regression Models Using Linear Algebra_
    
- **Presenter:** [Your Name], PhD Student – Global Computing Lab (Advisor: Dr. Michela Taufer)
    
- **Affiliation:** University of Tennessee, Knoxville (Dept. of Electrical Engineering & Computer Science)
    

**Speaker Notes:**  
Welcome to this talk on _“Building Polynomial Regression Models Using Linear Algebra.”_ My name is [Your Name], and I’m a PhD student in the Global Computing Laboratory at the University of Tennessee under Dr. Michela Taufer. Today I’ll be discussing how we construct polynomial regression models and why linear algebra is fundamental to this process. I’ll also highlight applications in High-Performance Computing (HPC), including results from our recent Surrogate-Based Modeling (SBM) study presented at ICCS 2025. By the end, I hope to convey both the theory behind polynomial regression using linear systems and its practical impact on modeling HPC application performance.

## Slide 2: Test Questions (Pre-Talk)

1. **Formulation:** How can fitting a polynomial be expressed as solving a linear system $A\mathbf{x} = \mathbf{b}$, and what linear algebra methods can solve it?
    
2. **HPC Motivation:** Why use surrogate models like polynomial regression for HPC performance tuning instead of exhaustive parameter searches?
    
3. **Model Complexity:** What is a potential risk of using a very high-degree polynomial in regression, and how can we mitigate it?
    

**Speaker Notes:**  
Before we dive in, consider these guiding questions. (1) _Formulation:_ How do we set up polynomial regression as a linear algebra problem $A x = b$, and which techniques (LU factorization, QR, SVD, etc.) help solve it efficiently? (2) _HPC Motivation:_ In the context of HPC, why might we prefer building a surrogate model (like a polynomial fit) to predict performance, rather than running exhaustive experiments for every configuration? (3) _Model Complexity:_ What happens if we make our polynomial model too complex (too high-degree) relative to the available data, and how do we guard against this issue (think overfitting and remedies like cross-validation)? Keep these questions in mind; we will answer them during the talk. We’ll revisit them at the end to check understanding.

## Slide 3: Presenter Introduction – Academic & Personal

- **Academic Background:** PhD Student in **Global Computing Lab** (GCLab) under Dr. Michela Taufer. Research focus on HPC performance analysis, surrogate modeling, and linear algebra applications.
    
- **Hometown:** [City, Country]. _(Include a map or image of hometown)_
    
- **Interests & Hobbies:** Passionate about coding and math; enjoy hiking in the Smoky Mountains and playing chess. Big fan of sci-fi movies and trying out new cuisines.
    
- **Fun Facts:** Proud owner of a mischievous cat (who occasionally tries to help me code). Have traveled to 10+ countries – love exploring new cultures and food.
    

**Speaker Notes:**  
Let me briefly introduce myself. I’m a second-year PhD student in the Global Computing Lab, which is led by Dr. Michela Taufer. My research revolves around **high performance computing** and how we can use mathematical modeling to understand and predict application performance. In particular, I’m interested in **surrogate-based modeling** – using simplified models like polynomial regressions to approximate complex system behaviors. I originally hail from [Your Hometown]; you can see it on the map here. Outside of the lab, I like to balance work with some fun: I go hiking (we have the Great Smoky Mountains near Knoxville, which are fantastic!), I enjoy playing chess, and I’m a huge movie buff – I can talk your ear off about the latest science fiction films. I also have a cat who keeps me company during late-night coding sessions. Through this talk, you’ll see how my interests in math and HPC intersect in the research I do. Now, let’s get into the outline of the presentation.

## Slide 4: Talk Outline

- **Introduction & Overview:** Polynomial regression and surrogate modeling – what are they and how do linear systems ($A\mathbf{x}=\mathbf{b}$) tie in? Key matrix decompositions (LU, QR, SVD) relevant to solving these models.
    
- **Historical Background:** Origins of polynomial regression (Legendre & Gauss and least squares)​[en.wikipedia.org](https://en.wikipedia.org/wiki/Polynomial_regression#:~:text=squares.%20The%20least,The%20first%20design%20of%20an), development of linear algebra techniques (Gaussian elimination, Householder’s QR​[nhigham.com](https://nhigham.com/2020/09/15/what-is-a-householder-matrix/#:~:text=Householder%20matrices%20for%20computational%20purposes,to%20construct%20the%20QR%20factorization), SVD​[utminers.utep.edu](https://utminers.utep.edu/xzeng/2017spring_math5330/MATH_5330_Computational_Methods_of_Linear_Algebra_files/ln15.pdf#:~:text=with%20C%20%3D%20AAt,The%20technique%20finds%20U%202)), and early surrogate modeling in science (e.g. response surface methods​[clas.iusb.edu](https://clas.iusb.edu/math-compsci/_prior-proposals/Nbradley_Proposal.pdf#:~:text=history,Moreover)).
    
- **Algorithms & Methods:** Formulating polynomial regression as a least-squares problem. Solving $A^T A \mathbf{x}=A^T\mathbf{b}$ via matrix factorization (normal equations vs. QR factorization vs. SVD). Illustrated with examples.
    
- **HPC Applications:** Use cases in High-Performance Computing – modeling performance of computational kernels (e.g. matrix multiplication (GEMM) and RAJAPerf benchmarks) with polynomial fits. How these surrogates aid in tuning HPC applications.
    
- **Implementation & Results:** Highlights from our ICCS 2025 paper on Surrogate-Based Modeling (SBM). Comparing polynomial surrogate models to k-Nearest Neighbors (kNN) for HPC performance data. Visualization of performance surfaces, error metrics (MSE, $R^2$), and the impact of polynomial degree on accuracy​file-7rhtrwtsjd5w8c8gletf19.
    
- **Open Issues & Future Work:** Current challenges in surrogate modeling for HPC – sampling strategies, generalizability across systems, dealing with non-linear “cliffs” in performance, avoiding overfitting, etc. Opportunities for improvement and research questions.
    
- **Discussion & Q&A:** Wrap up with references and open the floor for questions. Revisit test questions for discussion.

**Speaker Notes:**  
Here’s the roadmap for my talk. We’ll start with an **Introduction** to polynomial regression and surrogate modeling, establishing how linear algebra underpins these models. Then I’ll provide some **Historical Background**, touching on the key contributors and developments that got us where we are (from Legendre and Gauss’s least-squares method to modern HPC surrogate approaches). Next, we’ll dive into the **Algorithms & Methods** – how to set up the polynomial regression problem and solve it using linear algebra techniques like QR or SVD. After covering the theory, we move to **HPC Applications**, seeing how polynomial regression is applied to model the performance of real computational kernels (for example, how we predict the runtime of a matrix-multiplication operation on a supercomputer). Following that, I’ll share **Implementation & Results** from our recent research: we built surrogate models (polynomial fits) for HPC benchmark data and compared their performance to a traditional machine learning method (kNN). We’ll see some results like how increasing polynomial degree affected prediction accuracy and how our surrogate model outperformed kNN​file-7rhtrwtsjd5w8c8gletf19. Finally, we’ll discuss **Open Issues** – the challenges and open questions in this field – and conclude with a **Discussion/Q&A**, including revisiting those initial test questions to see if we’ve answered them.

## Slide 5: Overview – Polynomial Regression & Surrogates

- **Polynomial Regression:** A form of regression analysis where the relationship between input variables and an output is modeled as an $n$th-degree polynomial. Essentially an extension of linear regression that can fit curves. We seek coefficients $(a_0, a_1, ..., a_k)$ such that $y \approx a_0 + a_1 x + \cdots + a_k x^k$ for our data​[mathworld.wolfram.com](https://mathworld.wolfram.com/LeastSquaresFittingPolynomial.html#:~:text=Generalizing%20from%20a%20straight%20line,k%20th%20degree%20%2015).
    
- **Linear Algebra Formulation:** Fitting a polynomial of degree $k$ leads to an overdetermined linear system. We construct a **design matrix** $A$ (Vandermonde matrix with rows $[1, x_i, x_i^2, ..., x_i^k]$ for each data point $i$) and solve $A \mathbf{x} \approx \mathbf{b}$, where $\mathbf{x}=[a_0,\dots,a_k]^T$ are the polynomial coefficients and $\mathbf{b}=[y_1,...,y_n]^T$ are observed outputs​[mathworld.wolfram.com](https://mathworld.wolfram.com/LeastSquaresFittingPolynomial.html#:~:text=These%20lead%20to%20the%20equations). The optimal solution minimizes the sum of squared residuals $||A\mathbf{x}-\mathbf{b}||^2$.
    
- **Matrix Decompositions:** To solve $A\mathbf{x}=\mathbf{b}$ (or normal equations $A^T A \mathbf{x}=A^T \mathbf{b}$) reliably, we use linear algebra techniques:
    
    - _LU Decomposition:_ Factor $A$ or $A^T A$ into lower/upper triangular factors (less common for least-squares due to stability issues).
        
    - _QR Factorization:_ Decompose $A = Q R$ (with $Q$ orthogonal, $R$ upper triangular) to solve $R\mathbf{x}=Q^T\mathbf{b}$. Householder reflections (1958) provide a stable way to compute QR​[nhigham.com](https://nhigham.com/2020/09/15/what-is-a-householder-matrix/#:~:text=Householder%20matrices%20for%20computational%20purposes,to%20construct%20the%20QR%20factorization).
        
    - _Singular Value Decomposition (SVD):_ Compute $A=U \Sigma V^T$ – gives the pseudo-inverse solution $\mathbf{x}=V \Sigma^{+} U^T \mathbf{b}$, very stable especially if $A$ is ill-conditioned. Efficient algorithms for SVD emerged in the 1960s (Golub & Kahan 1965​[utminers.utep.edu](https://utminers.utep.edu/xzeng/2017spring_math5330/MATH_5330_Computational_Methods_of_Linear_Algebra_files/ln15.pdf#:~:text=with%20C%20%3D%20AAt,The%20technique%20finds%20U%202)).
        
- **Surrogate Modeling:** Using an approximate model to emulate a complex function or system. In HPC and simulation contexts, surrogate models (e.g. polynomial fits) provide fast predictions in place of expensive experiments. **Key idea:** sample the true system sparsely and fit a surrogate to predict outputs at untested points​file-7rhtrwtsjd5w8c8gletf19. Polynomial regression is a common surrogate model choice due to its simplicity and analytical tractability.
    

**Speaker Notes:**  
This slide gives an overview of the main concepts. **Polynomial regression** is simply fitting a polynomial curve through data points – it generalizes linear regression by allowing curved fits. For instance, instead of a straight-line fit $y = a_0 + a_1 x$, we might fit a quadratic $y = a_0 + a_1 x + a_2 x^2$, or higher degrees, to capture curvature in the data.

Crucially, we can express polynomial regression in a linear algebra framework. If we have data points $(x_i, y_i)$, $i=1\ldots n$, and we choose a polynomial degree $k$, we set up a **design matrix** $A$ where each row corresponds to a data point and contains $[1, x_i, x_i^2, ..., x_i^k]$. Our unknown coefficient vector $\mathbf{x}$ holds the polynomial coefficients, and the observed outputs go into vector $\mathbf{b}$. The fitting problem is $A \mathbf{x} \approx \mathbf{b}$. Typically $n$ (number of data points) is greater than $(k+1)$ (number of coefficients), so it’s an overdetermined system – we usually cannot solve it exactly, but we **minimize the least-squares error**. This leads to the normal equations $A^T A \mathbf{x} = A^T \mathbf{b}$.

Solving this efficiently and stably is where **matrix decompositions** come in. A naive solution uses $A^T A$ (normal equations) and then LU factorization, but $A^T A$ can be ill-conditioned. A better approach is to use **QR factorization** directly on $A$. Householder reflections (first described by Alston Householder in 1958) are a robust way to compute QR​[nhigham.com](https://nhigham.com/2020/09/15/what-is-a-householder-matrix/#:~:text=Householder%20matrices%20for%20computational%20purposes,to%20construct%20the%20QR%20factorization), and this method avoids squaring the condition number like normal equations do. Another powerful approach is **SVD (Singular Value Decomposition)** – it not only solves the least squares problem in a stable way but also gives insight into the solution (it can handle rank-deficient cases gracefully by zeroing small singular values). Gene Golub and William Kahan developed a practical SVD algorithm in 1965​[utminers.utep.edu](https://utminers.utep.edu/xzeng/2017spring_math5330/MATH_5330_Computational_Methods_of_Linear_Algebra_files/ln15.pdf#:~:text=with%20C%20%3D%20AAt,The%20technique%20finds%20U%202), which was a milestone in computational linear algebra.

Finally, **surrogate modeling** is the broader concept of which polynomial regression can be an example. In HPC, we often deal with functions or simulations that are extremely expensive to run for all possible inputs. Instead, we run a modest number of experiments and **fit a surrogate model** to those. The surrogate (here, a polynomial function) approximates the underlying behavior so we can predict outcomes without exhaustive measurement. This approach has been used to tune systems – for example, building a performance model of an application by sampling a few configurations and then predicting performance in other cases​file-7rhtrwtsjd5w8c8gletf19. Surrogate models strike a balance: they are much cheaper to evaluate than the real system, at the cost of some modeling error. The goal is to make that error small enough to still be useful.

With these basic ideas in mind, we’re ready to delve into how these techniques evolved and are applied.

## Slide 6: History and Key Developments

- **Legendre & Gauss – Least Squares (1805–1809):** The method of least squares, fundamental to regression, was first published by Adrien-Marie Legendre in 1805 and later by Carl Friedrich Gauss in 1809​[en.wikipedia.org](https://en.wikipedia.org/wiki/Polynomial_regression#:~:text=squares.%20The%20least,The%20first%20design%20of%20an). It provided a way to find the best-fit curve (or line) by minimizing squared errors. This set the stage for all polynomial regression techniques.
    
- **Early Linear Algebra (19th–20th Century):** Development of matrix theory enabled solving linear systems systematically. Gaussian elimination (Gauss/Jordan) became a standard method for solving $A\mathbf{x}=\mathbf{b}$. By mid-20th century, decompositions were introduced for numerical stability:
    
    - LU decomposition (algorithms by Doolittle, Crout, etc.) to factor matrices into lower and upper triangular form.
        
    - **Householder’s QR (1958):** Alston Householder demonstrated use of orthogonal reflections to safely compute QR factorization​[nhigham.com](https://nhigham.com/2020/09/15/what-is-a-householder-matrix/#:~:text=Householder%20matrices%20for%20computational%20purposes,to%20construct%20the%20QR%20factorization), greatly improving least-squares solution stability.
        
    - **Singular Value Decomposition:** Although the concept of SVD existed in mathematics, an efficient algorithm came in 1965 (Golub & Kahan)​[utminers.utep.edu](https://utminers.utep.edu/xzeng/2017spring_math5330/MATH_5330_Computational_Methods_of_Linear_Algebra_files/ln15.pdf#:~:text=with%20C%20%3D%20AAt,The%20technique%20finds%20U%202), allowing robust solution of linear systems and pseudoinverses.
        
- **Surrogate Modeling Origins:** In engineering and science, using polynomial approximations as “surrogate models” goes back to the 1950s. **Response Surface Methodology** (Box and Wilson, 1951) introduced fitting low-degree polynomials to experimental data to find optimal conditions​[clas.iusb.edu](https://clas.iusb.edu/math-compsci/_prior-proposals/Nbradley_Proposal.pdf#:~:text=history,Moreover). For example, they advocated using first-order (and later second-order) polynomial models to explore processes – an early form of surrogate modeling in the chemical industry.
    
- **Modern HPC Surrogates:** Surrogate models gained traction in computer performance in the 2000s. Notably, **Travis Johnston et al. (2015)** applied polynomial surrogate modeling to tune Hadoop/MapReduce jobs​file-7rhtrwtsjd5w8c8gletf19, demonstrating that a polynomial model could predict job execution time across configurations and yield near-optimal settings with far fewer experiments. In 2016, Johnston and colleagues introduced **HYPPO (Hybrid Piecewise Polynomial Modeling)** to handle non-smooth performance surfaces​file-7rhtrwtsjd5w8c8gletf19 – essentially using multiple polynomial segments to fit complex HPC performance data that a single global polynomial couldn’t capture.
    
- **Continuous Advancements:** The convergence of statistical regression and HPC performance tuning has led to tools that integrate these models into autotuning frameworks. Through the 2010s and 2020s, research by the HPC community (including our lab) has extended surrogate modeling to multi-dimensional parameter spaces and heterogeneous hardware. Our work builds on this foundation by applying polynomial regression surrogates to modern HPC benchmarks and refining techniques to improve accuracy and efficiency.
    

**Speaker Notes:**  
Let’s step back in time. The idea of fitting a model by **least squares** is over two centuries old. Adrien-Marie Legendre published the method in 1805, using it for astronomic and geodetic data, and Carl Gauss also formulated it (famously using it to predict a comet’s orbit) by 1809​[en.wikipedia.org](https://en.wikipedia.org/wiki/Polynomial_regression#:~:text=squares.%20The%20least,The%20first%20design%20of%20an). This was the birth of regression modeling – providing a mathematical way to find the best fitting curve by minimizing the sum of squared deviations. That’s the root of polynomial regression: it’s essentially applying least squares to a polynomial model.

On the linear algebra side, solving linear equations goes even further back (Gauss didn’t have matrices as we know them, but he solved normal equations by elimination). By the late 19th century, mathematicians like Cayley and Sylvester formalized matrix algebra. In the 20th century, we developed systematic methods: **Gaussian elimination** became the go-to for solving systems. In numerical analysis, improvements came to handle stability and efficiency. **LU decomposition** allowed solving systems quickly (once the matrix was factored, many $b$’s could be solved for cheaply). However, for least squares problems, $A^T A$ can be ill-conditioned, so direct LU on $A^T A$ could be unstable. That’s where **QR factorization** comes in – Householder’s 1958 paper introduced the use of orthogonal transformations (now called Householder reflections) to zero out parts of the matrix step by step​[nhigham.com](https://nhigham.com/2020/09/15/what-is-a-householder-matrix/#:~:text=Householder%20matrices%20for%20computational%20purposes,to%20construct%20the%20QR%20factorization). This was a breakthrough for solving least squares reliably. Similarly, the **SVD** – while known theoretically – wasn’t practical until Golub & Kahan’s algorithm in 1965​[utminers.utep.edu](https://utminers.utep.edu/xzeng/2017spring_math5330/MATH_5330_Computational_Methods_of_Linear_Algebra_files/ln15.pdf#:~:text=with%20C%20%3D%20AAt,The%20technique%20finds%20U%202), which made it feasible to compute singular values and vectors for moderately large matrices. These developments in linear algebra were crucial: as datasets got bigger and models more complex, we needed stable algorithms to compute the polynomial fits.

Parallel to these mathematical developments, the concept of **surrogate models** was emerging in experimental sciences. In 1951, statisticians George Box and K. Wilson introduced **Response Surface Methodology**, using polynomial equations as surrogates to guide chemical experiments​[clas.iusb.edu](https://clas.iusb.edu/math-compsci/_prior-proposals/Nbradley_Proposal.pdf#:~:text=history,Moreover). Instead of trying every combination of factors (which could be prohibitively expensive), they would fit a polynomial to a few experiments and use it to predict where optimum conditions might be – this is essentially surrogate modeling: a polynomial proxy for an underlying phenomenon.

Fast forward to recent decades, surrogate modeling has found a home in HPC. Systems and applications have many tunable parameters (thread counts, block sizes, input sizes, etc.), and testing all combinations on a supercomputer is infeasible. In 2015, researchers (Johnston et al.) used polynomial regression to tune MapReduce job configurations​file-7rhtrwtsjd5w8c8gletf19. They showed you can sample a handful of configurations, fit a polynomial model for job runtime, and then use that model to predict the best settings, **saving a ton of time** over brute force search. Building on that, in 2016 the same group tackled the issue that not all performance surfaces are smooth polynomials – sometimes adding more resources can cause sudden drops or plateaus in performance. They developed **HYPPO**, which essentially stitches together multiple polynomial models (piecewise) to better fit “bumpy” performance curves​file-7rhtrwtsjd5w8c8gletf19.

All these efforts lay the groundwork for our work. As hardware and applications evolve (think GPUs, multicore CPUs, etc.), surrogate models remain a powerful idea. The HPC community continues to refine these techniques – for example, integrating surrogate modeling with performance profiling tools, or developing adaptive sampling methods to build better models. In this talk’s context, we leverage this history to apply polynomial regression surrogates to a modern HPC benchmark suite and compare it with other approaches.

## Slide 7: Algorithms – Polynomial Regression via Least Squares

- **Setting up the Equations:** Given $n$ data points $(x_i, y_i)$, fitting a degree $k$ polynomial means finding $a_0,...,a_k$ minimizing $R^2 = \sum_{i=1}^n [y_i - (a_0 + a_1 x_i + \dots + a_k x_i^k)]^2$. Setting the derivative $\partial R^2/\partial a_j = 0$ for each coefficient yields the **normal equations**​[mathworld.wolfram.com](https://mathworld.wolfram.com/LeastSquaresFittingPolynomial.html#:~:text=The%20partial%20derivatives%20,are)​[mathworld.wolfram.com](https://mathworld.wolfram.com/LeastSquaresFittingPolynomial.html#:~:text=These%20lead%20to%20the%20equations) – a linear system:
    
![[Pasted image 20250411170121.png]]

