# Introduction-R

Teaching page (Drafted July 2022). 

TIP: Learn, Unlearn & Relearn.

# Operations in R

```R
height <- 1.81
weight <- 75
age    <- 26
job    <- "Researcher"

########################
# Generating Sequences
########################
rep(c(1:4),3)
rep(c(1:4), times = 3)
rep(c(1:4), each = 3)

seq(from = 1, to = 4, by = 1)
seq(4,19,3)

########################
# Generating Matrices
########################
y <- matrix(1:9, nrow=3, ncol=3)
y <- matrix(1:9, nrow=3, ncol=3, byrow=TRUE)

> y[1,2]
> y[1,]
> y[2,]

# Creating matrices in R
z <- rep(0,times=3*4)
dim(z) <- c(3,4)
z

z <- matrix( 0 , nrow = 3, ncol = 3 )
A <- matrix( 0, nrow = 3, ncol = 3 )
B <- matrix( 0, nrow = 3, ncol = 3 )

A[1,1] <- -2
A[1,2] <- 3
A[1,3] <- 1
A[2,1] <- 0
A[2,2] <- 0.5
A[2,3] <- 4
A[3,1] <- -3
A[3,2] <- 5
A[3,3] <- 3.5

B[1,1] <- -8
B[1,2] <- 4
B[1,3] <- 1
B[2,1] <- 2
B[2,2] <- 0.5
B[2,3] <- -4
B[3,1] <- 6
B[3,2] <- 2
B[3,3] <- 3

A %*% B
A * B

diag(5)
diag(A)
diag(B)
diag(A %*% B)
diag(A * B)

########################
# Generating Vectors 
########################
x <- c(10.4, 5.6, 3.1, 6.4, 21.7)
v <- 2*x + 1/x

min(x)
max(x)
range(x)
length(x) 

sum(x) 
prod(x)
mean(x)
var(x) 
sum((x-mean(x))^2)/(length(x)-1)

############################
# Descriptive Data Analysis
############################
Data_example <- rnorm( n = 100, mean = 10, sd = 5 )
summary( Data_example )
density( Data_example )
stem( Data_example )
hist( Data_example )
boxplot( Data_example )

```

# Looping in R

```R

# While Loop
i <- 1
while(i <= 7)
{
  print(i)
  i <- i + 1
}

# Repeat Loop
i <- 1
repeat
{
  print(i)
  i <- i + 1
  if(i > 10)	
  {
    break
  }
}

# For Loop
for(i in 1:n) 
{ < do operations in for loop > }

for(i in (1:4)) print(i)
for(i in (1:4)^2) print(i)
for(i in (1:4)^2) cat(i," ")
for(i in (1:4)^2) cat(i,"\n")
for (i in -2:4) {cat(i);cat("  ",i^2,"\n")} 

########################
# Conditional Execution
########################
A <- -2
if( A <0 ) 
{ Abs.A <- (-1)*A }
Abs.A

A <- 1
B <- 2
if((A>2) || (B>2)) 
{ C <- 1 } 
else 
{ C <- 0 }

```

# Functions in R

```R

# Example 1 
incomes      <- c(60, 49, 40, 61, 64, 60, 59, 54, 62, 69, 70, 42, 56, 61, 61, 61, 58, 51, 48, 65, 49, 49, 41, 48, 52, 46, 59, 46, 58, 43)
income_means <- tapply( X=incomes, INDEX=statef, FUN=mean)

std_error        <- function(x) sqrt( var(x)/length(x) )
income_std_error <- tapply( incomes, statef, std_error )

# Example 2 
average <- function(a,b) 
{ 
  compute_average <- (a+b)/2 
  return ( compute_average )
}

ave <- average(4,6)
> ave

# Example 3
Stand_dev_function <- function( y )
{  
  SD       <- sqrt( var( y ) )
  return ( SD )
}

> Stand_dev_function(  vector_x )

```

# Installing R packages 

