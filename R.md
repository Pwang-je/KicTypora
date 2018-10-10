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



## 두 그룹의 평균 비교 -  t-test, MWW test, Welch's t-test



```R

# 두 그룹의 평균 비교에는 3가지 통계법만 사용함.
#  - 1. t-test
#  - 2. Mann-Whitney U test(Wilcoxon rank-sum test) - 비모수적 통계방법.
#  - 3. Welch's t-test
 
#  1. 결과값이 연속변수냐? -> 정규분포를 하냐? -> 등분산인지? -> (1번방법 : t-test)
#                                               아닌지? -> (3번방법 : welch's t-test)
#                       ->         안하냐? -> (2번방법 : MWU test) 
#               아니냐?  -> (2번방법 : MWU test)


install.packages("moonBook")
library(moonBook)

data(acs)
summary(acs)
str(acs)
head(acs)

#   age    sex cardiogenicShock   entry              Dx   EF height weight
# 1  62   Male               No Femoral           STEMI 18.0    168     72
# 2  78 Female               No Femoral           STEMI 18.4    148     48
# 3  76 Female              Yes Femoral           STEMI 20.0     NA     NA
# 4  89 Female               No Femoral           STEMI 21.8    165     50
# 5  56   Male               No  Radial          NSTEMI 21.8    162     64
# 6  73 Female               No  Radial Unstable Angina 22.0    153     59

#        BMI obesity  TC LDLC HDLC  TG  DM HBP smoking
# 1 25.51020     Yes 215  154   35 155 Yes  No  Smoker
# 2 21.91381      No  NA   NA   NA 166  No Yes   Never
# 3       NA      No  NA   NA   NA  NA  No Yes   Never
# 4 18.36547      No 121   73   20  89  No  No   Never
# 5 24.38653      No 195  151   36  63 Yes Yes  Smoker
# 6 25.20398     Yes 184  112   38 137 Yes Yes   Never


# 1. 정규성을 먼저 검사. = p-value 가 0.05 보다 크면 정규성을 갖는다.
moonBook::densityplot(age ~ sex, data = acs)
shapiro.test(acs$age[acs$sex == "Male"])
    # data:  acs$age[acs$sex == "Male"]
    # W = 0.99631, p-value = 0.2098

shapiro.test(acs$age[acs$sex == "Female"])
    # data:  acs$age[acs$sex == "Female"]
    # W = 0.96138, p-value = 6.34e-07

wilcox.test(age ~ sex, data = acs)
    # W = 115270, p-value < 2.2e-16

# 2. 등분산을 검사. (두 그래프의 뾰족함의 정도가 비슷한지? 를 검증하는 방법 )
var.test(age ~ sex, data = acs)
    # F = 0.91353, num df = 286, denom df = 569, p-value = 0.3866
    # p-value 가 0.05 보다 크다면 등분산을 한다. (뾰족함의 정도가 비슷하다 = 둘이 비교해도 문제 없다.)

# 3. t-test;
# t.test(종속변수 ~ 단독변수, 데이터, 등분산을 했냐? = TRUE)
t.test(age ~ sex, data = acs, var.equal = T)
    # t = 10.071, df = 855, p-value < 2.2e-16
    # mean in group Female   mean in group Male 
    #             68.67596             60.61053 
    # 이 여성 그룹이 연령대가 더 높은 것은 통계적으로 의미를 갖는다.

# 3-1. 정규분포는 하지만, 등분산은 아닐때. = Welch's test. 
t.test(age ~ sex, data = acs, var.equal = F)
    # t = 10.222, df = 596.99, p-value < 2.2e-16
    # mean in group Female   mean in group Male 
    #             68.67596             60.61053 
```





## 세 그룹(혹은 그 이상의 평균 비교)

> 1) 결과값이 연속변수인지 아닌지,
> 2) 연속변수라면 ~ 정규분포를 따르는지 안따르는지,
> 3) 등분산을 만족 하는지 안하는지.

```R
# 세 그룹, 혹은 그 이상의 평균 비교에는 3가지 통계법만 사용함.
#  - 1. ANOVA test
#  - 2. Kruskal-wallis H test
#  - 3. Welch's ANOVA
 
#  1. 결과값이 연속변수냐? -> 정규분포를 하냐? -> 등분산인지? -> (1번방법 : ANOVA test)
#                                               아닌지? -> (3번방법 : Welch's ANOVA)
#                       ->         안하냐? -> (2번방법 : Kruskal-wallis H test) 
#               아니냐?  -> (2번방법 : Kruskal-wallis H test)


# 정규분포 확인
# 정규 1. 하나씩 다 쳐보기
shapiro.test(acs$LDLC[acs$Dx == "NSTEMI"])
# W = 0.89996, p-value = 1.56e-08   p-value < 0.05 정규분포 하지 않음!
shapiro.test(acs$LDLC[acs$Dx == "STEMI"])
# W = 0.99574, p-value = 0.6066  p-value > 0.05 정규분포!
shapiro.test(acs$LDLC[acs$Dx == "Unstable Angina"])
# W = 0.96889, p-value = 2.136e-07  p-value < 0.05 정규분포 하지 않음!

# 정규 2. 3개를 하나로 묶어서 p-value 뽑기.
out = aov(LDLC ~ Dx, data = acs)
shapiro.test(resid(out))
# shapiro.test(resid(aov(LDLC ~ Dx, data = acs))) = 한줄로 하기.
# W = 0.97137, p-value = 1.024e-11  세 그룹 중 하나 이상이 정규분포 안함.

# 3개 중 1개만 정규분포이기 때문에, 정규분포를 대체적으로 따르지 않는다고 봄.
# 따라서, Kruskal-wallis H test 를 한다.
```





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





#### Excel -> CSV

- 쉼표로 구분된 값으로 (다른이름으로 저장).





#### Power Analysis

```md
실험군과 대조군의 모집이 항상 필요하고, 실험군과 대조군의 모집인원에 따라 연구비의 규모가 달라짐
가장 이상적인건, 최소의 인원으로 충분히 의미있는 결과를 뽑아내는 것인데,
바로 이때 최소의 인원이 몇 명이 필요한지를 계산해 내는 것이 power analysis.
```

- 비모수 :  정규분포를 하지 않을 때,
- 모수적 : 정규분포를 할 때,

1. n 수가 적어서인지, (on going)
2. n 수는 충분하지만 실제로 두 그룹간의 결과가 차이가 없는지 모를때.

##### 비모수적 통계계산

```md
2개의 집단에서 평균을 내는데 있어서, 갑자기 A집단에 큰 숫자가 들어 왔을 때 급격하게 평균값이 상승하는것을 막기 위해 점수가 아닌 다른 방법(등수)으로 계산을 하기 위한 방법. (Rank-sum test)
```





