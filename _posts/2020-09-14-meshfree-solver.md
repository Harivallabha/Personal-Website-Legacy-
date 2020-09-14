---
title: 'Least Squares Kinetic Upwind Method based Meshfree Solver for Inviscid Compressible Flows'
date: 2020-09-14
permalink: /posts/2020/09/lsqum-meshfree-solver/
tags:
  - Meshfree Solver 
  - C++
  - Thesis
---

A couple of days ago, I finished implementing a q-LSKUM (Least Squares Kinetic Upwind Method) based meshfree solver for aerodynamic shape optimization, in C++, as a part of my M.Sc. Mathematics thesis at BITS Pilani - Hyderabad. 

The solver employs a least squares based spatial discretization of partial derivatives, for the numerical solution of Navier-Stokes equations for compressible fluid flows. We construct an upwind scheme for the 2-D Boltzmann quation, resulting from the conservation laws, through the Couran-Isaacson-Rees splitting of molecular velocities. Utilizing the defect correction procedure, outlined by Ghosh. A.K. and Deshpande S.M., we achieve second order accuracy. We use local time-stepping and discrete approximations to obtain the steady solution. The state updates are peformed using a four-stage Runge-Kutta scheme (SSP-RK3).

The fixed point iterative solver makes calls to five functions: q_variables, q_var_derivatives, q_var_derivatives_innerloop, calc_flux_residual and state_update, and offers scope for extensive data parallelism. The bulk of the computation time is taken up by the calc_flux_residual function. This brings us to the next stage of the project: GPU Parallelization of the primal solver. I shall be CUDAfying the functions, and hope to see significant speedup on the 10M and 40M grids. Post parallelism, I'll start writing the adjoint solver making use of CoDiPack to perform operator overloading based automatic differentiation to help us compute accurate shape sensitivities. 

Exciting work ahead, let's see what CUDA has in store for us!
