---
layout: post
comments: true
title: "Some thoughts after Converting ISLR book to Julialang"
excerpt: "Recently, I convert code of ISLR book from R to Julialang and this post is my thoughts after finishing this project"
date: 2020-12-25
---

[An Introduction to Statistical Learning with Applications in R](https://statlearning.com/) (ISLR) is an excellent book for introducing statistical learning to beginners. Its authors are well-known researchers in this field but this book is very intuitive and easy to follow. As a [Julialang](https://julialang.org/) advocate, I really want to see the Julia-version of this book. For this reason, I have translated all its materials to Julia with some inspiration from the Python project - [ISLR-python](https://github.com/JWarmenhoven/ISLR-python). 

My project is named [ISLR.jl](https://github.com/tndoan/ISLR.jl). It is a long project since I got the idea 3 years ago but I only seriously devote my time to this project last month. After finishing (nearly) all, I proudly shared it in [/r/julia](https://www.reddit.com/r/Julia/comments/kdrlz2/i_convert_an_introduction_to_statistical_learning/) and surprisingly, my post is well received by other advocates. Right now, it is my most starred repo in Github.

ISLR is a must-read book for beginners of data science so re-implementing the book in Julia is kind-of a proxy for me to measure the readiness of Julia eco-system for data science. In this post, I will share my thoughts on this topic.

## What do data scientist need?

In my opinion, a programming language and its eco-system are ready for data scientists when they can quickly apply their standard techniques e.g. PCA, linear regression to ***torture*** and plot their given data. For this reason, data scientists require

1. Good library of statistic
2. Good visualization library

## The good of Julia

Julia is getting more and more attention from researchers and developers around the world. Hence, its eco-system is becoming more and more mature. It means all basic need for data science is ready in Julia. For example, if we want to use support vector machine, we have [libsvm.jl](https://github.com/JuliaML/LIBSVM.jl). For visualization, we have [Plots.jl](https://github.com/JuliaPlots/PlotDocs.jl).

In case of not having ready library, we are able to borrow from other programming languages. For example, [PyCall.jl](https://github.com/JuliaPy/PyCall.jl) allows us to call Python within Julia or [PyPlot](https://github.com/JuliaPy/PyPlot.jl) triggers matplotlib.

## The bad of Julia

There are several disadvantage of Julia. Here are my thoughts.

1. **The poor document**: Since Julia is quite *new*, the maintainers of its libraries somehow do not care much about document. It is very hard when we encounter some issues during our coding process. For example, I have to dig into the source code of *Plots.jl* to find out how to draw [vertical/horizontal lines](https://github.com/JuliaPlots/Plots.jl/blob/3725a8d3875df2b45186bf248bdc7cda191969d5/src/shorthands.jl). An other example is that Generalized linear model is extremely popular in stat community but the [document of GLM.jl](https://juliastats.org/GLM.jl/stable/) is not that useful, I have to code and guess multiple times. Hopefully, the document becomes more reliable for users in future.
2. **The fragment of library**: In Python, [matplotlib](https://matplotlib.org/) is a de-facto library for visualization. However, I have found that besides *Plots.jl*, I still need to use [StatsPlots.jl](https://github.com/JuliaPlots/StatsPlots.jl) for some plots related to statistic. Moreover, we do not have a standard library which is similar to *sklearn* in Python. There are some efforts such as [MLJ.jl](https://github.com/alan-turing-institute/MLJ.jl) but it is not enough since these libraries are still in early state.
3. **The integrity of eco-system**: I believe Julia libraries should be implemented in Julia to use all of its benefits. However, there are still many libraries implemented in Julia but behind the scenes, they call other programming language. For example, [ScikitLearn.jl](https://github.com/cstjean/ScikitLearn.jl) totally calls scikit-learn and some parts of *MLJ.jl* are used other Python libraries. I understand that this approach can reduce the cost of development but in long run, I think it is better if the entire is done via Julia.

## Conclusion

Julia is a fantastic language and I believe it is the future of scientific computing. It cannot replace Python or R in near future but it gradually gets traction of the community. Hopefully, I will see more and more libraries and tools written in Julia.
