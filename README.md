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
  def drop_low(ballots_list, remove_list):
    copy_list = copy.deepcopy(ballots_list)
    for ballot in copy_list:
        for item in remove_list:
            if item in ballot:
                ballot.remove(item)
    return copy_list
  ```
  
</details>


