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

## 6.3 表table
一次元计数表
```r
> table(c(5,12,13,12,8,5))

 5  8 12 13 
 2  1  2  1 
 ```

三次元计数表
 ```r
 > v
  gender race pol
1      M    W   L
2      M    W   L
3      F    A   C
4      M    O   L
5      F    B   L
6      F    B   C
> vt<-table(v)
> vt
, , pol = C

      race
gender A B O W
     F 1 1 0 0
     M 0 0 0 0

, , pol = L

      race
gender A B O W
     F 0 1 0 0
     M 0 0 1 2
```

### 6.3.1 表的行列操作
可以求和  
apply(table,1,sum)

```r
> ct
  Vote.for.X Voted.for.X.Last.Time
1        Yes                   Yes
2        Yes                    No
3         No                    No
4   Not Sure                   Yes
5         No                    NO
> cttab<-table(ct)
> cttab
          Voted.for.X.Last.Time
Vote.for.X No NO Yes
  No        1  1   0
  Not Sure  0  0   1
  Yes       1  0   1
> cttab/5
          Voted.for.X.Last.Time
Vote.for.X  No  NO Yes
  No       0.2 0.2 0.0
  Not Sure 0.0 0.0 0.2
  Yes      0.2 0.0 0.2
> apply(cttab,1,sum)
      No Not Sure      Yes 
       2        1        2 
```