```R

# Install R package 'insuranceData'
install.packages( "insuranceData" )

# Call the R Library
library( insuranceData )

# Importa data from the R package 'insuranceData'
data( AutoClaims )
head( AutoClaims )

> head( AutoClaims )
     STATE CLASS GENDER AGE    PAID
1 STATE 14   C6       M  97 1134.44
2 STATE 15   C6       M  96 3761.24
3 STATE 15   C11      M  95 7842.31
4 STATE 15   F6       F  95 2384.67
5 STATE 15   F6       M  95  650.00
6 STATE 15   F6       M  95  391.12

age_variable    <- AutoClaims$AGE 
claims_variable <- AutoClaims$PAID

hist( claims_variable )

```

# Statistical Distribution Theory

## Probability Density Functions 

Obtain upper critical values (one-sided upper bound) from a standard Cauchy random variable. 

```R
> qcauchy(0.10, location = 0, scale = 1, lower.tail = FALSE, log.p = FALSE)
[1] 3.077684
> qcauchy(0.05, location = 0, scale = 1, lower.tail = FALSE, log.p = FALSE)
[1] 6.313752
> qcauchy(0.025, location = 0, scale = 1, lower.tail = FALSE, log.p = FALSE)
[1] 12.7062
> qcauchy(0.01, location = 0, scale = 1, lower.tail = FALSE, log.p = FALSE)
[1] 31.82052
> qcauchy(0.005, location = 0, scale = 1, lower.tail = FALSE, log.p = FALSE)
[1] 63.65674

```

## Transformation of Random Variables

### Example 1

```R
function (n) 
{ 
  # Let u be the sample of uniform distribution
  u<-runif(n)  
  
 # Let x be the new sample of the inverse of the given cdf
  x<-( sqrt(-log(1-u)) ) 
  
  makelabel<-paste(as.character(n), "samples from F(x)=1-exp(-x^2)")
  hist(x, prob=TRUE, main=makelabel, xlab='Sample value', ylab='Density')
  curve( (2*x*exp(-(x^2)) ), add=TRUE, col='red')
 
  # the function returns the sample median of the distribution
  return (median(x)) 
}
```

### Example 2

```R
############################
## Geometric Distribution ##
############################
N <- 1000
p <- 0.209205
U <- runif(N)
X <- log(U)/ log(1-p)
Y <- rgeom(N,p)

par(mfrow=c(1,2))
hist(X,freq=F,main="Geom from Uniform")
hist(Y,freq=F,main="Geom from R")

##############################
## Exponential Distribution ##
##############################
N <- 1000
U <- runif(N)
X <- -log(U)
Y <- rexp(N)

par(mfrow=c(1,2))
hist(X,freq=F,main="Exp from Uniform")
hist(Y,freq=F,main="Exp from R")

# Alternatively we can construct an R function as below 
expvar <-function(n=1,rate=1)
 {
   u<-runif(n)
   x<- -log(u)/rate
   return(x)
 }

# The function that computes an iid sample of size n from an exponential distribution with parameter rate. 
# It uses the inverse transformation method. 
```

<img src="https://github.com/christiskatsouris/Introduction-R/blob/main/Data/graph1.png" width="500"/>

### Example 3

```R

function (n)
  {
    x<-c(1:10000)
    for (i in 1:10000)
    {
      x[i]<-sum( runif(n) )
    }
    makelabel<-paste("10000 samples of sum X,with n= ", as.character(n))
    hist(x,prob=TRUE,xlab="X1+X2+...+Xn",ylab="Density",main=makelabel) 
                                         #ylim=c(0.0,1.5)only for the case n=1
    curve( dnorm (x, mean=(n*(1/2)), sd=( sqrt(n/12) ) ) , add=TRUE, col='red' )
 }
```

<img src="https://github.com/christiskatsouris/Introduction-R/blob/main/Data/graph2.png" width="500"/>

### Example 4

```R
# The function has 3 inputs: m=no. of realizations and n,p parameters of Binomial Distribution
function (m,n,p)  
{
  c<-(1:m)  # We create a 1-D array with m elements
  for (i in 1:m) #First for loop
   {
     flips <- c(1:n)
     for (j in 1:n) # Second for loop
      {
        flips[j]<-0  # We initialize all the elements of the array flips[]
        trial<-TRUE
        while (trial==TRUE) # The while loop will be repeated as soon as trial is false
         {
           flips[j]<-flips[j] + 1
           trial<- (runif(1)<p)
         }
      }
     c[i]<-sum(flips) #We use the built-in function sum() to add all the values
   }
  makelabel<-paste(as.character(m)," realizations of B(",as.character(n),",",as.character(p),")") 
  hist(c,prob=TRUE,xlab="X1+X2+...+Xn Bernoulli trials",main=makelabel)
 
 # The function returns the histogram of the sum of m bernoulli random variables
}
```

