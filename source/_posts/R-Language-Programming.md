---
layout: w
title: R Language Programming
date: 2018-08-09
tags:
    - R Language
toc: true
mathjax: true
---

## 第1章  R语言入门

1. 用帮助窗口(或命令)查看` t. test()`(t检验)函数的使用方法.

```R
> ?t.test()
starting httpd help server ... done
```

2. 运行命令`seq(0,10,by=3)`和`seq(0,10,length.out=4)`来体会两个参数`by`和`length.out`的差别.
```R
> seq(0,10,by=3)
[1] 0 3 6 9
> seq(0,10,length.out=4)
[1]  0.000000  3.333333  6.666667 10.000000
```

<!--more-->

3. 构造一个向量**x**, 向量是由5个1, 3个2, 4个3和2个4构成, 注意用到`rep()`函数.

```R
> rep(1:4,c(5,3,4,2))
 [1] 1 1 1 1 1 2 2 2 3 3 3 3 4 4
```

4. 构造4×5矩阵**A**和**B**, 其中**A**是将1, 2, … , 20按列输入, **B**是按行输入; 矩阵**C**是由**A**的前3行和前3列构成的矩阵; 矩阵**D**是由矩阵**B**的各列构成的矩阵, 但不含**B**的第3列.

```R
> A <- matrix(1:20,nrow=4,ncol=5,byrow=FALSE);A
     [,1] [,2] [,3] [,4] [,5]
[1,]    1    5    9   13   17
[2,]    2    6   10   14   18
[3,]    3    7   11   15   19
[4,]    4    8   12   16   20
> (B <- matrix(1:20,nrow=4,ncol=5,byrow=TRUE))
     [,1] [,2] [,3] [,4] [,5]
[1,]    1    2    3    4    5
[2,]    6    7    8    9   10
[3,]   11   12   13   14   15
[4,]   16   17   18   19   20
> (C <- A[1:3,1:3])
     [,1] [,2] [,3]
[1,]    1    5    9
[2,]    2    6   10
[3,]    3    7   11
> (D <- A[,-3])
     [,1] [,2] [,3] [,4]
[1,]    1    5   13   17
[2,]    2    6   14   18
[3,]    3    7   15   19
[4,]    4    8   16   20
```

5. $n$阶$ Hilbert$矩阵定义如下:

   $\textbf{H} = (h_{ij})_{n \times n}, h_{ij} = \frac{1}{i+j-1}, i,j = 1,2, \dots ,n.$

   用循环函数生成一个5阶的 $Hilbert$矩阵.

```R
x <- 5
H <- matrix(nrow=5,ncol=5)
for (i in 1:x){
	for (j in 1:x){
		H[i,j] <- 1/(i+j-1)
	}
};H
```

```R
          [,1]      [,2]      [,3]      [,4]      [,5]
[1,] 1.0000000 0.5000000 0.3333333 0.2500000 0.2000000
[2,] 0.5000000 0.3333333 0.2500000 0.2000000 0.1666667
[3,] 0.3333333 0.2500000 0.2000000 0.1666667 0.1428571
[4,] 0.2500000 0.2000000 0.1666667 0.1428571 0.1250000
[5,] 0.2000000 0.1666667 0.1428571 0.1250000 0.1111111
```

6. 已知有5名学生的数据, 如表1所示. 用数据框的形式读入数据.

   *表 1  学生数据*

   |      | 姓名 | 性别 | 年龄 | 身高/cm | 体重/kg |
   | :--: | ---- | ---- | ---- | ------- | ------- |
   |  1   | 张三 | 女   | 14   | 156     | 42.0    |
   |  2   | 李四 | 男   | 15   | 165     | 49.0    |
   |  3   | 王五 | 女   | 16   | 157     | 41.5    |
   |  4   | 赵六 | 男   | 14   | 162     | 52.0    |
   |  5   | 丁一 | 女   | 15   | 159     | 45.5    |

   ```R
   student_data <- data.frame(
   	姓名 = c('张三','李四','王五','赵六','丁一'),
   	性别 = c('女','男','女','女','男'),
   	年龄 = c(14,15,16,14,15),
   	'身高/cm'  = c(156,65,157,162,175),
   	'体重/kg' = c(42.0,49.0,41.5,52.0,45.5)
   );student_data
   ```

   ```R
     姓名 性别 年龄 身高.cm 体重.kg
   1 张三   女   14     156    42.0
   2 李四   男   15      65    49.0
   3 王五   女   16     157    41.5
   4 赵六   女   14     162    52.0
   5 丁一   男   15     175    45.5
   ```

