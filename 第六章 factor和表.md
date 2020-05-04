## tapply(x,f,g)
x: 要处理的vector
f: 分类的基准
g: 要怎么计算


```r
> d$over25<- ifelse(d$age>25,1,0)
> d
  gender age income over25
1      M  47  55000      1
2      M  59  88000      1
3      F  21  32450      0
4      M  32  76500      1
5      F  33 123000      1
6      F  24  45650      0
> tapply(d$income,list(d$gender,d$over25),mean)
      0         1
F 39050 123000.00
M    NA  73166.67
```

