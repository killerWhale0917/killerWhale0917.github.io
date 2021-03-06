---
title:  "[Data Visualization] Pie Chart"
excerpt: "Matplotlib์ Pie Chart"

categories:
  - datavis
tags:
  - [AI, Naver, BoostCamp, Python, Matplotlib]
toc: true
toc_sticky: true
 
date: 2022-02-11 01:00:00
last_modified_at: 2022-02-11 01:00:00
---
๐ **์๋ฆฝ๋๋ค!**<br>
์ด๋ฒ์ ์์ฑ๋๋ ๊ธ์ **๋ค์ด๋ฒ ๋ถ์คํธ์บ ํ AI Tech**๋ฅผ ์๊ฐํ๋ฉฐ ์ ๋ฆฌํ๋ ๊ธ์๋๋ค.<br>
์ฌ๊ธฐ์ ์กด์ฌํ๋ ๊ฐ์ ์๋ฃ์ ์ถ์ฒ๋ ๋ค์ด๋ฒ ๋ถ์คํธ์ฝ์ค/์บ ํ์๊ฒ ์์ต๋๋ค.
{: .notice--info}

# Pie Chart

![image](https://user-images.githubusercontent.com/91870042/153742270-34ed332a-534a-40ff-b3a7-b21ea8945c9b.png){: .align-center width="70%"}


- ์์ ๋ถ์ฑ๊ผด๋ก ๋ถํ ํ์ฌ ํํํ๋ ํต๊ณ์ฐจํธ
    - ์ ์ฒด๋ฅผ ๋ฐฑ๋ถ์๋ก ๋ํ๋ผ๋ ์ฌ์ฉํ๊ธฐ๊ฐ ์ข๋ค.
- ๊ฐ์ฅ ๋ง์ด ์ฌ์ฉํ๋ ์ฐจํธ์ง๋ง, ์ง์ํ๋ ๊ฒ์ด ์ข๋ค
    - ๊ฐ feature๋ณ๋ก ๋น๊ตํ๊ธฐ๊ฐ ์ด๋ ต๋ค
    - ์ ์ฉ์ฑ์ด ๋จ์ด์ง๋ค
    - ๊ฐ๋๊ฐ ๊ธธ์ด๋ณด๋ค ๋น๊ตํ๊ธฐ๊ฐ ์ด๋ ต๊ธฐ ๋๋ฌธ์, bar plot์ด ์ ์ฉํ๋ค.
    - ๋จ๋์ ์ผ๋ก ์ฌ์ฉํ๊ธฐ ๋ณด๋ค๋ ํจ๊ป ์ฌ์ฉํ๋ ๊ฒ์ ๊ถ์ฅํ๋ค.
    - `waffle chart` ๋ฅผ ์ฌ์ฉํ๋ ๊ฒ์ด ๋น๊ตํ๋๋ฐ ์์ด์ ๋ ์ ์ฉํ๋ค.

## Pie Chart ์์ฉ

### Donut Chart

![image](https://user-images.githubusercontent.com/91870042/153742272-3c12f2fe-74a3-4d65-84a3-5131f4e24d17.png){: .align-center width="70%"}

- ์ค๊ฐ์ด ๋ซ๋ ค์๋ Pie Chart
- ๊ธฐ์กด์ Pie Chart์ ๋ต๋ตํจ์ ํด์์์ผ์ฃผ๊ธฐ ๋๋ฌธ์ ๋์์ธ ์ ์ผ๋ก ์ ํธ๋๋ค.
- Presentation์ด๋, ์ธํฌ๊ทธ๋ํฝ์์ ์ข์ข ์ฌ์ฉ๋๋ค
- `Plotly` ์์ ์ฝ๊ฒ ์ฌ์ฉํ  ์ ์๋ค.

### Sunburst Chart

![image](https://user-images.githubusercontent.com/91870042/153742282-aaded025-943c-4a57-b1db-6f8bdc62457a.png){: .align-center width="70%"}

- ํ์ด(Sunburst)๋ฅผ ๋ฎ์ ์ฐจํธ
- ๊ณ์ธต์  ๋ฐ์ดํฐ๋ฅผ ์๊ฐํํ๋๋ฐ ๋ง์ด ์ฌ์ฉ๋๋ค.
- ๊ตฌํ ๋์ด๋์ ๋นํด์ ํ๋ คํ๋ค๋ ์ฅ์ ์ด ์์ง๋ง, ๊ฐ๋์ฑ์ด ์ข์ง๋ ์๋ค
- ์คํ๋ ค Sunburst๋ฅผ ์ฌ์ฉํ๊ธฐ ๋ณด๋ค๋ Treemap์ ์ฌ์ฉํ๋ค.
- `Plotly` ์์ ์ฝ๊ฒ ์ฌ์ฉํ  ์ ์๋ค.

<br>

# ์ค์ต

- `ax.pie()` ๋ฅผ ์ฌ์ฉํด์ pie plot์ ๊ทธ๋ฆฐ๋ค.

```python
labels = ['A', 'B', 'C', 'D']
data = np.array([60, 90, 45, 165]) # total 360

fig, ax = plt.subplots(1, 1, figsize=(7, 7))
ax.pie(data, labels=labels)
plt.show()
```

![image](https://user-images.githubusercontent.com/91870042/153742286-1c9ac389-97b2-4371-bfb8-5223b7175578.png){: .align-center width="40%"}

- ๋์ผํ ๋ฐ์ดํฐ์ ๋ํด์ Pie chart์ Bar Chart์ ์ฅ๋จ์ ์ ๋ค์๊ณผ ๊ฐ๋ค.
    - ์ฅ์ : Pie Chart๋ ๋น์จ์ ๋ํ ์ ๋ณด๋ฅผ ์ ๊ณตํด์ค ์ ์๋ค.
    - ๋จ์ : ๊ฐ feature์ ๋ํด์ ๊ตฌ์ฒด์ ์ธ ์์ ๋น๊ต๊ฐ ์ด๋ ต๋ค.

```python
fig, axes = plt.subplots(1, 2, figsize=(12, 7))

axes[0].pie(data, labels=labels)
axes[1].bar(labels, data)

plt.show()
```

![image](https://user-images.githubusercontent.com/91870042/153742290-305866c4-b63e-40f8-ada6-58c391a2fd9b.png){: .align-center width="70%"}

- `startangle` : feature์ ์์ ๊ฐ๋๋ฅผ ์ง์ ํ  ์ ์๋ค.

```python
fig, ax = plt.subplots(1, 1, figsize=(7, 7))
ax.pie(data, labels=labels, startangle=90)
plt.show()
```

![image](https://user-images.githubusercontent.com/91870042/153742295-81fd17f1-1e13-4f35-96be-63c37b432efa.png){: .align-center width="40%"}

- `explode` : pie ํ์กฐ๊ฐ์ ๋ถ๋ฆฌํด์ ๊ฐ์กฐํ  ์ ์๋ค.

```python
fig, ax = plt.subplots(1, 1, figsize=(7, 7))
explode = [0, 0, 0.2, 0]

ax.pie(data, labels=labels, explode=explode, startangle=90)
plt.show()
```

![image](https://user-images.githubusercontent.com/91870042/153742298-24ddea6a-927b-4e3a-a14e-1991a12d7fa7.png){: .align-center width="40%"}

- `shadow` : Pie Chart์ ๊ทธ๋ฆผ์๋ฅผ ์กฐ์ 

```python
fig, ax = plt.subplots(1, 1, figsize=(7, 7))
explode = [0, 0, 0.2, 0]

ax.pie(data, labels=labels, explode=explode, startangle=90, shadow=True)
plt.show()
```

![image](https://user-images.githubusercontent.com/91870042/153742302-43656d90-dbad-45eb-9c08-d5ff1370b537.png){: .align-center width="40%"}

- `autopct` : ๊ฐ ๋ฐ์ดํฐ๊ฐ ์ผ๋งํผ์ ์ฐจ์งํ๊ณ  ์๋์ง ๋ํ๋ผ ์ ์๋ค.

```python
fig, ax = plt.subplots(1, 1, figsize=(7, 7))
explode = [0, 0, 0.2, 0]

ax.pie(data, labels=labels, explode=explode, startangle=90,
      shadow=True, autopct='%1.1f%%')
plt.show()
```

![image](https://user-images.githubusercontent.com/91870042/153742305-dc5c9d66-9171-4cc1-bb76-2188f90bacad.png){: .align-center width="40%"}

- `labeldistance` : Pie Chart์ label์ด ๋๋ฌด ๊ธธ๊ฒฝ์ฐ, ๊ธ์๊ฐ Pie Chart์ ๊ฒน์น  ์ ์๋ค. ๊ทธ๊ฒ์ ๋ฐฉ์งํ๊ธฐ ์ํด์ Pie Chart์์ ๊ฑฐ๋ฆฌ๋ฅผ ๋ ๋ฉ๊ฒ ํ  ์ ์๋ค.
- `rotatelabels` : label์ ํ์ 

```python
fig, ax = plt.subplots(1, 1, figsize=(7, 7))
explode = [0, 0, 0.2, 0]

ax.pie(data, labels=labels, explode=explode, startangle=90,
      shadow=True, autopct='%1.1f%%', labeldistance=1.15, rotatelabels=90)
plt.show()
```

![image](https://user-images.githubusercontent.com/91870042/153742309-ea7f9e27-d95f-4505-b495-d166d5963d0c.png){: .align-center width="40%"}

- `counterclock` : feature๋ค์ ๋ฐฐ์ด์ ๋ฐ์๊ณ๋ฐฉํฅ์ด ์๋, ์๊ณ๋ฐฉํฅ์ผ๋ก ๋์ดํด๋ณผ ์ ์๋ค.

```python
fig, ax = plt.subplots(1, 1, figsize=(7, 7))
explode = [0, 0, 0.2, 0]

ax.pie(data, labels=labels, explode=explode, startangle=90, counterclock=False)
plt.show()
```

![image](https://user-images.githubusercontent.com/91870042/153742312-2f41f1c8-6615-4932-95fc-019f7d1d00bd.png){: .align-center width="40%"}

- `radius` : ์ ์์ฒด์ ํฌ๊ธฐ๋ฅผ ๊ฒฐ์ ํ  ์ ์๋ค.

```python
fig, axes = plt.subplots(1, 3, figsize=(12, 7))
explode = [0, 0, 0.2, 0]

for size, ax in zip([1, 0.8, 0.5], axes):
    ax.pie(data, labels=labels, explode=explode, startangle=90, counterclock=False,
           radius=size
          )
plt.show()
```

![image](https://user-images.githubusercontent.com/91870042/153742319-71c8ce38-0f94-4229-ac12-ae81eea84705.png){: .align-center width="70%"}

- Donut Chart๋ ๊ธฐ์กด์ Pie plot์ ๋ ํ๋์ ์์ ๊ทธ๋ฆฌ๋ ๋ฐฉ๋ฒ์ผ๋ก ๊ตฌํํ๋ค.

```python
fig, ax = plt.subplots(1, 1, figsize=(7, 7))

ax.pie(data, labels=labels, startangle=90,
      shadow=True, autopct='%1.1f%%')

# ์ขํ 0, 0, r=0.7, facecolor='white'
centre_circle = plt.Circle((0,0),0.70,fc='white')
ax.add_artist(centre_circle)

plt.show()
```

![image](https://user-images.githubusercontent.com/91870042/153742327-f300a06a-ffde-490c-a56c-3e41e2a3cb8d.png){: .align-center width="40%"}

- `pctdistance` : Percentage๊ฐ ์์ ์ค์ฌ์์ ์ผ๋ง๋ ๋จ์ดํธ๋ฆด์ง ๊ฒฐ์ ํ  ์ ์๋ค.
- `textprops` : ํ์คํธ์ ์์๊ณผ ๊ฐ์ ์ ๋ณด๋ฅผ ์ค์ ํ  ์ ์๋ค.

```python
fig, ax = plt.subplots(1, 1, figsize=(7, 7))

ax.pie(data, labels=labels, startangle=90,
      shadow=True, autopct='%1.1f%%', pctdistance=0.85, textprops={'color':"w"})

# ์ขํ 0, 0, r=0.7, facecolor='white'
centre_circle = plt.Circle((0,0),0.70,fc='white')
ax.add_artist(centre_circle)

plt.show()
```

![image](https://user-images.githubusercontent.com/91870042/153742331-90a57a59-8a09-45d9-a0b7-cb88651e53c2.png){: .align-center width="40%"}