### Task

Similar to Example 3, draw random samples from the Exponential distribution and plot the distribution of the sum of i.i.d Exponentially distributed random variables for different sample sizes (e.g., $n = 1,2,4,8)$.

<img src="https://github.com/christiskatsouris/Introduction-R/blob/main/Data/graph3.png" width="500"/>

## Maximum Likelihood Estimation using R

### Example 1 (Geometric Distribution)

Write-up the code for an R function that estimates the maximum likelihood estimate for the geometric distribution. HINT: Use a stopping rule by considering the convergence of the computational algorithm. 

```R

fs.geom <- function(theta,avg)
{#begin of function

  if (theta<0 | theta>1) stop ("theta not in [0,1]")
  if (avg<0) stop ("avg must be positive")
 
  maxit   <-100
  epsilon <- 1e-5  

  theta.trace    <- array(NA,maxit+1)
  theta.trace[1] <- theta #store initial estimate

  for (i in 1:maxit)
   {
     theta.old        <- theta
     theta            <- ((1-theta)^2 )*avg + theta^2
     theta.trace[i+1] <- theta
     converge         <- abs(theta-theta.old)/theta.old < epsilon
     if (converge) break
   }

  list (theta=theta, niter=i, theta.trace=theta.trace[1:(1+i)],converge=converge)

}#end of function 

```

### Example 2 (Cauchy Distribution)

Consider the MLE estimator for the Cauchy location model.

$$f(x ; \theta ) = \frac{ 1 }{ \pi \big[ 1 + (x - \theta)^2 \big] },$$

where $\theta$ is the unknown location parameter of the Cauchy distribution describing the center of the distribution (we set the scale parameter = 1). The maximum likelihood equation for the MLE is given by

$$ S( \hat{\theta} ) = 2 \sum_{i=1}^n \frac{ \left( x_i - \hat{\theta} \right) }{ \pi \big[ (x_i - \hat{\theta} )^2 + 1 \big] }.$$

```R
cauchy.mle <- function(x,start,eps=1.e-8,max.iter=50)
{# begin-of-function

   if (missing(start)) start <- median(x)
   theta <- start
   n <- length(x) 
   score <- sum(2*(x-theta)/(1+(x-theta)^2))
   iter <- 1
   conv <- T
   while (abs(score)>eps && iter<=max.iter)
   {
     info  <- sum((2-2*(x-theta)^2)/(1+(x-theta)^2)^2)
     theta <- theta + score/info
     iter  <- iter + 1
     score <- sum(2*(x-theta)/(1+(x-theta)^2))
    }
    if (abs(score)>eps)
    {
       print("No Convergence")
       conv <- F
    }
    loglik <- -sum(log(1+(x-theta)^2))
    info   <- sum((2-2*(x-theta)^2)/(1+(x-theta)^2)^2)
    return <- list(theta=theta,loglik=loglik,info=info,convergence=conv)
    return
    
}# end-of-function

x <- rcauchy(100) + 5 # 100 observations with theta = 5
r <- cauchy.mle(x,start=median(x))

$theta
[1] 4.950597

$loglik
[1] -154.3468

$info
[1] 40.62471

$convergence
[1] TRUE
```

### Example 3 (Weibull Distribution)

The Weibull distribution is one of the best-known life-time distributions. It adequently describes observed failures of many different types of components and phenomena. Sometimes it is also called the Frechet distribution and is considered to belong to the family of extremal distributions. The Weibull distribution has three parameters: $\alpha > 0$ the scale parameter, $\beta > 0$ the shape parameter that determines the shape of the distribution and $\tau > 0$, the location parameter.      

```R


```

# Linear Regression Model in R 

Consider fitting a linear regression model to the 'mortality' data.

