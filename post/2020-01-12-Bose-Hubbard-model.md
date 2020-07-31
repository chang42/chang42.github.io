# Bose-Hubbard model  
## Second quantization [1]
In schrodinger equation, the Hamiltonian can be written as the form of  
$$
H=\sum_{k=1}^{N} T\left(x_{k}\right)+\frac{1}{2} \sum_{k\neq l=1}^{N} V\left(x_{k}, x_{l}\right)
$$
where $T$ is the kinetic energy and $V$ is the potential energy of interaction between the particles. $x_{k}$ denotes the coordinates of the $k$th particle. The factor of $1/2$ subtracts double counts of the summation. The time-dependent Schrodinger equation is given by  
$$
i \hbar \frac{\partial}{\partial t} \Psi\left(x_{1} \cdots x_{N}, t\right)=H \Psi\left(x_{1} \cdots x_{N}, t\right)
$$
Expanding many particle wave function $\Psi$ in a complete set of time-independent single particle wave functions  
$$
\Psi\left(x_{1} \cdots x_{N}, t\right)=\sum_{E_{1}^{\prime} \cdots E_{N}^{\prime}} C\left(E_{1}^{\prime} \cdots E_{N}^{\prime},t\right) \psi_{E_{1}^{\prime}}\left(x_{1}\right) \cdots \psi_{E_{N}^{\prime}}\left(x_{\mathrm{N}}\right)
$$
where $E_{k}$ represents a complete set of a single particle quantum numbers. $C(E_{1}\cdots E_{N},t)$ is a time dependence coefficient. Inserting it into the Schrodinger equation, and then multiplying by the expression $\psi_{E_{1}}(x_{1})^{\dagger}\cdots\psi_{E_{N}}(x_{N})^{\dagger}$, after integrating over all the appropriate coordinates, the left hand side is given by  
$$
\begin{aligned}
i \hbar \frac{\partial}{\partial t} C\left(E_{1}\right.&\left.\cdots E_{N}, t\right)=\sum_{k=1}^{N} \sum_{W} \int d x_{k} \psi_{E_{k}}\left(x_{k}\right)^{\dagger} T\left(x_{k}\right) \psi_{W}\left(x_{k}\right) \\
& \times C\left(E_{1} \cdots \cdot E_{k-1} W E_{k+1} \cdots E_{N}, t\right) \\
&+\frac{1}{2} \sum_{k \neq l=1}^{N} \sum_{W} \sum_{W^{\prime}} \iint d x_{k} d x_{l} \psi_{E_{k}}\left(x_{k}\right)^{\dagger} \psi_{E_{l}}\left(x_{l}\right)^{\dagger} \\
& \times V\left(x_{k}, x_{l}\right) \psi_{W}\left(x_{k}\right) \psi_{W^{\prime}}\left(x_{l}\right) \\
& \times C\left(E_{1} \cdots \cdot E_{k-1} W E_{k+1} \cdots \cdot E_{l-1} W^{\prime} E_{l+1} \cdots \cdot E_{N}, t\right)
\end{aligned}
$$
The kinetic energy is a single particle operator only change one of the single particle wave functions. While the potential energy involves the coordinates of two particles, it can change the wave functions of two particles. Considering the statistical properties of particles, the many particle wave function is either symmetric (bosons) or antisymmetric (fermions) under the exchange of particles  
$$
\Psi(\cdots x_{i}\cdots x_{j}\cdots, t)=\pm\Psi(\cdots x_{j}\cdots x_{i}\cdots,t)
$$
and so does the expansion coefficients
$$
C(\cdots E_{i}\cdots E_{j}\cdots,t)=\pm C(\cdots E_{j}\cdots E_{i}\cdots,t)
$$
The symmetry property of bosons under interchange of quantum numbers allows us to regroup the quantum numbers appearing in any coefficient.  
$$
C(121324\cdots,t)=C(\underbrace{111\cdots}_{n_{1}}\ \underbrace{222\cdots}_{n_{2}}\ \cdots,t)
$$
The normalization property of the many particle wave function yields a corresponding condition on the expansion coefficients  
$$
\int|\Psi|^{2}d\tau=1\quad\Rightarrow\quad\sum_{E_{1}\cdots E_{N}}|C(E_{1}\cdots E_{N})|^{2}=1
$$
Rewriting the coefficient with two part, one is sum over all values of the quantum numbers $E_{1}E_{2}\cdots E_{N}$ consistent with the given set of occupation numbers ($n_{1}n_{2}n_{3}\cdots n_{\infty}$), which equals to the problem of putting $N$ objects into boxes with $n_{1}$ objects
in the first box, $n_{2}$ objects in the second box, and so on, which can be done in $N!/n_{1}!n_{2}!\cdots n_{\infty}!$ ways. Another is sum over all sets of occupation numbers.  
$$
\sum_{n_{1}n_{2}n_{3}\cdots n_{\infty}}|\bar{C}(n_{1}n_{2}\cdots n_{\infty})|^{2}\sum_{\substack{E_{1}\cdots E_{N}\\(n_{1}n_{2}n_{3}\cdots n_{\infty})}}1=\sum_{n_{1}n_{2}n_{3}\cdots n_{\infty}}|\bar{C}(n_{1}n_{2}\cdots n_{\infty})|^{2}\frac{N!}{n_{1}!n_{2}!\cdots n_{\infty}!}=1
$$
We define a new coefficient, which can be seen later, specifying the connection between first and second quantization  
$$
f(n_{1}n_{2}n_{3}\cdots n_{\infty},t)\equiv\left(\frac{N!}{n_{1}!n_{2}!n_{3}!\cdots n_{\infty}!}\right)\bar{C}(n_{1}n_{2}n_{3}\cdots n_{\infty},t)
$$
The original wave function can now be rewritten as follows:  
$$
\begin{aligned}
\Psi\left(x_{1} \cdots x_{N}, t\right)=& \sum_{E_{1}\cdots E_{N}} C\left(E_{1} \cdots E_{N}, t\right) \psi_{E_{1}}\left(x_{1}\right) \cdots \psi_{E_{N}}\left(x_{N}\right) \\
=& \sum_{E_{1}\cdots E_{N}} \bar{C}\left(n_{1} n_{2} \cdots n_{x}, t\right) \psi_{E_{1}}\left(x_{1}\right) \cdots\psi_{E_{N}}\left(x_{N}\right) \\
=& \sum_{n_{1} n_{2}\cdots n_{\infty}} f\left(n_{1} n_{2} \cdots n_{\infty}, t\right)\left(\frac{n_{1} ! n_{2} ! \cdots n_{\infty} !}{N !}\right)^{\frac{1}{2}}\sum_{\substack{E_{1}\cdots E_{N}\\(n_{1}n_{2}\cdots n_{\infty})}}\psi_{E_{1}}\left(x_{1}\right)\cdots\psi_{E_{N}}\left(x_{N}\right) \\
=& \sum_{\substack{n_{1} n_{2}\cdots n_{\infty}\\\left(\sum_{i}n_{i}=N\right)}} f\left(n_{1} n_{2} \cdots n_{\infty}, t\right)\Phi_{n_{1} n_{2}} \cdots n_{\infty}\left(x_{1} x_{2} \cdots x_{N}\right)
\end{aligned}
$$
where  
$$
\Phi_{n_{1}n_{2}n_{3}\cdots n_{\infty}}(x_{1}\cdots x_{N})\equiv \left(\frac{n_{1} ! n_{2} ! \cdots n_{\infty} !}{N !}\right)^{\frac{1}{2}}\sum_{\substack{E_{1}\cdots E_{N}\\(n_{1}n_{2}\cdots n_{\infty})}}\psi_{E_{1}}\left(x_{1}\right)\cdots\psi_{E_{N}}\left(x_{N}\right) 
$$
with the properties of  
$$
\Phi\left(\cdots x_{1} \cdots x_{j} \cdots\right)=\Phi\left(\cdots x_{j} \cdots x_{1} \cdots\right)
$$
$$
\int d x_{1} \cdots d x_{N} \Phi_{n_{1}^{\prime} n_{2}^{\prime}\cdots n_{\infty}^{\prime}}\left(x_{1} \cdots x_{N}\right)^{\dagger} \Phi_{n_{1} n_{2}\cdots n_{\infty}} \left(x_{1} \cdots x_{N}\right)=\delta_{n_{1}^{\prime} n_{1}} \cdots \delta_{n_{\infty}^{\prime} n_{\infty}}
$$
Considering the kinetic energy term, it is obvious that the quantum number $E_{k}$ occurs one less time and the quantum number $W$ occurs one more time. In the next, instead of performing a sum over $k$ from 1 to $N$, we can equally well sum over $E$, a sum over particles is equivalent to a sum over states and the equation becomes  
$$
\begin{aligned}
\sum_{k=1}^{N} \sum_{W}\left\langle E_{k}|T| W\right\rangle & C\left(E_{1} \cdots E_{k-1} W E_{k+1} \cdots E_{N}, t\right) \\
=& \sum_{E} \sum_{W}\langle E|T| W\rangle n_{E}\bar{C}\left(n_{1} n_{2} \cdots n_{E}-1 \cdots n_{W}+1 \cdots n_{\infty}, t\right)\\
=& \sum_{i} \sum_{j}\langle i|T| j\rangle n_{i}\bar{C}\left(n_{1} n_{2} \cdots n_{i}-1 \cdots n_{j}+1 \cdots n_{\infty}, t\right)
\end{aligned}
$$
Exactly the same manipulations apply to the potential energy term:  
$$
\begin{aligned}
&\frac{1}{2} \sum_{k\neq l=1} \sum_{W} \sum_{W^{\prime}} E_{k} E_{l}|V| W W^{\prime} C\left(E_{1} \cdots E_{k-1} W E_{k+1} \cdots E_{l-1} W^{\prime} E_{l+1} \cdots E_{N}, t\right)\\
=&\sum_{E}\sum_{E^{\prime}}\sum_{W}\sum_{W^{\prime}}\frac{1}{2}n_{E}(n_{E^{\prime}}-\delta_{EE^{\prime}})\langle EE^{\prime}|V|WW^{\prime}\rangle\\
&\times\bar{C}(n_{1}\cdots n_{E}-1\cdots n_{W}+1\cdots n_{E^{\prime}}-1\cdots n_{W^{\prime}}+1\cdots n_{\infty},t)\\
=&\sum_{i}\sum_{j}\sum{k}\sum_{l}\frac{1}{2}n_{i}(n_{i}-\delta_{ij})\langle ij|V|kl\rangle\\
&\times\bar{C}(n_{1}\cdots n_{i}-1\cdots n_{k}+1\cdots n_{j}-1\cdots n_{l}+1\cdots n_{\infty},t)
\end{aligned}
$$
Taking the coefficient $f$ into above equation, and multiplying the factor $(N!/n_{1}!n_{2}!\cdots n_{\infty})^{1/2}$, we arrive at the following set of coupled differential equations  
$$
\begin{aligned}
i \hbar \frac{\partial}{\partial t} f\left(n_{1} \cdots n_{\infty}, t\right)&=\sum_{i}\langle i|T| i\rangle n_{i} f\left(n_{1} \cdots n_{i} \cdots n_{\infty}, t\right) \\
&+\sum_{i \neq j}\langle i|T| j\rangle\left(n_{i}\right)^{1/2}\left(n_{j}+1\right)^{1/2} f\left(n_{1}\cdots n_{i}-1 \cdots n_{j}+1 \cdots n_{\infty}, t\right) \\
&+\sum_{i \neq j \neq k \neq l}\langle i j|V| k l\rangle \frac{1}{2}\left(n_{i}\right)^{1/2}\left(n_{j}\right)^{1/2}\left(n_{k}+1\right)^{1/2}\left(n_{l}+1\right)^{1/2} \\
& \times f\left(n_{1} \cdots n_{i}-1 \cdots n_{j}-1 \cdots n_{k}+1 \cdots n_{i}+1 \cdots n_{\infty}, t\right) \\
&+\sum_{i=j \neq k \neq l}\langle i i|V| k l\rangle \frac{1}{2}(n_{i})^{1/2}\left(n_{i}-1\right)^{1/2}\left(n_{k}+1\right)^{1/2}\left(n_{l}+1\right)^{1/2} \\
& \times f\left(n_{1} \cdots n_{i}-2 \cdots n_{k}+1 \cdots n_{i}+1 \cdots n_{\infty}, t\right)+\text { etc. }
\end{aligned}
$$
We introduce the creation and annihilation operator $b_{k}$, $b_{k}^{\dagger}$ of bosons with properties of  
$$
\begin{aligned}
&[b_{k},b_{k^{\prime}}^{\dagger}]=\delta_{kk^{\prime}},\quad [b_{k},b_{k^{\prime}}]=[b_{k}^{\dagger},b_{k^{\prime}}^{\dagger}]=0\\
b_{k}\left|n_{k}\right\rangle &=\left(n_{k}\right)^{1/2}\left|n_{k}-1\right\rangle,\quad b_{k}^{\dagger}\left|n_{k}\right\rangle =\left(n_{k}+1\right)^{1/2}\left|n_{k}+1\right\rangle\\
&b_{k}^{\dagger} b_{k}\left|n_{k}\right\rangle = n_{k}\left|n_{k}\right\rangle, \quad n_{k}=0,1,2, \cdots, \infty
\end{aligned}
$$
Rewrite the many particle wave function in the basis of occupation number states  
$$
|\Psi(t)\rangle=\sum_{n_{1}n_{2}\cdots n_{\infty}}f(n_{1}n_{2}\cdots n_{\infty},t)|n_{1}n_{2}\cdots n_{\infty}\rangle
$$
Taken into the Schrodinger equation  
$$
\begin{aligned}
i \hbar \frac{\partial}{\partial t}|\Psi(t)\rangle=&\sum_{n_{1} n_{2}\cdots n_{\infty}} i \hbar \frac{\partial}{\partial t} f\left(n_{1} n_{2} \cdots n_{\infty}, t\right)\left|n_{1} n_{2} \cdots n_{\infty}\right\rangle\\
=&\cdots +\sum_{\substack{n_{1} n_{2}\cdots n_{\infty}\\(\sum_{i}n_{i}=N)}}\sum_{i\neq j}\langle i|T|j\rangle f(\cdots n_{i}-1\cdots n_{j}+1\cdots,t)(n_{i})^{1/2}(n_{j}+1)^{1/2}\\
&\times|n_{1} n_{2} \cdots n_{\infty}\rangle+\cdots\\
=&\cdots +\sum_{\substack{n_{1} n_{2}\cdots n_{\infty}\\(\sum_{i}n_{i}=N)}}\sum_{i\neq j}\langle i|T|j\rangle f(\cdots n_{i}^{\prime}\cdots n_{j}^{\prime}\cdots,t)(n_{i}^{\prime}+1)^{1/2}(n_{j}^{\prime})^{1/2}\\
&\times|\cdots n_{i}^{\prime}+1\cdots n_{j}^{\prime}-1 \cdots\rangle+\cdots\\
=&\cdots +\sum_{\substack{n_{1} n_{2}\cdots n_{\infty}\\\left(\sum_{i}n_{i}=N\right)}}\sum_{i\neq j}\langle i|T|j\rangle f(\cdots n_{i}^{\prime}\cdots n_{j}^{\prime}\cdots,t)b_{i}^{\dagger}b_{j}| n_{1}^{\prime}n_{2}^{\prime}\cdots n_{\infty}^{\prime}\rangle+\cdots\\
=&\cdots+\sum_{i\neq j}\langle i|T|j\rangle b_{i}^{\dagger}b_{j}|\Psi(t)\rangle+\cdots\\
=&\hat{H}|\Psi(t)\rangle
\end{aligned}
$$
We can get the Hamiltonian given by the expression
$$
\hat{H}=\sum_{i j} b_{i}^{\dagger}\langle i|T| j\rangle b_{j}+\frac{1}{2} \sum_{j \neq l} b_{i}^{\dagger} b_{j}^{\dagger}\langle i j|V| k l\rangle b_{l} b_{k}
$$
## Bose-Hubbard model  
The second quantization many-body Hamiltonian of $N$ interacting condensate bosons confined in a potential $V(r)$ is given by [2]   
$$
\hat{H}=\int d\boldsymbol{r}\hat{\Psi}^{\dagger}(\boldsymbol{r})\left[-\frac{\hbar^{2}}{2m}\nabla^{2}+V(\boldsymbol{r})\right]\hat{\Psi}(\boldsymbol{r})+\frac{1}{2}\int d\boldsymbol{r}\int d\boldsymbol{r}^{\prime}\hat{\Psi}^{\dagger}(\boldsymbol{r})\hat{\Psi}^{\dagger}(\boldsymbol{r}^{\prime})U(\boldsymbol{r}-\boldsymbol{r}^{\prime})\hat{\Psi}(\boldsymbol{r}^{\prime})\hat{\Psi}(\boldsymbol{r})
$$
where $\hat{\Psi}^{\dagger}(\boldsymbol{r})$ and $\hat{\Psi}(\boldsymbol{r})$ are the bosonic field operators describe creation and annihilation of a particle at position $\boldsymbol{r}$, respectively. The first integral term describes the energy of a single particle in the potential $V(\boldsymbol{r})$ and the second integral term is the two-body interaction $U(\boldsymbol{r}-\boldsymbol{r}^{\prime})$.  
When $V(\boldsymbol{r})$ is a periodic lattice potential with the form $V(\boldsymbol{r})=\sum_{j=1,2,3}V_{0}\sin^{2}(kx_{j})$, where $k=2\pi/\lambda$ is wave vectors and $\lambda$ is the wavelength of laser light, corresponding to a lattice period $a=\lambda/2$. If we assume that the lattice potential is deep and atoms are tightly bound to the lattice sites, which is called \textbf{tight-binding model}. And we also consider that the energy gap between the ground band and first excited band is large enough comparing with other energy scales. As a consequence, we can reduce to focus on the lowest band. The eigenfunctions of the Schrodinger equation with periodic lattice potential is \textbf{Wannier function}. It has the form of $\phi_{j}(\boldsymbol{r})={\frac  {1}{{\sqrt{N}}}}\sum _{{{\boldsymbol{k}}}}e^{{-i{\boldsymbol{k}}\cdot {\boldsymbol{R}}}}\psi^{j}_{{{\boldsymbol{k}}}}({\boldsymbol{r}})$, where $\boldsymbol{R}$ is any lattice vector, $N$ is the normalization factor, $\boldsymbol{k}$ is the wave vectors in the Brillouin zone. The field operator can hence be expressed as $\hat{\Psi}(\boldsymbol{r})=\sum_{j}\phi_{j}(\boldsymbol{r})\hat{a}_{j}$, $\hat{a}_{j}$ is the annihilation of a particle in $j$th site.  
Then, we may rewrite the Hamiltonian as
$$
\begin{aligned}
\hat{H}&=\sum_{j, j^{\prime}}\left[\int d^{3} r \phi_{j}^{*}(\boldsymbol{r})\left[-\frac{\hbar^{2}}{2 m} \nabla^{2}+V_{\text {latt}}(\boldsymbol{r})\right] \phi_{j^{\prime}}(\boldsymbol{r})\right] \hat{a}_{j}^{\dagger} \hat{a}_{j^{\prime}}\\
&+\frac{1}{2} \sum_{j, j^{\prime}}\left[\iint d^{3} r d^{3} r^{\prime}\phi_{j}^{*}(\boldsymbol{r}) \phi_{l}^{*}\left(\boldsymbol{r}^{\prime}\right)U\left(\boldsymbol{r}-\boldsymbol{r}^{\prime}\right)\phi_{l^{\prime}}\left(\boldsymbol{r}^{\prime}\right) \phi_{j^{\prime}}(\boldsymbol{r})\right] \hat{a}_{j}^{\dagger} \hat{a}_{l}^{\dagger} \hat{a}_{l^{\prime}} \hat{a}_{j^{\prime}}
\end{aligned}
$$
Finally, if the condensate bose atoms are well separated, the corresponding overlap between neighboring sites is very weak. We only consider the nearest neighbor sites $j$ and $j^{\prime}$ in the first part and the "on-site" interaction in the second part, arriving at the standard **Bose-Hubbard Hamiltonian**  
$$
\hat{H}=-t \sum_{\langle j, j^{\prime}\rangle} \hat{a}_{j}^{\dagger} \hat{a}_{j^{\prime}}+\frac{U}{2} \sum_{j} \hat{n}_{j}\left(\hat{n}_{j}-1\right)+\sum_{j}\epsilon_{j}\hat{n}_{j}
$$
where $\langle j, j^{\prime}\rangle$ indicates the sum over nearest neighbor sites and $\hat{n}_{j}=\hat{a}^{\dagger}_{j}\hat{a}_{j}$ is the boson number operator at site $j$.  
$$
t \equiv-\int d^{3} r \phi_{j}^{*}(\boldsymbol{r})\left[\frac{-\hbar^{2}}{2 m} \nabla^{2}+V_{l a t t}(\boldsymbol{r})\right] \phi_{j^{\prime}}(\boldsymbol{r})
$$
is the tunneling term between nearest neighbors, which can be modified by changing the depth of the lattice. and  
$$
U \equiv \iint d^{3} r d^{3} r^{\prime}\left|\phi_{j}\left(\boldsymbol{r}^{\prime}\right)\right|^{2}\left|\phi_{j}(\boldsymbol{r})\right|^{2} U\left(\boldsymbol{r}-\boldsymbol{r}^{\prime}\right)
$$
is the "on-site" interactions. For a short-range interaction, it can be tuned by employing Feshbach resonances. $\epsilon_{j}$ is the energy of a particle in site $j$ absence of tunneling and interactions.  
## Extended Bose-Hubbard model [3, 4]  
Supposing there are long rang anisotropic dipole-dipolar interactions when all dipoles point in the same direction, an effective pseudo-potential can substitute the total interaction potential in the simple form with a contact term and a dipole-dipole part  
$$
U(\boldsymbol{r}-\boldsymbol{r}^{\prime})=g\delta(\boldsymbol{r}-\boldsymbol{r}^{\prime})+U_{dd}(\boldsymbol{r}-\boldsymbol{r}^{\prime})=g\delta(\boldsymbol{r}-\boldsymbol{r}^{\prime})+\frac{C_{dd}}{4\pi}\frac{1-3\cos^{2}\theta}{|\boldsymbol{r}-\boldsymbol{r}^{\prime}|^{3}}
$$
where $g$ is the amplitude of the contact interaction, $C_{dd}$ is the coupling constant with $\mu_{0}\mu^{2}$ for magnetic dipolar particles and $d/\varepsilon_{0}$ for electric dipolar particles, and $\theta$ is the angle between the polarization direction of the dipoles and their relative position vector $\boldsymbol{r}-\boldsymbol{r}_{0}$.  
We consider a stable two-dimensional geometry with a tight confinement in the direction of polarization of the dipoles. Loading the dipolar bosons in an optical lattice in the perpendicular $xy$ plane  
$$
V_{ext}(\boldsymbol{r})=V_{0}[\cos^{2}(\pi x/a)+\cos^{2}(\pi y/a)]+\frac{1}{2}m\omega^{2}_{z}z^{2}
$$
The Hamiltonian of the system is given by  
$$
\begin{aligned}
\hat{H}&=\int d\boldsymbol{r}\hat{\Psi}^{\dagger}(\boldsymbol{r})\left[-\frac{\hbar^{2}}{2m}\nabla^{2}+V(\boldsymbol{r})\right]\hat{\Psi}(\boldsymbol{r})+\frac{1}{2}\int d\boldsymbol{r}\int d\boldsymbol{r}^{\prime}\hat{\Psi}^{\dagger}(\boldsymbol{r})\hat{\Psi}^{\dagger}(\boldsymbol{r}^{\prime})U(\boldsymbol{r}-\boldsymbol{r}^{\prime})\hat{\Psi}(\boldsymbol{r}^{\prime})\hat{\Psi}(\boldsymbol{r})\\
&=\int d\boldsymbol{r}\hat{\Psi}^{\dagger}(\boldsymbol{r})\left[-\frac{\hbar^{2}}{2m}\nabla^{2}+V_{latt}(x,y)+\frac{1}{2}m\omega^{2}_{z}z^{2}\right]\hat{\Psi}(\boldsymbol{r})\\
&+\frac{1}{2}\int d\boldsymbol{r}\int d\boldsymbol{r}^{\prime}\hat{\Psi}^{\dagger}(\boldsymbol{r})\hat{\Psi}^{\dagger}(\boldsymbol{r}^{\prime})U(\boldsymbol{r}-\boldsymbol{r}^{\prime})\hat{\Psi}(\boldsymbol{r}^{\prime})\hat{\Psi}(\boldsymbol{r})
\end{aligned}
$$
Again, we use the expansion of the field operators in the basis of Wannier functions $\phi_{j}(\boldsymbol{r})$, expressed as $\hat{\Psi}(\boldsymbol{r})=\sum_{j}\Phi_{j}(\boldsymbol{r})\hat{a}_{j}$, where $\Phi_{j}=\phi_{j}(x,y)\varphi_{0}(z)$ and restrict our discussion to the lowest Bloch band.  
$$
\begin{aligned}
\hat{H}&=\sum_{j, j^{\prime}}\left[\int d^{3} r \Phi_{j}^{*}(\boldsymbol{r})\left[-\frac{\hbar^{2}}{2 m} \nabla^{2}+V_{\text {latt}}(\boldsymbol{r})\right] \Phi_{j^{\prime}}(\boldsymbol{r})\right] \hat{a}_{j}^{\dagger} \hat{a}_{j^{\prime}}\\
&+\frac{1}{2} \sum_{j, j^{\prime}}\left[\iint d^{3} r d^{3} r^{\prime}\Phi_{j}^{*}(\boldsymbol{r}) \Phi_{l}^{*}\left(\boldsymbol{r}^{\prime}\right)U\left(\boldsymbol{r}-\boldsymbol{r}^{\prime}\right)\Phi_{l^{\prime}}\left(\boldsymbol{r}^{\prime}\right) \Phi_{j^{\prime}}(\boldsymbol{r})\right] \hat{a}_{j}^{\dagger} \hat{a}_{l}^{\dagger} \hat{a}_{l^{\prime}} \hat{a}_{j^{\prime}}
\end{aligned}
$$
The Hamiltonian becomes the same as standard Bose–Hubbard Hamiltonian. As previously, in the tight-binding model, we only consider the nearest neighbor sites $j$ and $j^{\prime}$ in the first part, and the addition dipolar contributions which are coming from "on-site" with $j=j^{\prime}=l=l^{\prime}$ and "off-site" with $j=j^{\prime}\neq l=l^{\prime}$. The Hamiltonian reads as **extended Bose-Hubbard model**  
$$
\hat{H}=-t \sum_{\langle j, j^{\prime}\rangle} \hat{a}_{j}^{\dagger} \hat{a}_{j^{\prime}}+\frac{U_{0}}{2} \sum_{j} \hat{n}_{j}\left(\hat{n}_{j}-1\right)+\sum_{\delta\neq 0}\frac{U_{\delta}}{2}\sum_{j}\hat{n}_{j}\hat{n}_{j+\delta}+\sum_{j}\epsilon_{j}\hat{n}_{j}
$$
where $\langle j, j^{\prime}\rangle$ indicates the sum over nearest neighbor sites and $\hat{n}_{j}=\hat{a}^{\dagger}_{j}\hat{a}_{j}$ is the boson number operator at site $j$.  
$$
t \equiv-\int d^{3} r \Phi_{j}^{*}(\boldsymbol{r})\left[\frac{-\hbar^{2}}{2 m} \nabla^{2}+V_{l a t t}(\boldsymbol{r})\right] \Phi_{j^{\prime}}(\boldsymbol{r})
$$
is the tunneling term between nearest neighbors, and  
$$
U_{0} \equiv g\int d^{3}r|\Phi(\boldsymbol{r})|^{4}+\iint d^{3} r d^{3} r^{\prime}\left|\Phi_{j}\left(\boldsymbol{r}^{\prime}\right)\right|^{2}\left|\Phi_{j}(\boldsymbol{r})\right|^{2} U\left(\boldsymbol{r}-\boldsymbol{r}^{\prime}\right)
$$
is the "on-site" interactions, and  
$$
U_{\delta} \equiv \iint d^{3} r d^{3} r^{\prime}\left|\Phi_{j}\left(\boldsymbol{r}^{\prime}\right)\right|^{2}\left|\Phi_{j+\delta}(\boldsymbol{r})\right|^{2} U\left(\boldsymbol{r}-\boldsymbol{r}^{\prime}\right)
$$
is the "off-site'' interactions, depending on the angle of two dipolar and decaying by the rate of $1/\delta^{3}$. $\epsilon_{j}$ is the energy of a particle in site $j$ absence of tunneling and interactions.  

## Referece  
[1] Alexandre M Zagoskin. Second Quantization. InQuantum Theory of Many-BodySystems, volume 174, pages 3–32. Springer, 1998.   
[2] Franco Dalfovo, Stefano Giorgini, Lev P. Pitaevskii, and Sandro Stringari. The-ory of Bose-Einstein condensation in trapped gases.Reviews of Modern Physics,71(3):463–512, April 1999.  
[3] Omjyoti Dutta, Mariusz Gajda, Philipp Hauke, Maciej Lewenstein, Dirk-SörenLühmann, Boris A Malomed, Tomasz Sowiński, and Jakub Zakrzewski. Non-standard Hubbard models in optical lattices: A review.Reports on Progress inPhysics, 78(6):066001, May 2015.  
[4] Luis Santos. Theory of dipolar gases. InMany-Body Physics with Ultracold Gases,pages 231–272. Oxford University Press, 2010.7