7. 将表1的数据写成一个纯文本文件, 用函数`read.table()`读该文件, 然后再用函数 `write.csv()`写成一个能用 Excel表能打开的文件, 并用 Excel表打开.

   ```R
   write.csv(student_data, file="student_data.csv", row.names=FALSE)
   read.csv("student_data.csv")
   ```

8. 用`scan()`函数读下列数据, 并将它们放在列表中

   |   1   |   dog    |   3   |
   | :---: | :------: | :---: |
   | **2** | **cat**  | **5** |
   | **3** | **duck** | **7** |

   ```R
   animals <- scan(file="animals.txt", what=character())
   (Lst <- list(animals))
   (Lst <- as.list(animals))
   ```

9. 编写一个R程序(函数)输入一个整数$m$, 如果$n≤0$, 则中止运算,并输出一句话: **“要求输入一个正整数”**; 否则, 如果$m$是偶数, 则将$n$除2, 并赋给$n$; 否则, 将$3n+1$赋给$n$. 不断循环, 只到$n=1$, 才停止计算, 并输出一句话: **“运算成功”**. 这个例子是为了检验数论中的一个简单定理.

   ```R
   fun <- function(n){
   	if(n>0){
   		repeat{
   			if(n%%2==0) n<-n/2 else n<-(3*n+1)
   			if(n==1){
   				print("运算成功")
   				break
   			}
   		}
   	}
   	else{
   		print("要求输入一个正整数")
   	}
   }
   ```

   ```R
   > fun(-4)
   [1] "要求输入一个正整数"
   > fun(22)
   [1] "运算成功"
   ```

## 第2章  数值计算

1. 设$x=(1,2,3)^T, y=(4,5,6)^T$, 作如下运算: 

   (1) 计算$z=2x+y+e$,其中$e=(1,1,1)^T$;

   (2) 计算$x$与$y$的内积;

   (3) 计算$x$与$y$的外积.

   ```R
   > x <- matrix(c(1,2,3),nrow=3)
   > y <- matrix(c(4,5,6),nrow=3)
   > e <- matrix(c(1,1,1),nrow=3)
   > # 四则运算
   > (z = 2*x+y+e)
        [,1]
   [1,]    7
   [2,]   10
   [3,]   13
   > # 內积
   > crossprod(x,y)
        [,1]
   [1,]   32
   > # 外积
   > tcrossprod(x,y)
        [,1] [,2] [,3]
   [1,]    4    5    6
   [2,]    8   10   12
   [3,]   12   15   18
   ```

2. 设
   $ \mathbf{A} = \begin{bmatrix} 1 & \quad 2 & \quad 0 \\ 2 & \quad 5 & \quad -1 \\ 4 & \quad 10 & \quad -1 \end{bmatrix} $  

   计算: 

   (1) $\mathbf{B} = \mathbf{A}^T$; 

   (2) $\mathbf{C} = \mathbf{A} + \mathbf{B}$;

   (3) $\mathbf{D} = \mathbf{AB}$; 

   (4) $\mathbf{E} = (e_{ij})_{n \times n}$, 其中$e_{ij} = a_{ij}b_{ij},  i,j=1,2,3$.

   ```R
   > A <- matrix(c(1,2,0,2,5,-1,4,10,-1),nrow=3,byrow=TRUE);A
        [,1] [,2] [,3]
   [1,]    1    2    0
   [2,]    2    5   -1
   [3,]    4   10   -1
   > B <- t(A);B
        [,1] [,2] [,3]
   [1,]    1    2    4
   [2,]    2    5   10
   [3,]    0   -1   -1
   > C <- A + B;C
        [,1] [,2] [,3]
   [1,]    2    4    4
   [2,]    4   10    9
   [3,]    4    9   -2
   > D <- A %*% B;D
        [,1] [,2] [,3]
   [1,]    5   12   24
   [2,]   12   30   59
   [3,]   24   59  117
   > E <- A*B;E
        [,1] [,2] [,3]
   [1,]    1    4    0
   [2,]    4   25  -10
   [3,]    0  -10    1
   ```

