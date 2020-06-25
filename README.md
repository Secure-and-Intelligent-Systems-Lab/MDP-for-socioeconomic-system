# MDP-for-socioeconomic-system

1-Dependencies:
Numpy
Scipy
Matplotlib
Pandas
Math
Random
Tensorflow 
Keras
Pytorch

2-Results: 
	
	a)Sea level rise projections:

Regionally adjusted sea level rise projections from the National Oceanic and Atmospheric Administration (NOAA) is available in the link:
http://www.tbrpc.org/wp-content/uploads/2019/05/CSAP_SLR_Recommendation_2019.pdf
We obtained our fitted curve with help of the table in page 6 of the above pdf.  After converting the feet values to millimeter, we extracted the annual relative sea level.
This is implemented in  NOAA_fittings.ipynb

	b)Shortsighted policy:

We considered a shortsighted government policy that takes investment actions after observing a high cost from the nature based on its predetermined threshold. Under the three sea level projections, we found the optimum thresholds that minimize the average total cost of shortsighted policy in 100 years as 34, 28, and 21 for the intermediate low, intermediate, and high projections.  
This is implemented in  optimal_threshold_based_agent.ipynb

	c)MDP Based Agent:

The government cooperation index a_g, the residents’ cooperation index a_r, and the sea level projection selector a are user defined inputs. The user inputs a=0,1,2, respectively for intermediate low, intermediate, and high sea level rise projections. We use the standard DQN algorithm with experience replay.
This is implemented using DQN in slr_dqn.ipynb and Advantage Actro Critic algorithm in slr_A2C.ipynb
	
(i)DQN Hyperparameters:
	GAMMA = [0.1 , 0.3, 0.5, 0.7, 0.9] ***
	LEARNING_RATE = 0.001
	MEMORY_SIZE = 20000
	BATCH_SIZE = 1000
	EXPLORATION_MAX = 1.0
	EXPLORATION_MIN = 0.01
	EXPLORATION_DECAY = 0.9999
***  Gamma corresponds to the government cooperation index a_g, so we used it as an input to the function. 

DQN Model structure:
	Dense layer - input: 2, output: 12, activation: relu
	Dense layer - input: 12, output: 24, activation: relu
	Dense layer – input: 24, output: 12, activation: relu
	Dense layer – input: 12, output: 4, activation: linear
	Huber loss function
	Adam optimizer
	State (ln,sn) is a (1,2) size array
	Action is integer between 0 and 3
	Cost has a positive continuous value
	Next State (ln+1,sn+1) is a (1,2) size array
	Every 50 steps target network's weights are updated

(ii)Advantage Actor Critic(A2c) Hyperparameters:
	GAMMA = [0.1 , 0.3, 0.5, 0.7, 0.9] ***
	
***  Gamma corresponds to the government cooperation index a_g, so we used it as an input to the function. 

Actor Model structure: 
	Dense layer - input: 2, output: 12, activation: relu
	Dense layer - input: 12, output: 120, activation: relu
	Dense layer – input: 120, output: 12, activation: relu
	Dense layer – input: 12, output: 4, activation: softmax
	LEARNING_RATE = 3e-4r

CriticModel structure: 
	Dense layer - input: 2, output: 12, activation: relu
	Dense layer - input: 12, output: 120, activation: relu
	Dense layer – input: 120, output: 12, activation: relu
	Dense layer – input: 12, output: 1, activation: linear
	LEARNING_RATE = 3e-4r

	State (ln,sn) is a (1,2) size array
	Action is integer between 0 and 3
	Cost has a positive continuous value
	Next State (ln+1,sn+1) is a (1,2) size array
	
