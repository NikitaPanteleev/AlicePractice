# To run vm:
```
cd /home/quentin/workspace/EDX_SCALABLE_ML/mooc-setup-master/
vagrant up --provider=virtualbox
http://127.0.0.1:8001/
```

# Course Overview and ML basics.
typical ML piplenine:
obtain raw data -> extract features -> build model -> evaluate |\ --> predict
3 hours to read 1TB

#week 2 - introduction
Ridge search:
min || X * w - y||^2 + lambda * || w ||^2

grid search for free hyper-parametr lambda.
parallelist matrix multiplication by using outer product = sum over
column * row  = sum of matrices

Ram - cpu: 50gb\s,
HDD - cpu: 100mb/s
network - 1Gb/s

*Compute more, communicate less*
1. Computation and storage should be linear (in n, d).
2. Perform parallel and in-memory computation.
3. Minimize network communication

# week 4 Logistic regression.
 - 0/1 loss minimization. But sign is not convex, so minimize
 - min sum log(y(i) * wT * x(i)), y is -1 or 1.
 - features are numerical. Non-numerical are categorical (without
   order) and ordinal (categories with order)
   One-hot-encoding (OHE): Arg, Fr,US =>
   arg = [1,0,0]
   fr =  [0,1,0]
   us =  [0,0,1]
 - sparse representation
 