3. 设
   $ \mathbf{A} = \begin{bmatrix} 1 & \quad 2 & \quad 0 \\ 2 & \quad 5 & \quad -1 \\ 4 & \quad 10 & \quad -1 \end{bmatrix} $  $ \mathbf{b} = \begin{bmatrix} 1 \\ -1 \\ 1 \end{bmatrix} $  
   作如下运算:

   (1) 求矩阵**A**的行列式;

   (2) 求解线性方程组$\mathbf{Ax=b}$;

   (3) 求矩阵**A**的逆$\mathbf{A}^{-1}$, 并计算$\mathbf{A}^{-1} \mathbf{b}$.

   ```R
   > A <- matrix(c(1,2,0,2,5,-1,4,10,-1),nrow=3,byrow=TRUE);A
        [,1] [,2] [,3]
   [1,]    1    2    0
   [2,]    2    5   -1
   [3,]    4   10   -1
   > b <- matrix(c(1,-1,1),nrow=3,byrow=FALSE);b
        [,1]
   [1,]    1
   [2,]   -1
   [3,]    1
   > # 矩阵A的行列式
   > det(A)
   [1] 1
   > # 解线性方程组
   > solve(A,b)
        [,1]
   [1,]    1
   [2,]    0
   [3,]    3
   > # 矩阵A的逆
   > solve(A)
        [,1] [,2] [,3]
   [1,]    5    2   -2
   [2,]   -2   -1    1
   [3,]    0   -2    1
   > # 矩阵A的逆乘以b
   > solve(A) %*% b
        [,1]
   [1,]    1
   [2,]    0
   [3,]    3
   ```

