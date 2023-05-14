# Plasmatorch-LR


# # Electromagnetic field model in high-frequency plasmatron
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
