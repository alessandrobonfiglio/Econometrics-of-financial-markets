# Econometrics of Financial Markets

Gretl code for my final project in Econometrics of Financial Markets (MSc Applied Economics, University of Bologna, October 2025). The project is split into three exercises, one script each.

## Files

- `Esame esercizio 1.inp`: univariate volatility models (ARCH, GARCH, GARCH with t errors, EWMA)
- `Esame esercizio 2.inp`: multivariate models (EWMA, DCC, BEKK) on three assets
- `Esame esercizio 3.inp`: VAR and structural VAR on oil, inflation and growth
- `Report.pdf`: written analysis with all tables and figures
- `Bonfiglio_Alessandro.xlsx`: dataset used in all three exercises

## Requirements

You need Gretl and four function packages, which you can install from File > Function packages > On server: `gig`, `DCC`, `BEKK` and `SVAR`.

All scripts read data from `Bonfiglio_Alessandro.xlsx` (sheet `Foglio1` for exercise 1, `Foglio2` for exercise 2, `Foglio3` for exercise 3). Before running, change the `set workdir` line at the top of each script to the folder where you downloaded the repository. All results, with tables and figures, are in `Report.pdf`.

## Exercise 1

Starting from a log price series, I compute returns and check the usual stylized facts: no autocorrelation in returns, strong autocorrelation in squared returns, fat tails. An ARCH-LM test computed by hand confirms conditional heteroskedasticity.

I then estimate an ARCH(1), a GARCH(1,1) and a GARCH(1,1) with Student-t errors (using the `gig` package), and use an EWMA with λ = 0.94 as a benchmark. ARCH(1) leaves dependence in the squared residuals, while GARCH(1,1) removes it. Persistence is around 0.92 in both GARCH versions. The t distribution improves the log-likelihood (from 813 to 955, with about 7 degrees of freedom). The models are compared with QLIKE and MSE.

## Exercise 2

Three daily price series from 2012 to 2020. After the diagnostics, I build a multivariate EWMA to get time-varying volatilities and correlations, then estimate univariate GARCH(1,1) models followed by a scalar DCC, and finally a BEKK with a VAR(4) in the mean.

Correlations rise sharply in stress periods, especially in 2020. In the DCC both parameters are significant (a ≈ 0.06, b ≈ 0.78). The BEKK residuals have no autocorrelation of their own, but the Ljung-Box tests on their cross-products reject strongly, which suggests spillovers between the three series.

## Exercise 3

Monthly data on oil prices, inflation and growth (1973-2006). BIC and HQC select a VAR(1). I check the residuals for autocorrelation, ARCH effects and normality, then identify the structural shocks in two ways: a Cholesky decomposition with ordering oil, inflation, growth, and an AB model where only some contemporaneous links are restricted. IRFs come with 68% bootstrap bands.

An oil shock raises inflation on impact and lowers growth in the short run, and both effects die out within a few periods. The AB model gives similar results, with the oil-inflation link as the only significant contemporaneous relationship.
