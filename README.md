- 통계학 쉽게 한줄정리 ~
- R code 정리도 함께 올리려고 함. 

### Chapter 1. 탐색적 데이터 분석
### Chapter 2. 데이터와 표본분포
### Chapter 3. 통계적 실험과 유의성 검정

#### 생각해볼 것
`통계적 추론 과정` 
- 가설 세우기 -> 실험 설계하기 -> 데이터 수집하기 -> 추론 및 결론 도출하기

`가설검정의 목적은` 
- 관찰된 효과가 우연에 의해 발생한 것인지를 알아보기 위한 절차

`가설검정의 논리는` 
- 실제로는 우연히 일어난 일이지만, 흔하지 않다는 것에 주목하며 의미있고 우연이 아닐 것이라고 해석하려는 인간의 경향을 감안할 때, 실험에서 얻은 그룹간의 차이가 랜덤을 통해 얻을 수 있는 합리적인 수준과는 더 극단적으로 달라야 한다는 증거를 보여줘야 한다.

#### 통계학 vs 데이터 과학
- 비즈니스에서 사용하는 데이터 과학은 구체적인 비즈니스의 목표치(KPI)에 관심을 둔다.
- 통계학은 불확실성을 수치화하여 이해하고자 한다. 
> 빅데이터 시대에 통계학의 역할은 무엇일까 생각해보면, 빅데이터 시대라고 해서 모집단을 대표하는 데이터가 쌓이는 것이 아니고 데이터의 질이 낮은데도 불구하고 데이터 크기만 늘어나는 상황이다.
> 다양한 데이터를 효과적으로 다루고 데이터 편향을 최소화하기 위한 방법으로 표본추출, 모집단 추론은 중요하다. 
> 결국 예측 모델링을 할 때도 작은 표본으로 모델링하고, 테스트하기 때문이다. 


## 기초통계

#### 대표값 
- 주로 산술평균 사용하지만. 중앙값, 최빈값도 종종 사용함.
- 로버스트한값 필요 시,
- 1. 절사평균
   - 정해진 갯수의 극단값을 제외한 나머지 값들의 평균.
- 2. 가중평균
   - Xw = sum(X * W) / sum(W)
   - 본래 값이 다른 값에 비하여 변화량이 클 때 작은 가중치를 부여하여 사용하기도 함(신뢰도 낮은 센서에 작은 가중치)
   - 그룹간 N수가 차이가 날 때 작은 집단에 가중치를 줘서 동등한 비교가 가능하도록 하는 것.
- 3. 중간값

#### 산포의 측도
- 분산, 표준편차
- 변동계수(Coefficient of Variation) : 표준편차/평균 
     - 측정 단위가 다른 두 변수의 산포를 비교 가능함. 주로 10% 미만일 경우 평균 매우 안정적이며 30% 이상일 때는 불안정한 평균을 가진다는 의미로 해석가능.
- 범위 : 최대값 - 최소값 

#### 상관계수(Pearson상관계수)
- 변수간의 선형 관계를 파악할 때 사용함.
- 특이값에 민감하기 때문에, 로버스트한 값을 사용하기 위해서 데이터에 특이값을 제거하는 방법을 택하기도 한다.

#### 차원축소 
- row 축소 : Sampling 
   - 복원,비복원 / 층화,군집,계통 추출
- col 축소 : PCA, Factor Analysis등
   - 적은 차원의 변수를 새로 만들어서 기존의 많은 변수들이 제공했던 정보를 축약한다는 개념, 단 몇개의 변수로 알찬 정보를 담을 수 있다는 장점이 있음.

#### EDA 
- 연속형 vs 연속형 : scatter plot 
- 범주형 vs 연속형 : boxplot, barplot, violin plot
- 범주형 vs 범주형 : cross table


#### ERROR
- 제 1종오류 : 귀무가설 옳은데 귀무가설 기각할 확률 (실제로는 우연에 의한 것인데 효과가 있다고 잘못 결론내릴 확률) - 우연히 일어날 가능성을 제한하는 장치(비정상적 가능성의 임계 확률 값)
- 제 2종오류 : 귀무가설 거짓인데 귀무가설 채택할 확률 (실제로는 효과가 있는데 우연에 의한 것이라고 결론 내릴 확률)
- 검정력 : 귀무가설 거짓인데 귀무가설 거짓이라고 판단할 확률 (1-beta)

#### 신뢰구간 
- 모집단에서 반복적으로 표본을 추출할 때 데이터로부터의 평균이 모집단 평균을 100번 중 95번 포함하고 있다. 
- 95% 부트스트랩 신뢰구간이란 
   - 표본 통계량의 부트스트랩 표본 분포를 생성하고 각각의 통계량을 취해서 분포를 만들 수 있는데, 이때 부트스트랩 표본분포의 앞,뒤를 절단해서 중간 95%를 포함하는 구간을 의미함.
 - https://dermabae.tistory.com/184
 
