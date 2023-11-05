## Xavier/Glorot Initialization
- Initialize the weights with random values from a normal distribution with 
	- $\text{mean} = 0$ 
	- $\text{variance} = \frac{1}{n_{in} + n_{out}}$ 
		- $n_{in}$ is the number of input units in the layer  
		- $n_{out}$ is the number of output units
- Useful when using [[Activation Function#Sigmoid|Sigmoid]] or [[Activation Function#Tanh|Tanh]] activation function
## He Initialization
- Designed for [[Activation Function#ReLU|ReLU]] and its variants
- Initialize the weights with random values from a normal distribution with 
	- $\text{mean} = 0$  
	- $\text{variance} = 2/n$ 
		- $n$ is the number of input units in the layer
## LeCunn Initialization
- Designed for [[Activation Function#Tanh|Tanh]] and its variants
- Initialize the weights with random values from a normal distribution with 
	- $\text{mean} = 0$  
	- $\text{variance} = 1/n$  
		- $n$ is the number of input units in the layer