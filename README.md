# PK Modelling of Drug Concentration Trajectories with Ordinary Differential Equations and Differential Evolution

## Motivation
I explored pharmacokinetic (PK) modelling for drug concentration trajectories as part of a recent data science internship stint. While there are numerous concepts involved (and some background information in PK is required), the core data science concepts (e.g. loss function, optimization etc) still form the backbone of the entire project. Therefore, I felt it would be ideal to re-create the steps and clearly document the processes and flow involved. The drug in question for this data science project is that of Mirtazapine, which is a popular oral medication to treat depression.

To keep it concise, the codes involving experimentation are removed, but are instead described in text within the Jupyter notebook itself. 

The published poster for this project can be found here: https://drive.google.com/file/d/1JK4Y4ZWWLdHNXbz80pIaiHkybJPd2YZr/view

## Primers
As there are multiple concepts involved in this modelling, here are some conceptual primers to get you up to speed with the intricacies of the modelling project

### What is Pharmacokinetics (PK)
- Pharmacokinetics is the study of the time-course of drug movement through the body, and involves the quantification of absorption, distribution, metabolism and excretion (ADME) of the drug and its metabolites. These processes can be described mathematically by pharmacokinetic modelling, which is the representation of the drug in the body by mathematical models. 
- In simpler terms, pharmacokinetics can be described as “what the body does to the drug”
- When put together, these processes relate to the intensity and time profile of drug action, and knowledge of this is vital for understanding and guiding drug dosing therapies. For example, understanding the absorption and distribution patterns allows for the prediction of overall drug exposure and the amount of administered drug dose that reaches the bloodstream and the target site of action.  
  
![alt text](https://github.com/kennethleungty/ODE-Modelling-with-Differential-Evolution/blob/main/Images/pharmacokinetics.png)


### What is PK Modelling 
- The purpose of pharmacokinetic modelling is to describe how a drug transits through the body by modelling concentrations of the drug in different parts of the body. 

### What are Compartmental Models
- Compartmental models are model structures commonly adopted in pharmacokinetic modelling to simplify the conceptualization and quantification of the multiple biological processes taking place when a drug enters the body. 
- In a compartmental model, the body is characterized as a series of interconnected compartments that communicate reversibly with one another. 
- The advantage of using a compartmental approach is that it allows for the prediction of the drug concentration at any time point, and can be easily described and illustrated 
- The number of compartments in a system may vary across different cases, although typically the range is between one and three compartments
- A central compartment exists in all these compartmental models, and it typically represents the blood plasma and highly perfused, rapidly equilibrating organs such as the heart, liver and kidneys. Blood plasma is the liquid part of the blood that carries cells and proteins throughout the body. 
- Some examples of compartments:
![alt text](https://github.com/kennethleungty/ODE-Modelling-with-Differential-Evolution/blob/main/Images/compartment-images-1.png)

### What is Ordinary Differential Equations
- The common mathematical approach to describe temporal profiles of plasma concentrations from a drug dosage regimen is with a system of ordinary differential equations (ODEs). 
- ODEs are differential equations that contain one or more functions of a single variable along with its derivatives, and the variable in question in this case is the drug concentration
- This means that the behavior of a pharmacokinetic system can be represented by differential equations describing amounts of the drug in various compartments, with the rate constants describing the rates of drug exchange between compartments. 

### What is an Initial Value Problem
- An initial value problem (IVP) is an ordinary differential equation coupled with an initial condition, which specifies the value of the unknown function at a given time point. 
- The initial condition in this case is the starting point (i.e. t=0) when the Mirtazapine oral dose was initially administered.

### What is Differential Evolution
- The process to derive the optimal parameters that gives the lowest loss (of the defined loss function) is called optimization
- Differential evolution is a stochastic population-based evolutionary algorithm developed in 1995 by Stron and Price.
- It is a powerful population-based direct search algorithm for global optimization capable of handling non-differentiable, non-linear and multi-modal objective functions, with few control parameters
- Differential evolution involves the stages of initialization, mutation, recombination and selection to arrive at the global minima.  This technique is inspired by the concept of biological theory of evolution, where the fittest individuals (in this case, parameter vectors) of a population are the ones that produce more offspring, which in turn inherit the good traits of the parents. 
- More information on Differential Evolution can be found from this video: https://www.youtube.com/watch?v=UZGiapWcoA4  
  
Essentially Differential Evolution is based on the concept of Genetic Algorithms. Genetic algorithms (GAs) are a whole class of optimization algorithms of rather general applicability and are particularly well adapted for high-dimensional discrete search spaces. A genetic algorithm tries to mimic nature by simulating a population of feasible solutions to a(n optimization) problem as they evolve through several generations and survival of the fittest is enforced. There are two basic mechanisms for generating a new generation from the previous one. One is cross-breeding in which two individuals (feasible solutions) are combined to produce two offspring. The other one is mutation. With a given mutation probability, any individual can change any of their params to another valid value. Survival of the fittest is enforced by letting fitter individuals cross-breed with higher probability than less fit individuals. The fitness of an individual is of course the negative of the loss function.
