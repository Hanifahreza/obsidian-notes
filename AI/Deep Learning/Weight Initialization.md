#### Xavier/Glorot Initialization
- Initialize the weights with random values from a normal distribution with $mean = 0$ and $variance = \frac{1}{n_{in} + n_{out}}$ where $n_{in}$ is the number of input units in the layer and $n_{out}$ is the number of output units
- Useful when using sigmoid or tanh activation function
#### He Initialization
- Designed for ReLU and its variants
- Initialize the weights with random values from a normal distribution with $mean = 0$ and $variance = 2/n$ where $n$ is the number of input units in the layer
#### LeCunn Initialization
- Designed for tanh and its variants
- Initialize the weights with random values from a normal distribution with $mean = 0$ and $variance = 1/n$ where $n$ is the number of input units in the layer