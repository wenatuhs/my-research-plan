# Research Plan []{#theme-switch .fas .h1-icon} []{#scale-switch .fas .h1-icon}

==Updated: Dec 6, 2023 by [Zhe Zhang](https://zhezhang.info/resume/)==

*[SPEAR3]: Stanford Positron Electron Asymmetric Ring
*[LCLS]: Linac Coherent Light Source
*[RA]: Research Associate
*[SLAC]: SLAC National Accelerator Laboratory
*[ML]: Machine Learning
*[DL]: Deep Learning
*[ANN]: Artificial Neural Network
*[RL]: Reinforcement Learning
*[MLI]: Machine Learning Initiative
*[BBO]: Beam-based Online Optimization
*[ANL]: Argonne National Laboratory
*[BNL]: Brookhaven National Laboratory
*[ACR]: Accelerator Control Room
*[BO]: Bayesian Optimization
*[GP]: Gaussian Process
*[GAs]: Genetic Algorithms
*[RTC]: Real-time Communication
*[MLST]: Machine Learning: Science and Technology
*[PRAB]: Physical Review Accelerators and Beams
*[IPAC]: International Particle Accelerator Conference
*[ICML]: International Conference on Machine Learning
*[NeurIPS]: Neural Information Processing Systems
*[NIM A]: Nuclear Instruments and Methods in Physics Research Section A
*[RF]: Radio Frequency
*[BPM]: Beam Position Monitor
*[UED]: Ultrafast Electron Diffraction
*[DA-MA]: Dynamic Aperture and Momentum Aperture
*[BAX]: Bayesian Algorithm Execution
*[SIREN]: Sinusoidal Representation Networks

I served as a RA under the guidance of Dr. Xiaobiao Huang at SPEAR3 from 2019 to 2021. Currently, I hold the position of Data/ML Engineer under the supervision of Dr. Daniel Ratner at MLI in SLAC. Throughout my time at SPEAR3 and MLI, I actively contributed to diverse projects encompassing online optimization algorithms/frameworks and general machine learning applications.

## Summary of Previous and Ongoing Research Works

### MG-GPO

I initiated my optimization algorithm research by co-developing MG-GPO[^MGGPO], an innovative algorithm that merges genetic operations (mutation, crossover, and flock) with GP. MG-GPO demonstrates significantly improved sampling efficiency, crucial for online optimization scenarios where each machine acquisition is time-consuming. In comparison to traditional GAs like NSGA-II and PSO, MG-GPO excels in performance. Notably, it eliminates the need to optimize a non-convex acquisition function in each iteration, a typical requirement in GP algorithms. Successful applications of MG-GPO include addressing real-life accelerator tuning challenges at SLAC[^MGGPO-MLST] and BNL.

### Teeport

In addressing a common challenge in online optimization research — where optimization algorithms and problems often exist in different languages or demand specific resources, hindering seamless communication, I developed [Teeport](https://teeport.info/intro/), an RTC-based online optimization platform[^Teeport]. Teeport facilitates integration by offering adapters for various programming languages, allowing any algorithm or problem to be easily standardized and incorporated into the platform. This enables the creation of optimization tasks by specifying the algorithm and problem, with Teeport serving as an intermediary for data flow, monitoring, and control. Teeport functions both as a local package and a cloud-hosted service, supporting remote collaboration on optimizations. Successfully applied at SLAC and ANL, Teeport has demonstrated efficacy in performing, monitoring, benchmarking, and enhancing optimization algorithms.

### Badger

Teeport excels in remote optimizations and algorithm benchmarking, but for the daily tuning needs of ACR operators and the flexible requirements of accelerator physicists, I led the design and development of [Badger](https://slaclab.github.io/Badger/). Badger, an in-ACR optimization framework, boasts a versatile plugin system for high extensibility. Users can effortlessly integrate algorithms[^Xopt], optimization environments, and machine interfaces as plugins, tailoring Badger to their specific needs. The framework offers multiple modes, serving as a standard Python package for regular optimizations, a command line tool for no-monitor scenarios, and a GUI-enabled platform for operators to effortlessly create and monitor routines with just a few clicks[^Badger].

### RCDS-S

Thanks to the extensibility of Teeport and Badger, we successfully integrated classic optimization algorithms like Simplex and BO into the frameworks, applying them in daily accelerator operations. However, addressing optimization challenges in the accelerator field often demands the design of new algorithms due to the complexity of these large machines. I spearheaded the development of an online safety tuning algorithm, later named RCDS-S[^RCDS-S]. This algorithm is based on RCDS[^RCDS] adeptly tracks drifting trends and ensures the machine remains locked to its optimal working point without violating safety constraints set by operators. Proven effective for regular noisy drift real-life problems, RCDS-S operates safely, provided the system drift remains within acceptable limits compared to the noise level within one optimization iteration in RCDS-S.

### General ML stuff

In addition to the aforementioned work, I contributed to the development and benchmarking of CoAD, a DL-based anomaly detection algorithm. CoAD analyzes multiple channels of data, assessing a covariance-like metric among them to enhance the metric by updating the weights of each channel's processing model. Applied to real-life data, including RF and BPM data from LCLS, CoAD effectively auto-labels suspicious events. My contributions extend to a series of Machine Learning applications in UED auto-tuning[^UED1][^UED2]. Currently, I am actively engaged in a project involving user-side signal optimization with accelerator-side tuning knobs, as well as the development of an RL-based efficient optimization algorithm designed to learn the optimal policy for deterministic optimization problems[^DOP].

## Plan of Future Research Work

### Badger x Teeport

In my upcoming research, I aim to integrate the Badger and Teeport optimization frameworks to create a unified platform supporting cross-language plugins, remote optimization, multiple modes, and flexible extensibility.

### Continue with online optimization algorithm development

I'll continue to put effort into developing highly efficient, noise/drift-resistant optimization algorithms, potentially leveraging DL or GP models. One such example is an ongoing project, the learned policy optimization method that was introduced in the [previous section](#general-ml-stuff)[^SSP].

### Dynamic tuning range adaption

Addressing a common challenge in online tuning, determining optimal ranges for tuning knobs poses a dilemma. A range that is too small may not yield substantial improvements, while one that is too large risks triggering a beam trip. Exploring a solution to dynamically expand or shrink variable ranges during optimization could offer a safer and more efficient approach, eliminating the need for manual determination.

### CoAD improvements

For CoAD, I'd like to make further improvements include enhancing its internal structure using PyTorch Lightning for seamless computing resource management, and refining APIs for a smoother user experience. Additionally, we've identified potential applications for CoAD in real-life cases, such as dark matter detector data, offering exciting prospects.

### BAX and SIREN applications

Exploring advanced ML techniques in specific scenarios is another avenue, considering the application of the BAX[^BAX] framework for increased sampling efficiency in DA-MA optimization in storage rings. Another intriguing prospect involves leveraging SIREN[^SIREN], a powerful ANN architecture, in neutrino detector data processing and analysis for enhanced inference capabilities, such as more inferable information or higher resolution.

[^Teeport]: **Zhang, Z.**, Huang, X. and Song, M., 2021. [Teeport: break the wall between the optimization algorithms and problems](https://doi.org/10.3389/fdata.2021.734650), *Frontiers in big Data*
[^Badger]: **Zhang, Z.**, Edelen, A.L., Garrahan, J.R., Hidaka, Y., Mayes, C.E., Miskovich, S.A., Ratner, D.F., Roussel, R.J., Shtalenkova, J., Tomin, S. and Wang, G.M., 2022. [Badger: The missing optimizer in ACR](https://doi.org/10.18429/JACoW-IPAC2022-TUPOST058), *IPAC'22*
[^Xopt]: Through the optimization engine of Badger, [Xopt](https://github.com/ChristopherMayes/Xopt).
[^RCDS]: Huang, X., Corbett, J., Safranek, J. and Wu, J., 2013. [An algorithm for online optimization of accelerators](https://doi.org/10.1016/j.nima.2013.05.046), *NIM A*
[^RCDS-S]: **Zhang, Z.**, Song, M. and Huang, X., 2022. [An optimization method to compensate accelerator performance drifts](https://journals.aps.org/prab/abstract/10.1103/PhysRevAccelBeams.25.122801), *PRAB*
[^MGGPO]: Huang, X., **Zhang, Z.** and Song, M., 2021. [Multi-objective multi-generation Gaussian process optimizer](https://doi.org/10.18429/JACoW-IPAC2021-WEPAB304), *IPAC'21*
[^MGGPO-MLST]: **Zhang, Z.**, Song, M. and Huang, X., 2020. [Online accelerator optimization with a machine learning-based stochastic algorithm](https://doi.org/10.1088/2632-2153/abc81e), *MLST*
[^UED1]: **Zhang, Z.**, Yang, X., Huang, X., Li, J., Shaftan, T., Smaluk, V., Song, M., Wan, W., Wu, L. and Zhu, Y., 2021. [Accurate prediction of mega-electron-volt electron beam properties from UED using machine learning](https://doi.org/10.1038/s41598-021-93341-2), *Scientific Reports*
[^UED2]: **Zhang, Z.**, Yang, X., Huang, X., Shaftan, T., Smaluk, V., Song, M., Wan, W., Wu, L. and Zhu, Y., 2022. [Toward fully automated UED operation using two-stage machine learning model](https://doi.org/10.1038/s41598-022-08260-7), *Scientific Reports*
[^DOP]: Deterministic optimization problem here means that, assuming a maximization problem, given a system state $\mathbf{S}$, the optimal action that maximize the reward $r$: $\mathbf{A_{opt}} = \argmax_{\mathbf{A} | \mathbf{S}}r(\mathbf{S}, \mathbf{A})$, is solely a function of $\mathbf{S}$.
[^SSP]: The method utilizes an ANN to directly learn the optimal action for tuning the machine to its optimal state. Following training with a few thousand random initial machine states, the model can swiftly propose the optimal solution for the current machine state within a single step. This approach achieves remarkable speed, several orders of magnitude faster than classic local optimization methods, which typically require hundreds or thousands of steps to converge.
[^BAX]: Neiswanger, W., Wang, K.A. and Ermon, S., 2021. [Bayesian algorithm execution: Estimating computable properties of black-box functions using mutual information](https://doi.org/10.48550/arXiv.2104.09460), *ICML'21*
[^SIREN]: Sitzmann, V., Martel, J., Bergman, A., Lindell, D. and Wetzstein, G., 2020. [Implicit neural representations with periodic activation functions](https://doi.org/10.48550/arXiv.2006.09661), *NeurIPS'20*
