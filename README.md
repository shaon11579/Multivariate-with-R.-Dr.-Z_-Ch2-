# Multivariate-with-R.-Dr.-Z_-Ch2-
Ch2
# Quit R
Q()
## To explicitly remove a variable, we use the rm() command as in
> radius
[1] 3
      > rm(radius)
      > radius
Error: object ’radius’ not found

## Vectors are a natural feature of R and can be constructed using the c (con-
catenate) function:
> evens <- c(2, 4, 6, 8, 10) > evens
[1]2 4 6 810

## The rep( , ) function takes two arguments and is used to make multiple copies of the first argument. The first argument may be either a vector or a scalar. The each = option makes copies of individual elements of the list. Here are examples of its use:

> c(1, rep(2, 3), 4)
[1] 1 2 2 2 4
> rep( c(1, 2), 4)
[1] 1 2 1 2 1 2 1 2
> rep( c(3, 5), each = 4)
[1] 3 3 3 3 5 5 5 5

## The colon (:) operator produces an increasing or decreasing sequence of integers as in these two examples:
> 3 : 10
[1] 3 4 5 6 7 8 910
> 12 : 5
[1]121110 9 8 7 6 5

## A list of logical operators in R
 == Equal to
&& And, element-wise
|| Or, element-wise
> Greater than
>= Greater than or equal to
> evens > 9
! Not, negate
& And, pairwise
| Or, pairwise
< Less than
<= Less than or equal to

##
# The match() function allows us to find the location of specific elements in a vector. The match() function takes two arguments and finds the index of occurrences of the first argument in the second. So
>match(3:4, 2:12)
[1] 2 3


 