4. 设

   $ \mathbf{A} = \begin{bmatrix} 1 & \quad 2 & \quad 0 \\ 2 & \quad 5 & \quad -1 \\ 4 & \quad 10 & \quad -1 \end{bmatrix} $  

   作如下运算:

   (1) 列主元**LU分解**, 即求**P**, **L**和**U**, 使得$\mathbf{A=PLU}$;

   (2) **QR分解**, 即求正交阵**Q**和上三角阵**R**, 使得$\mathbf{A=QR}$;

   (3) 奇异值分解, 即求正交阵**U**, **V**和对角阵**D**, 使得$\mathbf{A=UDV}^{T}$;

   (4) 谱分解, 求矩阵**A**的特征值和对应特征值的特征向量.

   ```R
   > library(lattice);library(Matrix)
   > A <- matrix(c(1,2,0,2,5,-1,4,10,-1),nrow=3,byrow=TRUE)
   > # LU分解
   > A.lu <- lu(A);A.lu
   'MatrixFactorization' of Formal class 'denseLU' [package "Matrix"] with 4 slots
     ..@ x       : num [1:9] 4 0.25 0.5 10 -0.5 0 -1 0.25 -0.5
     ..@ perm    : int [1:3] 3 3 3
     ..@ Dimnames:List of 2
     .. ..$ : NULL
     .. ..$ : NULL
     ..@ Dim     : int [1:2] 3 3
   > ex <- expand(A.lu);ex
   $`L`
   3 x 3 Matrix of class "dtrMatrix" (unitriangular)
        [,1] [,2] [,3]
   [1,] 1.00    .    .
   [2,] 0.25 1.00    .
   [3,] 0.50 0.00 1.00
   
   $U
   3 x 3 Matrix of class "dtrMatrix"
        [,1]  [,2]  [,3] 
   [1,]  4.00 10.00 -1.00
   [2,]     . -0.50  0.25
   [3,]     .     . -0.50
   
   $P
   3 x 3 sparse Matrix of class "pMatrix"
             
   [1,] . | .
   [2,] . . |
   [3,] | . .
   
   > # QR分解
   > qr.A <- qr(A);qr.A
   $`qr`
              [,1]        [,2]      [,3]
   [1,] -4.5825757 -11.3473303 1.3093073
   [2,]  0.4364358  -0.4879500 0.2927700
   [3,]  0.8728716   0.8944272 0.4472136
   
   $rank
   [1] 3
   
   $qraux
   [1] 1.2182179 1.4472136 0.4472136
   
   $pivot
   [1] 1 2 3
   
   attr(,"class")
   [1] "qr"
   > qr.Q(qr.A)
              [,1]        [,2]          [,3]
   [1,] -0.2182179  0.97590007  1.110223e-16
   [2,] -0.4364358 -0.09759001 -8.944272e-01
   [3,] -0.8728716 -0.19518001  4.472136e-01
   > qr.R(qr.A)
             [,1]      [,2]      [,3]
   [1,] -4.582576 -11.34733 1.3093073
   [2,]  0.000000  -0.48795 0.2927700
   [3,]  0.000000   0.00000 0.4472136
   > # 奇异值分解
   > svd(A)
   $`d`
   [1] 12.3170620  0.5148993  0.1576778
   
   $u
              [,1]       [,2]       [,3]
   [1,] -0.1799112  0.5216823 -0.8339542
   [2,] -0.4433971 -0.7997847 -0.4046522
   [3,] -0.8780837  0.2969714  0.3752026
   
   $v
              [,1]      [,2]       [,3]
   [1,] -0.3717640 0.2136312 -0.9034120
   [2,] -0.9221067 0.0274913  0.3859580
   [3,]  0.1072886 0.9765275  0.1867705
   
   > # 谱分解，矩阵A的特征向量
   > eigen(A)
   eigen() decomposition
   $`values`
   [1] 3.7320508 1.0000000 0.2679492
   
   $vectors
              [,1]         [,2]       [,3]
   [1,] -0.2440169 4.472136e-01 -0.9106836
   [2,] -0.3333333 2.979534e-16  0.3333333
   [3,] -0.9106836 8.944272e-01 -0.2440169
   ```

5. 加载`Lattice`程序包和`Matrix`程序包, 由`Hilbert()`函数直接生成一个5阶`Hilbert`矩阵**H**, 作如下运算:

   (1) 对**H**作 **Cholesky分解**, 即求下三角阵**L**, 使得$\mathbf{H=LL}^{T}$;

   (2) 计算**H**的条件数 (关于2-范数条件数, 用`kappa()`函数精确计算) 和条件数的倒数 (用`rcond()`函数计算).

   ```R
   > library(lattice);library(Matrix)
   > H <- Hilbert(5);H
   5 x 5 Matrix of class "dpoMatrix"
             [,1]      [,2]      [,3]      [,4]      [,5]
   [1,] 1.0000000 0.5000000 0.3333333 0.2500000 0.2000000
   [2,] 0.5000000 0.3333333 0.2500000 0.2000000 0.1666667
   [3,] 0.3333333 0.2500000 0.2000000 0.1666667 0.1428571
   [4,] 0.2500000 0.2000000 0.1666667 0.1428571 0.1250000
   [5,] 0.2000000 0.1666667 0.1428571 0.1250000 0.1111111
   > # Cholesky分解
   > chol(H)
   5 x 5 Matrix of class "Cholesky"
        [,1]        [,2]        [,3]        [,4]        [,5]       
   [1,] 1.000000000 0.500000000 0.333333333 0.250000000 0.200000000
   [2,]           . 0.288675135 0.288675135 0.259807621 0.230940108
   [3,]           .           . 0.074535599 0.111803399 0.127775313
   [4,]           .           .           . 0.018898224 0.037796447
   [5,]           .           .           .           . 0.004761905
   > # 矩阵H的2范数下的精确条件数
   > kappa(H,exact=TRUE)
   [1] 476607.3
   > # 矩阵H的1范数下的条件数的倒数
   > rcond(H)
   [1] 1.059708e-06
   ```

