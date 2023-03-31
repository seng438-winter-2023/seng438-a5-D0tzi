**SENG 438- Software Testing, Reliability, and Quality**

**Lab. Report \#5 – Software Reliability Assessment**

| Group \#:      |   7  |
| -------------- | --- |
|Brenek Spademan               |30060822    |
|Ben Leggett                |30114359     |
|Arion Hamel                |30112662     |
|Jack Rovere                |30085670     |

# Introduction
In assignment 5 we aim to familiarize ourselves with reliability assessment using the reliability assessment techniques of reliability growth testing and developing reliability demonstration charts. This testing will be done using tools such as C-SFRAT and RDC-11. Similar to assignment 4, no one in the group has any previous experience with either of the testing techniques/methods and their associated tools. 

This assignment has the following objectives:
 * Introduce us to reliability growth testing and reliability demonstration charts. 
 * Give us practice with the reliability assessment tools C-SFRAT and RDC-11
 * Learn to measure the failure rate, MTTF, and overall reliability of the system under test through data analysis. 

The group began the reliability growth testing by first familiarizing our-selves with C-SFRAT and gaining an understanding of how it worked. Once we were familiar with C-SFRAT we used the tool to display time-between-failures, failure intensity and reliability graphs. Once the group moved on to part 2, we used RDC-11 to analyze whether the target failure rate and MTTF had been met. 

Below we go into further detail about our process and findings:
# 

# Assessment Using Reliability Growth Testing 

<img width="1197" alt="image" src="https://user-images.githubusercontent.com/98235387/228976814-97ec68a5-7e85-4062-9cb4-bff0c5900883.png">

<img width="1200" alt="image" src="https://user-images.githubusercontent.com/98235387/228977200-548cda7d-4a66-4d2d-a62f-e98a57b3d99d.png">

<img width="1200" alt="image" src="https://user-images.githubusercontent.com/98235387/228978355-23db8da4-0bea-4161-a1a8-4b74b56e80cb.png">

<h3>Result of model comparison (selecting top two models):</h3>

As seen above, the top two models selected to fit our failure data was the S distribution model and negative binomial 2 distribution model. They tend to fit closer to the shape of our data in the intensity graph as well. You may assume that these two models are similar due to the visually close resemblance they share. However they differ quite a lot, in which the S model is a parametric model that assumes time between failures follows an exponential distribution; whereas the NB2 model is a non-parametric model that assumes the time between failures follows a non-homogenous Poisson process. Further, because the NB2 model has a lower calculated AIC and BIC, the NB2 model is more suitted to this data than the S model

<h3>Result of range analysis (an explanation of which part of data is good for proceeding with the analysis):</h3>

When deciding what range of data to analyze, we must consider if the SUT has changed, or if the data is old. In our case, we have no indication of the SUT or it's version. We cannot presume when the failures occured. However because our data has only 54 failures, we can assume that it is relatively recent failure data as 40-50 failures is often the standard for proper analysis. Therefore we can analyze the data from the first interval to the end. 

<h3>A discussion on decision making given a target failure rate:</h3>

Target failure rate pertains to a desired or acceptable failure rate for a software system, in which a higher target failure rate implies a higher number of acceptable system failures, and vice versa. Target failure rate influences decision making by setting an expectation among developers to meet this rate. This is accomplished by increasing or decreasing the quantity of testing done on a system. Further, resource allocation and management is also affected as the target failure rate shifts towards more or less required testing. 

<h3>A discussion on the advantages and disadvantages of reliability growth analysis:</h3>

Reliability growth analysis provides a statistical method to analyze the improvement of software reliability against time. It is quantitative, systematic and cost-effective, allowing for timely intervention and improvement while providing objective means of measuring software reliability. It provides insights into deeper questions that a developer might ask, such as: Is the testing of the SUT sufficient? How is our reliability evolving? At what point do we believe our system will reach target reliability? This data is essential for allowing developers to make informed decisions, and improving the reliability of a system over time.

However, in order to properly analyze a system there is a heavy reliance on complex data within a limited scope. The nature of this analysis requires that we have extensive data on software failures and improvements, and that this data is accurate. It also requires specialized knowledge and tools - such as C-SFRAT - that some development teams may lack. Further, RGA fails to incorporate other factors that may contribute to overall software quality. 

# Assessment Using Reliability Demonstration Chart 

The RDC-11 EXCEL worksheet and macro was used alongside the provided failure data to create the Reliability Demonstration Charts (RDCs). 
The provided default risk values were used, and are as follows:
- Discrimination Ratio (γ) = 2  
- Developer's Risk (α) = 0.1  
- User's Risk (β) = 0.1  

