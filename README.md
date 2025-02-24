Download Link :https://programming.engineering/product/cse341-assignment-4-2/


# CSE-341-Assignment-4-You-will-write-10-Racket-functions-not-counting-helper-functions-
CSE 341 Assignment 4 You will write 10 Racket functions (not counting helper functions)
You will write 10 Racket functions (not counting helper functions) and 1 Racket macro.

Download the starter code from the course website which includes some image files to make testing more fun, and the two Racket fileshw4.rkt and hw4tests.rkt. Add to these files to complete your homework.

Provided Code:

The code at the top of hw4tests.rkt uses a graphics library to provide a simple, entertaining (?) outlet for your streams. You need not understand this code (though it is not complicated) or even use it, but it may make the homework more fun. This is how you use it:

(open-window) returns a graphics window you can pass as the first argument to place-repeatedly.

(place-repeatedly window pause stream n) uses the first n values produced by stream. Each stream element must be a pair where the first value is an integer between 0 and 5 inclusive and the second value is a string that is the name of an image file (e.g., .jpg). (Sample image files that will work well are available on the course website. Put them in the same directory as your code.) Every pause seconds (where pause is a decimal, i.e., floating-point, number), the next stream value is retrieved, the corresponding image file is opened, and it is placed in the window using the number in the pair to choose its position in a 2×3 grid as follows:

0

1

2

3

4

5

Two of the provided tests demonstrate how to use place-repeatedly. The provided tests require you to complete several of the problems, of course. We hope these tests’ expected (visual) behavior is not difficult for you to figure out.

Helpful Guide / Warning:

The first three problems are “warm-up” exercises for Racket. Subsequent problems dive into streams (4–8) and memoization (10). Some short problems may be difficult. Go slowly and focus on using what you learned about thunks, streams, etc.

Some problems require that you use a few standard-library functions that were not used in lecture. See the Racket documentation at http://docs.racket-lang.org/, particularly The Racket Guide, as necessary — looking up library functions even in languages new to you is an important skill. It is fine to discuss with others in the class what library functions are useful and how they work.

Problems:

Write a function sequence that takes 3 arguments spacing, low, and high, all assumed to be numbers. Further, assume spacing is positive. sequence produces a list of numbers from low to high (including low and possibly high) separated by spacing and in sorted order. Sample solution: 4 lines. Examples:

Call

Result

(sequence 2 3 11)

’(357911)

(sequence 3 3 8)

’(3 6)

(sequence 1 3 2)

’()

Write a function string-append-map that takes a list of strings xs and a string suffix and returns a list of strings. Each element of the output should be the corresponding element of the input appended with suffix (with no extra space between the element and suffix). You must use Racket-library functions map and string-append. Sample solution: 2 lines.


Write a function list-nth-mod that takes a list xs and a number n. If the number is negative, terminate the computation with (error “list-nth-mod: negative number”). Else if the list is empty, terminate the computation with (error “list-nth-mod: empty list”). Else return the ith element of the list where we count from zero and i is the remainder produced when dividing n by the list’s length. Library functions length, remainder, car, and list-tail are all useful – see the Racket documentation. Sample solution is 6 lines.

Write a function stream-first-k-such-that that takes a one-argument function f, a number k, and a stream s. It returns a list holding the first k values produced by s (in the order s produced them) for which calling f with the value does not return #f. Assume k is non-negative. Sample solution: 7 lines. Note: You can test your streams with this function instead of the graphics code. Note: This function will not terminate if f does not produce a truthy result for k stream values.

Write a stream funny-number-stream that is like the stream of natural numbers (i.e., 1, 2, 3, …) except numbers divisble by 6 are negated (i.e., 1, 2, 3, 4, 5, -6, 7, 8, 9, 10, 11, -12, 13, …). Remember a stream is a thunk that when called produces a pair. Here the car of the pair will be a number and the cdr will be another stream.

Write a stream dan-then-dog, where the elements of the stream alternate between the strings “dan.jpg” and “dog.jpg” (starting with “dan.jpg”). More specifically, dan-then-dog should be a thunk that when called produces a pair of “dan.jpg” and a thunk that when called produces a pair of “dog.jpg” and a thunk that when called… etc. Sample solution: 4 lines.

Write a function stream-add-one that takes a stream s and returns another stream. If s would produce v for its ith element, then (stream-add-one s) would produce the pair (1 . v) for its ith element. Sample solution: 4 lines. Hint: Use a thunk that when called uses s and recursion. Note: One of the provided tests uses (stream-add-one dan-then-dog) with place-repeatedly.

