.. include:: ../../../references.txt

.. _psf_3gauss:

``psf_3gauss`` format
=====================

Multi-Gauss mixture models are a common way to model distributions
(for source intensity profiles, PSFs, anything really), see e.g.
`2013PASP..125..719H`_.
For H.E.S.S., radial PSFs have been modeled as 1, 2 or 3 two-dimensional
Gaussians :math:`dP/d\Omega`.

.. note::

    A two-dimensional Gaussian distribution :math:`dP/d\Omega = dP/(dx dy)` is
    equivalent to an exponential distribution in :math:`dP/x`, where :math:`x=r^2`
    and a Rayleigh distribution in :math:`dP/dr`.


In this format, the triple-Gauss distribution is parameterised as follows:

.. math::

    dP/d\Omega(r, S, \sigma_1, A_2, \sigma_2, A_3, \sigma_3) =
     \frac{S}{\pi}
     \left[
        \exp\left(-\frac{r^2}{2\sigma_1^2}\right) + 
        A_2 \exp\left(-\frac{r^2}{2\sigma_2^2}\right) +
        A_3 \exp\left(-\frac{r^2}{2\sigma_3^2}\right)
     \right],

where :math:`S` is ``SCALE``, :math:`\sigma_i` is ``SIGMA_i`` and
:math:`A_i` is ``AMPL_i`` (see columns listed below).

TODO: give analytical formula for the integral, so that it's easy to check
if the PSF is normalised for a given set of parameters.

TODO: give test case value and Python function for easy checking?

.. note::

    By setting the amplitudes of the 3rd (and 2nd) Gaussians to 0 one can
    implement double (or single) Gaussian models as well. 

Columns:

* ``THETA_LO``, ``THETA_HI`` -- ndim: 1, unit: deg
    * Field of view offset axis
* ``ENERG_LO``, ``ENERG_HI`` -- ndim: 1, unit: TeV
    * Energy axis
* ``SCALE`` -- ndim: 2, unit: none
    * Absolute scale of the 1st Gaussian
* ``SIGMA_1``, ``SIGMA_2``, ``SIGMA_3`` -- ndim: 2, unit: deg
    * Model parameter (see formula above)
* ``AMPL_2``, ``AMPL_3`` -- ndim: 2, unit: none
    * Model parameter (see formula above)

Recommended axis order: ``ENERGY``, ``THETA``

Header keywords: none

Example data file: TODO: add HESS HAP example file as soon as available.
