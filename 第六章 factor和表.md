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
## 6.3.2 部份表的提取
这部分没怎么懂，打算全部翻译一下
```r
> cttab
          Voted.for.X.Last.Time
Vote.for.X No Yes
  No        2   0
  Not Sure  0   1
  Yes       1   1
```

数据里包含了not sure，我们只想提取投票的结果，也就是yes or no  
接下来是要写一个函数subtable()来达到这个目的  
substable()里包含了一下两个参数

- tbl,对象表格
- subnames,想要提取部分的list，这个list的成分是想要统计的水平名字  
list(Vote.for.X=c("No","Yes"),
    Voted.for.X.Last.Time=c("No","Yes"))

do.call()函数  
do.call(f,arglist)  
do.call 的功能就是执行一个函数，而这个函数的参数呢，放在一个list里面, 是list的每个子元素。  
```r
> tmp <- data.frame('letter' = letters[1:10], 'number' = 1:10, 'value' = c('+','-'))
> tmp
   letter number value
      a      1     +
      b      2     -
      c      3     +
      d      4     -
      e      5     +
      f      6     -
      g      7     +
      h      8     -
      i      9     +
     j     10     -
> tmp[[1]]
 [1] a b c d e f g h i j
> tmp[[2]]
 [1]  1  2  3  4  5  6  7  8  9 10
> tmp[[3]]
 [1] + - + - + - + - + -
> do.call("paste", c(tmp, sep = ""))
 [1] "a1+"  "b2-"  "c3+"  "d4-"  "e5+"  "f6-"  "g7+"  "h8-"  "i9+"  "j10-"
 ```

 ```r
 > number_add <- list(101:110, 1:10)
> number_add
[[1]]
 [1] 101 102 103 104 105 106 107 108 109 110

[[2]]
 [1]  1  2  3  4  5  6  7  8  9 10

> add <- function(x,y) {x + y}
> add
function(x,y) {x + y}

> do.call(add, number_add)
 [1] 102 104 106 108 110 112 114 116 118 120
> add(number_add[[1]], number_add[[2]])
 [1] 102 104 106 108 110 112 114 116 118 120
 ```

array( )  
array(data,dim,dimnames)

```r
# Create two vectors of different lengths.
vector1 <- c(5,9,3)
vector2 <- c(10,11,12,13,14,15)

# Take these vectors as input to the array.
result <- array(c(vector1,vector2),dim=c(3,3,2))
print(result)
当我们上面的代码执行时，它产生以下结果：

, , 1

     [,1] [,2] [,3]
[1,]    5   10   13
[2,]    9   11   14
[3,]    3   12   15

, , 2

     [,1] [,2] [,3]
[1,]    5   10   13
[2,]    9   11   14
[3,]    3   12   15
```

### 6.3.3 检测表内最大值
```r
tabdom<-function(tbl,k){
  tbldf<-as.data.frame(tbl)
  freqord<-order(tbldf$Freq,decreasing = T)
  dom<-tbldf[freqord,][1:k,]
  return(dom)
}

d<-c(5,12,13,4,3,28,12,12,9,5,5,13,5,4,12)
dtab<-table(d)
dtab
tabdom(dtab,3)
```
order( )







