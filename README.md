# PIM
Polarizable ion model force field development.   
**Note:** The following formula can be viewed normally on chrome by installing MathJax Plugin for Github

The potential of ionic interaction energy is best described as the sum of four different components: charge-charge, dispersion, overlap repulsion and polarization:
$$V^{total}=V^{charge} + V^{dispersion} + V^{repulsion} + V^{polarization} $$

The first term corresonds to the electrostatic interation between two charges:
$$V^{charge}=\frac{q^i*q^j}{r^{ij}} $$

# Related work
## Thole-Applequist model
This model treats the system in terms of site (atomic) point dipoles that interact via many-body polarization equations, which is suitable for the calculating  of the atom ion interaction in polyatomic molecules.

**references:**  
1. [Atom dipole interaction model for molecular polarizability. Application to polyatomic molecules and determination of atom polarizabilities - 1972](https://pubs.acs.org/doi/abs/10.1021/ja00764a010?journalCode=jacsat)  
2. [Molecular polarizabilities calculated with a modified dipole interaction - 1981](https://www.sciencedirect.com/science/article/abs/pii/0301010481851762)  
3. [Molecular and Atomic Polarizabilities:  Thole's Model Revisited - 1998](https://pubs.acs.org/doi/abs/10.1021/jp980221f)

