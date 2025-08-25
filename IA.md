"Faire exécuter par l'ordinateur des tâches pour lesquelles l'Homme est aujourd'hui meilleur que la machine" - sinon ça devient de l'algorithmique

---
# [Elements of AI](https://course.elementsofai.com)

## Chapter I - What is AI ?

- Autonomous and adaptive systems
- Turing test (chatbot)
- Chinese room thought experiment

![[Pasted image 20250821131955.png]]

## Chapter II - AI problem solving

### Search and problem solving

#Terminology

- **State space :** set of possible situations 
- **Transitions :** possible moves from one state to the other ($\ne$ a path $\rightarrow$ multiple transitions)
- **Costs :** value we give the transitions (it can represent a distance, a weight, ...)
#### Chicken crossing problem

![chicken crossing with best path](https://course.elementsofai.com/static/2_1_chicken-crossing-4-57543f806699fab02de96a18ed42626b.svg)

![[Pasted image 20250821151342.png]]

#### Tower of Hanoi

![[Pasted image 20250821151421.png]]

### Search and games

#### Min-Max algorithm

**Tic-Tac-Toe**

![[Pasted image 20250821225312.png]]

Some game trees are simply too big to use the Min-Max algorithm (like chess or Go) hence the need to use heuristics.

## Chapter III - Real world AI

### Odds and probability

Modern [[IA|AI]] methods work in real life du to their ability to deal with uncertainty.

In general, if the odds in favor of an event are $x:y$, the probability of the event is given by $\frac{x}{x+y}$ 

### The Bayes rule

**Likelihood ratio :** probability of the observation in case of event / probability of the observation  
**Example :** It rains 9 days out of 10, so the likelihood ratio is $\frac{9/10}{1/10}=9$ 

**Bayes formula :** $\text{posterior odds}=\text{likelihood ratio}\times\text{prior odds}$  
In other words : $$P(A|B)=\frac{P(B|A)\times P(A)}{P(B)}$$ 
Proof : $$\text{We know that }P(A|B)=\frac{P(A\cap B)}{P(B)}\text{ and }P(B|A)=\frac{P(B\cap A)}{P(A)}\text{ hence }P(B\cap A) = P(A\cap B) = P(B|A)P(A)\text{ so } P(A|B)=\frac{P(B|A)\times P(A)}{P(B)}$$
### Naive Bayes classification

Machine learning technique used to classify objects into classes (called naive because of the models oversimplification of reality).

Example : Spam filter

## Chapter IV - Machine Learning

Modified National Institute of Standards and Technology (MNIST) dataset
![[Pasted image 20250822174224.png]]

### The types of machine learning

- **Supervised learning :** given an input, the task is the predict the correct output (ex: recognizing an hand-written number)
- **Unsupervised learning :** there are no labels or outputs, the task is to discover the structure of the data (clustering similar items) (ex: supermarket customers) 
- **Reinforcement learning :** the [[IA|AI]] agent operates in an environment where a delayed feedback is available (ex: self driving cars of games)

**Be aware of overfitting :** "trying to be too smart" - adding too much rules to a model so that it works well on the training data, but it may have terrible results in testing data.

### The nearest neighbor classifier

One of the simplest possible classifiers, based on the notion of distance between instances that must be clearly defined (Euclidean distance, pixel-by-pixel matches, ...).

Ex: predicting the next shopping item :

<table>
  <thead>
    <tr>
      <th>User</th>
      <th colspan="4">Merged Header</th>
      <th>Purchase</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Sanni</td>
      <td>boxing gloves</td>
      <td>Moby Dick (novel)</td>
      <td>headphones</td>
      <td>sunglasses</td>
      <td>coffee beans</td>
    </tr>
    <tr>
      <td>Jouni</td>
      <td>t-shirt</td>
      <td>coffee beans</td>
      <td>coffee maker</td>
      <td>coffee beans</td>
      <td>coffee beans</td>
    </tr>
    <tr>
      <td>Janina</td>
      <td>sunglasses</td>
      <td>sneakers</td>
      <td>t-shirt</td>
      <td>sneakers</td>
      <td>ragg wool socks</td>
    </tr>
    <tr>
      <td>Henrik</td>
      <td>2001: A Space Odyssey (dvd)</td>
      <td>headphones</td>
      <td>t-shirt</td>
      <td>boxing gloves</td>
      <td>flip flops</td>
    </tr>
    <tr>
      <td>Ville</td>
      <td>t-shirt</td>
      <td>flip flops</td>
      <td>sunglasses</td>
      <td>Moby Dick (novel)</td>
      <td>sunscreen</td>
    </tr>
    <tr>
      <td>Teemu</td>
      <td>Moby Dick (novel)</td>
      <td>coffee beans</td>
      <td>2001: A Space Odyssey (dvd)</td>
      <td>headphones</td>
      <td>coffee beans</td>
    </tr>
	<tr>
	 <td>Travis</td>
	 <td>green tea</td>
	 <td>t-shirt</td>
	 <td>sunglasses</td>
	 <td>flip flops</td>
	 <td>?</td>
	</tr>
  </tbody>
</table>


Travis's Shopping history is more similar to Ville's (3 matching items) so our prediction is : sunscreen

### Regression

Regression is a bit different form classification because it doesn't produce a whole number. It is best suited to predict prices, distances and so on.

The basic idea in linear regression is to add up the feature variables to produce the predicted value. The technical term for adding up process is linear combination. 

**Intercept :** technical term for the starting point before any input (ex: women that don't smoke nor eat vegetables, number of lines of code written without drinking any coffee).

**Ex:** Suppose that we're given the gender, the amounts of cigarettes smoked and vegetables handfuls eaten and the life expectancy of many people. With linear regression it is possible to find the weight of every input.
**Ex:** find the price of each item given the bill with the total and the amount of products bought.

**Logistic regression** is used to find the label of a test data with regression
![[Pasted image 20250823223836.png]]

## Chapter V - Neural networks

### Neural network basics

