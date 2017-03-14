[![General Assembly Logo](https://camo.githubusercontent.com/1a91b05b8f4d44b5bbfb83abac2b0996d8e26c92/687474703a2f2f692e696d6775722e636f6d2f6b6538555354712e706e67)](https://generalassemb.ly/education/web-development-immersive)

# Computer Science: Algorithms

What does computer science have to do with modern web development? Not much, on
the surface. As application developers, we can do our job well by following best
practices, guided by our experience. There will rarely be a time when you are
interested in the time-complexity of a method you write. Complexity and data
structures are something **language** designers worry about, not developers,
right?

Well, no. While it is true that we don't usually care much about optimization,
there are a few reasons why developers should care a bit about classic topics in
introductory computer science (CS). First, classic problems allow us to practice
our problem solving skills; in fact, most of our lesson today can be completed
without coding. Second, being familiar with the tradeoffs inherent in choosing
an algorithm or a data structure have direct parallels in choices you make
writing your application code. Lastly, some of your colleagues will have CS
degrees, and being able to understand the jargon and figures of speech they use
will help you communicate with them. Perhaps most importantly, these colleagues
will probably have a say in hiring you! Nearly every technical interview touches
on these topics.

## Prerequisites

-   [Computer Science: An introduction](https://github.com/ga-wdi-boston/cs).

## Objectives

By the end of this, developers should be able to:

-   Define "algorithm"
-   Identify what Big-O time-complexity measures
-   Give an example of a divide-and-conquer algorithm
-   Predict the time-complexity of a given algorithm

## Preparation

1.  [Fork and clone](https://github.com/ga-wdi-boston/meta/wiki/ForkAndClone)
    this repository.

## Algorithms

> algorithm (n.) - a process or set of rules to be followed to attain a goal

Algorithm is a fancy word for recipe. When we have a problem, we take a series
of steps to solve that problem. Say I want a peanut butter and jelly sandwich,
and Robin has agreed to make it for me. The problem is, he doesn't know how.
Assuming an otherwise-adult set of knowledge, how might we tell Robin to make me
a sandwich?

> 1.  Go to the 12th floor
> 1.  Go to the kitchen
> 1.  Find the bread, toaster, utensils, peanut butter, and jelly
> 1.  Toast the bread
> 1.  Using a knife or spoon, spread one slice of toast with peanut butter
> 1.  Spread the other slice of toast with jelly
> 1.  Place the two pieces of bread together
> 1.  Return to me with the sandwhich

If Robin needed to make sandwiches for all of us, how would he do that? What's
the "easy" or naïve way to obtain many sandwiches? What is a more efficient way?

### Lab: Outline an Algorithm

Take a few minutes to describe your morning algorithm... uh, routine. Share it
with a neighbor. How many steps are there? How do you save time if you're in a
rush?

### Follow Along: Sorting Cards

I have a deck of unsorted playing cards. Describe in English an algorithm for
sorting them. How would this algorithm change if my goal were not only to sort
the deck, but to kill time while doing it?

## Sorting

A well-known problem in computer science is sorting an array. There are many
strategies (read: algorithms) for accomplishing this. Here is an incomplete
list:

-   Bubble sort
-   Quick sort
-   Merge sort
-   Insertion sort
-   Selection sort
-   Heap sort

This illustrates something important about algorithms: you nearly always have a
choice. There is no "one way" to solve a problem, no "right" way. Different
algorithms are better in different contexts, or with different constraints. It's
up to you to consider the options and pick the one that best meets your needs.

### Lab: Research Quick Sort

Work with a partner to read the [pseudocode](http://rosettacode.org/wiki/Sorting_algorithms/Quicksort) and [ruby](http://rosettacode.org/wiki/Sorting_algorithms/Quicksort#Ruby) implementations of quick sort. One of you will be asked to explain quick sort in your own words.

### Lab: Visualize an Algorithm or two

Let's visualize both selection sort and insertion sort with six volunteers
holding cards.

## Big-O (Asymptotic Analysis)

We use "Big-O" notation to describe an algorithm's complexity. Complexity
measures how time needed and space required scale with input. A common
optimization technique is to trade increased space complexity for reduced time
complexity (and less commonly vice versa).

**Question:** Why do we focus on time-complexity?

Take a simple algorithm for demonstration purposes: printing an element of an
array to the screen.

```ruby
[1, 2, 3].each do |n|
  puts n
end
```

This procedure iterates through an array and prints each element to the screen.
This example has three steps. If the array had five elements, five steps would
be require to print all the elements complete. We say that this procedure has
linear time-complexity: the time-to-complete grows in lock-step with the number
of elements.  This is denoted `O(n)` and pronounced "Big o of n", "O of n", or
simply "linear".

To identify an algorithm's complexity, we focus on the "family" of scaling
functions the algorithm belongs to. We don't care about exact values. For
example:

```ruby
[1, 2, 3].each do |n|
  puts "hello!"
  puts n
end
```

This procedure prints two lines to the screen on each iteration, for a total of
six lines. If we had a five-item array, it would print ten items to the screen.
You might be tempted to say this algorithm has complexity `O(2n)`. But, `y =
2n` is still a linear function, so it is more appropriate to say that this
procedure is linear (`O(n)`).

Another way of saying we care about the "family" of scaling functions is to say
we care about the shape of the scaling function for an algorithm. In both of the
previous examples, graphing elements (`n`) against completion time yields a
straight line, hence we say that the procedures scale linearly.

### Lab: Study Big-O Families

Study the [Big-O
table](http://www.daveperrett.com/articles/2010/12/07/comp-sci-101-big-o-notation/)
to become familiar with these scaling functions, and compare the table to the
[running time
graph](http://science.slc.edu/~jmarshall/courses/2002/spring/cs50/BigO/).

## Predicting Complexity

How can you predict the complexity of a given algorithm? We can look for certain
features to help us characterize it.

-   Loops take linear time to complete (`O(n)`).
-   Nested loops take quadratic time to complete (`O(n^2)`), or worse, cubic
    time (`O(n^3)`)
-   For consecutive statements, add the times-to-complete.
-   For branching statements (`if/else`), take the complexity of the worse
    branch.

Here's a party trick that is sure to make you popular. Bet someone you can state
with certainty a number they've chosen, between one and one hundred, after seven
questions. The questions will all be "Is `<number>` less than the number you've
chosen?"  Before I show you how, let's look at a simplistic solution that takes,
at worst, 100 guesses:

```md
1.  Guess "1". If no,
2.  Guess "2". If no,
3.  Guess "3". If no,
...
100.  Guess "100". You win!
```

**Question:** What is the complexity of this algorithm?

The algorithm that gets you there in the minimum number of guesses is called a
"binary search". It goes like this:

1.  Divide the range in half. Ask if the number in the middle is less than
    their chosen number.
1.  If not, the answer is in the upper half-range. If so, it's in the lower
    half-range.
1.  Repeat the above steps until their are only two number left.
1.  The final "less than" question gives you the answer.

It's relatively easy to see in a tree diagram. Can you see the binary structure
of the tree?

Would checking if the middle number is the correct answer speed things up?

A binary search works with any direct access weakly ordered set (an ordered
array with elements that may compare equal). See
[here](https://en.wikipedia.org/wiki/Binary_search_algorithm#Procedure) for a
more rigorous algorithm.

**Question:** Explain why this algorithm is an example of divide-and-conquer in
your own words.

## Additional Resources

-   [Big-O Algorithm Complexity Cheat Sheet](http://bigocheatsheet.com/)
-   [Sorting Algorithm Animations](http://www.sorting-algorithms.com/)
-   [A Beginner’s Guide to Big O Notation « Rob Bell](http://rob-bell.net/2009/06/a-beginners-guide-to-big-o-notation/)
-   [Fibonacci sequence - Rosetta Code](http://rosettacode.org/wiki/Fibonacci_sequence#Recursive_51)
-   [Bubble-sort with Hungarian ("Csángó") folk dance - YouTube](https://www.youtube.com/watch?v=lyZQPjUT5B4)
-   [Quick-sort with Hungarian (Küküllőmenti legényes) folk dance - YouTube](https://www.youtube.com/watch?v=ywWBy6J5gz8)
-   [CS50's Sort lesson](https://youtu.be/IEOO5UToo6A?list=PLhQjrBD2T383Xfn0zECHrOTpfOSlptPAB&t=1109)

## [License](LICENSE)

1.  All content is licensed under a CC­BY­NC­SA 4.0 license.
1.  All software code is licensed under GNU GPLv3. For commercial use or
    alternative licensing, please contact legal@ga.co.