#### P-value 
- `랜덤 모델이 주어졌을 때 , 그 결과가 관찰된 결과보다 더 극단적인 확률`
- 우연히 발생한 것인지 정말 특별한것인지 구분하기 위하여, 즉 통계적 유의성을 측정하기 위한 하나의 지표.
- 귀무가설 하에서의 확률분포에서 관찰된 값보다 극단적인 값이 관찰될 확률 
- 값이 매우 낮다면, 귀무가설 하에서는 통계량이 관측될 확률이 매우 낮다는 의미이고, 귀무가설 하에서의 값이 아니라는 증거가 된다.
- Ex. p-value=0.3이라면 우연히 얻은 결과의 30%가 관찰한 것만큼 극단적이거나 그보다 더 극단적인 결과를 얻을 것이라고 기대된다는 의미.
- 

#### CLT (중심극한정리 Central Limit Theorem)
- 모집단의 분포와는 상관 없이(정규분포가 아니더라도) 충분히 많은 독립적인 표본이 있으면, 표본의 분포는 근사적으로는 정규분포를 따른다
    - 이 분포의 평균은 모집단의 평균과 같고, 분산은 모집단의 분산에 표본 크기만큼을 나누어준 값과 같게 된다.
- 표본을 정규성 가정하여 추론 방법 사용할 수 있다. 
- 신뢰구간 구하거나, 가설 검증할 때 t 분포와 같은 정규 근사 분포를 사용 가능함.

#### QQ Plot
- 표본이 그 분포에 얼마나 가까운지 알기 위해 사용하는 방법
- Ex. Normal Q-Q Plot일 때 데이터A가 정규분포를 따르는지 알고싶을 때
   - 데이터A를 정규화된 값으로 변환 (z-value) 
   - y축은 정규화된 값의 정렬된 값, x축은 해당 z값의 정규분포에서의 분위수
   
#### 분포 
- 이항분포
   - 성공확률이 p인 사건을 n번 시행할 때 성공한 횟수의 분포. 즉 X~ Ber(n,p) 
   - Ex. 한번의 클릭이 구매로 이어질 확률이 0.02일 때 200회 클릭 시 0회 매출 관찰할 확률은?
- 포아송분포 
   - 단위시간동안 발생한 사건 수의 분포 X~ Poisson(lambda)
   - Ex. 고객 서비스센터에 접수되는 문의전화가 분당 2회라면, 100분당 문의전화 횟수는? 
- 지수분포 
   - 사건과 사건간의 시간의 분포 X~ Exp(lambda)
   - Ex. 고장 발생 시간, 개별 고객 상담에 소요되는 시간
- 웨이블 분포 
   - 지수분포는 사건 발생률이 시간이 지남에 따라 변하지 않기 때문에 이런 단점을 보완하기 위하여 shape parameter beta를 이용해 확률 변화시킬 수 있음. 
   - beta >1 : 고장률 증가 , beta < 1 : 고장률 감소

#### 3.3 재표본추출(Resampling)
- 목적 : 랜덤한 변동성을 알아보자! (관측된 표본은 우연히 얻어진거니까 이 하나의 표본은 불확실성이 너무 커! 이 하나의 샘플로부터 또 샘플링해서 여러 샘플을 더 많이 생성한다면 불확실성을 더 줄일것이다!) 
`순열검정`
- 




### Chapter 6. 통계적 머신러닝














https://zzsza.github.io/data/2018/02/17/datascience-interivew-questions/
https://m.blog.naver.com/mykepzzang/220853827288

### 면접 질의
#### 1.통계
- `c1)중심극한정리(central limit theorem)는 무엇이며 왜 중요합니까?`
- 중심극한 정리란 모집단의 분포에 관계없이 표본수가 커지면 표본 평균의 분포가 정규분포로 수렴한다는 것인데, 이를 통해 통계적 추론이나 검정과 같은 통계 방법론을 활용할 수 있게 된다. 결국 표본으로부터 모집단 분포를 알아내는 데 과학적인 방법을 사용할 수 있어서 중요하다. 

- `2)샘플링이란 무엇입니까? 얼마나 많은 샘플링 방법을 알고 있습니까?`
- 모집단을 알기 위해 일부를 추출하여 조사를 수행하거나, 
- 랜덤추출
- 층화추출
- 군집추출
- 계통추출 

- `3)Type I과 Type II 에의 차이점은 무엇입니까?`

4)선형 회귀 분석이란 무엇입니까? P-value, coefficient, R-Squared value란 무엇을 의미합니까? 이 구성 요소 각각의 의미는 무엇입니까?

5)선형 회귀에 필요한 가정은 무엇입니까? 

6)통계적 상호 작용(statistical interaction)이란 무엇입니까?

7)선택 편향(selection bias)이란 무엇입니까?

8)가우스 분포가 아닌 데이터 세트의 예는 무엇입니까?

9)이항 확률 공식(Binomial Probability Formula)은 무엇입니까?




https://m.cafe.daum.net/statsas/OG7f/57
