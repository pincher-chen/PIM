# PIM
Polarizable ion model force field development.   
**Note:** The following formula can be viewed normally on chrome by installing MathJax Plugin for Github

The potential of ionic interaction energy is best described as the sum of four different components: charge-charge, dispersion, overlap repulsion and polarization:
$$V^{total}=V^{charge} + V^{dispersion} + V^{repulsion} + V^{polarization} $$

The first term corresonds to the electrostatic interaction between two charges:
$$V^{charge}=\sum_{i<j}(\frac{q^iq^j}{r^{ij}}) $$
The second term corresponds to dispersion component due to the instantaneous correlations of density fluctuations bettween the electronic clouds, which includes dipole-dipole and dipole-quadrupole terms:
$$V^{dispersion}=-\sum_{i<j}[f_6^{ij}\frac{C_6^{ij}}{(r_ij)^6}+f_8^{ij}\frac{C_8^{ij}}{(r_ij)^8}] $$
Where $C^{ij}_6$ and $C^{ij}_8$ are the dipole-dipole and dipole-quadrupole dispersion coefficients and $r_ij$ is the distance between the two atoms i and j. The Tang-Toennies damping function $f^{ij}_n$ is used to currect the shot-range interaction as：

$$f_n^{ij}(r_{ij}) = 1 - e^{-b_n^{ij} r_{ij}} \sum_{k=0}^{n} \frac {(b_n^{ij} r_{ij} )^k} {k!}$$

The third term corresponds to the short-range repulsion, descriped by a simple exponential from

$$V^{repulsion}=\sum_{i<j}A^{ij}e^{-B^{ij}r_{ij}}$$

Where $A^{ij}$ and $B^{ij}$ are two parameters.

Finally, the last term corresponds to the polarization, composted of three contributions: charge-dipole and dipole-dipole interactions a well as the energy cost for deforming the electronic cloud of the atom.

$$V^{polarization} = \sum_{i,j} - (q_{i} u_{j,a} f_{4}^{ij} (r_{ij}) - q_{j} u_{i,a} f_{4}^{ji}(r_{ij}) t) T_{a}^{(1)} (r_{ij}) - \sum_{i,j} u_{i,a} u_{j,b} T_{ab}^{(2)} (r_{ij}) + \sum_{i} \frac {1}{2 a_{i}} |u_{i}^2|$$

Here, $a_{i}$ is the polarizability of ion i, $u_{i}$ are the dipoles and $T^(1)$ and $T^(2)$ are the charge-dipole and dipole-dipole interaction tensors,
$$T_{a}^{(1)} (r) = -r_{a} / r^{3} $$
$$T_{ab}^{(2)} (r) = (3 r_{a} r_{b} - r^{2} delta_{ab}^{2})/r^{5}$$

The instantaneous values of these moments are obtained by minimizaion of this expression with respect to the dipoles of all ions at each MD time step. This ensures that we regain the condition that the dipole induced by an electrical field E is $aE$ and that the dipole values are mutually consistent. The short-rnage indection effects on the dipoles are taken into account by the Tang-Toennies damping functions,
$$f_n^{ij} (r_{ij}) = 1 - c^{ij} e^{-d^{ij} r_{ij}} \sum_{(k=0)}^{n} {(d^{ij} r_{ij})^k} / {K!}$$

The parameters $d^{ij}$ determine the range at which the overlap of the charge densities affects the induced dipoles, and the parameters $c^{ij}$ determine the strength of the ion response to this effect.  It is important to note that anion-anion damping terms have been taken into account. The additoin of anion-anion damping terms was found to greatly improve the ability to match the first-principles data.

With thest simplifications, the potential now includes only three additional degrees of freedom per ion, associated with the induced dipoles, which are calculated in a single minimizaion procedure:
$$(\frac {aV_{PIM}^{polarizaion} } {a u_{a}^{i}})_{u_a^N} = 0$$

# Related work
## Thole-Applequist model
This model treats the system in terms of site (atomic) point dipoles that interact via many-body polarization equations, which is suitable for the calculating  of the atom ion interaction in polyatomic molecules.

The potential of Thole-Applequist model is described as the sum of four different components: repulsion，charge-charge  and polarization:
$$V^{total}= V^{repulsion} + V^{charge} + V^{polarization} $$
The first term corresonds to the standard 12/6 Lennard-Jones potential, given by
$$E = 4\epsilon [(\frac {\sigma} {r})^{12} - (\frac {\sigma} {r})^6]$$

The second term corresonds to Coulombic pairwise interaction, given by
$$E = \frac {C q_i q_j} {\epsilon r}$$

The third term corresonds to polarization, Consider a static electric field applied to a molecule. The induced dipole on
this molecule will be equal to
$$\vec{\mu} = \alpha \vel{E^static}$$


**references:**  
1. [Atom dipole interaction model for molecular polarizability. Application to polyatomic molecules and determination of atom polarizabilities - 1972](https://pubs.acs.org/doi/abs/10.1021/ja00764a010?journalCode=jacsat)  
2. [Molecular polarizabilities calculated with a modified dipole interaction - 1981](https://www.sciencedirect.com/science/article/abs/pii/0301010481851762)  
3. [Molecular and Atomic Polarizabilities:  Thole's Model Revisited - 1998](https://pubs.acs.org/doi/abs/10.1021/jp980221f)

