# HyperDualMatrixTools.jl

<p>
  <a href="https://travis-ci.com/briochemc/HyperDualMatrixTools.jl">
    <img alt="Build Status" src="https://travis-ci.com/briochemc/HyperDualMatrixTools.jl.svg?branch=master">
  </a>
  <a href='https://coveralls.io/github/briochemc/HyperDualMatrixTools.jl?branch=master'>
    <img src='https://coveralls.io/repos/github/briochemc/HyperDualMatrixTools.jl/badge.svg?branch=master' alt='Coverage Status' />
  </a>
  <a href="https://codecov.io/gh/briochemc/HyperDualMatrixTools.jl">
    <img src="https://codecov.io/gh/briochemc/HyperDualMatrixTools.jl/branch/master/graph/badge.svg" />
  </a>
  <a href="https://github.com/briochemc/HyperDualMatrixTools.jl/blob/master/LICENSE">
    <img alt="License: MIT" src="https://img.shields.io/badge/License-MIT-yellow.svg">
  </a>
</p>

This module overloads `factorize` and `\` to work with hyperdual-valued arrays.

It uses the HyperDualNumbers.jl package.

The idea is that for a hyperdual-valued matrix

<a href="https://www.codecogs.com/eqnedit.php?latex=\fn_phv&space;M&space;=&space;A&space;&plus;&space;\varepsilon_1&space;B&space;&plus;&space;\varepsilon_2&space;C&space;&plus;&space;\varepsilon_1&space;\varepsilon_2&space;D" target="_blank"><img src="https://latex.codecogs.com/svg.latex?\fn_phv&space;M&space;=&space;A&space;&plus;&space;\varepsilon_1&space;B&space;&plus;&space;\varepsilon_2&space;C&space;&plus;&space;\varepsilon_1&space;\varepsilon_2&space;D" title="M = A + \varepsilon_1 B + \varepsilon_2 C + \varepsilon_1 \varepsilon_2 D" /></a>,

its inverse is given by

<a href="https://www.codecogs.com/eqnedit.php?latex=\fn_phv&space;M^{-1}&space;=&space;(I&space;-&space;\varepsilon_1&space;A^{-1}&space;B&space;-&space;\varepsilon_2&space;A^{-1}&space;C&space;-&space;\varepsilon_1&space;\varepsilon_2&space;A^{-1}&space;(D&space;-&space;C&space;A^{-1}&space;B&space;-&space;B&space;A^{-1}&space;C))&space;A^{-1}" target="_blank"><img src="https://latex.codecogs.com/svg.latex?\fn_phv&space;M^{-1}&space;=&space;(I&space;-&space;\varepsilon_1&space;A^{-1}&space;B&space;-&space;\varepsilon_2&space;A^{-1}&space;C&space;-&space;\varepsilon_1&space;\varepsilon_2&space;A^{-1}&space;(D&space;-&space;C&space;A^{-1}&space;B&space;-&space;B&space;A^{-1}&space;C))&space;A^{-1}" title="M^{-1} = (I - \varepsilon_1 A^{-1} B - \varepsilon_2 A^{-1} C - \varepsilon_1 \varepsilon_2 A^{-1} (D - C A^{-1} B - B A^{-1} C)) A^{-1}" /></a>.

Therefore, only the inverse of <a href="https://www.codecogs.com/eqnedit.php?latex=\fn_phv&space;A" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\fn_phv&space;A" title="A" /></a> is required to evaluate the inverse of <a href="https://www.codecogs.com/eqnedit.php?latex=\fn_phv&space;M" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\fn_phv&space;M" title="M" /></a>.
This package makes available a `HyperDualFactors` type which containts the factors of <a href="https://www.codecogs.com/eqnedit.php?latex=\fn_phv&space;A" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\fn_phv&space;A" title="A" /></a> and the non-real parts of <a href="https://www.codecogs.com/eqnedit.php?latex=\fn_phv&space;M" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\fn_phv&space;M" title="M" /></a>, and overloads `factorize` to create an instance of `HyperDualFactors`, which can then be called with `\` to efficiently solve hyperdual-valued linear systems. 

## Usage

- Create your hyperdual-valued matrix `M`:
    ```julia
    julia> M = A + ε₁ * B + ε₂ * C + ε₁ε₂ * D
    ```

- Factorize `M`:
    ```julia
    julia> Mf = factorize(M)
    ```

- Apply `\` to solve systems of the type `M * x = y`
    ```julia
    julia> x = Mf \ y
    ```




