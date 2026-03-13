# FAST AND ACCURATE SABR CALIBRATION FOR AAPL OPTIONS: A HYBRID OPTIMIZATION APPROACH 


**Author:** PRATIT GOSWAMI

## 1. Introduction

Volatility modeling plays a central role in derivatives pricing, risk management, and quantitative trading. While the Black–Scholes model assumes constant volatility, real markets exhibit volatility smiles and skews that vary with strike and maturity. The SABR (Stochastic Alpha, Beta, Rho) model is widely used in equity, currency, and rates markets to describe these dynamics by introducing stochastic volatility and a log-normal leverage structure.

This project focuses on calibrating the SABR model to market option data for Apple Inc. (AAPL), evaluating calibration accuracy and computational efficiency across three optimization approaches:

1. L-BFGS-B  
2. Differential Evolution  
3. Hybrid Method (Differential Evolution → L-BFGS-B)

The objective is to balance speed (calibration runtime) and fit quality (RMSE error between model and market implied volatilities), and to visualize both single-expiry smile fits and a multi-expiry 3D volatility surface. AAPL option chain data is automatically downloaded through the Yahoo Finance API.

---

## 2. SABR Model and Calibration

The SABR model specifies forward rate dynamics:

$$dF_t = {\alpha_t} F_t{^\beta} dW_t, \hspace{1cm} {d\alpha_t} = {\nu} {\alpha_t} {dZ_t,} \hspace{1cm} dW_t d{Z_t} = {\rho} dt$$ 

where $\alpha$ (volatility level), $\beta$ (elasticity parameter), $\rho$ (correlation), and $\nu$ (volatility of volatility) are calibrated. Here $F_t$ stands for forward price or underlying asset price, $\alpha_t$ means instantaneous volatility of F_t and {W_t, Z_t} are Brownian motions.

The Hagan (2002) approximation is used to compute implied volatility efficiently.

Calibration minimizes the Root Mean Square Error (RMSE) between model and market implied volatilities:

$$RMSE = \sqrt{\frac{1}{N} \sum_{i=1}^N (\sigma_{model}(K_i)) - (\sigma_{market}(K_i))^2} $$.

---

## 3. Methodology and Results

The calibration is repeated under the three methods (L-BFGS-B, Differential Evolution, Hybrid (DE → L-BFGS-B)), measuring: RMSE (model fit error), computation time.

All three methods successfully calibrate the SABR parameters, but with different performance profiles:

• L-BFGS-B is fast but sometimes lands in suboptimal minima,  
• Differential Evolution is more robust but slower,  
• Hybrid DE → L-BFGS-B achieves the best trade-off, producing: lowest RMSE, good computational efficiency, smooth smile fit across strikes.

The Speed vs Accuracy scatter plot visually confirms this relationship and a 3D surface plot of strike × expiry × implied volatility compares market surface with the SABR-generated surface, showing strong agreement across maturities.

---

## 4. Conclusion

This project demonstrates:

• how to retrieve real market option data,  
• how to compute market implied volatilities,  
• how to calibrate the SABR model effectively,  
• how optimization choice impacts calibration performance.

The Hybrid DE → L-BFGS-B method proves to be the most effective approach for SABR calibration, offering a strong balance of global robustness and local precision.
