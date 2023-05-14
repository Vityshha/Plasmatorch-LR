# Plasmatorch-LR

This Python code uses the sweep method to solve the electrodynamic equation for the plasma torch model. The Plasmatron class is used to set the parameters of the model, and the sweep method is used to solve the equation. The DataExploration class is used to build dependency graphs,
and the LRModel class is used to initialize the linear regression model.

## Requirements

- os
- numpy
- pandas
- matplotlib
- seaborn
- sklearn
- joblib

## Plasmatron class:

The Plasmatron class is used to set the parameters of the plasma torch model. In the **__init__** method, the default values of the model parameters are initialized: the radius of the plasma torch R, the magnetic field at the end H_R, the number of steps N, the step h, the initial conductivity value sigma_start, the final conductivity value sigma_end and the conductivity step sigma_step,
the initial value of the electric field E_start, the final value of the electric field E_end and the electric field step E_step. 

The **sweep** method is used to solve the electrodynamics equation for the plasma torch model. This method takes the values sigma, N, R, h, E, and H_R as arguments, which correspond to the model parameters. The method returns the H and r values.

The **Computingdata** method is used to calculate data. If the data.xlsx file already exists, the method loads its contents into the DataFrame df. Otherwise, the method calculates H, r, E, and sigma for each combination of sigma and E parameters and saves the results to the data.xlsx file. The method returns DataFrame df.

## DataExploration class

The **DataExploration** class is used to build dependency graphs. In the __init__ method of the class, the DataFrame df is initialized. The charts method is used to build dependency graphs between all feature pairs in a df.

## LRModel class

The class implements linear regression and polynomial regression. You can get the metrics of each model and see the optimal degree of the polynomial. Implemented a check, if the model is trained, then the model is simply loaded and not retrained.



## Electromagnetic field model in high-frequency plasmatron
To model the electrical parameters of a high-frequency plasma torch, we write down the Maxwell equation. The complex form of the Maxwell equation in one dimension is given by
<p style="text-align: center;">
$$\Large\frac{d\dot{H}}{dr}=(\sigma + i\epsilon_0\epsilon)\dot{E}$$
</p>
Applying the complex amplitude method to this:
<p style="text-align: center;">
$$\Large\dot{H}=H\exp(iωt+ψ_H)$$
</p>
Getting the equation:
<p style="text-align: center;">
$$\Large\frac{1}{r}\frac{d}{dr}(\frac{r}{σ}\frac{dH^2}{dr})=2σE^2$$
</p>
Boundary conditions are presented in the following form:
<p style="text-align: center;">
$$\Large\frac{dH^2}{dr}(0)=0$$
$$\LargeH^2(R)=H_R^2$$
</p>
Let us write the equation in a general form:
<p style="text-align: center;">
$$\Large\frac{d}{dr}(rV\frac{dy}{dr})=rf$$
</p>
And we will develop a numerical scheme for it. We will approximate the coefficients r and V at points shifted by h/2 to achieve an accuracy of O(h^2) for the difference scheme. We will write the equation in the difference form:
<p style="text-align: center;">
$$\Large r_i^{-}V_i^{-}y_{i-1}-(r_i^{-}V_i^{-}+r_i^{+}V_i^{+})y_i+r_i^{+}V_i^{+}y_{i+1}=-(-r_if_ih^2)$$
</p>
Where
<p style="text-align: center;">
$$\Large r_i^{-}=r_i-\frac{h}{2}$$
</p>
<p style="text-align: center;">
$$\Large r_i^{+}=r_i+\frac{h}{2}$$
</p>
General form of the sweep method:
<p style="text-align: center;">
$$\Large A_i y_{i-1}-C_i y_i + B_i y_{i+1}=-F_i$$
</p>
Then the coefficients of the difference scheme take the following form:
<p style="text-align: center;">
$$\Large A_i= r_i V_i^{-}$$
</p>
<p style="text-align: center;">
$$\Large B_i= r_i^{+} V_i^{+}$$
</p>
<p style="text-align: center;">
$$\Large C_i= r_i^{-} V_i^{-} + r_i^{+} V_i^{+}$$
</p>
<p style="text-align: center;">
$$\Large F_i= -r_i f_ih^2$$
</p>
Progonic coefficients take the form:
<p style="text-align: center;">
$$\Large α_i= \frac{A_i}{C_i-α_{i+1}B_i}$$
</p>
<p style="text-align: center;">
$$\Large β_i= \frac{B_iβ_{i+1}+F_i}{C_i-α_{i+1}B_i}$$
</p>
<p style="text-align: center;">
$$\Large i=N-1,...,1$$
</p>
<p style="text-align: center;">
$$\Large y_0=\frac{µ_1+k_1 β_1}{1-α_1 k_1}$$
</p>
Where µ and κ are the coefficients obtained by approximating the boundary condition in the form of:
<p style="text-align: center;">
$$\Large y_0=k_1 y_1+µ_1$$
</p>
Then:
<p style="text-align: center;">
$$\Large V=\frac{1}{σ}, f_i=2σE^2, F_i=-r_i 2σE^2 h^2$$
</p>
