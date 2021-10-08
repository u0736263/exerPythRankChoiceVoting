# Python Ranked-Choice Voting Assignment

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

A note about the sample code presented in this assignment: This is one way of accomplishing this task. It's not guaranteed to be the best way or most efficient way. This is simply an example of trying to break a problem down into steps and coding each step. If you can come up with your own solution, try it out. I'd love to see it.


### Create list of candidates: `candidates`

* Create a list called `candidates` which has the names of individuals being considered for office.

<details>
  <summary>Sample code</summary>
  
  ```Python
  candidates = ['Aragorn','Arwen','Bilbo','Elrond','Faramir','Frodo','Gandalf','Gimli','Gollum', 'Legolas','Saruman']
  ```
  
</details>


### Create list of simulated ballots: `ballots`

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


### Create function: `counts()`

* Create a function called `counts` which accepts a parameter called `ballotsList`.
* This function will accept a list of ballots and calculate counts from the first choice on each ballot and store count totals for candidates in a dictionary using the name of the candidate as the key and the number of votes as the value.
* Have the function create an empty dictionary called `results`.
* Loop through the ballots in the list `ballotsList`.
  * If there is no ballot, continue to the next step.
  * If the first name in the ballot is NOT found in the dictionary `results`, add the name to the dictionary and set the count to 1.
  * If the first name in the ballot is found in the dictionary `results`, increment the count for that name up by 1.
* return the dictionary `results`.

<details>
  <summary>Sample code</summary>
  
  ```Python
  def counts(ballotsList):
    results = {}
    for ballot in ballotsList:
        if not ballot:
            continue
        elif ballot[0] not in results:
            results[ballot[0]] = 1
        else:
            results[ballot[0]] += 1
    return results
  ```
  
</details>


### Create function: `create_report()`

* Create a function called `create_report` which accepts a parameter called `dict`.
* This function will accept a dictionary with candidate names as keys and counts of votes for each candidate as values and generate text of a summary report for some select results.
* Have the function include text for the value for the lowest count using the format `low count: [value]` on a separate line.
* Have the function include text for a list of the names that have the low count using the format `remove: [list]` on a separate line.
* Have the function include text for the value for the highest count using the format `high count: [value]` on a separate line.
* Have the function include text for a list of the names that have the high count using the format `lead: [list]` on a separate line.
* return the text for the report.

<details>
  <summary>Sample code</summary>
  
  ```Python
  def create_report(dict):
    text = ''
    text += 'low count: ' + str(min(dict.values())) + '\n'
    text += 'remove: ' + str(key_list(dict, min(dict.values()))) + '\n'
    text += 'high count: ' + str(max(dict.values())) + '\n'
    text += 'lead: ' + str(key_list(dict, max(dict.values()))) + '\n'
    return text
  ```
  
</details>


### Create function: `key_list()`

* Create a function called `key_list` which accepts parameters called `dict` and `num`.
* This function will accept a dictionary with candidate names as keys and counts of votes for each candidate and a number value and generate a list of names from the dictionary keys which have a value which matches the number submitted as a parameter.
  * Create an empty list called `names`.
  * Loop through the dictionary keys and values.
  * If the value for a key matches the value for `num`, add the dictionary key to the list `names`.
* return the list `names`.

<details>
  <summary>Sample code</summary>
  
  ```Python
  def key_list(dict, num):
    names = []
    for key, value in dict.items():
        if value == num:
            names.append(key)
    return names
  ```
  
</details>


### Create function: `drop_low()`

* Create a function called `drop_low` which accepts parameters called `ballots_list` and `remove_list`.
* This function will accept a list of ballots and a list of names to remove from ballots, create a copy of the list of ballots, and remove names on `remove_list` from the copy of `ballots_list`.
* Import the `copy` package.
  * Create a deep copy of `ballots_list` called `copy_list`. (A deep copy of a list allows you to make changes to the copy without affecting the original.)
  * Loop through the ballots in `copy_list` and remove each name in `remove_list` from the ballots in `copy_list`.
* return the list `copy_list`.

<details>
  <summary>Sample code</summary>
  
  ```Python
  import copy
  
  def drop_low(ballots_list, remove_list):
    copy_list = copy.deepcopy(ballots_list)
    for ballot in copy_list:
        for item in remove_list:
            if item in ballot:
                ballot.remove(item)
    return copy_list
  ```
  
</details>


### Report information about the simulated election

* Print a list of the candidates using the format `The candidates are: ` and a list of the candidates.
* Print the total number of ballots using the format `total ballots: [value]`.
* Determin how many votes are needed to win and assign that number to a variable named `majority` and print the result using the format `needed to win: [value]`.

<details>
  <summary>Sample code</summary>
  
  ```Python
import math

# get starting information about the vote
print("The candidates are: ", candidates)
print("total ballots: ", len(ballots))

# determine how many votes needed to win
if (len(ballots) % 2) == 0:
    majority = math.ceil(len(ballots) * .5) + 1
else:
    majority = math.ceil(len(ballots) * .5)
print("needed to win: ", majority, '\n\n\n')
  ```
  
</details>


### Run the simulated election and print the result of each round

* Create a variable called `winner` which is an empty string.
* Create a variable called `round` and give it a starting value of 1.
* Create an empty list called `adjusted_ballots`.
* Append the list `ballots` into `adjusted_ballots`.
* Create a while loop which runs while the variable `winner` is empty.
  * Count the ballots.
    * Hint: `results = counts(adjusted_ballots[(round-1)])`
  * Print the results for the round.
    * Hint: `report = create_report(results)`
  * Check to see if a majority has been reached. If it has, assign the winner.
    * Hint: `winner = key_list(results, max(results.values()))`
  * If there is no winner, remove candidates with low votes.
    * Hint: `adjusted = drop_low(adjusted_ballots[(round-1)],remove_list)`
  * Add the latest round of adjusted ballots to the `adjusted_ballots` list.
* Print the winner using the format `The winner is: ` and the name of the winner. 

<details>
  <summary>Sample code</summary>
  
  ```Python
winner = ''
round = 1
adjusted_ballots = []
adjusted_ballots.append(ballots)

while winner == '':
    # count the ballots
    results = counts(adjusted_ballots[(round-1)])
    print("results from round ", round, "-", results)
    report = create_report(results)
    print(report)
    
    # check to see if majority reached
    if max(results.values()) >= majority:
        winner = key_list(results, max(results.values()))
    else:
        print("no majority yet\n\n")
        
        
    # remove low votes
    remove_list = key_list(results, min(results.values()))
    adjusted = drop_low(adjusted_ballots[(round-1)],remove_list)
    adjusted_ballots.append(adjusted)
    
    # increment the round variable
    round += 1
    
print("The winner is: ",winner)
  ```
  
</details>


