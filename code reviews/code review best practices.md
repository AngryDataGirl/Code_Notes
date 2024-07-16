
- [Reference(s)](#references)
- [purpose of code reviews](#purpose-of-code-reviews)
- [standard guidelines](#standard-guidelines)
- [principles](#principles)
- [what to look for in code review](#what-to-look-for-in-code-review)
  - [design](#design)
  - [functionlity](#functionlity)
  - [complexity](#complexity)
  - [tests](#tests)
  - [naming](#naming)
  - [comments](#comments)
- [every line](#every-line)
- [good things](#good-things)
- [speed of code review](#speed-of-code-review)
- [tips on writing code review comments](#tips-on-writing-code-review-comments)
- [code review tips for SQL specifically](#code-review-tips-for-sql-specifically)
  - [join order](#join-order)
    - [biggest dataset on left](#biggest-dataset-on-left)
    - [exploding joins (duplications)](#exploding-joins-duplications)
    - [imploding joins (losing rows)](#imploding-joins-losing-rows)
  - [input data](#input-data)
  - [clear and logical CTE](#clear-and-logical-cte)
  - [where clause on left join](#where-clause-on-left-join)

# Reference(s)
1. (Standard of Code Review, Google eng-practices)[https://google.github.io/eng-practices/review/reviewer/standard.html]
2. https://coffeeanddata.ca/PR-reviews-for-SQL-code

# purpose of code reviews 
- improve code health over time
- make progress
- ensure quality 

# standard guidelines
- doesn't have to be perfect but if it improves the overall code health, then CL should be approved 
- no such thing as "perfect code" only better code 
- use `Nit:` to prefix polish tips that person can choose to ignore 

# principles
- technical facts , data an principles of software design overrule opinions and personal prefs
- otherwise be consistent with current codebase 
- style guide should be absolute authority 

# what to look for in code review 
  ## design
  - do interactions make sense?
  - does change belong in codebase?
  - does it integrate well?
  ## functionlity
  - does the code do what the dev intended? (users are both end users and devs who have to use code in future)
  - think about edge cases, concurrency problems and bugs
  ## complexity 
  - are individual lines too complex?
  - are functions too complex?
  - are classes to complex?
  - is it over-engineered? ie, code too generic, future problem to be solved once it arrives and once you have actual requirements\
  ## tests
  - Will the tests actually fail when the code is broken? 
  - If the code changes beneath them, will they start producing false positives? 
  - Does each test make simple and useful assertions? 
  - Are the tests separated appropriately between different test methods?
  ## naming
  - good names? fully communicates what item does withotu being so long that it becomes hard to read 
  ## comments
  - comments are useful when they explain why code exists, and not just explain what some code is doing
  - if code is not clear enough to explain itself then the code should be made simpler 

# every line
- you're supposed to look at every line of code you've been assigned to review
- if you don't understand it and it's slowing down the review, you should let the developer know 

# good things
- tell something nice to dev when you see good practices 

# speed of code review
- If you are not in the middle of a focused task, you should do a code review shortly after it comes in.
- One business day is the maximum time it should take to respond to a code review request (i.e., first thing the next morning).
- Following these guidelines means that a typical CL should get multiple rounds of review (if needed) within a single day.

# tips on writing code review comments 
- Be kind.
- Explain your reasoning.
- Balance giving explicit directions with just pointing out problems and letting the developer decide.
- Encourage developers to simplify code or add code comments instead of just explaining the complexity to you.

# code review tips for SQL specifically

## join order 

### biggest dataset on left
```sql
SELECT *
FROM big_table
JOIN medium_table USING (_key1)
JOIN small_table USING (_key2)
```
### exploding joins (duplications)
- ensure every grain is as expected
- if first row has 1 in second column then good , grain is respected
  
```sql
SELECT grain, count (*)
FROM table
GROUP BY 1
ORDER BY 2 DESC
LIMIT 10
```

### imploding joins (losing rows)

```sql
SELECT count (*)
FROM table_a
JOIN table_b
 ON table_a.id = table_b.id
```


```sql
SELECT count (*)
FROM table_a
FULL OUTER JOIN  table_b
 ON table_a.id = table_b.id
```

## input data
- does data already exist?

## clear and logical CTE
- logical and ordered, sequential if possible 
- make sure each grain of CTE is clear 
- CTEs have clear and self explanatory names 

## where clause on left join 
- if there's a where clause on the right table, it's back to an `INNER JOIN` since any NULL from the right table gets deleted by the WHERE 
- make sure there is no WHERE clause on the right table 