Write a function cycle-lists that takes two lists xs and ys and returns a stream. The lists may or may not be the same length, but assume they are both non-empty. The elements produced by the stream are pairs where the first part is from xs and the second part is from ys. The stream cycles forever through the lists. For example, if xs is ’(1 2 3) and ys is ’(“a” “b”), then the stream would produce, (1 . “a”), (2 . “b”), (3 . “a”), (1 . “b”), (2 . “a”), (3 . “b”), (1 . “a”), (2 . “b”), etc.

Sample solution is 6 lines and is more complicated than the previous stream problems. Hints: Use one of the functions you wrote earlier. Use a recursive helper function that takes a number n and calls itself with (+ n 1) inside a thunk.

Write a function vector-assoc that takes a value v and a vector vec. It should behave like Racket’s assoc library function except (1) it processes a vector (Racket’s name for an array) instead of a list,

it allows vector elements not to be pairs in which case it skips them, and (3) it always takes exactly two arguments. Process the vector elements in order starting from 0. You must use library functions vector-length, vector-ref, and equal?. Return #f if no vector element is a pair with a car field equal to v, else return the first pair with an equal car field. Sample solution is 9 lines, using one local recursive helper function.

Write a function caching-assoc that takes a list xs and a positive number n and returns a function that takes one argument v and returns the same thing that (assoc v xs) would return. However, you should use an n-element cache of recent results to possibly make this function faster than just calling assoc (if xs is long and a few elements are returned often). The cache should be a vector of length n that is created by the call to caching-assoc and used-and-possibly-mutated each time the function returned by caching-assoc is called.

The cache starts empty (all elements #f). When the function returned by caching-assoc is called, it first checks the cache for the answer. If it is not there, it uses assoc and xs to get the answer and if


the result is not #f (i.e., xs has a pair that matches), it adds the pair to the cache before returning (using vector-set!). The cache slots are used in a round-robin fashion: the first time a pair is added to the cache it is put in position 0, the next pair is put in position 1, etc. up to position n − 1 and then back to position 0 (replacing the pair already there), then position 1, etc.

Hints:

In addition to a variable for holding the vector whose contents you mutate with vector-set!, use a second variable to keep track of which cache slot will be replaced next. After modifying the cache, increment this variable (with set!) or set it back to 0.

To test your cache, it can be useful to add print expressions so you know when you are using the

cache and when you are not. But remove these print expressions before submitting your code. Sample solution is 15 lines.

Define a macro that is used like (while-greater e1 do e2) where e1 and e2 are expressions and while-greater and do are syntax (keywords). The macro should do the following:

It evaluates e1 exactly once.

It evaluates e2 at least once.

It keeps evaluating e2 until and only until the result is not a number greater than the result of the evaluation of e1 .

Assuming evaluation terminates, the result is #t.

Assume e1 and e2 produce numbers; your macro can do anything or fail mysteriously otherwise.

Hint: Define and use a recursive thunk. Sample solution is 9 lines. Example:

(define a 7)

(while-greater 2 do (begin (set! a (- a 1)) (print “x”) a))

(while-greater 2 do (begin (set! a (- a 1)) (print “x”) a))

Evaluating the second line will print “x” 5 times and change a to be 2. So evaluating the third line will print “x” 1 time and change a to be 1.

Challenge Problem: Write cycle-lists-challenge. It should be equivalent to cycle-lists, but its implementation must be more efficient. In particular, for each time the stream produces a new value, the code must perform only two car operations and two cdr operations, including operations performed by any function calls. So, for example, you cannot use length because it uses cdr multiple times to compute a list’s length.

Challenge Problem: Write caching-assoc-lru, which is like caching-assoc except it uses a policy of “least recently used” for deciding which cache slot to replace. That is, when replacing a pair in the cache, you must choose the pair that was least recently returned as an answer. Doing so requires maintaining extra state.

Test your functions: While have provided a few tests, add more to the same testing file.

Assessment: Your solutions should be correct, in good style, and use only features we have used in class. Do not use mutation except in problems 10 and 13. (You also need mutation to test problem 11.)

Turn-in Instructions

Put all your solutions in hw4.rkt.

Put your tests in hw4tests.rkt.

Upload your hw4.rkt and hw4tests.rkt to Gradescope.