6. 求方程$2x^3-6x-1=0$在区间$[1,2]$内的根.

   ```R
   > # 定义函数
   fun <- function(x){
   	f <- 2*x^3-6*x-1
   }
   > # 求非线性方程的根
   > uniroot(fun,c(1,2))
   $`root`
   [1] 1.810013
   
   $f.root
   [1] -0.0003438167
   
   $iter
   [1] 5
   
   $init.it
   [1] NA
   
   $estim.prec
   [1] 6.103516e-05
   ```

7. 求方程$54x^6 + 45x^5 - 102x^4 - 69x^3 + 35x^2 + 16x - 4 = 0$的全部实根.

   ```R
   > # 定义函数
   fun <- function(x){
   	f <- 54*x^6+45*x^5-102*x^4-69*x^3+35*x^2+16*x-4
   };fun
   > # 求方程的全部实根
   > roots <- polyroot(c(-4,16,35,-69,-102,45,54))
   > Re(roots)
   [1]  0.2051829 -0.6666667 -0.6666667  0.5000000  1.1761156 -1.3812985
   ```

8. 求解非线性方程组

   $ \begin{cases} -13+x_1+ ((15-x_2)x2-2) x_2=0 \\ -29+x_1+((x_2+1)x_2-14) x_2=0 \end{cases}$

   取初始点$\mathbf{x}^{(0)}=(0.5, -2)^T$, 精度要求$\epsilon=10^{-5}$.

   ```R
   # P8 source code
   funs <- function(x){
   	f <- c(-13+x[1]+((15-x[2])*x[2]-2)*x[2], 
   		   -29+x[1]+((x[2]+1)*x[2]-14)*x[2] )
   	J <- matrix(c( 1, 30*x[2]-3*x[2]*x[2]-2, 1, 3*x[2]*x[2]+2*x[2]-14 ),
   			   nrow=2,byrow=TRUE)
        list(f=f,J=J)
   }
   source("Newtons.R")
   Newtons(funs,x=c(0,1))
   ```

   ```R
   # "Newtons.R"
   Newtons <- function(funs,x,ep=1e-5,it_max=100){
   	index <- 0
   	k <- 1
   	while(k <= it_max){
   		x1 <- x;
   		obj <- funs(x)
   		x <- x - solve(obj$J,obj$f)
   		norm <- sqrt((x-x1) %*% (x-x1))
   		if(norm < ep){
   			index <- 1
   			break
   		}
   		k <- k+1
   	}
   	obj <- funs(x)
   	list(root=x,it=k,index=index,FunVal=obj$f)
   }
   ```

   ```R
   # P8 run results
   > funs <- function(x){
   + f <- c(-13+x[1]+((15-x[2])*x[2]-2)*x[2], 
   +    -29+x[1]+((x[2]+1)*x[2]-14)*x[2] )
   + J <- matrix(c( 1, 30*x[2]-3*x[2]*x[2]-2, 1, 3*x[2]*x[2]+2*x[2]-14 ),
   +    nrow=2,byrow=TRUE)
   +      list(f=f,J=J)
   + }
   > source("Newtons.R")
   > Newtons(funs,x=c(0,1))
   $`root`
   [1] -413.788513    7.889084
   
   $it
   [1] 13
   
   $index
   [1] 1
   
   $FunVal
   [1] 5.684342e-14 1.705303e-13
   ```

9. 求一元函数$f(x)=e^x-3x$ 在区间 $[0, 2]$ 内的极小点.

   ```R
   # P9 source code
   fun <- function(x){
   	f <- exp(x)-3*x
   }
   optimize(fun,lower=0,upper=2)
   ```

   ```R
   # P9 run results
   > fun <- function(x){
   + f <- exp(x)-3*x
   + }
   > optimize(fun,lower=0,upper=2)
   $`minimum`
   [1] 1.098599
   
   $objective
   [1] -0.2958369
   ```

