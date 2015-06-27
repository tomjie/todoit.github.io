---
layout: post
title:  Geting and Cleaning Data(第三周学习记录)
categories:
- R
tags:
- R
- coursera学习
---

---
title: "week3_1"
author: "todoit"
date: "2015年6月27日"
output: html_document
---

## 1 subsetting and sorting

```{r}
setwd("/Users/Eric/study/RProject/coursear/datasciencecoursera/2_getdata/week3")

x <- data.frame(var1 = 1:10, var2 = 20:11, var3 = 15:24)
```

###sort排序，是对原数据的重新排列

```{r}
sort(x$var2)
#降序排列
sort(x$var3, decreasing = TRUE)
#让所有NA数据都放在最后
sort(x$2, na.last = TRUE)
```


###使用order函数取得顺序
```{r}
#同时对两列进行排序
order(x$var1, x$var2)

#使用该函数的思想使得数据框根据某一列排序
x[order(x$var2),]

x[order(x$var2, x$var1), ]
```


###使用plyr函数进行排序
```{r}
library(plyr)

#对某一列进行排序
arrange(x, var2)
#降序排列
arrange(x, desc(var1))

```

###增加数据框的列
```{r}
x$var4 <- rnorm(10)

#使用cbind也可以增加数据框的列，生成新的数据框
y <- cbind(x, rnorm(10))
#当然也可以使用rbind增加行

```

## 2 summary data

https://data.baltimorecity.gov/Culture-Arts/Restaurants/k5ry-ef3g?
https://data.baltimorecity.gov/api/views/k5ry-ef3g/rows.csv?accessType=DOWNLOAD

###从网上获得数据
```{r}
#创建目录
if(!file.exists("./data")){
        dir.create("./data")
}
#文件下载地址
fileUrl <- "https://data.baltimorecity.gov/api/views/k5ry-ef3g/rows.csv?accessType=DOWNLOAD"
#下载文件
download.file(fileUrl, destfile = "./data/restaurants.csv", method = "curl")
#读取数据
rest_data <- read.csv("./data/restaurants.csv")
```

### 查看部分数据

```{r}
#如果不指定参数，显示前6行
head(rest_data, n = 3)
#显示最后几行
tail(rest_data, n = 3)
```

### 使用summary来查看数据
```{r}
#可以对每个变量进行汇总，比如求和或者计算最大最小值等
summary(rest_data)

```

### 使用str函数获得更多信息
```{r}
str(rest_data)

```
### 使用quantile查看定量变量的变异度

```{r}
quantile(rest_data$councilDistrict, na.rm = TRUE)
```


### 使用table来汇总单个数据
```{r}
#默认情况下，table函数并不会告诉NA的个数
#useNA = "ifany" 表示如果表中出现缺失值，则在统计结果中加入NA列，并返回NA的个数p
table(rest_data$zipCode, useNA = "ifany")
```

### 使用table函数来制作二维表
```{r}
table(rest_data$councilDistrict, rest_data$zipCode)

```

### 统计缺失值
```{r}
#计算缺失值的个数
sum(is.na(rest_data$councilDistrict))
# 如果有一个NA， 则返回true， any用来查看是否存在不满足条件的
any(is.na(rest_data$councilDistrict))

all(rest_data$zipCode > 0)
```

### 对行或列求和

```{r}
#计算每一列的NA值个数
colSums(is.na(rest_data))

all(colSums(is.na(rest_data)) == 0)

```

### 计算等于某个子集的情况
```{r}
#使用 %in% 命令，返回的是逻辑结果，true false
rest_data$zipCode %in% c("21212", "21213")
table(rest_data$zipCode %in% c("21212", "21213"))

```

###使用 %in% 去子集
```{r}
#取子集的所有列
rest_data[rest_data$zipCode %in% c("21212", "21213"), ]
#去子集的一列
rest_data$zipCode[rest_data$zipCode %in% c("21212", "21213")]
#去子集的多列
rest_data[rest_data$zipCode %in% c("21212", "21213"), c("name", "zipCode")]
```


### 制作联表
```{r}
#使用伯克利分校的招生数据
data(UCBAdmissions)
DF <- as.data.frame(UCBAdmissions)
summary(DF)
#制作交叉表，列显示性别分组，行显示admit分组,数字显示Freq
xt <- xtabs(Freq ~ Gender + Admit, data = DF)

# 制作多个变量的联表
xt_2 <- xtabs(Freq ~ ., data = DF)
xt_2
#由于上述表很难看全，使用ftables制作平面表
ftable(xt_2)
```
### 查看数据集所占的空间大小

```{r}
fake_data <- rnorm(1e5)
object.size(fake_data)
#转换显示单位
print(object.size(fake_data), units = "Mb")

```