```R

#  Fitting the linear model
> calciummod<-lm(mortality~calcium)
> summary(calciummod)
> par(mfrow=c(2,2))
> plot(calciummod)

# To add the regression line on the plot
> plot(mortality~calcium)
> abline(calciummod$coef)

# The box-cox transformation

> boxcox(lm1)
> lm1 <- lm(yield~tissue+pctp,data=RNA)
> lm2 <- lm(yield~tissue,data=RNA)
> anova(lm1,lm2)

```

 ### Reference:
 
 - Agarwal, Subhashish, et al. "Coronary calcium score and prediction of all-cause mortality in diabetes: the diabetes heart study." Diabetes care 34.5 (2011): 1219-1224.

# Using Jupyter with R 

- R scripts can be runned using either [R](https://cran.r-project.org/bin/windows/base/) or using [R Studio](https://www.rstudio.com/). Furthermore, for writing R packages the best option is to use R Studio which can be linked to Github. Note that 'R Studio' is becoming ['posit'](https://posit.co/) from Octomber 2022. 

- An alternative solution to execute R commands is using [Jupyter](https://jupyter.org/) which is a browser-based (web-based) running environment which runs with the help of '[Anaconda](https://en.wikipedia.org/wiki/Anaconda_(Python_distribution))', an open-source Python distribution platform. Notice that to access the Anaconda Powershell Prompt this can be done either using a Virtual Desktop (where the software is already installed) or by donwloading the 'Anaconda Distribution' [here](https://www.anaconda.com/products/distribution).  

- The Anaconda software provides a Power Shell environment where the R kernel can be installed using the following code: 

```R

conda install -c conda-forge r-irkernel

```

- Then, in order to run the Jupyter browser-based notebook we select from the Start Menu: Anaconda > Jupyter Notebook.  

- Another useful functionality of Jupeter is that once a section of code is written on a Jupyter notebook it can be saved as an .ipynb file extension which can be opened in Jupeter (using any web browser). Moreover, any R-script can be also saved as a pdf file. This can be done using the steps below:

```R

# Step 1: Open the Anaconda Powershell Prompt from the Start Menu
# Step 2: Install the 'nbconvert' package by typing the folling into the command prompt:

pip install pyppeteer
pip install nbconvert[webpdf]
jupyter nbconvert --to webpdf --allow-chromium-download 
Example1.ipynb

```


# Reading List

- [An Introduction to R](https://intro2r.com/). 
- Crawley, M. J. (2012). [The R book](https://www.wiley.com/en-gb/The+R+Book%2C+2nd+Edition-p-9780470973929). John Wiley & Sons.


# Disclaimer

The author (Christis G. Katsouris) declares no conflicts of interest.

The proposed Course Syllabus is currently under development and has not been officially undergone quality checks. All rights reserved.

Any errors or omissions are the responsibility of the author.

# Historical Background

### Maurice Fréchet

Maurice Fréchet (2 September 1878 – 4 June 1973) was a French mathematician who made major contributions to the topology of point sets and defined and founded the theory of abstract spaces. He also made several important contributions to the field of statistics and probability, as well as calculus. Fréchet wrote an outstanding doctoral dissertation: "Sur quelques points du calcul fonctionnel". In it he introduced the concept of a metric space, although he did not invent the name 'metric space' which is due to Hausdorff. The thesis concerns 'functional operations' and 'functional calculus' and is developed from ideas due to Hadamard and Volterra. The importance of the thesis is that it develops axiomatic analysis systems providing an abstraction of different objects studied by analysis in a similar way to group theory providing an abstraction of algebraic systems. This parallel is drawn by Fréchet himself who requires sufficient structure on his abstract systems so that limits and continuity can be studied. He defines a functional operation as a numerically valued function defined on arbitrary objects which he wants to include points, lines, functions, numbers, surfaces etc. The functional calculus of his thesis is then the systematic study of functional operations. His dissertation opened the entire field of functionals on metric spaces and introduced the notion of compactness. Independently of Riesz, he discovered the representation theorem in the space of Lebesgue square integrable functions. He is often referred to as the founder of the theory of abstract spaces.

### Reference: 

Fréchet, M. (1943). [Sur l'extension de certaines évaluations statistiques au cas de petits échantillons](https://www.jstor.org/stable/1401114#metadata_info_tab_contents). Revue de l'Institut International de Statistique, 182-205.
