
 ----

# Introducing Neural Networks

Neural Networks or Artificial Neural Networks (ANN) are a type of [[What is Machine Learning |Machine Learning]] 

![Set_Map_1.png | center | 256](Set_Map_1.png)


**Note:** Deep Neural Networks is neural network with two or more [[hidden layers]] 

# Brief History
Since the advent of **computers**, scientists have been formulating ways to enable machines to take input and produce desired output for tasks like [Classification](https://www.investopedia.com/terms/r/regression.asp) and [Regression](https://www.investopedia.com/terms/r/regression.asp). Additionally, in general, there’s **supervised** and **unsupervised machine learning**. [[Supervised Learning]] is used when you have pre-established and labeled data that can be used for training. 

---- 
Let’s say you have **sensor data** for a **server** with metrics such as upload/download rates, temperature, and humidity, all organized by time for every 10 minutes. Normally, this server operates as intended and has no outages, but sometimes parts fail and cause an outage. We might collect data and then divide it into two classes: one class for times/observations when the server is operating normally, and another class for times/observations when the server is experiencing an outage. When the server is failing, we want to label that sensor data leading up to failure as data that preceded a failure. When the server is operating normally, we simply label that data as “normal.”

----

What each sensor measures in this example is called a **feature**. A group of features makes up a feature set (represented as vectors/arrays), and the values of a feature set can be referred to as a sample. Samples are fed into **neural network models** to train them to fit desired outputs from these inputs or to predict based on them during the inference phase.

The “normal” and “failure” labels are **classifications** or **labels**. You may also see these referred to as **targets** or **ground-truths** while we fit a machine learning algorithm. These targets are the classifications that are the goal or target, known to be true and correct, for the algorithm to learn. For this example, the aim is to eventually train an algorithm to read sensor data and accurately predict when a failure is imminent. This is just one example of supervised learning in the form of **classification**. In addition to classification, there’s also **regression**, which is used to predict numerical values, like stock prices. There’s also **unsupervised machine learning**, where the machine finds structure in data without knowing the labels/classes ahead of time. There are additional concepts (e.g., **reinforcement learning** and **semi-supervised machine learning**) that fall under the umbrella of neural networks. For this book, we will focus on classification and regression with neural networks, but what we cover here leads to other use-cases.

**Neural networks** were conceived in the 1940s, but figuring out how to train them remained a mystery for 20 years. The concept of **backpropagation** (explained later) came in the 1960s, but neural networks still did not receive much attention until they started winning competitions in 2010. Since then, neural networks have been on a meteoric rise due to their sometimes seemingly magical ability to solve problems previously deemed unsolvable, such as image captioning, language translation, audio and video synthesis, and more.

Currently, **neural networks** are the primary solution to most competitions and challenging technological problems like **self-driving cars**, calculating risk, detecting fraud, and early cancer detection, to name a few.