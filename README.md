# Python Rank Choice Voting Assignment

The residents of Middle Earth have seen a lot about ranked-choice voting in the news lately and have decided to hold elections for the newly created office of President of Middle Earth.

* https://ballotpedia.org/Ranked-choice_voting_(RCV)
* https://en.wikipedia.org/wiki/Instant-runoff_voting
* https://utgop.org/rcv/
* https://politics.stackexchange.com/questions/9749/clarification-on-ranked-choice-voting-tie-breaker-algorithm

## Gollum for President

![Gollum for President Issues](/images/GollumPresident1.jpg)

![Gollum for President Issues](/images/GollumPresidentIssues.jpg)

## Ranked-choice Voting Simulator

Write a Python program to simulate ballots for an election and tabulate the results to find the winner of a simulated election using ranked-choice voting algorithms.


### List of candidates

* Create a list called `candidates` which has the names of individuals being considered for office.

<details>
  <summary>Sample code</summary>
  
  ```Python
  candidates = ['Aragorn','Arwen','Bilbo','Elrond','Faramir','Frodo','Gandalf','Gimli','Gollum', 'Legolas','Saruman']
  ```
  
</details>


### Simulate ballots

* Import the `random` package.
* Create an empty list called `ballots`.
* Create a variable called `ballots_count` and assign the number of ballots you want to simulate.
* Create simulated ballots by randomly selecting members from the `candidates` list. (I used the `random.sample()` function from the `random` package.) 
* Add each simulated ballot to the `ballots` list so you end up with a list of lists.

<details>
  <summary>Sample code</summary>
  
```Python
import random

ballots = []
ballots_count = 20

for i in range (0,ballots_count):
    random_number = random.randint(1, len(candidates))
    ballots.append(random.sample(candidates,random_number))
```
  
</details>
