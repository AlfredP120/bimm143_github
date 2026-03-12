# Class 12 HW: Population analysis
Alfred Phyo (PID: A18129346)

## Section 4: Population analysis

One sample is obviously not enough to know what is happening in a
population. You are interested in assessing genetic differences on a
population scale. So, you processed about ~230 samples and did the
normalization on a genome level. Now, you want to find whether there is
any association of the 4 asthma-associated SNPs (rs8067378…) on ORMDL3
expression.

> Q13: Read this file into R and determine the sample size for each
> genotype and their corresponding median expression levels for each of
> these genotypes.

How many samples do we have?

``` r
expr <- read.table("rs8067378_ENSG00000172057.6.txt")
head(expr)
```

       sample geno      exp
    1 HG00367  A/G 28.96038
    2 NA20768  A/G 20.24449
    3 HG00361  A/A 31.32628
    4 HG00135  A/A 34.11169
    5 NA18870  G/G 18.25141
    6 NA11993  A/A 32.89721

``` r
nrow(expr)
```

    [1] 462

The sample size for each genotype are as follows:

``` r
table(expr$geno)
```


    A/A A/G G/G 
    108 233 121 

``` r
AA <- expr$exp[expr$geno == "A/A"]
AG <- expr$exp[expr$geno == "A/G"]
GG <- expr$exp[expr$geno == "G/G"]

summary(AA)
```

       Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
      11.40   27.02   31.25   31.82   35.92   51.52 

``` r
summary(AG)
```

       Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
      7.075  20.626  25.065  25.397  30.552  48.034 

``` r
summary(GG)
```

       Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
      6.675  16.903  20.074  20.594  24.457  33.956 

The median for genotype **AA** is 31.25. The median for genotype **AG**
is 25.07. The median for genotype **GG** is 20.07.

> Q14: Generate a boxplot with a box per genotype, what could you infer
> from the relative expression value between A/A and G/G displayed in
> this plot? Does the SNP effect the expression of ORMDL3?

``` r
library(ggplot2)
```

Let’s make a boxplot

``` r
ggplot(expr) + aes(geno, exp, fill = geno) +
  geom_boxplot(notch=TRUE)
```

![](class12hw_files/figure-commonmark/unnamed-chunk-6-1.png)

From the relative expression value between A/A and G/G displayed in this
plot, I can infer individuals with A/A genotype have a higher expression
of ORMDL3 than individuals with G/G genotype. The SNP appears to
influence gene expression of ORMDL3, suggesting its contribution to
asthma susceptibility.