10. 用`nlm()`函数求解无约束间题
    $min \quad f(x)=(x_1+10x_2)^2 + 5(x_3-x_4)^2 + (x_2-2x_3)^4 + 10(x_1-x_4)^4$
    取初始点$x^{(0)} = (3,-1,0,1)^T$, 并为`nlm()`函数提供目标函数的梯度.

    ```R
    # P10 source code
    source("Rosenbrock.R")
    nlm(obj, c(3,-1,0,1))
    ```

    ```R
    # "Rosenbrock.R"
    obj <- function(x){
    	F <- c( x[1]+10*x[2], sqrt(5)*(x[3]-x[4]), (x[2]-2*x[3])^2, (sqrt(10)*(x[1]-x[4]))^2 )
    	g <- function(x,F){
    		J <- matrix( c(1,10,0,0, 0,0,sqrt(5),-sqrt(5), 0,2*x[2],-4*x[3],0, 2*sqrt(10)*x[1],0,0,2*sqrt(10)*x[4]),
    					nrow=4,ncol=4,byrow=TRUE )
    		2*t(J)%*%F
    	}
    	f <- t(F) %*% F
    	attr(f, "gradient") <- g(x,F)
    	f
    }
    ```

11. 用` optim()`函数求解问题10, 并指定使用**BFGS算法**.

    ```R
    # P11 source code
    # 目标函数
    fun <- function(x){
    #	f <- (x[1]+10*x[2])^2 + 5*(x[3]-x[4])^2 + 
    #          (x[2]-2*x[3])^4  + 10*(x[1]-x[4])^4 )	
    	F <- c( x[1]+10*x[2], sqrt(5)*(x[3]-x[4]), (x[2]-2*x[3])^2, (sqrt(10)*(x[1]-x[4]))^2 )
    	t(F) %*% F
    }
    # 梯度函数
    grad <- function(x){
    	F <- c( x[1]+10*x[2], sqrt(5)*(x[3]-x[4]), (x[2]-2*x[3])^2, (sqrt(10)*(x[1]-x[4]))^2 )
    	J <- matrix( c(1,10,0,0, 0,0,sqrt(5),-sqrt(5), 0,2*x[2],-4*x[3],0, 2*sqrt(10)*x[1],0,0,2*sqrt(10)*x[4]),nrow=4,ncol=4,byrow=TRUE )
    	2*t(J) %*% F	
    }
    # 调用optim()函数
    optim(c(3,-1,0,1),fun,grad,method="BFGS")
    ```

    ```R
    # P11 run results
    > # 目标函数
    > fun <- function(x){
    + #f <- (x[1]+10*x[2])^2 + 5*(x[3]-x[4])^2 + 
    + #          (x[2]-2*x[3])^4  + 10*(x[1]-x[4])^4 )
    + F <- c( x[1]+10*x[2], sqrt(5)*(x[3]-x[4]), (x[2]-2*x[3])^2, (sqrt(10)*(x[1]-x[4]))^2 )
    + t(F) %*% F
    + }
    > # 梯度函数
    > grad <- function(x){
    + F <- c( x[1]+10*x[2], sqrt(5)*(x[3]-x[4]), (x[2]-2*x[3])^2, (sqrt(10)*(x[1]-x[4]))^2 )
    + J <- matrix( c(1,10,0,0, 0,0,sqrt(5),-sqrt(5), 0,2*x[2],-4*x[3],0, 2*sqrt(10)*x[1],0,0,2*sqrt(10)*x[4]),nrow=4,ncol=4,byrow=TRUE )
    + 2*t(J) %*% F
    + }
    > # 调用optim()函数
    > optim(c(3,-1,0,1),fun,grad,method="BFGS")
    $`par`
    [1]  0.042534955 -0.004201827  0.056920304  0.057480557
    
    $value
    [1] 0.0002009827
    
    $counts
    function gradient 
         228       30 
    
    $convergence
    [1] 0
    
    $message
    NULL
    ```

