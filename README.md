# Data_Science_Probability

# HarvardX: PH125.3x | Data Science: Probability

## Abstract

This is the third in a series of courses in a [Professional Certificate in Data Science program](https://www.edx.org/professional-certificate/harvardx-data-science). The courses in the Professional Certificate program are designed to prepare you to do data analysis in R, from simple computations to machine learning. The courses are designed to be taken in order. A prerequisite for this course is courses 1 and 2 of the series or equivalent knowledge of basic R coding and data visualization. If you need to learn or refresh some basic R, check out Data Science: R Basics, the first course in this series.

The textbook for the Data Science course series is [freely available online](https://rafalab.github.io/dsbook/). This course corresponds to the Probability section of textbook, starting [here](https://rafalab.github.io/dsbook/probability.html).

This course assumes you are comfortable with basic math, algebra, and logical operations. HarvardX has partnered with DataCamp for all assignments in R that allow you to program directly in a browser-based interface. You will not need to download any special software.

Using a combination of a guided introduction through short video lectures and more independent in-depth exploration, you will get to practice your new R skills on real-life applications.

Probability theory is the mathematical foundation of statistical inference which is indispensable for analyzing data affected by chance, and thus essential for data scientists. In this course, you will learn important concepts in probability theory. The motivation for this course is the circumstances surrounding the financial crisis of 2007-2008. Part of what caused this financial crisis was that the risk of certain securities sold by financial institutions was underestimated. To begin to understand this very complicated event, we need to understand the basics of probability. We will introduce important concepts such as random variables, independence, Monte Carlo simulations, expected values, standard errors, and the Central Limit Theorem. These statistical concepts are fundamental to conducting statistical tests on data and understanding whether the data you are analyzing are likely occurring due to an experimental method or to chance. Statistical inference, covered in the next course in this series, builds upon probability theory.

## Learning Objectives
- Important concepts in probability theory including random variables and independence
- How to perform a Monte Carlo simulation
- The meaning of expected values and standard errors and how to compute them in R
- The importance of the Central Limit Theorem

Course Overview

Section 1: Discrete Probability
You will learn about basic principles of probability related to categorical data using card games as examples.

Section 2: Continuous Probability
You will learn about basic principles of probability related to numeric and continuous data.

Section 3: Random Variables, Sampling Models, and The Central Limit Theorem
You will learn about random variables (numeric outcomes resulting from random processes), how to model data generation procedures as draws from an urn, and the Central Limit Theorem, which applies to large sample sizes.

Section 4: The Big Short
You will learn how interest rates are determined and how some bad assumptions led to the financial crisis of 2007-2008.
Section 1 Overview

Section 1 introduces you to Discrete Probability. Section 1 is divided into three parts:

    Introduction to Discrete Probability
    Combinations and Permutations
    Addition Rule and Monty Hall

After completing Section 1, you will be able to:

    Apply basic probability theory to categorical data.
    Perform a Monte Carlo simulation to approximate the results of repeating an experiment over and over, including simulating the outcomes in the Monty Hall problem.
    Distinguish between: sampling with and without replacement, events that are and are not independent, and combinations and permutations.
    Apply the multiplication and addition rules, as appropriate, to calculate the probably of multiple events occurring.
    Use sapply instead of a for loop to perform element-wise operations on a function.

The textbook for this section is available here
1.1 Introduction to Discrete Probability
Discrete Probability

Example 1: If I have two red beads and three blue beads inside an urn and I pick one at random, what is the probability of picking a red one?

red <- 2
blue <- 3
beads <- red + blue
p <- red/beads
p

## [1] 0.4

Monte Carlo Simulation

Random number generators permit us to mimic the process of picking at random. An example is the sample() function in R.

beads <- rep(c("red", "blue"), times = c(2,3))
beads

## [1] "red"  "red"  "blue" "blue" "blue"

#use sample() to pick a bead at random:
sample(beads, 1)

## [1] "blue"

An example of Monte Carlo Simulation is that repeat the experiment a large enough number of times to make the results practically equivalent to doing it over and over forever. To perform our first Monte Carlo simulation, we use the replicate() function, which permits us to repeat the same task any number of times. Here, we repeat the random event B = 10,000 times

B <- 10000
events <- replicate(B, sample(beads, 1))

#Use table to see the distribution:
tab <- table(events)
tab

## events
## blue  red 
## 5902 4098

#and prop.table gives us the proportions:
prop.table(tab)

## events
##   blue    red 
## 0.5902 0.4098

The function sample has an argument that permits us to pick more than one element from the urn. However, by default, this selection occurs without replacement.

#Without Replacement:
sample(beads, 5)

## [1] "blue" "red"  "red"  "blue" "blue"

sample(beads, 5)

## [1] "red"  "blue" "red"  "blue" "blue"

sample(beads, 5)

## [1] "blue" "blue" "red"  "blue" "red"

#With Replacement:
events <- sample(beads, B, replace = TRUE)
prop.table(table(events))

## events
##   blue    red 
## 0.5982 0.4018

Probability Distributions

If you’re are randomly calling likely voters from a population that has 44% Democrat, 44% Republican, 10% undecided, and 2% green, these proportions define the probability for each group. For this example, the probability distribution is simply these four proportions.
Independence

Every time we toss a fair coin, the probability of seeing heads is 1/2 regardless of what previous tosses have revealed.
Non-Independent Events

The first outcome affects the second. If we deal a King for the first card, and don’t replace it into the deck, the probabilities of a second card being a King is less because there are only three Kings left: the probability is 3 out of 51. more…
Assessment 1: Introduction to Discrete Probability

    Probability of cyan
    One ball will be drawn at random from a box containing: 3 cyan balls, 5 magenta balls, and 7 yellow balls. What is the probability that the ball will be cyan?

cyan <- 3
magenta <- 5
yellow <- 7
balls <- cyan + magenta + yellow
p_cyan <- cyan/balls
p_cyan

## [1] 0.2

    Probability of not cyan
    One ball will be drawn at random from a box containing: 3 cyan balls, 5 magenta balls, and 7 yellow balls. What is the probability that the ball will not be cyan?

cyan <- 3
magenta <- 5
yellow <- 7
balls <- cyan + magenta + yellow
p_cyan <- cyan/balls
p_not_cyan= 1 - p_cyan
p_not_cyan

## [1] 0.8

#or
p_not_cyan= (magenta+yellow)/balls
p_not_cyan

## [1] 0.8

    Sampling without replacement
    Instead of taking just one draw, consider taking two draws. You take the second draw without returning the first draw to the box. We call this sampling without replacement. What is the probability that the first draw is cyan and that the second draw is not cyan?

#p=p1_cyan * p2_not_cyan, without replacement
p_1= cyan/balls 
p_2=1 - (cyan-1)/(balls-1)
p_1 * p_2

## [1] 0.1714286

    Sampling with replacement
    Now repeat the experiment, but this time, after taking the first draw and recording the color, return it back to the box and shake the box. We call this sampling with replacement. What is the probability that the first draw is cyan and that the second draw is not cyan?

#p=p1_cyan * p2_not_cyan, with replacement
p_1= cyan/balls
p_2=1 - cyan/balls
p_1 * p_2

## [1] 0.16

1.2 Combinations and Permutations

let’s start by constructing a deck of cards using R. For this, we will use the function expand.grid() and the function paste()

Here is how we generate a deck of cards:

suits <- c("Diamonds", "Clubs", "Hearts", "Spades")
numbers <- c("Ace", "Deuce", "Three", "Four", "Five", 
             "Six", "Seven", "Eight", "Nine", "Ten", 
             "Jack", "Queen", "King")
deck <- expand.grid(number=numbers, suit=suits)
deck <- paste(deck$number, deck$suit)

With the deck constructed, we can now double check that the probability of a King in the first card is 1/13. We simply compute the proportion of possible outcomes that satisfy our condition:

kings <- paste("King", suits)
mean(deck %in% kings)

## [1] 0.07692308

which is 1/13.

Now, how about the conditional probability of the second card being a King given that the first was a King? Earlier, we deduced that if one King is already out of the deck and there are 51 left, then this probability is 3/51. Let’s confirm by listing out all possible outcomes.

To do this, we can use the permutations() function from the gtools package. For any list of size n, this function computes all the different combinations we can get when we select r items. Here are all the ways we can choose two numbers from a list consisting of 1,2,3:

#here all the ways we can choose 2 numbers from the list 1, 2, 3, 4, 5.
#Notice that the order matters. So 3, 1 is different than 1, 3, So it appears in our permutations.
#Also notice that 1, 1; 2, 2; and 3, 3 don't appear, because once we pick a number, it can't appear again.
library(gtools)
library(permutations)
library(dplyr)

permutations(5, 2)

##       [,1] [,2]
##  [1,]    1    2
##  [2,]    1    3
##  [3,]    1    4
##  [4,]    1    5
##  [5,]    2    1
##  [6,]    2    3
##  [7,]    2    4
##  [8,]    2    5
##  [9,]    3    1
## [10,]    3    2
## [11,]    3    4
## [12,]    3    5
## [13,]    4    1
## [14,]    4    2
## [15,]    4    3
## [16,]    4    5
## [17,]    5    1
## [18,]    5    2
## [19,]    5    3
## [20,]    5    4

Optionally for this function permutations, we can add a vector. So for example, if you want to see 5 random 7-digit phone numbers out of all possible phone numbers, you could type code like this.

all_phone_numbers <- permutations(10, 7, v = 0:9)
n <- nrow(all_phone_numbers)
index <- sample(n, 5)
all_phone_numbers[index,]

##      [,1] [,2] [,3] [,4] [,5] [,6] [,7]
## [1,]    5    3    1    2    8    6    9
## [2,]    7    3    5    8    1    9    6
## [3,]    3    4    0    5    7    8    9
## [4,]    0    9    8    4    5    7    1
## [5,]    2    6    1    5    3    9    8

#Here we're defining a vector of digits that goes from 0 to 9 rather than 1 through 10.
#So these four lines of code generate all phone numbers, picks 5 at random.

To compute all possible ways that we can choose 2 cards when the order matters, we simply type the following piece of code.

To compute all possible ways that we can choose 2 cards when the order matters, we simply type the following piece of code. Here we use permutations.

hands <- permutations(52, 2, v = deck)

There’s 52 cards, we’re going to choose 2, and we’re going to select them out of the vector that includes our card names, which we called deck earlier. This is going to be a matrix with 2 dimensions, 2 columns, and in this case, it’s going to have 2,652 rows. Those are all the permutations.

Define the first card and the second card by grabbing the first and second columns using this simple piece of code.

first_card <- hands[,1]
second_card <- hands[,2]

#Now the cases for which the first hand was a King can be computed like this:
kings <- paste("King", suits)
sum(first_card %in% kings)

## [1] 204

#To get the conditional probability, we compute what fraction of these have a King in the second card:
sum(first_card %in% kings & second_card %in% kings) /
  sum(first_card %in% kings)

## [1] 0.05882353

#which is exactly 3/51, as we had already deduced. Notice that the code above is equivalent to:
mean(first_card %in% kings & second_card %in% kings) /
  mean(first_card %in% kings)

## [1] 0.05882353

the difference between the permutations functions, which lists all permutations, and the combination function, where order does not matter.

permutations(3,2)

##      [,1] [,2]
## [1,]    1    2
## [2,]    1    3
## [3,]    2    1
## [4,]    2    3
## [5,]    3    1
## [6,]    3    2

combinations(3,2)

##      [,1] [,2]
## [1,]    1    2
## [2,]    1    3
## [3,]    2    3

#In the second line, the outcome does not include (2,1) because (1,2) already was enumerated. The same applies to (3,1) and (3,2).

So to compute the probability of a Natural 21 in Blackjack, we can do this:

aces <- paste("Ace", suits)

facecard <- c("King", "Queen", "Jack", "Ten")
facecard <- expand.grid(number = facecard, suit = suits)
facecard <- paste(facecard$number, facecard$suit)

hands <- combinations(52, 2, v = deck)
mean(hands[,1] %in% aces & hands[,2] %in% facecard)

## [1] 0.04826546

In the last line, we assume the Ace comes first. This is only because we know the way combination enumerates possibilities and it will list this case first. But to be safe, we could have written this and produced the same answer:

mean((hands[,1] %in% aces & hands[,2] %in% facecard) |
       (hands[,2] %in% aces & hands[,1] %in% facecard))

## [1] 0.04826546

Monte Carlo example

Instead of using combinations to deduce the exact probability of a Natural 21, we can use a Monte Carlo to estimate this probability.

B <- 10000
results <- replicate(B, {
  hand <- sample(deck,2)
 ((hands[,1] %in% aces & hands[,2] %in% facecard) |
       (hands[,2] %in% aces & hands[,1] %in% facecard))
})
mean(results)

## [1] 0.04826546

In this case, we draw two cards over and over and keep track of how many 21s we get. We can use the function sample to draw two cards without replacements:

hand <- sample(deck, 2)
hand

## [1] "Seven Diamonds" "Deuce Diamonds"

And then check if one card is an Ace and the other a face card or a 10. Going forward, we include 10 when we say face card. Now we need to check both possibilities:

(hands[1] %in% aces & hands[2] %in% facecard) | 
  (hands[2] %in% aces & hands[1] %in% facecard)

## [1] FALSE

If we repeat this 10,000 times, we get a very good approximation of the probability of a Natural 21.

Let’s start by writing a function that draws a hand and returns TRUE if we get a 21. The function does not need any arguments because it uses objects defined in the global environment.

blackjack <- function(){
   hand <- sample(deck, 2)
  (hand[1] %in% aces & hand[2] %in% facecard) | 
    (hand[2] %in% aces & hand[1] %in% facecard)
}

Here we do have to check both possibilities: Ace first or Ace second because we are not using the combinations function. The function returns TRUE if we get a 21 and FALSE otherwise:

blackjack()

## [1] FALSE

Now we can play this game, say, 10,000 times:

B <- 10000
results <- replicate(B, blackjack())
mean(results)

## [1] 0.0468

The Birthday Problem

If we assume this is a randomly selected group of 50 people, what is the chance that at least two people have the same birthday?
ere we use a Monte Carlo simulation. For simplicity, we assume nobody was born on February 29. This actually doesn’t change the answer much.

#birthdays can be represented as numbers between 1 and 365, so a sample of 50 birthdays can be obtained like this:
n <- 50
bdays <- sample(1:365, n, replace = TRUE)

To check if in this particular set of 50 people we have at least two with the same birthday, we can use the function duplicated, which returns TRUE whenever an element of a vector is a duplicate. Here is an example:

duplicated(c(1,2,3,1,4,3,5))

## [1] FALSE FALSE FALSE  TRUE FALSE  TRUE FALSE

#The second time 1 and 3 appear, we get a TRUE. So to check if two birthdays were the same, we simply use the any and duplicated functions like this:
any(duplicated(bdays))

## [1] TRUE

In this case, we see that it did happen. At least two people had the same birthday.

To estimate the probability of a shared birthday in the group, we repeat this experiment by sampling sets of 50 birthdays over and over:

same_birthday <- function(n){
  bdays <- sample(1:365, n, replace=TRUE)
  any(duplicated(bdays))
}

B <- 10000
results <- replicate(B, same_birthday(50))
mean(results)

## [1] 0.9722

Were you expecting the probability to be this high?

People tend to underestimate these probabilities. To get an intuition as to why it is so high, think about what happens when the group size is close to 365. At this stage, we run out of days and the probability is one.

Say we want to use this knowledge to bet with friends about two people having the same birthday in a group of people. When are the chances larger than 50%? Larger than 75%?

Let’s create a look-up table. We can quickly create a function to compute this for any group size:

compute_prob <- function(n, B=10000){
  results <- replicate(B, same_birthday(n))
  mean(results)
}

#Using the function sapply, we can perform element-wise operations on any function:
n <- seq(1,60)
prob <- sapply(n, compute_prob)

We can now make a plot of the estimated probabilities of two people having the same birthday in a group of size n :

library(tidyverse)

prob <- sapply(n, compute_prob)
qplot(n, prob)

Now let’s compute the exact probabilities rather than use Monte Carlo approximations. To make the math simpler, instead of computing the probability of it happening, we will compute the probability of it not happening. For this, we use the multiplication rule.

Let’s start with the first person. The probability that person 1 has a unique birthday is 1. The probability that person 2 has a unique birthday, given that person 1 already took one, is 364/365. Then, given that the first two people have unique birthdays, person 3 is left with 363 days to choose from. We continue this way and find the chances of all 50 people having a unique birthday is:

1 ? 364/365 ? 363/365 . 365???n+1/365

We can write a function that does this for any number:

exact_prob <- function(n){
  prob_unique <- seq(365,365-n+1)/365 
  1 - prod( prob_unique)
}
eprob <- sapply(n, exact_prob)

qplot(n, prob) + 
  geom_line(aes(n, eprob), col = "red")

How many Monte Carlo experiments are enough?

We know that the larger B, the better the approximation. But how big do we need it to be? This is actually a challenging question and answering it often requires advanced theoretical statistics training.

One practical approach we will describe here is to check for the stability of the estimate. The following is an example with the birthday problem for a group of 22 people.

B <- 10^seq(1, 5, len = 100)
compute_prob <- function(B, n=25){
  same_day <- replicate(B, same_birthday(n))
  mean(same_day)
}
prob <- sapply(B, compute_prob)
qplot(log10(B), prob, geom = "line")

In this plot, we can see that the values start to stabilize (that is, they vary less than .01) around 1000. Note that the exact probability, which we know in this case, is 0.569.
Assessment 2: Combinations and Permutations

    Independence
    Imagine you draw two balls from a box containing colored balls. You either replace the first ball before you draw the second or you leave the first ball out of the box when you draw the second ball.

Under which situation are the two draws independent of one another?

Remember that two events A and B are independent if Pr(A and B)=Pr(A)P(B).

A. You don’t replace the first ball before drawing the next.

B. You do replace the first ball before drawing the next.

C. Neither situation describes independent events.

D. Both situations describe independent events.

    Sampling with replacement
    Say you’ve drawn 5 balls from the a box that has 3 cyan balls, 5 magenta balls, and 7 yellow balls, with replacement, and all have been yellow.

What is the probability that the next one is yellow?

cyan <- 3
magenta <- 5
yellow <- 7

# Assign the variable 'p_yellow' as the probability that a yellow ball is drawn from the box.
p_yellow <- yellow/(cyan+magenta+yellow)
# Using the variable 'p_yellow', calculate the probability of drawing a yellow ball on the sixth draw. Print this value to the console.
p_yellow

## [1] 0.4666667

    Rolling a die
    If you roll a 6-sided die once, what is the probability of not seeing a 6? If you roll a 6-sided die six times, what is the probability of not seeing a 6 on any roll?

# Assign the variable 'p_no6' as the probability of not seeing a 6 on a single roll.
p_no6 <- 5/6

# Calculate the probability of not seeing a 6 on six rolls using `p_no6`. Print your result to the console: do not assign it to a variable.
p_no6^6

## [1] 0.334898

    Probability the Celtics win a game
    Two teams, say the Celtics and the Cavs, are playing a seven game series. The Cavs are a better team and have a 60% chance of winning each game.

What is the probability that the Celtics win at least one game? Remember that the Celtics must win one of the first four games, or the series will be over!

    Calculate the probability that the Cavs will win the first four games of the series.

    Calculate the probability that the Celtics win at least one game in the first four games of the series.

# Assign the variable `p_cavs_win4` as the probability that the Cavs will win the first four games of the series.
p_cavs_win4 <- 0.6^4

# Using the variable `p_cavs_win4`, calculate the probability that the Celtics win at least one game in the first four games of the series.
(1-p_cavs_win4)

## [1] 0.8704

    Monte Carlo simulation for Celtics winning a game
    Create a Monte Carlo simulation to confirm your answer to the previous problem by estimating how frequently the Celtics win at least 1 of 4 games. Use B <- 10000 simulations.

The provided sample code simulates a single series of four random games, simulated_games

    Use the replicate function for B <- 10000 simulations of a four game series.
    Within each simulation, replicate the sample code to simulate a four-game series named simulated_games.
    Then, use the any function to indicate whether the four-game series contains at least one win for the Celtics.
    Use the mean function to find the proportion of simulations that contain at least one win for the Celtics out of four games.

# This line of example code simulates four independent random games where the Celtics either lose or win. Copy this example code to use within the `replicate` function.
simulated_games <- sample(c("lose","win"), 4, replace = TRUE, prob = c(0.6, 0.4))

# The variable 'B' specifies the number of times we want the simulation to run. Let's run the Monte Carlo simulation 10,000 times.
B <- 10000

# Use the `set.seed` function to make sure your answer matches the expected result after random sampling.
set.seed(1)

# Create an object called `celtic_wins` that replicates two steps for B iterations: (1) generating a random four-game series `simulated_games` using the example code, then (2) determining whether the simulated series contains at least one win for the Celtics.
celtic_wins <- replicate(B, {
  simulated_games <- sample(c("lose","win"), 4, replace = TRUE, prob = c(0.6, 0.4))
  any(simulated_games=="win")
})

# Calculate the frequency out of B iterations that the Celtics won at least one game. Print your answer to the console.
mean(celtic_wins)

## [1] 0.8757

##1.3 Addition rule
The addition rule tells us that:

Pr(A or B) = Pr(A) + Pr(B) ??? Pr(A and B)

This rule is intuitive: think of a Venn diagram. If we simply add the probabilities, we count the intersection twice so we need to substract one instance.
The Monty Hall Problem

In the 1970s, there was a game show called “Let’s Make a Deal” and Monty Hall was the host. At some point in the game, contestants were asked to pick one of three doors. Behind one door there was a prize. The other doors had a goat behind them to show the contestant they had lost. After the contestant picked a door, before revealing whether the chosen door contained a prize, Monty Hall would open one of the two remaining doors and show the contestant there was no prize behind that door. Then he would ask “Do you want to switch doors?” What would you do?

We can use probability to show that if you stick with the original door choice, your chances of winning a prize remain 1 in 3. However, if you switch to the other door, your chances of winning double to 2 in 3! This seems counterintuitive. Many people incorrectly think both chances are 1 in 2 since you are choosing between 2 options. You can watch a detailed mathematical explanation of why this is here or read one here. Below we use a Monte Carlo simulation to see which strategy is better. Note that this code is written longer than it should be for pedagogical purposes.

Let’s start with the stick strategy:

B <- 10000
stick <- replicate(B, {
  doors <- as.character(1:3)
  prize <- sample(c("car", "goat", "goat"))
  prize_door <- doors[prize == "car"]
  my_pick  <- sample(doors, 1)
  show <- sample(doors[!doors %in% c(my_pick, prize_door)],1)
  stick <- my_pick
  stick == prize_door
})
mean(stick)

## [1] 0.3388

As we write the code, we note that the lines starting with my_pick and show have no influence on the last logical operation since we stick to our original choice anyway. From this we should realize that the chance is 1 in 3, what we began with.

Now let’s repeat the exercise, but consider the switch strategy:

switch <- replicate(B, {
  doors <- as.character(1:3)
  prize <- sample(c("car", "goat", "goat"))
  prize_door <- doors[prize == "car"]
  my_pick  <- sample(doors, 1)
  show <- sample(doors[!doors %in% c(my_pick, prize_door)], 1)
  stick <- my_pick
  switch <- doors[!doors%in%c(my_pick, show)]
  switch == prize_door
})
mean(switch)

## [1] 0.6708

The Monte Carlo estimate confirms the 2/3 calculation. This helps us gain some insight by showing that we are removing a door, show, that is definitely not a winner from our choices. We also see that unless we get it right when we first pick, you win: 1 - 1/3 = 2/3.
Assessment 3: The Addition Rule and Monty Hall

    The Cavs and the Warriors
    Two teams, say the Cavs and the Warriors, are playing a seven game championship series. The first to win four games wins the series. The teams are equally good, so they each have a 50-50 chance of winning each game.

If the Cavs lose the first game, what is the probability that they win the series?

# Assign a variable 'n' as the number of remaining games.
n <-6

# Assign a variable `l` to a list of all possible outcomes in all remaining games. Use the `rep` function on `list(outcomes)` to create list of length `n`.
l <- list(0:1)

# Create a data frame named 'possibilities' that contains all combinations of possible outcomes for the remaining games.
possibilities <- expand.grid(rep(l, n))

# Create a vector named 'results' that indicates whether each row in the data frame 'possibilities' contains enough wins for the Cavs to win the series.
results <- rowSums(possibilities)>=4

# Calculate the proportion of 'results' in which the Cavs win the series. Print the outcome to the console.
mean(results)

## [1] 0.34375

    The Cavs and the Warriors - Monte Carlo
    Confirm the results of the previous question with a Monte Carlo simulation to estimate the probability of the Cavs winning the series after losing the first game.

# The variable `B` specifies the number of times we want the simulation to run. Let's run the Monte Carlo simulation 10,000 times.
B <- 10000

# Use the `set.seed` function to make sure your answer matches the expected result after random sampling.
set.seed(1)

# Create an object called `results` that replicates for `B` iterations a simulated series and determines whether that series contains at least four wins for the Cavs.
results <- replicate(B, {
   cavs_wins <- sample(c(0,1), 6, replace = TRUE)
   sum(cavs_wins)>=4
})

# Calculate the frequency out of `B` iterations that the Cavs won at least four games in the remainder of the series. Print your answer to the console.
mean(results)

## [1] 0.3371

    A and B play a series - part 1
    Two teams, A and B, are playing a seven series game series. Team A is better than team B and has a p>0.5 chance of winning each game.

# Let's assign the variable 'p' as the vector of probabilities that team A will win.
p <- seq(0.5, 0.95, 0.025)

# Given a value 'p', the probability of winning the series for the underdog team B can be computed with the following function based on a Monte Carlo simulation:
prob_win <- function(p){
  B <- 10000
  result <- replicate(B, {
    b_win <- sample(c(1,0), 7, replace = TRUE, prob = c(1-p, p))
    sum(b_win)>=4
    })
  mean(result)
}

# Apply the 'prob_win' function across the vector of probabilities that team A will win to determine the probability that team B will win. Call this object 'Pr'.
Pr <- sapply(p, prob_win)

# Plot the probability 'p' on the x-axis and 'Pr' on the y-axis.
plot(p, Pr)

    A and B play a series - part 2
    Repeat the previous exercise, but now keep the probability that team A wins fixed at p <- 0.75 and compute the probability for different series lengths. For example, wins in best of 1 game, 3 games, 5 games, and so on through a series that lasts 25 games.

# Given a value 'p', the probability of winning the series for the underdog team B can be computed with the following function based on a Monte Carlo simulation:
prob_win <- function(N, p=0.75){
      B <- 10000
      result <- replicate(B, {
        b_win <- sample(c(1,0), N, replace = TRUE, prob = c(1-p, p))
        sum(b_win)>=(N+1)/2
        })
      mean(result)
    }

# Assign the variable 'N' as the vector of series lengths. Use only odd numbers ranging from 1 to 25 games.
N <- seq(1, 25, 2)

# Apply the 'prob_win' function across the vector of series lengths to determine the probability that team B will win. Call this object `Pr`.
Pr<- sapply(N, prob_win)

# Plot the number of games in the series 'N' on the x-axis and 'Pr' on the y-axis.
plot(N, Pr)

Section 2 Overview

Section 2 introduces you to Continuous Probability.

After completing Section 2, you will:

    understand the differences between calculating probabilities for discrete and continuous data.
    be able to use cumulative distribution functions to assign probabilities to intervals when dealing with continuous data.
    be able to use R to generate normally distributed outcomes for use in Monte Carlo simulations.
    know some of the useful theoretical continuous distributions in addition to the normal distribution, such as the student-t, chi-squared, exponential, gamma, beta, and beta-binomial distributions.

The textbook for this section is available here
Continuous Probability

library(tidyverse)
library(dslabs)

data(heights)
x <- heights %>% filter(sex=="Male") %>% pull(height)

#We defined the empirical distribution function as:
F <- function(a) mean(x<=a)

Keep in mind that we have not yet introduced probability in the context of CDFs. Let’s do this by asking the following: if I pick one of the male students at random, what is the chance that he is taller than 70.5 inches? Because every student has the same chance of being picked, the answer to this is equivalent to the proportion of students that are taller than 70.5 inches. Using the CDF we obtain an answer by typing:

1 - F(70)

## [1] 0.3768473

Once a CDF is defined, we can use this to compute the probability of any subset. For instance, the probability of a student being between height a and height b is:

F(b)-F(a)
Theoretical Distribution

obtained with the function pnorm. Using the normal distribution:

plot(prop.table(table(x)), xlab= "a= Height in inches", ylab= "Pr(x = a")

The cumulative distribution for the normal distribution is defined by a mathematical formula, which in R can be obtained with the function pnorm. Using the normal distribution:

1 - pnorm(70.5, mean(x), sd(x))

## [1] 0.371369

#the normal distribution is useful for approximating the proportion of students reporting values in intervals like the following three:
#This is actual:
mean(x <= 68.5) - mean(x <= 67.5)

## [1] 0.114532

mean(x <= 69.5) - mean(x <= 68.5)

## [1] 0.1194581

mean(x <= 70.5) - mean(x <= 69.5)

## [1] 0.1219212

Note how close we get with the normal approximation:

#and this is the approximation:
pnorm(68.5, mean(x), sd(x)) - pnorm(67.5, mean(x), sd(x)) 

## [1] 0.1031077

pnorm(69.5, mean(x), sd(x)) - pnorm(68.5, mean(x), sd(x)) 

## [1] 0.1097121

pnorm(70.5, mean(x), sd(x)) - pnorm(69.5, mean(x), sd(x)) 

## [1] 0.1081743

However, the approximation is not as useful for other intervals. For instance, notice how the approximation breaks down when we try to estimate:

mean(x <= 70.9) - mean(x<=70.1)

## [1] 0.02216749

#with
pnorm(70.9, mean(x), sd(x)) - pnorm(70.1, mean(x), sd(x))

## [1] 0.08359562

In general, we call this situation discretization. Although the true height distribution is continuous, the reported heights tend to be more common at discrete values, in this case, due to rounding. As long as we are aware of how to deal with this reality, the normal approximation can still be a very useful tool.
Probability Density

The probability density at x is defined as the function, we’re going to call it little f of x, such that the probability distribution big F of a, which is the probability of x being less than or equal to a, is the integral of all values up to a of little f of x dx.

dnorm() is the probability density function for the normal distribution:

# the probability that a person is higher than 76 inch
avg <- mean(x)
s <- sd(x)
1 - pnorm(76, avg, s)

## [1] 0.03206008

dnorm(76, mean(x), sd(x))

## [1] 0.01990735

Monte Carlo simulations for continuous variables

R provides functions to generate normally distributed outcomes. Specifically, the rnorm function takes three arguments: size, average (defaults to 0), and standard deviation (defaults to 1) and produces random numbers. Here is an example of how we could generate data that looks like our reported heights:

x <- heights %>% filter(sex=="Male") %>% .$height
n <- length(x)
m <- mean(x)
s <- sd(x)
simulated_heights <- rnorm(n, m, s)

ds_theme_set()
data.frame(simulated_heights) %>% ggplot(aes(simulated_heights)) + geom_histogram(color='black', fill='#595959', binwidth=2)

This is one of the most useful functions in R as it will permit us to generate data that mimics natural events and answers questions related to what could happen by chance by running Monte Carlo simulations.

If, for example, we pick 800 males at random, what is the distribution of the tallest person? How rare is a seven footer in a group of 800 males? The following Monte Carlo simulation helps us answer that question:

B <- 10000
tallest <- replicate(B, {
  simulated_data <- rnorm(800, m, s)
  max(simulated_data)
})

#Having a seven footer is quite rare:

mean(tallest >= 7*12)

## [1] 0.0214

#Here is the resulting distribution, note that it does not look normal.
ds_theme_set()
data.frame(tallest) %>% ggplot(aes(tallest)) + geom_histogram(color='black', fill='#595959', binwidth=1)

Other Continuous Distributions

Other continuous distributions that we may encounter are the student-t, chi-squared, exponential, gamma, beta, and beta-binomial. R provides functions to compute the density, the quantiles, the cumulative distribution functions and to generate Monte Carlo simulations. R uses a convention that lets us remember the names, namely using the letters d, q, p and r in front of a shorthand for the distribution. We have already seen the functions dnorm, pnorm and rnorm for the normal distribution. The functions qnorm gives us the quantiles. We can therefore draw a distribution like this:

x <- seq(-4, 4, length.out = 100)
data.frame(x, f = dnorm(x)) %>% 
  ggplot(aes(x, f)) + 
  geom_line()

For example, for the student-t, described later in Section 17.10, the shorthand t is used so the functions are dt for the density, qt for the quantiles, pt for the cumulative distribution function, and rt for Monte Carlo simulation.
Assessment 4: Continuous Probability

    Distribution of female heights - 1
    Assume the distribution of female heights is approximated by a normal distribution with a mean of 64 inches and a standard deviation of 3 inches. If we pick a female at random, what is the probability that she is 5 feet or shorter?

    Use pnorm to define the probability that a height will take a value less than 5 feet given the stated distribution.

# Assign a variable 'female_avg' as the average female height.
female_avg <- 64

# Assign a variable 'female_sd' as the standard deviation for female heights.
female_sd <- 3

# Using variables 'female_avg' and 'female_sd', calculate the probability that a randomly selected female is shorter than 5 feet. Print this value to the console.
pnorm(5*12, female_avg,female_sd)

## [1] 0.09121122

    Distribution of female heights - 2
    Assume the distribution of female heights is approximated by a normal distribution with a mean of 64 inches and a standard deviation of 3 inches. If we pick a female at random, what is the probability that she is 6 feet or taller?

    Use pnorm to define the probability that a height will take a value of 6 feet or taller.

# Assign a variable 'female_avg' as the average female height.
female_avg <- 64

# Assign a variable 'female_sd' as the standard deviation for female heights.
female_sd <- 3

# Using variables 'female_avg' and 'female_sd', calculate the probability that a randomly selected female is 6 feet or taller. Print this value to the console.
1-pnorm(6*12, female_avg,female_sd)

## [1] 0.003830381

    Distribution of female heights - 3
    Assume the distribution of female heights is approximated by a normal distribution with a mean of 64 inches and a standard deviation of 3 inches. If we pick a female at random, what is the probability that she is between 61 and 67 inches?

    Use pnorm to define the probability that a randomly chosen woman will be shorter than 67 inches.
    Subtract the probability that a randomly chosen will be shorter than 61 inches.

# Assign a variable 'female_avg' as the average female height.
female_avg <- 64

# Assign a variable 'female_sd' as the standard deviation for female heights.
female_sd <- 3

# Using variables 'female_avg' and 'female_sd', calculate the probability that a randomly selected female is between the desired height range. Print this value to the console.
pnorm(67, female_avg,female_sd) - pnorm(61, female_avg,female_sd)

## [1] 0.6826895

    Distribution of female heights - 4
    Repeat the previous exercise, but convert everything to centimeters. That is, multiply every height, including the standard deviation, by 2.54. What is the answer now?

    Convert the average height and standard deviation to centimeters by multiplying each value by 2.54.
    Repeat the previous calculation using pnorm to define the probability that a randomly chosen woman will have a height between 61 and 67 inches, converted to centimeters by multiplying each value by 2.54.

# Assign a variable 'female_avg' as the average female height. Convert this value to centimeters.
female_avg <- 64*2.54

# Assign a variable 'female_sd' as the standard deviation for female heights. Convert this value to centimeters.
female_sd <- 3*2.54

# Using variables 'female_avg' and 'female_sd', calculate the probability that a randomly selected female is between the desired height range. Print this value to the console.
pnorm(67*2.54, female_avg,female_sd) - pnorm(61*2.54, female_avg,female_sd)

## [1] 0.6826895

    Probability of 1 SD from average
    Compute the probability that the height of a randomly chosen female is within 1 SD from the average height.

    Calculate the values for heights one standard deviation taller and shorter than the average.
    Calculate the probability that a randomly chosen woman will be within 1 SD from the average height.

# Assign a variable 'female_avg' as the average female height.
female_avg <- 64

# Assign a variable 'female_sd' as the standard deviation for female heights.
female_sd <- 3

# To a variable named 'taller', assign the value of a height that is one SD taller than average.
taller <- female_avg + female_sd

# To a variable named 'shorter', assign the value of a height that is one SD shorter than average.
shorter <- female_avg - female_sd

# Calculate the probability that a randomly selected female is between the desired height range. Print this value to the console.
pnorm(taller, female_avg,female_sd) - pnorm(shorter, female_avg,female_sd)

## [1] 0.6826895

    Distribution of male heights
    Imagine the distribution of male adults is approximately normal with an expected value of 69 inches and a standard deviation of 3 inches. How tall is a male in the 99th percentile?

    Determine the height of a man in the 99th percentile, given an average height of 69 inches and a standard deviation of 3 inches.

# Assign a variable 'male_avg' as the average male height.
male_avg <- 69

# Assign a variable 'male_sd' as the standard deviation for male heights.
male_sd <- 3

# Determine the height of a man in the 99th percentile of the distribution.
qnorm(0.99, male_avg, male_sd)

## [1] 75.97904

    Distribution of IQ scores
    The distribution of IQ scores is approximately normally distributed. The expected value is 100 and the standard deviation is 15. Suppose you want to know the distribution of the person with the highest IQ in your school district, where 10,000 people are born each year.

Generate 10,000 IQ scores 1,000 times using a Monte Carlo simulation. Make a histogram of the highest IQ scores.

    Use the function rnorm to generate a random distribution of 10,000 values with a given average and standard deviation.
    Use the function max to return the largest value from a supplied vector.
    Repeat the previous steps a total of 1,000 times. Store the vector of the top 1,000 IQ scores as highestIQ.
    Plot the histogram of values using the function hist.

# The variable `B` specifies the number of times we want the simulation to run.
B <- 1000

# Use the `set.seed` function to make sure your answer matches the expected result after random number generation.
set.seed(1)

# Create an object called `highestIQ` that contains the highest IQ score from each random distribution of 10,000 people.
highestIQ <- replicate(B, {
    r <- rnorm(10000,100,15)
    max(r)
})

# Make a histogram of the highest IQ scores.
hist(highestIQ)

Section 3 Overview

Section 3 introduces you to Random Variables, Sampling Models, and the Central Limit Theorem.

Section 3 is divided into two parts:

    Random Variables and Sampling Models
    The Central Limit Theorem.

After completing Section 3, you will:

    understand what random variables are, how to generate them, and the correct mathematical notation to use with them.
    be able to use sampling models to estimate characteristics of a larger population.
    be able to explain the difference between a distribution and a probability distribution.
    understand the Central Limit Theorem and the law of large numbers.

The textbook for this section is available here
Random variables

Random variables are numeric outcomes resulting from random processes. We can easily generate random variables using some of the simple examples we have shown. For example, define X to be 1 if a bead is blue and red otherwise:

beads <- rep( c("red", "blue"), times = c(2,3))
X <- ifelse(sample(beads, 1) == "blue", 1, 0)

#Here X is a random variable: every time we select a new bead the outcome changes randomly. See below:

ifelse(sample(beads, 1) == "blue", 1, 0)

## [1] 1

ifelse(sample(beads, 1) == "blue", 1, 0)

## [1] 1

ifelse(sample(beads, 1) == "blue", 1, 0)

## [1] 1

#Sometimes it's 1 and sometimes it's 0.

Sampling Models

For example, we can model the process of polling likely voters as drawing 0’s- Republicans- and 1’s- Democrats- from an urn containing the 0 and 1 code for all likely voters.

In epidemiological studies, we often assume that the subjects in our study are a random sample from the population of interest. The data related to a specific outcome can be modeled as a random sample

Similarly, in experimental research, we often assume that the individual organisms we are studying- for example, worms, flies, or mice- are a random sample from a larger population.

Casino games offer a plethora of examples of real-world situations in which sampling models are used to answer specific questions.

Roulette wheel example

color <- rep(c("Black", "Red", "Green"), c(18,18,2))

n <- 1000
X <- sample(ifelse(color =="Red", -1, 1), n, replace = TRUE)

X <- sample(c(-1,1), n, replace = TRUE, prob=c(9/19, 10/19))
S <- sum(X)
S

## [1] 38

Running a Monte Carlo Simulation with the above example:

a <- 0
n <- 1000
B <- 10000
roulette_winnings <- function(n){
  X <- sample(c(-1,1), n, replace = TRUE, prob=c(9/19, 10/19))
  sum(X)
}
S <- replicate(B, roulette_winnings(n))

#Now we can ask the following: in our simulations, how often did we get sums less than or equal to a?

mean(S <= a)

## [1] 0.0492

#Now we can easily answer the casino's question: how likely is it that we will lose money?
mean(S<0)

## [1] 0.0438

s <- seq(min(S), max(S), length = 100)
normal_density <- data.frame(S = s, f=dnorm(s, mean(S), sd(S)))
data.frame(S=S) %>% ggplot(aes(S, ..density..)) +
  geom_histogram(color = "black", binwidth = 10) +
  ylab("Probability") +
  geom_line(data = normal_density, mapping=aes(s,f), color="blue")

In the histogram above, we see that the distribution appears to be approximately normal. A qq-plot will confirm that the normal approximation is close to perfect. If, in fact, the distribution is normal, then all we need to define the distribution is the average and the standard deviation. Because we have the original values from which the distribution is created, we can easily compute these:

mean(S)

## [1] 52.842

sd(S)

## [1] 31.50489

Distributions versus Probability Distributions

Previously we described how any list of numbers, let’s call it x1 through xn,has a distribution. The definition is quite straightforward. We define capital F of a as a function that answers the question, what proportion of the list is less than or equal to a. Because they are useful summaries, when the distribution is approximately normal, we define the average and the standard deviation. These are defined with a straightforward operation of the list. In r we simply compute the average and standard deviation this way,

m <- sum(x)/length(x)
s <- sqrt(sum((x - m)^2) / length(x))

A random variable x has a distribution function. To define this, we do not need a list of numbers. It’s a theoretical concept. In this case, to define the distribution, we define capital F of a as a function that answers the question, what is the probability that x is less than or equal to a. There is no list of numbers. However, if x is defined by drawing from an urn with numbers in it, then there is a list, the list of numbers inside the urn. In this case, the distribution of that list is the probability distribution of x and the average and standard deviation of that list are the expected value and standard errors of the random variable. Another way to think about it that does not involve an urn is to run a Monte Carlo simulation and generate a very large list of outcomes of x. These outcomes are a list of numbers. The distribution of this list will be a very good approximation of the probability distribution of x. The longer the list, the better the approximation. The average and standard deviation of this list will approximate the expected value and standard error of the random variable.
Central Limit Theorem (CLT)

The Central Limit Theorem-or the CLT for short tells us that when the number of independent draws-also called sample size-is large, the probability distribution of the sum of these draws is approximately normal.
Assessment 5: Random Variables and Sampling Models

    American Roulette probabilities
    An American roulette wheel has 18 red, 18 black, and 2 green pockets. Each red and black pocket is associated with a number from 1 to 36. The two remaining green slots feature “0” and “00”. Players place bets on which pocket they think a ball will land in after the wheel is spun. Players can bet on a specific number (0, 00, 1-36) or color (red, black, or green).

What are the chances that the ball lands in a green pocket?

# The variables `green`, `black`, and `red` contain the number of pockets for each color
green <- 2
black <- 18
red <- 18

# Assign a variable `p_green` as the probability of the ball landing in a green pocket
p_green <- green/(green+black+red)

# Print the variable `p_green` to the console
p_green

## [1] 0.05263158

    American Roulette payout
    In American roulette, the payout for winning on green is $17. This means that if you bet $1 and it lands on green, you get $17 as a prize.

Create a model to predict your winnings from betting on green one time.

    Use the sample function return a random value from a specified range of values.
    Use the prob = argument in the sample function to specify a vector of probabilities for returning each of the values contained in the vector of values being sampled.
    Take a single sample (n = 1).

# Use the `set.seed` function to make sure your answer matches the expected result after random sampling.
set.seed(1)

# The variables 'green', 'black', and 'red' contain the number of pockets for each color
green <- 2
black <- 18
red <- 18

# Assign a variable `p_green` as the probability of the ball landing in a green pocket
p_green <- green / (green+black+red)

# Assign a variable `p_not_green` as the probability of the ball not landing in a green pocket
p_not_green <- 1-p_green

# Create a model to predict the random variable `X`, your winnings from betting on green. Sample one time.
x <- sample(c(17,-1), 1, replace = TRUE, prob=c(p_green, p_not_green))

# Print the value of `X` to the console
x

## [1] -1

    American Roulette expected value
    In American roulette, the payout for winning on green is $17. This means that if you bet $1 and it lands on green, you get $17 as a prize.In the previous exercise, you created a model to predict your winnings from betting on green.

Now, compute the expected value of X, the random variable you generated previously.

    Using the chances of winning $17 (p_green) and the chances of losing $1 (p_not_green), calculate the expected outcome of a bet that the ball will land in a green pocket.

# The variables 'green', 'black', and 'red' contain the number of pockets for each color
green <- 2
black <- 18
red <- 18

# Assign a variable `p_green` as the probability of the ball landing in a green pocket
p_green <- green / (green+black+red)

# Assign a variable `p_not_green` as the probability of the ball not landing in a green pocket
p_not_green <- 1-p_green

# Calculate the expected outcome if you win $17 if the ball lands on green and you lose $1 if the ball doesn't land on green
p_green * 17 + p_not_green * (-1)

## [1] -0.05263158

    American Roulette standard error
    The standard error of a random variable X tells us the difference between a random variable and its expected value. You calculated a random variable X in exercise 2 and the expected value of that random variable in exercise 3.

Now, compute the standard error of that random variable, which represents a single outcome after one spin of the roulette wheel.

    Compute the standard error of the random variable you generated in exercise 2, or the outcome of any one spin of the roulette wheel.
    Recall that the payout for winning on green is $17 for a $1 bet.

# The variables 'green', 'black', and 'red' contain the number of pockets for each color
green <- 2
black <- 18
red <- 18

# Assign a variable `p_green` as the probability of the ball landing in a green pocket
p_green <- green / (green+black+red)

# Assign a variable `p_not_green` as the probability of the ball not landing in a green pocket
p_not_green <- 1-p_green

# Compute the standard error of the random variable
abs((17 - -1))*sqrt(p_green*p_not_green)

## [1] 4.019344

    American Roulette sum of winnings
    You modeled the outcome of a single spin of the roulette wheel, X, in exercise 2.

Now create a random variable S that sums your winnings after betting on green 1,000 times.

    Use set.seed to make sure the result of your random operation matches the expected answer for this problem.
    Specify the number of times you want to sample from the possible outcomes.
    Use the sample function to return a random value from a vector of possible values.
    Be sure to assign a probability to each outcome and to indicate that you are sampling with replacement.

# The variables 'green', 'black', and 'red' contain the number of pockets for each color
green <- 2
black <- 18
red <- 18

# Assign a variable `p_green` as the probability of the ball landing in a green pocket
p_green <- green / (green+black+red)

# Assign a variable `p_not_green` as the probability of the ball not landing in a green pocket
p_not_green <- 1-p_green

# Use the `set.seed` function to make sure your answer matches the expected result after random sampling
set.seed(1)

# Define the number of bets using the variable 'n'
n <- 1000

# Create a vector called 'X' that contains the outcomes of 1000 samples
X <- sample(c(17,-1), size = n, replace=TRUE, prob=c(p_green, p_not_green))

# Assign the sum of all 1000 outcomes to the variable 'S'
S <- sum(X)

# Print the value of 'S' to the console
S

## [1] -10

    American Roulette winnings expected value
    In the previous exercise, you generated a vector of random outcomes, S, after betting on green 1,000 times.

What is the expected value of S?

    Using the chances of winning $17 (p_green) and the chances of losing $1 (p_not_green), calculate the expected outcome of a bet that the ball will land in a green pocket over 1,000 bets.

# The variables 'green', 'black', and 'red' contain the number of pockets for each color
green <- 2
black <- 18
red <- 18

# Assign a variable `p_green` as the probability of the ball landing in a green pocket
p_green <- green / (green+black+red)

# Assign a variable `p_not_green` as the probability of the ball not landing in a green pocket
p_not_green <- 1-p_green

# Define the number of bets using the variable 'n'
n <- 1000

# Calculate the expected outcome of 1,000 spins if you win $17 when the ball lands on green and you lose $1 when the ball doesn't land on green
n * (p_green * 17 + p_not_green * (-1))

## [1] -52.63158

    American Roulette winnings expected value
    You generated the expected value of S, the outcomes of 1,000 bets that the ball lands in the green pocket, in the previous exercise.

What is the standard error of S?

    Compute the standard error of the random variable you generated in exercise 5, or the outcomes of 1,000 spins of the roulette wheel.

# The variables 'green', 'black', and 'red' contain the number of pockets for each color
green <- 2
black <- 18
red <- 18

# Assign a variable `p_green` as the probability of the ball landing in a green pocket
p_green <- green / (green+black+red)

# Assign a variable `p_not_green` as the probability of the ball not landing in a green pocket
p_not_green <- 1-p_green

# Define the number of bets using the variable 'n'
n <- 1000

# Compute the standard error of the sum of 1,000 outcomes
sqrt(n) * abs((17 + 1))*sqrt(p_green*p_not_green)

## [1] 127.1028

The Central Limit Theorem Continued

Property 1: The first, is that the expected value of a sum of random variables is the sum of the expected values of the individual random variables.

Prperty 2: is that the expected value of random variables times a non-random constant is the expected value times that non-random constant.

Property 3: is that the square of the standard error of the sum of independent random variables is the sum of the square of the standard error of each random variable.

Property 4: is that the standard error of random variables times a non-random constant is the standard error times a non-random constant.
Law of Large Numbers

An important implication of the final result is that the standard error of the average becomes smaller and smaller as n grows larger. When n is very large, then the standard error is practically 0 and the average of the draws converges to the average of the urn. This is known in statistical textbooks as the law of large numbers or the law of averages.
How Large is Large in CLT?

In the lottery, the chance of winning are less than 1 in a million. Thousands of people play, so the number of draws is very large. So the central limit should work. Yet, the number of winners, the sum of the draws, range between 0, and in very extreme cases, four. This sum is certainly not well approximated by the normal distribution. So the central limit theorem doesn’t apply, even with a very large sample size. This is generally true when the probability of success is very low. In these cases, the Poisson distribution is more appropriate.
Assessment 6: The Central Limit Theorem

    American Roulette probability of winning money
    The exercises in the previous chapter explored winnings in American roulette. In this chapter of exercises, we will continue with the roulette example and add in the Central Limit Theorem.

In the previous chapter of exercises, you created a random variable S that is the sum of your winnings after betting on green a number of times in American Roulette.

What is the probability that you end up winning money if you bet on green 100 times?

    Execute the sample code to determine the expected value avg and standard error se as you have done in previous exercises.
    Use the pnorm function to determine the probability of winning money.

# Assign a variable `p_green` as the probability of the ball landing in a green pocket
p_green <- 2 / 38

# Assign a variable `p_not_green` as the probability of the ball not landing in a green pocket
p_not_green <- 1-p_green

# Define the number of bets using the variable 'n'
n <- 100

# Calculate 'avg', the expected outcome of 100 spins if you win $17 when the ball lands on green and you lose $1 when the ball doesn't land on green
avg <- n * (17*p_green + -1*p_not_green)

# Compute 'se', the standard error of the sum of 100 outcomes
se <- sqrt(n) * (17 - -1)*sqrt(p_green*p_not_green)

# Using the expected value 'avg' and standard error 'se', compute the probability that you win money betting on green 100 times.
1-pnorm(0,avg,se)

## [1] 0.4479091

    American Roulette Monte Carlo simulation
    Create a Monte Carlo simulation that generates 10,000 outcomes of S, the sum of 100 bets.

Compute the average and standard deviation of the resulting list and compare them to the expected value (-5.263158) and standard error (40.19344) for S that you calculated previously.

    Use the replicate function to replicate the sample code for B <- 10000 simulations.
    Within replicate, use the sample function to simulate n <- 100 outcomes of either a win (17)oraloss(-1) for the bet. Use the order c(17, -1) and corresponding probabilities. Then, use the sum function to add up the winnings over all iterations of the model. Make sure to include sum or DataCamp may crash with a “Session Expired” error.
    Use the mean function to compute the average winnings.
    Use the sd function to compute the standard deviation of the winnings.

# Assign a variable `p_green` as the probability of the ball landing in a green pocket
p_green <- 2 / 38

# Assign a variable `p_not_green` as the probability of the ball not landing in a green pocket
p_not_green <- 1-p_green

# Define the number of bets using the variable 'n'
n <- 100

# The variable `B` specifies the number of times we want the simulation to run. Let's run the Monte Carlo simulation 10,000 times.
B <- 10000

# Use the `set.seed` function to make sure your answer matches the expected result after random sampling.
set.seed(1)

# Create an object called `S` that replicates the sample code for `B` iterations and sums the outcomes.
S <- replicate(B,{
   X <- sample(c(17,-1), size = n, replace = TRUE, prob = c(p_green, p_not_green))
   sum(X)
   })

# Compute the average value for 'S'
mean(S)

## [1] -5.9086

# Calculate the standard deviation of 'S'
sd(S)

## [1] 40.30608

    American Roulette Monte Carlo vs CLT
    In this chapter, you calculated the probability of winning money in American roulette using the CLT.

Now, calculate the probability of winning money from the Monte Carlo simulation. The Monte Carlo simulation from the previous exercise has already been pre-run for you, resulting in the variable S that contains a list of 10,000 simulated outcomes.

    Use the mean function to calculate the probability of winning money from the Monte Carlo simulation, S.

# Calculate the proportion of outcomes in the vector `S` that exceed $0
mean(S>0)

## [1] 0.4232

    American Roulette Monte Carlo vs CLT comparison
    The Monte Carlo result and the CLT approximation for the probability of losing money after 100 bets are close, but not that close. What could account for this?

A. 10,000 simulations is not enough. If we do more, the estimates will match.

B. The CLT does not work as well when the probability of success is small.

C. The difference is within rounding error.

D. The CLT only works for the averages.

    American Roulette average winnings per bet
    Now create a random variable Y that contains your average winnings per bet after betting on green 10,000 times.

    Run a single Monte Carlo simulation of 10,000 bets using the following steps. (You do not need to replicate the sample code.)
    Specify n as the number of times you want to sample from the possible outcomes.
    Use the sample function to return n values from a vector of possible values: winning $17 or losing $1. Be sure to assign a probability to each outcome and indicate that you are sampling with replacement.
    Calculate the average result per bet placed using the mean function.

# Use the `set.seed` function to make sure your answer matches the expected result after random sampling.
set.seed(1)

# Define the number of bets using the variable 'n'
n <- 10000

# Assign a variable `p_green` as the probability of the ball landing in a green pocket
p_green <- 2 / 38

# Assign a variable `p_not_green` as the probability of the ball not landing in a green pocket
p_not_green <- 1 - p_green

# Create a vector called `X` that contains the outcomes of `n` bets
X <- sample(c(17,-1), size = n, replace = TRUE, prob = c(p_green, p_not_green))

# Define a variable `Y` that contains the mean outcome per bet. Print this mean to the console.
Y <- mean(X)
Y

## [1] 0.008

    American Roulette per bet expected value
    What is the expected value of Y, the average outcome per bet after betting on green 10,000 times?

    Using the chances of winning $17 (p_green) and the chances of losing $1 (p_not_green), calculate the expected outcome of a bet that the ball will land in a green pocket.
    Print this value to the console (do not assign it to a variable).

# Assign a variable `p_green` as the probability of the ball landing in a green pocket
p_green <- 2 / 38

# Assign a variable `p_not_green` as the probability of the ball not landing in a green pocket
p_not_green <- 1 - p_green

# Calculate the expected outcome of `Y`, the mean outcome per bet in 10,000 bets
Y <- p_green * 17 + p_not_green * (-1)
Y

## [1] -0.05263158

    American Roulette per bet standard error
    What is the standard error of Y, the average result of 10,000 spins?

    Compute the standard error of Y, the average result of 10,000 independent spins.

# Define the number of bets using the variable 'n'
n <- 10000

# Assign a variable `p_green` as the probability of the ball landing in a green pocket
p_green <- 2 / 38

# Assign a variable `p_not_green` as the probability of the ball not landing in a green pocket
p_not_green <- 1 - p_green

# Compute the standard error of 'Y', the mean outcome per bet from 10,000 bets.
abs((17 - (-1))*sqrt(p_green*p_not_green) / sqrt(n))

## [1] 0.04019344

    American Roulette winnings per game are positive
    What is the probability that your winnings are positive after betting on green 10,000 times?

    Execute the code that we wrote in previous exercises to determine the average and standard error.
    Use the pnorm function to determine the probability of winning more than $0.

# We defined the average using the following code
avg <- 17*p_green + -1*p_not_green

# We defined standard error using this equation
se <- 1/sqrt(n) * (17 - -1)*sqrt(p_green*p_not_green)

# Given this average and standard error, determine the probability of winning more than $0. Print the result to the console.
1 - pnorm(0, avg, se)

## [1] 0.0951898

    American Roulette Monte Carlo again
    Create a Monte Carlo simulation that generates 10,000 outcomes of S, the average outcome from 10,000 bets on green.

Compute the average and standard deviation of the resulting list to confirm the results from previous exercises using the Central Limit Theorem.

    Use the replicate function to model 10,000 iterations of a series of 10,000 bets.
    Each iteration inside replicate should simulate 10,000 bets and determine the average outcome of those 10,000 bets. If you forget to take the mean, DataCamp will crash with a “Session Expired” error.
    Find the average of the 10,000 average outcomes.
    Compute the standard deviation of the 10,000 simulations.

# The variable `n` specifies the number of independent bets on green
n <- 10000

# The variable `B` specifies the number of times we want the simulation to run
B <- 10000

# Use the `set.seed` function to make sure your answer matches the expected result after random number generation
set.seed(1)

# Generate a vector `S` that contains the the average outcomes of 10,000 bets modeled 10,000 times
S <- replicate(B,{  
  X <- sample(c(17,-1), size = n, replace = TRUE, prob = c(p_green, p_not_green))
  mean(X)
})

# Compute the average of `S`
mean(S)

## [1] -0.05223142

# Compute the standard deviation of `S`
sd(S)

## [1] 0.03996168

    American Roulette comparison
    In a previous exercise, you found the probability of winning more than $0 after betting on green 10,000 times using the Central Limit Theorem. Then, you used a Monte Carlo simulation to model the average result of betting on green 10,000 times over 10,000 simulated series of bets.

What is the probability of winning more than $0 as estimated by your Monte Carlo simulation? The code to generate the vector S that contains the the average outcomes of 10,000 bets modeled 10,000 times has already been run for you.

    Calculate the probability of winning more than $0 in the Monte Carlo simulation from the previous exercise.
    You do not need to run another simulation: the results of the simulation are in your workspace as the vector S.

# Compute the proportion of outcomes in the vector 'S' where you won more than $0
mean(S>0)

## [1] 0.0977

    American Roulette comparison analysis
    The Monte Carlo result and the CLT approximation are now much closer than when we calculated the probability of winning for 100 bets on green. What could account for this difference?

A. We are now computing averages instead of sums.

B. 10,000 Monte Carlo simulations was not enough to provide a good estimate.

C. The CLT works better when the sample size is larger.

D. It is not closer. The difference is within rounding error.
Section 4 Overview

Section 4 introduces you to the Big Short.

After completing Section 4, you will:

    understand the relationship between sampling models and interest rates as determined by banks.
    understand how interest rates can be set to minimize the chances of the bank losing money.
    understand how inappropriate assumptions of independence contributed to the financial meltdown of 2007.

The textbook for this section is available here
Interest Rates Explained

Suppose your bank will give out 1,000 loans for 180,000 this year. Also suppose that your bank loses, after adding up all the costs, $200,000 per foreclosure.For simplicity, we assume that that includes all operational costs. A sampling model for this scenario is coded like this.

#Code: Interest rate sampling model
n <- 1000
loss_per_foreclosure <- -200000
p <- 0.02
defaults <- sample( c(0,1), n, prob=c(1-p, p), replace = TRUE)
sum(defaults * loss_per_foreclosure)

## [1] -5e+06

We either default and lose money, or not default and not lose money. If we run the simulation we see that we lose $2.8 millions. Note that the total loss defined by the final sum is a random variable. Every time you run the code you get a different answer. This is because it’s a probability of defaulting. It’s not going to happen for sure. We can easily construct a Monte Carlo simulation to get an idea of the distribution of this random variable. Here’s the distribution.

#Code: Interest rate Monte Carlo simulation
B <- 10000
losses <- replicate(B, {
    defaults <- sample( c(0,1), n, prob=c(1-p, p), replace = TRUE) 
  sum(defaults * loss_per_foreclosure)
})

#Code: Plotting expected losses
library(tidyverse)

data.frame(losses_in_millions = losses/10^6) %>%
  ggplot(aes(losses_in_millions)) +
  geom_histogram(binwidth = 0.6, col = "black")

We don’t really need a Monte Carlo simulation though. Using what we’ve learned, the CLT tells us that because our losses are a sum of independent draws, its distribution is approximately normal with expected value and standard deviation given by the following formula.

#Expected value and standard error of the sum of 1,000 loans
n*(p*loss_per_foreclosure + (1-p)*0) # expected value   

## [1] -4e+06

sqrt(n)*abs(loss_per_foreclosure)*sqrt(p*(1-p)) # standard error 

## [1] 885437.7

#Code: Calculating interest rate for 1% probability of losing money

l <- loss_per_foreclosure
z <- qnorm(0.01)
x <- -l*( n*p - z*sqrt(n*p*(1-p)))/ ( n*(1-p) + z*sqrt(n*p*(1-p)))
x    # required profit when loan is not a foreclosure

## [1] 6249.181

x/180000    # interest rate

## [1] 0.03471767

loss_per_foreclosure*p + x*(1-p)    # expected value of the profit per loan

## [1] 2124.198

n*(loss_per_foreclosure*p + x*(1-p)) # expected value of the profit over n loans

## [1] 2124198

we get that the x has to be about 6,249, which is an interest rate of about 3%, which is still pretty good. Note also that by choosing this interest rate, we now have an expected profit per loan of about $2,124, which is a total expected profit of about $2 million. We can run a Monte Carlo simulation and check our theoretical approximation. We do that, and we indeed get that value again. And again, the probability of profit being less than zero according to the Monte Carlo simulation is about 1%.

#Code: Monte Carlo simulation for 1% probability of losing money

B <- 100000
profit <- replicate(B, {
    draws <- sample( c(x, loss_per_foreclosure), n, 
                        prob=c(1-p, p), replace = TRUE) 
    sum(draws)
})
mean(profit)    # expected value of the profit over n loans

## [1] 2122535

mean(profit<0)    # probability of losing money

## [1] 0.01237

###The Big Short
One of our employees points out that since the bank is making about $2,000 per loan, that you should give out more loans. Why just n? You explain that finding those n clients was hard. You need a group that is predictable, and that keeps the chances of defaults low. He then points out that even if the probability of default is higher, as long as your expected value is positive, you can minimize your chances of losing money by increasing n, the number of loans, and relying on the law of large numbers. He claims that even if the default rate is twice as high, say 4%, if we set the rate just a bit higher so that this happens, you will get a positive expected value. So if we set the interest rate at 5%, we are guaranteed a positive expected value of $640 per loan. And we can minimize our chances of losing money by simply increasing the number of loans, since the probability of S being less than 0 is equal to the probability of Z being less than negative expected value of S divided by standard error S, with Z a standard normal random variable, as we saw earlier. And if we do the math, we will see that we can pick an n so that this probability is 1 in 100.

#Code: Expected value with higher default rate and interest rate

p <- .04
loss_per_foreclosure <- -200000
r <- 0.05
x <- r*180000
loss_per_foreclosure*p + x*(1-p)

## [1] 640

#Code: Calculating number of loans for desired probability of losing money

#The number of loans required is:

z <- qnorm(0.01)
l <- loss_per_foreclosure
n <- ceiling((z^2*(x-l)^2*p*(1-p))/(l*p + x*(1-p))^2)
n    # number of loans required

## [1] 22163

n*(loss_per_foreclosure*p + x * (1-p))    # expected profit over n loans

## [1] 14184320

#Code: Monte Carlo simulation with known default probability

#This Monte Carlo simulation estimates the expected profit given a known probability of default . Note that your results will differ from the video because the seed is not set.

B <- 10000
p <- 0.04
x <- 0.05 * 180000
profit <- replicate(B, {
    draws <- sample( c(x, loss_per_foreclosure), n, 
                        prob=c(1-p, p), replace = TRUE) 
    sum(draws)
})
mean(profit)

## [1] 14090646

#Code: Monte Carlo simulation with unknown default probability

#This Monte Carlo simulation estimates the expected profit given an unknown probability of default , modeling the situation where an event changes the probability of default for all borrowers simultaneously. Note that your results will differ from the video because the seed is not set.

p <- 0.04
x <- 0.05*180000
profit <- replicate(B, {
    new_p <- 0.04 + sample(seq(-0.01, 0.01, length = 100), 1)
    draws <- sample( c(x, loss_per_foreclosure), n, 
                        prob=c(1-new_p, new_p), replace = TRUE) 
    sum(draws)
})
mean(profit)    # expected profit

## [1] 14109853

mean(profit < 0)    # probability of losing money

## [1] 0.3479

mean(profit < -10000000)    # probability of losing over $10 million

## [1] 0.2422

#The Central Limit Theorem states that the sum of independent draws of a random variable follows a normal distribution. However, when the draws are not independent, this assumption does not hold.

Assessment7: The Big Short

    Bank earnings
    Say you manage a bank that gives out 10,000 loans. The default rate is 0.03 and you lose $200,000 in each foreclosure.

Create a random variable S that contains the earnings of your bank. Calculate the total amount of money lost in this scenario.

    Using the sample function, generate a vector called defaults that contains n samples from a vector of c(0,1), where 0 indicates a payment and 1 indicates a default
    Multiply the total number of defaults by the loss per foreclosure.

# Assign the number of loans to the variable `n`
n <- 10000

# Assign the loss per foreclosure to the variable `loss_per_foreclosure`
loss_per_foreclosure <- -200000

# Assign the probability of default to the variable `p_default`
p_default <- 0.03

# Use the `set.seed` function to make sure your answer matches the expected result after random sampling
set.seed(1)

# Generate a vector called `defaults` that contains the default outcomes of `n` loans
defaults <- sample( c(0,1), n, replace = TRUE, prob=c(1-p_default, p_default))

# Generate `S`, the total amount of money lost across all foreclosures. Print the value to the console.
S <- sum(defaults * loss_per_foreclosure)
S

## [1] -6.3e+07

    Bank earnings Monte Carlo
    Run a Monte Carlo simulation with 10,000 outcomes for S, the sum of losses over 10,000 loans. Make a histogram of the results.

    Within a replicate loop with 10,000 iterations, use sample to generate a list of 10,000 loan outcomes: payment (0) or default (1). Use the outcome order c(0,1) and probability of default p_default.
    Still within the loop, use the function sum to count the number of foreclosures multiplied by loss_per_foreclosure to return the sum of all losses across the 10,000 loans. If you do not take the sum inside the replicate loop, DataCamp may crash with a “Session Expired” error.
    Plot the histogram of values using the function hist.

# Assign the number of loans to the variable `n`
n <- 10000

# Assign the loss per foreclosure to the variable `loss_per_foreclosure`
loss_per_foreclosure <- -200000

# Assign the probability of default to the variable `p_default`
p_default <- 0.03

# Use the `set.seed` function to make sure your answer matches the expected result after random sampling
set.seed(1)

# The variable `B` specifies the number of times we want the simulation to run
B <- 10000

# Generate a list of summed losses 'S'. Replicate the code from the previous exercise over 'B' iterations to generate a list of summed losses for 'n' loans.  Ignore any warnings for now.
S <- replicate(B, {
    defaults <- sample( c(0,1), n, prob=c(1-p_default, p_default), replace = TRUE) 
  sum(defaults * loss_per_foreclosure)
})

# Plot a histogram of 'S'.  Ignore any warnings for now.
hist(S)

    Bank earnings expected value
    What is the expected value of S, the sum of losses over 10,000 loans? For now, assume a bank makes no money if the loan is paid.

    Using the chances of default (p_default), calculate the expected losses over 10,000 loans.

# Assign the number of loans to the variable `n`
n <- 10000

# Assign the loss per foreclosure to the variable `loss_per_foreclosure`
loss_per_foreclosure <- -200000

# Assign the probability of default to the variable `p_default`
p_default <- 0.03

# Calculate the expected loss due to default out of 10,000 loans
n*(p_default*loss_per_foreclosure + (1-p_default)*0)

## [1] -6e+07

    Bank earnings standard error
    What is the standard error of S?

    Compute the standard error of the random variable S you generated in the previous exercise, the summed outcomes of 10,000 loans.

# Assign the number of loans to the variable `n`
n <- 10000

# Assign the loss per foreclosure to the variable `loss_per_foreclosure`
loss_per_foreclosure <- -200000

# Assign the probability of default to the variable `p_default`
p_default <- 0.03

# Compute the standard error of the sum of 10,000 loans
sqrt(n) * abs(loss_per_foreclosure) * sqrt(p_default*(1 - p_default))

## [1] 3411744

    Bank earnings interest rate - 1
    So far, we’ve been assuming that we make no money when people pay their loans and we lose a lot of money when people default on their loans. Assume we give out loans for $180,000. How much money do we need to make when people pay their loans so that our net loss is $0?

In other words, what interest rate do we need to charge in order to not lose money?

    If the amount of money lost or gained equals 0, the probability of default times the total loss per default equals the amount earned per probability of the loan being paid.
    Divide the total amount needed per loan by the loan amount to determine the interest rate.

# Assign the loss per foreclosure to the variable `loss_per_foreclosure`
loss_per_foreclosure <- -200000

# Assign the probability of default to the variable `p_default`
p_default <- 0.03

# Assign a variable `x` as the total amount necessary to have an expected outcome of $0
x <- -(loss_per_foreclosure*p_default) / (1 - p_default)

# Convert `x` to a rate, given that the loan amount is $180,000. Print this value to the console.
x / 180000

## [1] 0.03436426

    Bank earnings interest rate - 2
    With the interest rate calculated in the last example, we still lose money 50% of the time. What should the interest rate be so that the chance of losing money is 1 in 20?

In math notation, what should the interest rate be so that Pr(S<0)=0.05?

Remember that we can add a constant to both sides of the equation to get:
Bank_earnings_interest_rate

    Use the qnorm function to compute a continuous variable at given quantile of the distribution to solve for z.
    In this equation, l, p, and n are known values. Once you’ve solved for z, solve for x.
    Divide x by the loan amount to calculate the rate.

# Assign the number of loans to the variable `n`
n <- 10000

# Assign the loss per foreclosure to the variable `loss_per_foreclosure`
loss_per_foreclosure <- -200000

# Assign the probability of default to the variable `p_default`
p_default <- 0.03

# Generate a variable `z` using the `qnorm` function
z <- qnorm(0.05)

# Generate a variable `x` using `z`, `p_default`, `loss_per_foreclosure`, and `n`
x <- -loss_per_foreclosure*( n*p_default - z*sqrt(n*p_default*(1 - p_default)))/ ( n*(1 - p_default) + z*sqrt(n*p_default*(1 - p_default)))

# Convert `x` to an interest rate, given that the loan amount is $180,000. Print this value to the console.
x / 180000

## [1] 0.03768738

    Bank earnings - minimize money loss
    The bank wants to minimize the probability of losing money. Which of the following achieves their goal without making interest rates go up?

A. A smaller pool of loans

B. A larger probability of default

C. A reduced default rate

D. A larger cost per loan default
