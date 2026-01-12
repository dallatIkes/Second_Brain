---
aliases:
  - IA
---
"Faire exécuter par l'ordinateur des tâches pour lesquelles l'Homme est aujourd'hui meilleur que la machine" - sinon ça devient de l'algorithmique

---
# [Elements of AI](https://course.elementsofai.com)

## Chapter I - What is [[AI]] ?

- Autonomous and adaptive systems
- Turing test (chatbot)
- Chinese room thought experiment

![[Pasted image 20250821131955.png]]

## Chapter II - [[AI]] problem solving

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

## Chapter III - Real world [[AI]]

### Odds and probability

Modern [[AI]] methods work in real life du to their ability to deal with uncertainty.

In general, if the odds in favor of an event are $x:y$, the probability of the event is given by $\frac{x}{x+y}$ 

### The Bayes rule

**Likelihood ratio :** probability of the observation in case of event / probability of the observation  
**Example :** It rains 9 days out of 10, so the likelihood ratio is $\frac{9/10}{1/10}=9$ 

**Bayes formula :** $\text{posterior odds}=\text{likelihood ratio}\times\text{prior odds}$  
In other words : $$P(A|B)=\frac{P(B|A)\times P(A)}{P(B)}$$ 
Proof : $$\text{We know that }P(A|B)=\frac{P(A\cap B)}{P(B)}\text{ and }P(B|A)=\frac{P(B\cap A)}{P(A)}\text{ hence }P(B\cap A) = P(A\cap B) = P(B|A)P(A)\text{ so } P(A|B)=\frac{P(B|A)\times P(A)}{P(B)}$$
### Naive Bayes [[Classification|classification]]

[[Machine Learning]] technique used to classify objects into classes (called naive because of the models oversimplification of reality).

Example : Spam filter

## Chapter IV - [[Machine Learning]]

Modified National Institute of Standards and Technology (MNIST) dataset
![[Pasted image 20250822174224.png]]

### The types of [[Machine Learning]]

- **Supervised learning :** given an input, the task is the predict the correct output (ex: recognizing an hand-written number) here we talk more of ![[Classification|classification]]
- **Unsupervised learning :** there are no labels or outputs, the task is to discover the structure of the data (clustering similar items) (ex: supermarket customers)  here we talk more of ![[Clustering]]
- **Reinforcement learning :** the [[AI]] agent operates in an environment where a delayed feedback is available (ex: self driving cars of games)

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

### [[Regression]]

![[Regression#Basics]]

## Chapter V - [[Neural networks]]

![[Pasted image 20250825211353.png]]

![[Pasted image 20250825211449.png]]

## Implications 

We CANNOT predict the future !

**The value alignement problem :** <iframe title="L'horreur existentielle de l'usine à trombones." src="https://www.youtube.com/embed/ZP7T6WAK3Ow?feature=oembed" height="113" width="200" allowfullscreen="" allow="fullscreen" style="aspect-ratio: 1.76991 / 1; width: 100%; height: 100%;"></iframe>

**Issue :** privacy from data collection (ethics)

---

[[Hierarchical models]]