12. 用`n1minb()`函数求解约束问题

    $min \quad f(x) = -x_1x_2(x_3-x_1-2x_2) \\ s.t. \\ \quad \quad \quad 0 \le x_1 \le 42,  \\ \quad \quad \quad 0 \le x_2 \le 36, \\ \quad \quad \quad 0 \le x_3 \le 72, $

    取初始点 $x^{(0)} =(10,10,10)^T$.

    ```R
    # P12 source code
    # 目标函数
    func <- function(x){
    	f <- -x[1]*x[2]*(x[3]-x[1]-2*x[2])
    }
    # 梯度函数
    grad <- function(x){
    	g <- c( -x[2]*x[3]+2*x[1]*x[2]+2*x[2]*x[2], -x[1]*x[3]+x[1]*x[1]+4*x[1]*x[2], -x[1]*x[2])
    }
    # 调用nlminb()函数
    nlminb( c(10,10,10), func, grad,
            lower=c(0,0,0), upper=c(42,36,72))
    ```

    ```R
    # P12 run results
    > # 目标函数
    > func <- function(x){
    + f <- -x[1]*x[2]*(x[3]-x[1]-2*x[2])
    + }
    > # 梯度函数
    > grad <- function(x){
    + g <- c( -x[2]*x[3]+2*x[1]*x[2]+2*x[2]*x[2], -x[1]*x[3]+x[1]*x[1]+4*x[1]*x[2], -x[1]*x[2])
    + }
    > # 调用nlminb()函数
    > nlminb( c(10,10,10), func, grad,
    +         lower=c(0,0,0), upper=c(42,36,72))
    $`par`
    [1] 24 12 72
    
    $objective
    [1] -6912
    
    $convergence
    [1] 0
    
    $iterations
    [1] 14
    
    $evaluations
    function gradient 
          19       15 
    
    $message
    [1] "relative convergence (4)"
    ```

13. 用`constrOptim()`函数求解约束问题

    $ min \quad f(x) = 2x_1^2 + 2x_1x_2 + 2x_1x_3 + 2x_2^2 + x_3^2 - 8x_1 - 6x_2 - 4x_3$

    $s.t. \\\ \quad \quad \quad x_1+x_2+2x_3 \le 3, \\ \quad \quad \quad x_1 \ge 0, x_2 \ge 0, x_3 \ge 0$

    取初始点$x^{(0)}=(0.1, 0.1, 0.1)^T$.

    ```R
    # P13 source code
    # 目标函数
    func <- function(x){
    	f <- 2*x[1]*x[1]+2*x[1]*x[2]+2*x[1]*x[3]+
    	     2*x[2]*x[2]+x[3]*x[3]-8*x[1]-6*x[2]-4*x[3]
    }
    # 梯度函数
    grad <- function(x){
    	g <- c( 4*x[1]+2*x[2]+2*x[3]-8,
                 2*x[1]+4*x[2]-6,
                 2*x[1]+2*x[3]-4)
    }
    # 系数矩阵
    z <- c( -1,-1,-2,
             1, 0, 0,
             0, 1, 0,
             0, 0, 1)
    A <- matrix(z,ncol=3,byrow=TRUE)
    # 右端向量
    b <- c( -3,0,0,0)
    # 调用constrOpim()函数,初始点(0.5,0.5,0.5)
    constrOptim(rep(0.5,3),func,grad,ui=A,ci=b)
    ```

    ```R
    # P13 run results
    > # 目标函数
    > func <- function(x){
    + f <- 2*x[1]*x[1]+2*x[1]*x[2]+2*x[1]*x[3]+
    +      2*x[2]*x[2]+x[3]*x[3]-8*x[1]-6*x[2]-4*x[3]
    + }
    > # 梯度函数
    > grad <- function(x){
    + g <- c( 4*x[1]+2*x[2]+2*x[3]-8,
    +              2*x[1]+4*x[2]-6,
    +              2*x[1]+2*x[3]-4)
    + }
    > # 系数矩阵
    > z <- c( -1,-1,-2,
    +          1, 0, 0,
    +          0, 1, 0,
    +          0, 0, 1)
    > A <- matrix(z,ncol=3,byrow=TRUE)
    > # 右端向量
    > b <- c( -3,0,0,0)
    > # 调用constrOpim()函数,初始点(0.5,0.5,0.5)
    > constrOptim(rep(0.5,3),func,grad,ui=A,ci=b)
    $`par`
    [1] 1.3334954 0.7777538 0.4443754
    
    $value
    [1] -8.888889
    
    $counts
    function gradient 
         106       24 
    
    $convergence
    [1] 0
    
    $message
    NULL
    
    $outer.iterations
    [1] 3
    
    $barrier.value
    [1] -2.722476e-05
    ```

