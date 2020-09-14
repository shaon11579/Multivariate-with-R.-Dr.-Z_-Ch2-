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

# from book 


#####################################################

#         Chapter 2: Some R

#####################################################

setwd("C:/Users/zeldan/Desktop/Projects/Multivariate/Data")

#####################################################

#   Section 2.1: Getting Started in R

#####################################################

3 + 4

2 * 6

2 ^ 4

###########

radius <- 3
radius

circum <- 2 * pi * radius
circum

##############

radius
rm(radius)
radius

##########

evens <- c(2, 4, 6, 8, 10)
evens


2 * evens


c(1, rep(2, 3), 4)
rep( c(1, 2), 4) 
rep( c(3, 5), each = 4)

3 : 10
12 : 5
4 : 8 / 4

#############

evens
evens <- c(evens, 2 * (6 : 10))
evens


#####################

evens
evens[4 : 7]
evens[ c(1, 5, 6) ]

evens
evens[-3]

evens
length(evens)

####################

evens > 9
evens[evens > 9]

#############################

3 %in% ( 1 : 5 )
8 %in% ( 1 : 5 )

###############

match( 3 : 4,  2 : 12)

which( ( 2 : 5 ) > 3)

#############################

x <- 1 / (6: 7)
print(x)
print(x, digits = 2)

print(c("x is", x))
cat(c("x is", x))
cat(c("x is", format(x, digits = 3)))


##################################################

#     Section 2.3: Simulation

##################################################


rnorm(3)

############################

nsim <- 500
x <- rnorm(nsim)
x <- x ^ 2
sum(.5 < x  &  x < 1.2) / nsim

#####################

x <- runif(10)
x
sort(x)
min(x)
max(x)
mean(x)
sd(x)
var(x)

##########################################################

#  Figure 2.1: Histogram of random normals

###pdf(file = "hist.pdf")
hist(rnorm(75))
###dev.off()

###########################################################

#                  Section 2.4

###########################################################


housing <- read.table(file = "Housing.txt")
housing
housing$Apartment
housing[1]

housing[,1]
housing[1 : 4, ]
 
housing[ housing$Apartment > 1000, ]

housing[ housing$Apartment > 1000, ][-3, ]

log(housing$Apartment)
log(housing[1])

attach(housing)
Apartment

lh <- cbind(housing,log(housing[1]))
lh[1:5,]

colnames(lh)
colnames(lh)[3] <- "Log Apt"
lh[1:5,]


sort(housing$Apartment)

order(housing$Apartment)

housing[order(housing$Apartment),]

housing[order( -housing$Apartment),]

colMeans(housing)

var(housing)

cor(housing)

sapply(housing, mean)

sapply(housing, sd)

##########  Illustrate MERGE:

first <- data.frame(
   name = c("Charles", "Bill", "Amy", "Fred"), 
   age  = c(15, 25, NA, 22))
first

second <- data.frame(
   handle = c("Charles", "George", "Amy", "Bill"), 
   height = c(61, 65, 60, 67))
second

m1 <- merge(first, second, by.x = "name", by.y = "handle")
m1

m2 <- merge(first, second, by.x = "name", by.y = "handle", all = TRUE)
m2

complete.cases(m2)

m2[complete.cases(m2), ]

#######################################################

#    Section 2.4:  Writting Programs in R

#######################################################


addA <- function(x) x + A

A <- 4
addA(5)

A <- 6
addA(2)

addA

#################################################

addTwo <- function(x)
{
  first <- x + A
  second <- 2 * x
  return(c ( first, second))
}

A <- 5
addTwo(6)

first

########################################################

spacing <- function(x)

# Calculate spacings in vector x

{
   n <- length(x)
   if(n < = 1)return(NA)  # undefined if x is empty or scalar
   sortx <- sort(x)       # sorted values of x
   sortx[ -1 ] - sortx[ -n] # return spacings
}


#  run spacing

z <- sample(25, 5)
z
spacing(z)

spacing(5)

sortx


################################################

#    Section 2.5: A larger simulation

################################################

library(mvtnorm)
rmvnorm(5, mean = c(0, 0), 
        sigma = matrix(c(1,.8, .8, 1), 2, 2 ))

matrix(c(1,-.8, -.8, 1), 2, 2 )

####################################################

#   Figure 2.2: Bivariate normals

###pdf(file = "rmvnorm.pdf")
library(mvtnorm)
plot(rmvnorm(2000, mean = c(0,0), 
    sigma = matrix(c(1, -.8, -.8, 1), 2,2)),
    xlab = "x1", ylab = "x2", pch = 16, col = "red")
###dev.off()

########################################################

#  A simulation of the correlation coefficient


simcor <- function(ncor, nnor, rho)

#  Simulate ncor random correlation coefficients based on nnor 
#  pairs of bivariate normals with population correlation rho.

{

# Check validity of arguments:
   if( ncor < 1 || nnor < 2 || rho < -1 || rho > 1 )return(NA)
   library(mvtnorm)            # access library
   
   vm <- matrix(c(1, rho, rho, 1), 
                2, 2)          # variance matrix
   simcor <- NULL              # start a list of values
   for (i in 1 : ncor)         # For every simulated correlation: 
      {
       norv <- rmvnorm(nnor,   # generate normal pairs 
          mean = c(0,0), sigma = vm )
       sc <-  cor(norv)[1, 2]  # correlation of these pairs
       simcor <- c(simcor, sc) # add to list of values
      }
   simcor                      # Done
}

#########################################################

# Check error processing:

simcor(ncor = -1, nnor = 10, rho = 0)

simcor(ncor = 10, nnor = -1, rho = 0)

simcor(ncor = 5, nnor = 15, rho = 1.8)

simcor(ncor = 6, nnor = 12, rho = -1.2)

# Try with legitimate values:

simcor(ncor = 5, nnor = 15, rho = -.8)

# Try at full strength:

sim <- simcor(ncor = 2500, nnor = 15, rho = .8)
mean(sim)

##############################################################

# Figure 2.3: Histogram of simulated correlation coefficients

### pdf(file = "simcor.pdf")
hist(sim, main = "", col = "red", 
     xlab = "Simulated correlation")
### dev.off()

##############################################################

#   Section 2.6: Advanced Numerical Operations

##############################################################

#              Section 2.7:  Housekeeping

##############################################################

getwd()
setwd("C:/Users/My Name/Desktop/Projects/multivariate/data")

install.packages()


###########################################################

# Section 2.8:  Exercises

################################# Exercise 2.4

pchisq(1.2, 1) - pchisq(.5, 1)


###############################  Exerise 2.10

5/0
sqrt(-3)
0/0

########################### Exercise 2.11:

#  This is a simple answer, without error checking:
spacing(x) <- function(x)  diff(sort(x))

#  Error checking is included in this definition:
spacing <- function(x) if(length(x) > 1) diff(sort(x)) else NA


###########################################################

#        End of this file

###########################################################

 
