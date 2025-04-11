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