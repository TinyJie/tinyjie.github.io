---
layout: post
title: Discriminatively Trained Deformable Part Models-Compile
categories:
- blog
---
Platform:Mac OS X EI Caption(version 10.11.4) with MATLAB R2014b

Error output from matlab:

> /Users/jieliu/Downloads/voc-release3.1/fconvblas.cc:72:7: error: no matching function for call to 'dgemv_'
      dgemv(chn, &m, &n, &one, A_off, &lda, B_off, &incx, &one, C_off, &incy);

> /Applications/MATLAB_R2014b.app/extern/include/blas.h:604:13: note: candidate function not viable: no known
conversion from 'int *' to 'ptrdiff_t *' (aka 'long *') for 2nd argument

## Step 1: Downlaod and unpack [voc-release3.1.tgz](http://cs.brown.edu/~pff/latent-release3/voc-release3.1.tgz) 

## Step 2: Start matlab
 
## Step 3: Modify source code
replace 9th line of compile.m: `mex -O fconvblas.cc -lmwblas -o fconv` with `mex -O fconvblas.cc -lmwblas -output fconv`

replace 67-71th line of fconvblas.cc:
    {% highlight c %}
      int m = C_dims[0];
      int n = B_dims[1]*B_dims[2];
      int lda = A_dims[0];
      int incx = 1;
      int incy = 1;
    {% endhighlight %}
   with: 
    {% highlight c %}
      long int m = C_dims[0];
      long int n = B_dims[1]*B_dims[2];
      long int lda = A_dims[0];
      long int incx = 1;
      long int incy = 1;
    {% endhighlight %}


