---
title:  "[Data Visualization] Polar Coordinate"
excerpt: "Matplotlib์ Polar Plot, Radar Plot"

categories:
  - datavis
tags:
  - [AI, Naver, BoostCamp, Python, Matplotlib]
toc: true
toc_sticky: true
 
date: 2022-02-11 00:00:00
last_modified_at: 2022-02-11 00:00:00
---
๐ **์๋ฆฝ๋๋ค!**<br>
์ด๋ฒ์ ์์ฑ๋๋ ๊ธ์ **๋ค์ด๋ฒ ๋ถ์คํธ์บ ํ AI Tech**๋ฅผ ์๊ฐํ๋ฉฐ ์ ๋ฆฌํ๋ ๊ธ์๋๋ค.<br>
์ฌ๊ธฐ์ ์กด์ฌํ๋ ๊ฐ์ ์๋ฃ์ ์ถ์ฒ๋ ๋ค์ด๋ฒ ๋ถ์คํธ์ฝ์ค/์บ ํ์๊ฒ ์์ต๋๋ค.
{: .notice--info}

# Polar Plot

![image](https://user-images.githubusercontent.com/91870042/153741886-28a2775c-2b53-4966-bcd0-bce8388849b8.png){: .align-center width="40%"}


- ๊ทน์ขํ๊ณ๋ฅผ ์ฌ์ฉํ๋ plot
    - ๊ฑฐ๋ฆฌ(r), ๊ฐ(Theta)๋ฅผ ์ฌ์ฉํ์ฌ ์๊ฐํ
- ํ์ , ์ฃผ๊ธฐ์ฑ์ ํํํ๊ธฐ์ ์ ํฉํ๋ค
- `projection=polar` ์ ์ถ๊ฐํด์ ์ฌ์ฉ๊ฐ๋ฅ
- Scatter, Line, Bar plot์์ ๋ชจ๋ ์ฌ์ฉ ๊ฐ๋ฅ

![image](https://user-images.githubusercontent.com/91870042/153741890-0d0b90ac-ffab-468e-b87c-d8653403f800.png){: .align-center width="70%"}

- Matplotlib ๋ก๊ณ ์์๋ ์ฌ์ฉ
    - ๊ณต์๋ก๊ณ ๋ matplotlib๋ก ๊ทธ๋ฆด์๊ฐ ์๋ค.

## DataConverting

- ๊ผญ ๊ทน์ขํ๊ณ์์ ๊ทธ๋ฆดํ์๋ ์๊ณ , ์ง๊ต์ขํ๊ณ์์๋ ์ฌ์ฉํ  ์ ์๋ค.

![image](https://user-images.githubusercontent.com/91870042/153741893-f6f58b39-e62d-4e1e-b60d-fed00906b829.png){: .align-center width="50%"}

- ์ผ๊ฐํจ์๋ก ์ขํ๋ฅผ ๋ณํํด์ ์ฌ์ฉํ๋ฉด ๋๋ค.

# Radar Plot

## Radar Plot

![image](https://user-images.githubusercontent.com/91870042/153741895-3d1c69e2-72b0-4a73-a043-3727474649b6.png){: .align-center width="70%"}

- ๊ทน์ขํ๊ณ๋ฅผ ์ฌ์ฉํ๋ ๋ํ์ ์ธ ์ฐจํธ
- ๋ณ ๋ชจ์์ผ๋ก ์๊ฒจ์ Star Plot์ผ๋ก ๋ถ๋ฆฌ๊ธฐ๋ ํ๋ค.
- ์ค์ฌ์ ์ ๊ธฐ์ค์ผ๋ก N๊ฐ์ ๋ณ์ ๊ฐ์ ์ด์ด์ ๋ฉด์ ์ผ๋ก ํํํ๋ค.
- ๋ฐ์ดํฐ์ ์ง์ ์ธ ๋ถ๋ถ์ ํํํ๊ธฐ๊ฐ ์ข๋ค.
    - ์บ๋ฆญํฐ์ ๊ฐํจ
    - ์ด๋์ ์ ๋ถ์
    - ๋น๊ต์๋ ์ ํฉ

## Radar Plot ์ฃผ์์ 

- ๊ฐ feature๋ ๋๋ฆฝ์ ์ด๋ฉฐ, ์ฒ๋๊ฐ ๊ฐ์์ผ ํ๋ค.
    - ์์ํ ๋ณ์์ ์์นํ ๋ณ์๊ฐ ํจ๊ป ์๋ค๋ฉด ๊ณ ๋ ค๊ฐ ํ์ํ๋ค.
- ์๋ฅผ ๋ค์ด, ์๋์ฐจ๋ฅผ ๋ณด์.
    - ์์ ์ฑ ํ๊ฐ์ ์๋น์ ๋ง์กฑ๋๋ฑ์ 5์  ๋ง์ ์ผ๋ก ํํ๋๊ณ 
    - ์ต๋ ์๋์ ์ฐ๋น๋ฑ์ 10km/L ์ฒ๋ผ ์ ๋์  ์์น๋ก ๋ํ๋ธ๋ค.
    - ์ด๋ฐ ๊ฒฝ์ฐ, ํ๋์ Radar Plot์ ๋ํ๋ด๋ ๊ฒ์ ์ข์ง ์๋ค.

![image](https://user-images.githubusercontent.com/91870042/153741900-e1333288-c722-4326-aae8-90a4113c5b8f.png){: .align-center width="70%"}

- ๋ฉด์  ์์ฒด๊ฐ ๊ฐ์ง ์๋ฏธ๋ ํฌ์ง๊ฐ ์๋ค.
    - ๋ค๊ฐํ์ ๋ฉด์ ์ด ์ค์ํ์ง๋ง feature์ ์์์ ๋ฐ๋ผ์ ๋ง์ด ๋ฌ๋ผ์ง๊ฒ ๋๋ค.

![image](https://user-images.githubusercontent.com/91870042/153741907-05ff8a61-a7cf-4edb-a171-e2b6695af098.png){: .align-center width="70%"}

- feature์ ์๊ฐ ๋ง์์ง๋ฉด ๊ฐ๋์ฑ์ด ๋จ์ด์ง๋ค.

<br>

# ์ค์ต

```python
fig = plt.figure()
ax = fig.add_subplot(111, projection='polar')
plt.show()
```

![image](https://user-images.githubusercontent.com/91870042/153741910-01ec5142-c30c-42a0-a19a-3e8967063d93.png){: .align-center width="40%"}

- `projection='polar'` ๋์ ์, `polar=True` ๋ฅผ ์ฌ์ฉํ  ์ ์๋ค.

```python
fig = plt.figure()
ax = fig.add_subplot(111, polar=True)
plt.show()
```

- `set_rmax` ,`set_rmin` : ๋ฐ์ง๋ฆ ์กฐ์ 
- `set_rticks` : ๋ฐ์ง๋ฆ ํ๊ธฐ grid์กฐ์ 

```python
fig = plt.figure()
ax = fig.add_subplot(111, polar=True)

ax.set_rmax(2)
# ax.set_rmin(1)
ax.set_rticks([1, 1.5, 2])  

plt.show()
```

![image](https://user-images.githubusercontent.com/91870042/153741914-de0f6d13-f7ed-44ab-b9d5-20f704ac8a98.png){: width="49%"} ![image](https://user-images.githubusercontent.com/91870042/153741917-8cffab04-2d06-418c-96f9-2e58848dcd6c.png){: width="49%"}

- `set_rmin` ์ ํ๋ค๊ณ  ํ๋๋ผ๋ ๋๋๊ณผ ๊ฐ์ ํํ๊ฐ ๋๋ ๊ฒ์ด ์๋๋ผ, ์์์ ์ ๊ธฐ์ค์ด ๋ฐ๋๋ ๊ฒ์ด๋ค.
- `set_rlabel_position` : ๋ฐ์ง๋ฆ label์ด ์ ํ๋ ์์น์ ๊ฐ๋๋ฅผ ์กฐ์ ํ๋ค.

```python
fig = plt.figure()
ax = fig.add_subplot(111, polar=True)
ax.set_rlabel_position(-90)  
plt.show()
```

![image](https://user-images.githubusercontent.com/91870042/153741924-c8d731f3-0106-4c2f-8832-793719f9b867.png){: .align-center width="40%"}

- ๊ฐ๋๋ฅผ ์กฐ์ ํ์ฌ ๋ถ์ฑ๊ผด์ ๋ชจ์๋ง ๋ํ๋ด๊ณ  ์ถ์ ๊ฒฝ์ฐ,
    - `set_thetamin` : ๊ฐ๋์ min๊ฐ
    - `set_thetamax` : ๊ฐ๋์ max๊ฐ

```python
fig = plt.figure()
ax = fig.add_subplot(111, polar=True)

ax.set_thetamin(45)
ax.set_thetamax(135)
plt.show()
```

![image](https://user-images.githubusercontent.com/91870042/153741928-4e99907c-4f92-49e3-ba68-ebf881abf574.png){: .align-center width="40%"}

- scatter plot์์ ์ฌ์ฉํ๋ polar plot

```python
np.random.seed(19680801)

N = 100
r = 2 * np.random.rand(N)
theta = 2 * np.pi * np.random.rand(N)
area = 200 * r**2
colors = theta

fig = plt.figure()
ax = fig.add_subplot(111, projection='polar')
c = ax.scatter(theta, r, c=colors, s=area, cmap='hsv', alpha=0.75)
plt.show()
```

![image](https://user-images.githubusercontent.com/91870042/153741932-7e7a968b-7542-41f8-9a86-9726fce0b87d.png){: .align-center width="40%"}

- bar plot์์ ์ฌ์ฉํ๋ polar plot
- 2 ๊ฐ์ ๋ถํฌ๊ฐ ์ผ๋ง๋ ์ฐจ์ด๋๋์ง ์์๋ณด๊ธฐ๋ ํ๋ค๊ธฐ ๋๋ฌธ์ ์ฃผ์ํด์ ์ฌ์ฉํ๋ ๊ฒ์ด ์ข๋ค.

```python
np.random.seed(19680801)

N = 6
r = np.random.rand(N)
theta = np.linspace(0, 2*np.pi, N, endpoint=False)

fig = plt.figure()
ax = fig.add_subplot(111, projection='polar')
ax.bar(theta, r, width=0.5, alpha=0.5)
plt.show()
```

![image](https://user-images.githubusercontent.com/91870042/153741945-f4b0fc49-8b81-4945-a902-3a0efeb9b631.png){: .align-center width="40%"}

- plot (์ ๊ทธ๋ํ)๋ฅผ polar plot์ ๊ทธ๋ฆฌ๊ธฐ

```python
np.random.seed(19680801)

N = 1000
r = np.linspace(0, 1, N)
theta = np.linspace(0, 2*np.pi, N)

fig = plt.figure()
ax = fig.add_subplot(111, projection='polar')
ax.plot(theta, r)

plt.show()
```

![image](https://user-images.githubusercontent.com/91870042/153741946-1ceb49f2-2807-456e-b2a1-defb763b13a4.png){: .align-center width="40%"}

- `fill` ์ ์ฌ์ฉํด์ area chart ํํํ๊ธฐ

```python
np.random.seed(19680801)

N = 1000
r = np.linspace(0, 1, N)
theta = np.linspace(0, 2*np.pi, N)

fig = plt.figure()
ax = fig.add_subplot(111, projection='polar')
ax.fill(theta, r) # <-- ์ด๋ถ๋ถ ์ถ๊ฐ
plt.show()
```

![image](https://user-images.githubusercontent.com/91870042/153741953-2472c819-30cf-4104-8893-ed32c52bc401.png){: .align-center width="40%"}

- ๋ฐฉ๊ธ ์ฌ์ฉํ, `fill` ์ ์ ํฉํ๊ฒ ์ฌ์ฉํ๋ฉด Radar Chart๋ฅผ ์ฌ์ฉํ  ์ ์๋ค.
- ์ค์ต์์๋ Pockemon with stat ๋ฐ์ดํฐ์์ ์ฌ์ฉํ๋ค.

```python
pokemon = pd.read_csv('./pokemon.csv')
pokemon.head()
```

![image](https://user-images.githubusercontent.com/91870042/153741962-dc0373f8-46ed-4cbf-a1c6-916db25bc66e.png){: .align-center width="70%"}

- ํฌ์ผ๋ชฌ์ ๋ฐ์ดํฐ ํต๊ณ ์ดํด๋ณด๊ธฐ

```python
pokemon.describe()
```

![image](https://user-images.githubusercontent.com/91870042/153741971-26678e3e-dedd-4908-9b4e-860e967fed83.png){: .align-center width="70%"}

- ๋ฐ์ดํฐ์์ ์์ธํ ๋ณด๋ฉด, **HP, Attack, Defense, Sp.Atk, Sp.Def, Speed** ์ด 6๊ฐ์ง feature๊ฐ ํฌ์ผ๋ชฌ์ ์ญ๋์ ๋ํ๋ด๋ ์์น์ด๋ค.
- ์ด 6๊ฐ์ feature์ ๋ํ RadarChar๋ฅผ ๊ทธ๋ ค๋ณด์
- ๋จผ์ , ํด๋นํ๋ feature์ ๋ํ ๊ฐ๋ง ์ถ์ถํด ์์ผํ๋ค.

```python
stats = ["HP", "Attack", "Defense", "Sp. Atk", "Sp. Def", "Speed"]
values = pokemon.iloc[0][stats].to_list()
print(values)
-----------------------------------------------------
[45, 49, 49, 65, 65, 45]
```

- ๊ฐ์ ๋ํ๋ด๊ธฐ ์ํด์ ์ ์ฒด $`2\pi`$ ๋ฅผ 6๋ฑ๋ถํ๋ค.

```python
theta = np.linspace(0, 2*np.pi, 6, endpoint=False)
print(theta)
```

- ์ด์ , `fill` ๊ณผ `plot` ์ ์ฌ์ฉํด์ ๊ทธ๋ ค๋ณผ ์ ์๋ค.

```python
fig = plt.figure()
ax = fig.add_subplot(111, projection='polar')

ax.plot(theta, values)
ax.fill(theta, values, alpha=0.5)
plt.show()
```

![image](https://user-images.githubusercontent.com/91870042/153741976-5a9c3074-7aba-4cda-a2f8-73ab99ca86fd.png){: .align-center width="40%"}

- ์์์ ๋ณด๋ฉด ๊ฒฐ๊ณผ๋ฌผ์ ํ๋๋ฆฌ๊ฐ ๋ง์ง๋ง์ด ๋น์ด์๋ ๊ฒ์ ์ ์ ์๋ค.
- ์ด๋ฅผ ํด๊ฒฐํ๊ธฐ ์ํด์ ๊ฐ๋ list์ ๋ฐ์ดํฐ list๋ง์ง๋ง์ ์ฒซ๋ฒ์งธ ๊ฐ์ ๊ฐ๊ฐ ์ถ๊ฐํด์ค๋ค.

```python
fig = plt.figure()
ax = fig.add_subplot(111, projection='polar')

values.append(values[0]) # <--- ์ฒซ๋ฒ์งธ ๋ฐ์ดํฐ๋ฅผ ์ถ๊ฐ
theta = theta.tolist() + [theta[0]] # <--- ์ฒซ๋ฒ์งธ ๊ฐ๋๋ฅผ ์ถ๊ฐ

ax.plot(theta, values)
ax.fill(theta, values, alpha=0.5)

plt.show()
```

![image](https://user-images.githubusercontent.com/91870042/153741980-111208a1-25d2-40b0-8ce1-a9d8b7adbae2.png){: .align-center width="40%"}

- ์์์ ๊ฐ feature๊ฐ ๋ฌด์์ ๋ํ๋ด๋์ง ๋ชจ๋ฅด๊ณ , ๊ฐ feature๊ฐ์ ๋ฐฐ๊ฒฝ์ ์ ๋ง์ถฐ์ฃผ๊ธฐ ์ํด์ ๋ค์ 2๊ฐ์ง ๋ฉ์๋๋ฅผ ์ฌ์ฉํด๋ณผ ์ ์๋ค.
    - `set_thetagrids` : ๊ฐ๋์ ๋ฐ๋ฅธ ๊ทธ๋ฆฌ๋ ๋ฐ ticklabels ๋ณ๊ฒฝ
    - `set_theta_offset` : ์์ํ๋ ๊ฐ๋๋ฅผ ๋ณ๊ฒฝ

```python
fig = plt.figure(figsize=(4, 4))
ax = fig.add_subplot(111, projection='polar')

values = pokemon.iloc[0][stats].to_list()
values.append(values[0])

ax.plot(theta, values)
ax.fill(theta, values, alpha=0.5)

ax.set_thetagrids([n*60 for n in range(6)], stats) # <-- ๊ทธ๋ฆฌ๋ ๋ณ๊ฒฝ, label์ค์ 
ax.set_theta_offset(np.pi/2) # <-- ์์๊ฐ๋ ๋ณ๊ฒฝ

plt.show()
```

![image](https://user-images.githubusercontent.com/91870042/153741983-256ddfe1-67cf-4668-88d5-5f6c19ee7f07.png){: .align-center width="40%"}

- ํฌ์ผ๋ชฌ์ ์งํ์ ๋ฐ๋ฅธ ๋ฅ๋ ฅ ๋ณํ ์ดํด๋ณด๊ธฐ

```python
fig = plt.figure(figsize=(14, 4))

for idx in range(3):
    ax = fig.add_subplot(1,3,idx+1, projection='polar')

    values = pokemon.iloc[idx][stats].to_list()
    values.append(values[0])

    ax.plot(theta, values, color='forestgreen')
    ax.fill(theta, values, color='forestgreen', alpha=0.3)
    
    ax.set_rmax(100)
    ax.set_thetagrids([n*60 for n in range(6)], stats)
    ax.set_theta_offset(np.pi/2)
    
plt.show()
```

![image](https://user-images.githubusercontent.com/91870042/153741990-ecef9999-0444-4b87-80e6-6a5d01fea3af.png){: .align-center width="70%"}

```python
fig = plt.figure(figsize=(7, 7))

ax = fig.add_subplot(111, projection='polar')

for idx in range(3):

    values = pokemon.iloc[idx][stats].to_list()
    values.append(values[0])

    ax.plot(theta, values, color='forestgreen')
    ax.fill(theta, values, color='forestgreen', alpha=0.3)
    
ax.set_rmax(110)
ax.set_thetagrids([n*60 for n in range(6)], stats)
ax.set_theta_offset(np.pi/2)
    
plt.show()
```

![image](https://user-images.githubusercontent.com/91870042/153741996-25a0c3a0-de7e-41d1-af17-cbe7bd3c7a45.png){: .align-center width="40%"}