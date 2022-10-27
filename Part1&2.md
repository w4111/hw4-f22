# Homework 4

* Assigned: 11/01 Thursday
* Due: 11/29 Tuesday, 11:59 PM.
* Value: 3.75% of your grade

# HW4 consists of 3 parts

Please find corresponding instructions in the repo.

## [Part 1 & 2 in Gradescope](https://www.gradescope.com)

# Part 1

**Note: All questions are designed to have just one numerical answer. In each of the below blanks, please enter only a numerical value (without leading zeros) as the answer. For example, say the answer to Question 1.1 is 1000 pages. Please enter "1000" in the blank (without the quotes).**

Assume a table Emp(**ssn**, name, salary) of employee records, where `ssn` is the primary key.  Assume the following characteristics:

* Num records = 6,688,000 records
* Page size = 8000 bytes
* Tuple size = 100 bytes
* Directory entry size = 10 bytes
* No other overhead when storing data on pages.
* You can assume that there are no overflow pages in the hash index
* The queries always return a result

Clarification

* assume that each page accessed is from disk (memory only has space for one page)
* For questions that do not specify fill factor, please assume 100% fill.
* For questions without indexes, please assume the file type as: Unsorted heap

### Q1.1

Suppose we run `select name from Emp where ssn=1000`.

If there are no indices, how many page accesses does this query cost **on average**?

[____]

### Q1.2

Suppose we run `select name from Emp where ssn=1000`.

Assume a **primary** B+-tree index on `emp(ssn)`, and fill factor of 1. How many page accesses will the query cost?

It will be helpful to compute (you only need to submit the final cost)

* Number of leaf pages
* Fan out 
* Height of the tree

[____]

### Q1.3

Suppose we run `select name from Emp where ssn=1000`.

Assume only a **secondary** B+-tree on `emp(ssn)`, and fill factor of 1. How many page accesses will the query cost?

It will be helpful to compute (you only need to submit the final cost)

* Number of leaf pages
* Fan out 
* Height of the tree

[____]

### Q1.4

What is the cost for **Q1.3** if the fill factor is **50%**?

[____]

### Q1.5

Suppose we run `select name from Emp where ssn=1000`.

Assume only a secondary hash index on `Hash(emp.ssn)`. How many page accesses will the query cost?

[____]

### Q1.6

Suppose we run `select max(salary) from Emp`

Assuming no indices, how many disk accesses are required to run this query?

[____]


### Q1.7

Suppose we run `select max(salary) from Emp`

How many disk accesses are required if there is a secondary B+ tree index on `emp(salary)`?

[____]



# Part 2

Assume schedule S as
**S: R3(e) W4(a) R1(b) R1(c) W3(e) R4(e) W1(c) W2(b) C2 W3(c) C3 W4(c) C4 W1(d) C1**
where Ri(a)/Wi(a) indicates transaction Ti reads/writes data item a, and Ci indicates Ti commits.


### Q2.1
Show the precedence graph of S.

### Q2.2
Is S serializable? Explain.

### Q2.3
Enumerate all serial schedules that are equivalent to S.

### Q2.4
Is this a valid schedule under Strict 2PL? If yes, give an **example**. If not, show the **first** operation that is not allowed under Strict 2PL and explain.