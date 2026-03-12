# Class 6: R functions
Alfred Phyo (PID: A18129346)

- [Background](#background)
- [Our first function](#our-first-function)
- [A second function](#a-second-function)
- [A Protein generating function](#a-protein-generating-function)

## Background

All functions in R have at least 3 things:

- A **name** that we use to call the function.
- One or more input **arguments**
- The **body** the lines of R code that do the work

## Our first function

Let’s write a silly wee function called `add()` to add some numbers (the
input arguments)

``` r
add <- function(x, y){
  x + y
}
```

Now we can use this function

``` r
add(100, 1)
```

    [1] 101

``` r
add(x=10, y=10)
```

    [1] 20

``` r
add(x=c(100, 1, 100), y=1)
```

    [1] 101   2 101

> Q. What if I give multiple element vector to `x` and `y`?

``` r
add(x=c(100,1), y=c(100,1))
```

    [1] 200   2

> Q. What if I give three inputs to the function?

``` r
#add(x=c(100,1), y=1, z=1)
```

> Q. What if I give only one input to the add function?

``` r
addnew <- function(x, y=1){
  x + y
}
```

``` r
addnew(x=100)
```

    [1] 101

``` r
addnew(c(100,1), 100)
```

    [1] 200 101

If we write out function with input arguments having no default value
then the user will be required to set them when they use the function.
We can give our input arguments “default” values by setting them equal
to some sensible value - e.g. y=1 in the `addnew()` function.

## A second function

Let’s try something more interesting: Make a sequence generating tool..

The `sample()` function can be a useful starting point here:

``` r
sample(1:10, size=4)
```

    [1]  8 10  5  4

> Q. Generate 9 random numbers taken from the input vector 1:10?

``` r
sample(1:10, size = 9)
```

    [1]  7 10  9  5  8  1  4  3  6

> Q. Generate 12 random numbers taken from the input vector 1:10?

``` r
sample(1:10, size = 12, replace = T)
```

     [1]  5  7 10  8  6  1  2  5  4  1  6  3

> Q. Write code for the `sample()` function that generates nucleotide
> sequences of length 6?

``` r
sample(x=c("A","T","G","C"), size = 6, replace = T)
```

    [1] "A" "A" "T" "A" "T" "T"

> Q. Write a first function `generate_dna()` that returns a user
> specified length DNA sequence:

``` r
generate_dna <- function(len=6){
  sample(x=c("A","T","G","C"), size=len, replace = T)
}
```

``` r
generate_dna()
```

    [1] "T" "T" "A" "A" "T" "G"

> **Key-Points** Every function in R looks fundamentally the same in
> terms of its structure. Basically 3 things: name, input, and body

    name <- function(input){
      body
    }

> Functions can have multiple inputs. These can be **required**
> arguments or **optional** arguments. With optional arguments having a
> set default values.

> Q. Modify and improve our `generate_dna()` function to return it’s
> generated sequence in a more standard format like “AGTAGTA” rather
> than the vector “A”, “C”, “G”, “A”

``` r
generate_dna <- function(len=6, fasta=TRUE){
  ans <- sample(x=c("A","T","G","C"), 
                size=len, replace = T)
  if(fasta){
    cat("Single-element vector output")
  ans <- paste(ans, collapse = "")
  } else{
    cat("Multi-element vector output")
  }
  return(ans)
}
```

``` r
generate_dna(fasta=T)
```

    Single-element vector output

    [1] "GTACAC"

The `paste()` function - its job is to join up or stick together (a.k.a.
paste) input strings together

``` r
paste("joseph", "loves R", spe=" ")
```

    [1] "joseph loves R  "

Flow control means where the R brain goes in your code

``` r
good_mood <- TRUE

if(good_mood){
  cat("GREAT!")
}else{
  cat("Bummer!")
}
```

    GREAT!

## A Protein generating function

> Q. Write a function called `generate_protein()`, that generates a user
> specifed length protein sequence.

> Q. Use that function to generate random protein sequences between
> length 6 and 12.

> Q. Are any of your sequences unique i.e. not found anywhere in nature?
> Yes, sequences of le

There are 20 natural amino-acids

``` r
aa <- c("G","A", "V", "P", "L", "I", "M", "S", "C", "T", "N", "Q", "F", "Y", "W", "D", "E", "K", "R", "H")
```

``` r
generate_protein <- function(len, space = T){
  # The amino-acids to sample from
  aa <- c("G","A", "V", "P", "L", "I", "M", "S", "C", "T", "N", "Q", "F", "Y", "W", "D", "E", "K", "R", "H")
  
  # Draw n-len amino acids to make our sequence
  ans<-sample(aa, size=len, replace = T)
  
  if(space == T){
  ans<-paste(ans, collapse = "")
  }
  return (ans)
}
```

``` r
myseq <- generate_protein(42) 
myseq
```

    [1] "MSHDRNLLWGPSKYLTFKKMDNKAHATLCTSWHVEGYNAYNN"

> Q. Use that function to generate random protein sequences between
> length 6 and 12.

``` r
generate_protein(6)
```

    [1] "CLAQAQ"

``` r
generate_protein(7)
```

    [1] "FLGRRAV"

``` r
generate_protein(8)
```

    [1] "EYDHKDMH"

``` r
generate_protein(9)
```

    [1] "IKMENFQKY"

``` r
generate_protein(10)
```

    [1] "TWLISNCWEV"

``` r
generate_protein(11)
```

    [1] "DIDTKVFINIM"

``` r
generate_protein(12)
```

    [1] "NNVAGYMQRDLM"

``` r
for(i in 6:12){
  # FASTA ID line ">id"
  cat(">", i, sep="", "\n")
  # Protein sequence line
  cat(generate_protein(i), "\n")
}
```

    >6
    CQRNPL 
    >7
    MFAFYMA 
    >8
    KHQAPGCD 
    >9
    KNWSGEMCQ 
    >10
    RYITQFYSIQ 
    >11
    EAIQHVFRNDT 
    >12
    DGRCFVFTLFMF 

> Q. Are any of your sequences unique i.e. not found anywhere in nature?

Yes, sequences of length 8 to 12 were unique.