14. 已知某大型工件轮廓数据如表2所示, 加工时需要 $x$ 每改变 $0.1m$ 时的 $y$ 值, 试用三次样条插值估计 $y$ 的值, 并画出轮廓曲线.

    *表 2  某大型工件轮廓数据*

    |      | x    | y    |      | x    | y    |
    | ---- | ---- | ---- | ---- | ---- | ---- |
    | 1    | 0    | 0.0  | 6    | 11   | 2.0  |
    | 2    | 3    | 1.2  | 7    | 12   | 1.8  |
    | 3    | 5    | 1.7  | 8    | 13   | 1.2  |
    | 4    | 7    | 2.0  | 9    | 14   | 1.0  |
    | 5    | 9    | 2.1  | 10   | 15   | 1.6  |

    ```R
    # P14 source code
    # 三次样条函数spline()
    x <- c(0,3,5,7,9,11,12,13,14,15)
    y <- c(0.0,1.2,1.7,2.0,2.1,2.0,1.8,1.2,1.0,1.6)
    s <- spline(x,y,xout=seq(0,15,0.1))
    # 绘图
    par(mai = c(0.8,0.8,0.2,0.2))
    #plot(s$x,s$y,pch=19,type='l',
    #     lwd=2,col='blue',
    #     xlab='x',ylab='y',
    #     main='Problem 14')
    plot( x, y, pch=19, cex=1.2, col=2)
    lines( s$x, s$y, lwd=2, col=4 )
    ```

    ![](https://i.imgur.com/aGb6enT.png)

15. 已知某地区在不同月份的平均日照时间的观测数据如表3所示, 试用三次样条插值函数分析日照时间的变化规律.
    *表 3  某地区的平均日照时间*

    | 月份 | 日照 | 月份 | 日照 | 月份 | 日照 |
    | ---- | ---- | ---- | ---- | ---- | ---- |
    | 1    | 80.9 | 5    | 32.0 | 9    | 52.3 |
    | 2    | 67.2 | 6    | 33.6 | 10   | 62.0 |
    | 3    | 67.1 | 7    | 36.6 | 11   | 64.1 |
    | 4    | 50.5 | 8    | 46.8 | 12   | 71.2 |

    ```R
    # P15 source code
    # 三次样条函数splinefun()
    sunlight <- c(80.9, 67.2, 67.1, 50.5, 32.0, 33.6, 36.6, 46.8, 52.3, 62.0, 64.1, 71.2)
    monthlen <- c(31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31)
    month = rep( 1:12, monthlen)
    midmonth <- tapply(1:365, month, median)
    x <- c(midmonth, midmonth[1]+365)
    y <- sunlight[c(1:12,1)]
    s = splinefun(x,y,method="periodic")
    # 绘图
    par(mai=c(0.9, 0.9, 0.6, 0.2))
    plot(1:365, s(1:365),
         type='l', lwd=2, col='blue',
         xlab='x',ylab='y',
         main='Problem 14')
    points(x[-13], y[-13], pch=19, cex=1.2, col="red")
    ```
    
    ![](https://i.imgur.com/jrPJnLn.png)

## Open the Door

If you want to enter another room to explore the treasure you are looking for, you can open the door by clicking at **[https://niwanli.github.io/](https://niwanli.github.io/ "Wanli | Home")**. Or, if you want to contact me, please email me at **niwanli@yahoo.com**.
