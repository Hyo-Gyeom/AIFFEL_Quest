# AIFFEL Campus Online 5th Code Peer Review Templete
- 코더 : 이효겸
- 리뷰어 : 신유진


# PRT(PeerReviewTemplate) 
각 항목을 스스로 확인하고 토의하여 작성한 코드에 적용합니다.

- [X] 코드가 정상적으로 동작하고 주어진 문제를 해결했나요?
  
- [X] 주석을 보고 작성자의 코드가 이해되었나요?
  > 이해됐음, task별로 잘 구분되어있음
- [X] 코드가 에러를 유발할 가능성이 없나요?
  >위 항목에 대한 근거 작성 필수
- [X] 코드 작성자가 코드를 제대로 이해하고 작성했나요?
  > 넵, 디버깅까지 한 흔적이 보임.
- [X] 코드가 간결한가요?
  > 알아보기 쉽고 직관적임

# 전체 코드의 pipeline이 알기 쉽고 직관적이었음
1. 데이터 불러오기 및 형변환
2. 데이터 분포 확인 후 모델링 (모델링 부분은 코드 생략)
```python
# 
train_data_path = join('data', 'train.csv')
sub_data_path = join('data', 'test.csv')
data = pd.read_csv(train_data_path)
sub = pd.read_csv(sub_data_path)
data_id = data['id']
del data['id']
sub_id = sub['id']
del sub['id']
train_len = len(data)
y = data['price']
df = pd.concat((data, sub), axis=0, ignore_index=True)
df.isna().sum().sum()
6468
df['date'] = df['date'].apply(lambda x : str(x[:6])).astype(int)
df
date	price	bedrooms	bathrooms	sqft_living	sqft_lot	floors	waterfront	view	condition	grade	sqft_above	sqft_basement	yr_built	yr_renovated	zipcode	lat	long	sqft_living15	sqft_lot15
0	201410	221900.0	3	1.00	1180	5650	1.0	0	0	3	7	1180	0	1955	0	98178	47.5112	-122.257	1340	5650
1	201502	180000.0	2	1.00	770	10000	1.0	0	0	3	6	770	0	1933	0	98028	47.7379	-122.233	2720	8062
2	201502	510000.0	3	2.00	1680	8080	1.0	0	0	3	8	1680	0	1987	0	98074	47.6168	-122.045	1800	7503
3	201406	257500.0	3	2.25	1715	6819	2.0	0	0	3	7	1715	0	1995	0	98003	47.3097	-122.327	2238	6819
4	201501	291850.0	3	1.50	1060	9711	1.0	0	0	3	7	1060	0	1963	0	98198	47.4095	-122.315	1650	9711
...	...	...	...	...	...	...	...	...	...	...	...	...	...	...	...	...	...	...	...	...
21498	201406	NaN	3	1.75	1500	11968	1.0	0	0	3	6	1500	0	2014	0	98010	47.3095	-122.002	1320	11303
21499	201501	NaN	3	2.00	1490	1126	3.0	0	0	3	8	1490	0	2014	0	98144	47.5699	-122.288	1400	1230
21500	201502	NaN	3	2.50	1310	1294	2.0	0	0	3	8	1180	130	2008	0	98116	47.5773	-122.409	1330	1265
21501	201406	NaN	2	0.75	1020	1350	2.0	0	0	3	7	1020	0	2009	0	98144	47.5944	-122.299	1020	2007
21502	201501	NaN	3	2.50	1600	2388	2.0	0	0	3	8	1600	0	2004	0	98027	47.5345	-122.069	1410	1287
21503 rows × 20 columns

df.loc[df['yr_renovated'] != 0, 'yr_built'] = df['yr_renovated']
del df['yr_renovated']
df['date'] = df['date'] - 201400
df['lat'] = df['lat'].apply(lambda x : str(x)[3:7]).astype(int)
df['long'] = df['long'].apply(lambda x : str(x)[5:]).astype(int)
df['yr_built'] = df['yr_built'] - 1900
df.loc[df['sqft_basement'] != 0, 'sqft_basement'] = 1
df['lat'] = df['lat'] / df['lat'].max()
df['long'] = df['long'] / df['long'].max()
df['yr_built'] = df['yr_built'] / df['yr_built'].max()
df = df.round(2)
df
date	price	bedrooms	bathrooms	sqft_living	sqft_lot	floors	waterfront	view	condition	grade	sqft_above	sqft_basement	yr_built	zipcode	lat	long	sqft_living15	sqft_lot15
0	10	221900.0	3	1.00	1180	5650	1.0	0	0	3	7	1180	0	0.48	98178	0.66	0.26	1340	5650
1	102	180000.0	2	1.00	770	10000	1.0	0	0	3	6	770	0	0.29	98028	0.95	0.23	2720	8062
2	102	510000.0	3	2.00	1680	8080	1.0	0	0	3	8	1680	0	0.76	98074	0.79	0.05	1800	7503
3	6	257500.0	3	2.25	1715	6819	2.0	0	0	3	7	1715	0	0.83	98003	0.40	0.33	2238	6819
4	101	291850.0	3	1.50	1060	9711	1.0	0	0	3	7	1060	0	0.55	98198	0.53	0.32	1650	9711
...	...	...	...	...	...	...	...	...	...	...	...	...	...	...	...	...	...	...	...
21498	6	NaN	3	1.75	1500	11968	1.0	0	0	3	6	1500	0	0.99	98010	0.40	0.00	1320	11303
21499	101	NaN	3	2.00	1490	1126	3.0	0	0	3	8	1490	0	0.99	98144	0.73	0.29	1400	1230
21500	102	NaN	3	2.50	1310	1294	2.0	0	0	3	8	1180	1	0.94	98116	0.74	0.41	1330	1265
21501	6	NaN	2	0.75	1020	1350	2.0	0	0	3	7	1020	0	0.95	98144	0.76	0.30	1020	2007
21502	101	NaN	3	2.50	1600	2388	2.0	0	0	3	8	1600	0	0.90	98027	0.69	0.07	1410	1287
21503 rows × 19 columns

fig, ax = plt.subplots(9, 2, figsize=(20, 60))

# id 변수는 제외하고 분포를 확인합니다.
count = 0
columns = df.columns
for row in range(9):
    for col in range(2):
        sns.kdeplot(df[columns[count]], ax=ax[row][col])
        ax[row][col].set_title(columns[count], fontsize=15)
        count+=1
 
```

# 참고 링크 및 코드 개선
```python
# 없는 것 같음.
# 코드 리뷰를 통해 개선한 코드가 있다면 코드와 간략한 설명을 첨부합니다.
```
