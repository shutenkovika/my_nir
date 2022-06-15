# Код программы

``` {.julia xleftmargin=1em,linenos}
using Pkg
using Plots
using DifferentialEquations
using ParameterizedFunctions
a = 2
b = 5
g = 1
a1 = 0.51
a2 = 1.2
b1 = 0.51
b2 = 1.2
c1 = 1.2
c2 = 0.51
P = 0
u0 = 1
v0 = 1
pp! = @ode_def PP begin
    du = u*((1+a1*P)/(1+a2*P) - u*(1+b2*P)/(1+b1*P)) - u*v/(1+a*u)
    dv = g*(-v*(1+c1*P)/(1+c2*P) + b*u*v/(1+a*u))
end a1 a2 b1 b2 c1 c2 
u = [u0,v0]
param=[a1, a2, b1, b2, c1, c2, a, b, g, P]
timespan = (0.0,100.0)
problem = ODEProblem(pp!, u, timespan, param)
solution = solve(problem)
plot(solution, title = "Predator - Prey model", xlabel = "t", ylabel = "u, v", label=["Prey (u)" "Predator (v)"])

plot(solution, vars=(1,2), xaxis="Prey", yaxis="Predator",legend=false)
```