The failure data used had to be modified as follows to due to the format the selected failure data was in. This was done by assuming that the failure count was uniformly distributed over the interval it occured in. For example, data where Failure Observation Number (T), Count of Failures (FC), and total time for T to occur (E) are as follows 

![image](https://user-images.githubusercontent.com/101438680/229073461-b11e6342-fe04-49f6-8f43-27541235dbf6.png)

 Would be converted as follows: T=1, there is one failure so it can be assumed that the time between failures is 0.01, T=2 there are two failures so the time between failures are assumed to be at T=1.5 and T=2

![image](https://user-images.githubusercontent.com/101438680/229074684-e0d8adff-11b4-4c19-969b-a74e06bdd5a0.png)

And so the provided failure data is broken down in a way that each Failure Observation Number (T) is accounted for with the assumption that all failures happening in that interval are unifromly distibuted.

The FIO (Failure Intensity Objective) = Max Number of Errors (16) / Number of Input Events (5 Failure Observations) = 3.2, providing a calculated MTTF for the SUT where MTTF = 1/3.2 = 0.3125
<h3>3 plot for MTTFmin</h3>
![image](https://user-images.githubusercontent.com/101438680/229082850-09c53196-80b2-462b-9c24-5776df98c29f.png)  

<h3>3 plot for twice of the MTTFmin</h3>
![image](https://user-images.githubusercontent.com/101438680/229083211-09dc94af-7f44-4dce-a720-df3209491563.png)  


<h3>3 plots for half of the MTTFmin</h3>
![image](https://user-images.githubusercontent.com/101438680/229083393-a27f66e4-fec8-449b-b8e8-2af9012d340b.png)  

--

<h3>Explain your evaluation and justification of how you decide the MTTFmin</h3>  
Our MTTF minimum provides the best line of fit out of the three above charts, no pieces of the plot are within the rejection range and while there are many points indicating to continue testing, there are still some that have been accepted. The minimum MTTF for the system is the lowest MTTF value for the system to be considered acceptable. This was determined by experimentally adjusting the Failure Intensity Objective until a minimum, where the plot provided by the RDC just enters the accepted region of the chart, was found. 

Our MTTF if very low becuase the time between each of our tests was very short, and while the first few Failure Observations had only one to two counted failures, the following occurences had significantly larger failure counts that impacted the data.


--

<h3>A discussion on the advantages and disadvantages of RDC</h3>

Advantages of RDC:
 * Allows for estimation of the minimum and average MTTF.
 * Provides a clear visual representation of the required reliability level and whether or not that level is reached. 
 * Can be used to compare the reliability levels of systems. 
-------------------------------------------------------------
Disadvantages of RDC:
 * Results can be skewed by outliers 
 * Without a significant amount of data the results can be inaccurate 
 * Does not account for the fact that the failure rate can change over time. 

# 

# Comparison of Results

--

# Discussion on Similarity and Differences of the Two Techniques

Similarities:
 * Both techniques are used to evaluate the reliability of a system.
 * Both techniques require adequate data in order to provide accurate results.
 * Both techniques identify areas in the system that are lacking in reliability.
 * Both techniques enable the analyzer to determine if the target level of reliability has been met. 

Differences: 
 * Reliability growth testing is better suited for evaluating possible future performance, while RDC is better suited to evaluate the performance of the software at the current state.
 * Reliability growth testing is a dynamic testing technique, while RDC is a static technique.
 * Reliability growth testing is an interactive process, while RDC uses a one-time analysis. 
 * Reliability growth testing is better for identifying defects, while RDC is better for demonstrating that software has met reliability requirements. 

# How the team work/effort was divided and managed

Jack and Arion focused on using C-SFRAT to analyze data and create charts using the failure data provided. 

Ben and Brenek used RDC-11 to create graphs with the failure data provided.

# Difficulties encountered, challenges overcome, and lessons learned

A difficulty the group had to overcome during this lab was deciphering exactly what we were supposed to do. The assignment guideline gave less detail than the previous four assignments. Our group overcame this challenge by all working together in order to decipher exactly what we were supposed to do; the group also used external educational resources to better understand the software we were using. A lesson learned by the group in this lab was to make sure we have educated ourselves on the software we are using as the group originally ran into some difficulties attempting to use the software before we fully understood how to actually use it.

# Comments/feedback on the lab itself

Overall our group found this lab to be quite different from the previous four labs. What we actually learned was beneficial to our understanding of course material, however our group initially struggled with the lack of direction provided in the assignment guideline. We feel that further instruction in the assignment guideline would greatly benefit students doing this assignment in the future. 
