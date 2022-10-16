# Hopfield Network
A Hopfield network is a type of neural network commonly used for pattern recognition. In <a href="https://github.com/TomMakesThings/Hopfield-Network/blob/main/Hopfield_network.ipynb">this notebook</a>, the Hopfield net is evaluated based on its capacity to recall patterns using either the Hebbian or Storkey learning rules.

<div align="center">
  <img src="https://github.com/TomMakesThings/Hopfield-Network/blob/assets/Images/Hopfield_Network.png" width=800>
</div>

# Network Initialisation
To create the network, an array of $p$ same size patterns is given and the number of neurons $N$ is set as the pattern size. The network weights are initialised as a lower triangle matrix of zeros as Hopfield net weights between all neurons are symmetric. Weights are then calculated depending on the learning rule. If the Hebbian learning rule was specified, weights are set by the equation below, where $x_{i}^{\mu}$ denotes the $i^{th}$ component of pattern $\mu$.

$w_{ij} = \frac{1}{N} \sum_{\mu = 1}^{p} x_{i}^{\mu}x_{j}^{\mu}$

If the learning rule is set as the Storkey learning rule, weights are determined through the equations below, where $h_{ij}$ is a form of local field.

$w_{ij}^{0} = 0,  \mbox{for all i,j}$

$w_{ij}^{\mu} = w_{ij}^{\mu - 1} + \frac{1}{N} (x_{i}^{\mu} x_{j}^{\mu} - \frac{1}{N} x_{i}^{\mu} h_{ij} - \frac{1}{N} h_{ij} x_{j}^{\mu})$

$h_{ij}^{\mu} = \sum_{k = 1 \mbox{ } k \neq i,j}^{N} w_{ik}^{\mu - 1} x_{k}^{\mu}$

When the network is run, its initial state is set as the input pattern and the energy of the whole network calculated, where $v_{i}$ is the state of unit $i$ and $v_{i} \in \{-1, 1\}$.

$E = -\frac{1}{2} \sum_{ij} w_{ij}v_{i}v_{j}$

The state $s$ of all neurons are then repeatedly updated until the network converges to a stable state. This is determined by the network's energy not changing for $n$ iterations, where in this case $n = 500$. By default, neuron state updates are set to be asynchronous, in which neurons are randomly selected to be updated one at a time.

$\text{if } \sum_{j = 1}^{N} w_{ij}v_{j} - \theta_{i} \geq 0 \text{, } s_{i} = 1$

$\text{else } s_{i} = -1$
