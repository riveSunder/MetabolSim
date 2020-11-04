# MetabolSim

A numerical differential equation solver for biochemical networks, based on a descriptive netlist format inspired by [SPICE](https://en.wikipedia.org/wiki/SPICE) to describe electronic circuits for simulation. 

MetabolSim netlist entries describe network elements like so:

```
ICD> -5 6 [0.000008 0.006625 0.00013 0.00006625] (1.0)
```

In this example ICD is [socitrate dehydrogenase](https://en.wikipedia.org/wiki/Isocitrate_dehydrogenase), an important enzyme in the [citric acid cycle](). The parameters in the list are enzyme kinetics coefficients, and the number in parenthesis is the relative concentration of the enzymei. The two naked numbers in between the enzyme designation and the list of kinetics coefficients denotes the nodes that the enzyme connects to, and defines the sign convention for normal flux. 
of this

Following the biochemical network description, MetabolSim expects extra information in the `*Met` section. This section contains the starting concentrations (again in parenthesis) for the metabolites themselves, each assigned to a node.

```
Met
1 (0.0005)
2 (0.0000014)
3 (0.0000001)
4 (0.009)
5 (0.00015)
6 (0.0002)
7 (0.00004)
8 (0.006)
9 (0.0003)
10 (0.005)
11 (0.004)
12 (0.0001)
```

Finally, the last line contains some recommended parameters for running the network model.  


```
*Run(t,10.0,0.01)* 
```

MetabolSim currently uses a second order [Runge-Kutta](https://en.wikipedia.org/wiki/Runge%E2%80%93Kutta_methods) method for computing metabolite concentrations.


# Usage

To run a simulation of the demo biochemical network with default settings, simply cd to the project root folder and run:

```
python metabolsim/metabolsim.py
```

# Backstory

If you spend some time reading the code of MetabolSim, you may quickly recognize that it is almost entirely, ehm, not good. MetabolSim was my first Python project. It's clear that I had never heard of NumPy (yes NumPy was already established in 2011), and so I wrote my own (slow) classes for matrix and vector math. On the plus side this means there are almost no dependencies as the project was written in pure Python (but it does use `time` to timestamp results files). 

Although the demo network runs quickly on a modern computer, there are plenty of readily accessible changes that should amount to substantial speedups. 

Updating MetabolSim for better performance and stylistic consistency is on a TODO list, but it's a pretty long list at this point. ;)
