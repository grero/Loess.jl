# Loess

[![Build Status](https://travis-ci.org/JuliaStats/Loess.jl.svg?branch=master)](https://travis-ci.org/JuliaStats/Loess.jl)

This is a pure Julia loess implementation, based on the fast kd-tree based
approximation described in the original Cleveland, et al papers[1,2], implemented
in the netlib loess C/Fortran code, and used by many, including in R's loess
function.

## Synopsis

`Loess` exports two functions: `loess` and `predict`, that train and apply the model, respectively.


```julia
using Loess

xs = 10 .* rand(100)
ys = sin.(xs) .+ 0.5 * rand(100)

model = loess(xs, ys)

us = range(extrema(xs)...; step = 0.1)
vs = predict(model, us)

using Gadfly
p = plot(x=xs, y=ys, Geom.point, Guide.xlabel("x"), Guide.ylabel("y"),
         layer(Geom.line, x=us, y=vs))
draw(SVG("loess.svg", 6inch, 3inch), p)
```

![Example Plot](http://JuliaStats.github.io/Loess.jl/loess.svg)

There's also a shortcut in Gadfly to draw these plots:

```julia
plot(x=xs, y=ys, Geom.point, Geom.smooth, Guide.xlabel("x"), Guide.ylabel("y"))
```


## Status

Multivariate regression is not yet fully implemented, but most of the parts
are already there, and wouldn't require too much additional work.

## References
[1] William S. Cleveland (1979) Robust Locally Weighted Regression and Smoothing Scatterplots, Journal of the American Statistical Association, 74:368, 829-836, DOI: 10.1080/01621459.1979.10481038

[2] William S. Cleveland & Susan J. Devlin (1988) Locally Weighted Regression: An Approach to Regression Analysis by Local Fitting, Journal of the American Statistical Association, 83:403, 596-610, DOI: 10.1080/01621459.1988.10478639
