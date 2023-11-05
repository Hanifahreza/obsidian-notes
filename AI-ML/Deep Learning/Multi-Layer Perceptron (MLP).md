- Clearly, almost all complex things irl is not linear, hence shallow learning usually is not sufficient
- Therefore, we introduce **hidden layers** between the input and output
- These **hidden layers** ($H$) will feature the same kind of linear equation $wx + b$, but we put it inside an [[Activation Function]] to make it non-linear
- That's why the expression $wx + b$ is called *pre-activation* or *logit*
![[mlp.png]]
- These hidden layers of course have their own weights
- So the more the hidden layers, the more the weights, the more complex is the model
- A one-layered MLP can be written as:
> 	$H = \sigma(XW^{(1)} + b^{(2)})$
		$O = HW^{(2)} + b^{(2)}$	
- Where $\sigma$ is an activation function