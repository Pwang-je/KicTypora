---
R	
---



[TOC]



## 1. 용어





##### Vector

```R
x[n] : 벡터 x 의 n번째 요소.
x[-n] : 벡터 x 에서 n번째 요소를 제외한 나머지.
x[start:end] : 벡터 x의 start 부터 end 까지.

# 길이 관련 함수.
length() : 객체의 길이.
nrow() : 행의 수.

#
x <- c(1,3,4)
naems(x) <- c("kim","park","choi")
# kim park choi 
#   1    3    4 
```



##### Factor

```factor```  데이터가 사전에 정해진 특정 유형으로만 분류되는 경우.

​			범주형 데이터를 표현하기 위한 데이터 타입.

```R
범주형 데이터 -> 명목형 -> 값들 간에 크기 비교가 불가능한 경우. (정치성향)
			-> 순서형 -> 대,중,소 와 같이 값에 순서를 둘 수 있는 경우.

수치형 데이터 -> 숫자로 나온 값을 의미. (방의 크기를 기록하거나, 학생들 성적의 경우)

- factor 인지 확인.
is.factor()

#example.
# 성별은 범주형 데이터이며 명목형이다. ("m"남성과 "f"여성.)
sex <- factor("m", c("m","f"))
```

##### NA, NULL

```R
NA (Not Available)
NA 확인 -> is.na (na 가 있을 시 TRUE, 없을 시 FALSE)

NULL, na 랑 다름.
is.null 로 확인가능.

na 는 값이 빠져 있는 경우.
null 은 변수값이 아직 미정인 상태.
```





### 독립변수와 종속변수

독립변수 : 다른 변수에 영향을 받지 않는 변수.

종속변수 : 독립변수에 영향을 받아서 변화하는 변수.





## 2. 선형회귀







## 3. 추론 통계

#### 1. 가설

##### 귀무가설 (영가설 = H0)

`일반적으로 맞다고 가정하는 가설`

##### 대립가설 (H1)

`새롭게 맞다고 증명하려는 가설`





## 4. 상관분석

두 변수가 상관이 있는지 없는지.

`상관계수 = -1 < x < 1`

모수일떄는 pearson 상관계수 분석.
서열변수 일때는 spearman 상관계수 분석.

```R
# 대표적인 상관계수 방법.
# Pearson 상관계수 (N) ***
# Spearman (S)
# Kendall 의 tau (K)

# t-test		<->		MWW
# Anova			<->		WRS
# pared t		<->		WSR
# 모수 정규분포		정규분포 않거나, 서열 변수일때.



# 상관계수 구하기.
install.packages("UsingR")
library(UsingR)

data("galton")
str(galton)
head(galton)

#   child parent
# 1  61.7   70.5
# 2  61.7   68.5
# 3  61.7   65.5
# 4  61.7   64.5
# 5  61.7   64.0
# 6  62.2   67.5

#1. 그래프 먼저 그려서 상관관계 보기.
plot(child ~ parent, data = galton)

#2. 상관분석 - cor.test()
cor.test(galton$child, galton$parent)

#   Pearson's' product-moment correlation

# data:  galton$child and galton$parent
# t = 15.711115, df = 926, p-value < 0.00000000000000022204
# alternative hypothesis: true correlation is not equal to 0
# 95 percent confidence interval:
#  0.4064066627 0.5081153026
# sample estimates:
#          cor 
# 0.4587623683 
#
# p-value 가 0.05보다 작기 때문에 상관관계가 있다고 본다.
# 상관관계 = 0.458

#3. 선형모델 만들기
out = lm(child ~ parent, data = galton)
summary(out)

# Residuals:
#        Min         1Q     Median         3Q        Max 
# -7.8050162 -1.3661445  0.0486932  1.6338555  5.9264367 

# Coefficients:
#                Estimate  Std. Error  t value               Pr(>|t|)    
# (Intercept) 23.94153018  2.81087834  8.51746 < 0.000000000000000222 ***
# parent       0.64629058  0.04113588 15.71112 < 0.000000000000000222 ***
# ---
# Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

# Residual standard error: 2.238547 on 926 degrees of freedom
# Multiple R-squared:  0.2104629, Adjusted R-squared:  0.2096103 
# F-statistic: 246.8391 on 1 and 926 DF,  p-value: < 0.00000000000000022204
#
# parent의 0.64629058 이 기울기.
# y = 23.94153 + 0.64629 * x

abline(out, col = "red")
```

