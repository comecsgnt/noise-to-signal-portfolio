# References

Papers used as theoretical foundations for this project.

---

**Marchenko, V. A., & Pastur, L. A. (1967)**
*Distribution of Eigenvalues for Some Sets of Random Matrices.*
Mathematics of the USSR-Sbornik, 1(4), 457–483.
— Foundational result establishing the Marchenko–Pastur law for the eigenvalue distribution of large random matrices. Provides the theoretical basis for identifying noise eigenvalues in empirical covariance matrices.

---

**Laloux, L., Cizeau, P., Bouchaud, J. P., & Potters, M. (1999)**
*Noise Dressing of Financial Correlation Matrices.*
Physical Review Letters, 83(7), 1467–1470.
— First application of Random Matrix Theory to financial correlation matrices. Shows that most empirical eigenvalues of stock return covariance matrices are consistent with pure noise, motivating eigenvalue cleaning for portfolio optimization.

---

**Ledoit, O., & Wolf, M. (2004)**
*A Well-Conditioned Estimator for Large-Dimensional Covariance Matrices.*
Journal of Multivariate Analysis, 88(2), 365–411.
— Introduces the Ledoit–Wolf linear shrinkage estimator, which produces a well-conditioned covariance matrix by optimally combining the sample covariance with a structured target. Used as the LW estimator throughout this project.

---

**Markowitz, H. (1952)**
*Portfolio Selection.*
Journal of Finance, 7(1), 77–91.
— Seminal paper introducing mean-variance optimization and the efficient frontier. The Global Minimum Variance (GMV) portfolio used in this project is a direct application of Markowitz's framework.

---

**Scherer, B. (2007)**
*Can Robust Portfolio Optimisation Help to Build Better Portfolios?*
Journal of Asset Management, 7(6), 374–387.
— Proposes the robust mean–variance objective used in this project, penalizing portfolios that are overly sensitive to estimation errors in expected returns via an ellipsoidal uncertainty set.

---

**Bongiorno, C., Challet, D., & Loeper, G. (2023)**
*Filtering Time-Dependent Covariance Matrices Using Time-Independent Eigenvalues.*
Journal of Statistical Mechanics: Theory and Experiment, 2023(2), 023402.
— Introduces the Average Oracle (AO) estimator, which fixes eigenvectors from the full-sample covariance while averaging eigenvalues across rolling windows. Directly related to the dynamic covariance content of the course.
