![IronHack Logo](https://s3-eu-west-1.amazonaws.com/ih-materials/uploads/upload_d5c5793015fec3be28a63c4fa3dd4d55.png)

# Lab | Advanced MySQL

## Introduction

In this lab you will practice MySQL Subqueries and Action Queries. We will again use the publications database.

Create a `solutions.ipynb` file in the `your-code` directory to record your solutions to all challenges.

## Challenge 1 - Most Profiting Authors

In this challenge let's have a close look at the bonus challenge of the previous *SQL SELECT* lab -- **who are the top 3 most profiting authors**? Even if you have solved or think you have solved that problem in the previous lab, please still complete this challenge because the step-by-step guidances are helpful to train your problem-solving thinking.

In order to solve this problem, it is important for you to keep the following points in mind:

* In table `sales`, a title can appear several times. The royalties need to be calculated for each sale.

* Despite a title can have multiple `sales` records, the advance must be calculated only once for each title.

* In your eventual solution, you need to sum up the following profits for each individual author:
    * All advances which is calculated exactly once for each title.
    * All royalties in each sale.

Therefore, you will not be able to achieve the goal with a single SELECT query. Instead, you will need to follow several steps in order to achieve the eventual solution. Below is an overview of the steps:

1. Calculate the royalty of each sale for each author.

1. Using the output from Step 1 as a temp table, aggregate the total royalties for each title for each author.

1. Using the output from Step 2 as a temp table, calculate the total profits of each author by aggregating the advances and total royalties of each title.

Below we'll guide you through each step. In your `solutions.ipynb`, please include the SELECT queries of each step so that your TA can review your problem-solving process.

### Step 1: Calculate the royalties of each sales for each author

Write a SELECT query to obtain the following output:

* Title ID
* Author ID
* Royalty of each sale for each author
    * The formula is:
        ```
        sales_royalty = titles.price * sales.qty * titles.royalty / 100 * titleauthor.royaltyper / 100
        ```
    * Note that `titles.royalty` and `titleauthor.royaltyper` are divided by 100 respectively because they are percentage numbers instead of floats.

In the output of this step, each title may appear more than once for each author. This is because a title can have more than one sales.

### Step 2: Aggregate the total royalties for each title for each author

Using the output from Step 1, write a query to obtain the following output:

* Title ID
* Author ID
* Aggregated royalties of each title for each author
    * Hint: use the *SUM* subquery and group by both `au_id` and `title_id`

In the output of this step, each title should appear only once for each author.

### Step 3: Calculate the total profits of each author

Now that each title has exactly one row for each author where the advance and royalties are available, we are ready to obtain the eventual output. Using the output from Step 2, write a query to obtain the following output:

* Author ID
* Profits of each author by aggregating the advance and total royalties of each title

Sort the output based on a total profits from high to low, and limit the number of rows to 3.

## Challenge 2

Elevating from your solution in Challenge 1 , create a table named `most_profiting_authors` to hold the data about the most profiting authors. The table should have 2 columns:

* `au_id` - Author ID
* `profits` - The profits of the author aggregating the advances and royalties

Include your solution in `solutions.ipynb`.