correlation graph :         <img src = "C:\work\Typora\KicTypora\assets\correlation-1538989860139.png" width="500px">



#### 4-1. 겹친 데이터 그래프.

```R
plot(jitter(child,5) ~ jitter(parent,5), galton)
abline(out, col = "red") # 그래프대로 선 넣기.
sunflowerplot(galton) # 꽃모양. 잎의 숫자대로 많이 겹쳐있다는 뜻.

# sample data;
install.packages("SwissAir")
library(SwissAir)
data("AirQual")
head(AirQual)

Ox <- AirQual[, c("ad.O3", "lu.O3", "sz.O3")] + AirQual[, c("ad.NOx", "lu.NOx","sz.NOx")] - AirQual[, c("ad.NO", "lu.NO", "sz.NO")]
View(Ox)
names(Ox) <- c("ad", "lu", "sz")

plot(lu ~ sz, data = Ox)

install.packages("hexbin")
library(hexbin)
bin <- hexbin(Ox$lu, Ox$sz, xbins = 50) # 육각형으로.
plot(bin)

smoothScatter(Ox$lu, Ox$sz) # 육각형 연하게.

install.packages("IDPmisc")
library(IDPmisc)
iplot(Ox$lu, Ox$sz) # 온도 색깔로. 빨간색은 진한거.
```





## etc

```R
# 인자 변환
as.factor(c())
as.numeric(x)

```



```R
# lm summary

lm(formula = Sepal.Length ~ Sepal.Width + Petal.Length + Petal.Width, 
    data = iris)

# 회귀식에 의해 추정된 값과 실제값(입력값)의 차이. - Residuals
Residuals:
     Min       1Q   Median       3Q      Max 
-0.82816 -0.21989  0.01875  0.19709  0.84570 
#	최소값   1사분위  중앙값    3사분위     최대값
# 1사분위는 데이터의 25%, 3사분위는 데이터의 75%.

# 추정된 회귀식의 계수.
Coefficients:
             Estimate Std. Error t value Pr(>|t|)    
#			 추정된계수   표준오차    t값    p-value
(Intercept)   1.85600    0.25078   7.401 9.85e-12 ***
# intercept 는 절편을 의미.
# (y절편) 회귀식에서 계수의 유의성을 판단하기 위해 t분포를 이용한다.
Sepal.Width   0.65084    0.06665   9.765  < 2e-16 ***
Petal.Length  0.70913    0.05672  12.502  < 2e-16 ***
Petal.Width  -0.55648    0.12755  -4.363 2.41e-05 ***
---
Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

# Residual standard error 잔차 표준오차
#	잔차표준오차: 0.3145, 자유도: 146.  관측값에서 -1 한 값이 자유도가 된다.
Residual standard error: 0.3145 on 146 degrees of freedom

# 	Multiple R-squared 결정계수
#		종속변수의 변화(변동)을 얼마나 설명하는지 나타내는 지표.(0~1)
#	Adjusted R-squared 수정결정계수
#		결정계수와 차이가 크면 회귀모형 재검토 해야함.
Multiple R-squared:  0.8586,	Adjusted R-squared:  0.8557 
# F-statistic : F-검정통계량, 모형 전체의 유의성을 판단하기 위한 통계량.
# p-value: 0.05 "이하" 모형은 유의함.
F-statistic: 295.5 on 3 and 146 DF,  p-value: < 2.2e-16

# * 이 많을 수록 통계에 유의함.
#
# R-Square : 결정계수
#		회귀식의 검정에 쓰인다.
#- 1에 가까울 수록 회귀식이 자료를 잘 설명하고 있다.
#- 결정계수는 독립변수로부터 예측되는 종속변수의 분산의 비율을 의미함. (중요)
#	- 결정계수는 0 과 1 사이의 값을 가짐.
#	- R2 = 0 이면 독립변수는 종속변수를 전혀 예측할 수 없다는것을 의미.
#	- R2 = 1 이면 독립변수는 종속변수를 오차없이 예측할 수 있다는것을 의미.
#	0과 1 사이의 R2 값은 종속변수가 예측 가능하냐를 의미함.
#	F검정통계량은 295.5, 제 1,제 2 자유도는 3,146
#
# T값은 각 독립변수의 유의성을 판단하기 위한 통계량이고,
# F값은 모형의 유의성을 판단하기 위한 통계량.
# P-value 는 분포에서 통계량이 확률적으로 봤을 때 어떤 값을 가지는지 "통계량을 확률로 환산한 수치".
```



#### SVM





