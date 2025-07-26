
---

## 📊 **Categorical Plots (`seaborn.catplot`)**

These are for visualizing data with categorical variables:

* `sns.catplot()` – General interface for categorical plots
* `sns.stripplot()` – Scatterplot with a categorical axis
* `sns.swarmplot()` – Non-overlapping categorical scatterplot
* `sns.boxplot()` – Box-and-whisker plot
* `sns.violinplot()` – KDE + boxplot combo
* `sns.boxenplot()` – Better boxplot for large data
* `sns.pointplot()` – Shows mean and CI over categories
* `sns.barplot()` – Bar chart showing mean and CI
* `sns.countplot()` – Bar chart showing counts of observations


---

## 📊 **Categorical Plots – ক্যাটাগরিকাল ভেরিয়েবল বিশ্লেষণের জন্য**

ধরো তোমার কাছে একটা রেস্টুরেন্টের ডেটাসেট আছে যেখানে সপ্তাহের দিন অনুযায়ী কাস্টমারদের বিলের পরিমাণ (total\_bill) আছে। এখন তুমি জানতে চাও কোন দিনে গড় বিল বেশি ছিল, বা কোন দিনে outlier ছিল কিনা — তখন এই প্লটগুলো খুব উপকারী।

আমরা `tips` নামের Seaborn-এর ইন-বিল্ট ডেটাসেট ব্যবহার করবো।

```python
import seaborn as sns
import matplotlib.pyplot as plt
tips = sns.load_dataset("tips")
```

---

### 1. 🟣 `catplot()`

**কাজ:** এটি একটি general প্লট ফাংশন। `kind` দিয়ে তুমি ঠিক করো কোন টাইপের ক্যাটাগরিকাল প্লট বানাবে (box, violin, bar ইত্যাদি)।

**কখন ব্যবহার করবো:** যখন একই ধরণের প্লট বারবার করতে চাও বিভিন্ন ক্যাটাগরির উপর faceting সহ।

```python
sns.catplot(data=tips, x="day", y="total_bill", kind="box")
plt.show()
```

**ব্যবহারিক পরিস্থিতি:**
👉 তুমি দেখতে চাও সপ্তাহের কোন দিনে বিলের বৈচিত্র্য (variation) সবচেয়ে বেশি।

---

### 2. 🔵 `stripplot()`

**কাজ:** প্রতিটি ডেটা পয়েন্ট আলাদাভাবে দেখায় (scatter), ক্যাটাগরিকাল এক্স-অ্যাক্সিসে। জিটার দিলে একে অপরের ওপর না পড়ে।

```python
sns.stripplot(data=tips, x="day", y="total_bill", jitter=True)
plt.show()
```

**ব্যবহারিক পরিস্থিতি:**
👉 যখন ডেটা ছোট এবং তুমি প্রত্যেকটা রেকর্ড আলাদাভাবে দেখতে চাও।

---

### 3. 🟠 `swarmplot()`

**কাজ:** `stripplot` এর মতো, কিন্তু এটি ডেটা পয়েন্টগুলোকে overlap না করে এমনভাবে সাজায়।

```python
sns.swarmplot(data=tips, x="day", y="total_bill")
plt.show()
```

**ব্যবহারিক পরিস্থিতি:**
👉 যদি ডেটা বেশি হয় কিন্তু তবুও প্রত্যেকটা পয়েন্ট দেখতে চাও (jitter না দিয়ে)।

---

### 4. 🟡 `boxplot()`

**কাজ:** মিনিমাম, ম্যাক্সিমাম, মিডিয়ান এবং quartile দেখায় (5-number summary)। Outlier আলাদা করে চিহ্নিত করে।

```python
sns.boxplot(data=tips, x="day", y="total_bill")
plt.show()
```

**ব্যবহারিক পরিস্থিতি:**
👉 দেখতে চাও কোন দিনে খুব বেশি বিল (outlier) ছিল।

---

### 5. 🟢 `violinplot()`

**কাজ:** `boxplot` এর সাথে KDE যোগ করে। এটি ডিস্ট্রিবিউশনের আকারও দেখায়।

```python
sns.violinplot(data=tips, x="day", y="total_bill")
plt.show()
```

**ব্যবহারিক পরিস্থিতি:**
👉 দেখতে চাও ডেটা কেমনভাবে ছড়িয়ে আছে এবং তা কোন দিকে বেশি ঝুঁকে (skewed) আছে কি না।

---

### 6. 🔴 `boxenplot()`

**কাজ:** `boxplot` এর মতো, কিন্তু বড় ডেটাসেটের জন্য ভালো। এটি বেশি quantile দেখায়।

```python
sns.boxenplot(data=tips, x="day", y="total_bill")
plt.show()
```

**ব্যবহারিক পরিস্থিতি:**
👉 যখন তোমার ডেটা অনেক বড় এবং ডিস্ট্রিবিউশন অনেক খুঁটিনাটি জানতে চাও।

---

### 7. 🟤 `pointplot()`

**কাজ:** প্রতিটি ক্যাটাগরির জন্য গড় (mean) দেখায়, সাথে কনফিডেন্স ইন্টারভাল।

```python
sns.pointplot(data=tips, x="day", y="total_bill", capsize=0.2)
plt.show()
```

**ব্যবহারিক পরিস্থিতি:**
👉 তুলনা করতে চাও কোন দিনে গড় বিল বেশি ছিল এবং তার উপর কতটা ভ্যারিয়েশন ছিল।

---

### 8. 🟣 `barplot()`

**কাজ:** `pointplot` এর মতো, কিন্তু বার আকারে দেখায়। গড় এবং ভ্যারিয়েশন বোঝায়।

```python
sns.barplot(data=tips, x="day", y="total_bill", ci="sd")
plt.show()
```

**ব্যবহারিক পরিস্থিতি:**
👉 রিপোর্ট বা প্রেসেন্টেশনের জন্য গড় ভ্যালু দেখানোর সেরা উপায়।

---

### 9. ⚫ `countplot()`

**কাজ:** প্রতিটি ক্যাটাগরিতে কতগুলো রেকর্ড আছে (count) তা দেখায়।

```python
sns.countplot(data=tips, x="day")
plt.show()
```

**ব্যবহারিক পরিস্থিতি:**
👉 দেখতে চাও কোন দিনে কাস্টমারের সংখ্যা বেশি ছিল।

---

## ✅ সারাংশ টেবিল (বাংলায়)

| ফাংশন          | কী দেখায়                                 | কখন ব্যবহার করবো                   |
| -------------- | ----------------------------------------- | ---------------------------------- |
| `catplot()`    | যেকোনো ক্যাটাগরিকাল প্লট এক ফ্রেমওয়ার্কে | ফেসেট বা সাবপ্লট দরকার হলে         |
| `stripplot()`  | প্রতিটি রেকর্ড একেকটা পয়েন্ট             | ছোট ডেটা ও বৈচিত্র্য দেখতে         |
| `swarmplot()`  | পয়েন্টগুলো overlap ছাড়া                 | ডেটা বেশি হলেও পয়েন্ট আলাদা রাখতে |
| `boxplot()`    | মিন, ম্যাক্স, মিডিয়ান সহ আউটলাইয়ার       | গড় ছাড়াও বিস্তারিত জানতে           |
| `violinplot()` | KDE + boxplot (ডিস্ট্রিবিউশনের আকার)      | ডেটার ছড়ানো দেখাতে                |
| `boxenplot()`  | অনেক কুয়ানটাইল (বড় ডেটা)                | ডেটা বড় হলে                       |
| `pointplot()`  | গড় এবং তার উপরে ভরসার সীমা                | দুই ক্যাটাগরি তুলনায়              |
| `barplot()`    | গড় মান বার আকারে                          | রিপোর্ট বা উপস্থাপনার জন্য         |
| `countplot()`  | কতবার ঘটেছে (ফ্রিকোয়েন্সি)               | দেখা কোন ক্যাটাগরি বেশি            |



## 🔍 `sns.catplot()`

```python
sns.catplot(data=tips, x="day", y="total_bill", kind="box", hue="sex", col="time")
```

### 📌 গুরুত্বপূর্ণ প্যারামিটার:

| Parameter    | মান (উদাহরণ)                                    | কাজ                          |
| ------------ | ----------------------------------------------- | ---------------------------- |
| `data`       | `DataFrame`                                     | কোন ডেটা ব্যবহার করবে        |
| `x`, `y`     | কলাম নাম                                        | কোন ভেরিয়েবল প্লটে থাকবে    |
| `kind`       | `'box'`, `'bar'`, `'violin'`, `'strip'` ইত্যাদি | কোন টাইপের ক্যাটাগরিকাল প্লট |
| `hue`        | `'sex'`, `'smoker'` ইত্যাদি                     | আলাদা গ্রুপ রঙে আলাদা করে    |
| `col`, `row` | ফিচার নাম                                       | subplot বানাতে               |
| `order`      | list (e.g., `['Thur', 'Fri', 'Sat', 'Sun']`)    | ক্যাটাগরি কীভাবে সাজাবে      |
| `height`     | সংখ্যা (e.g., 4)                                | subplot-এর উচ্চতা            |
| `aspect`     | সংখ্যা (e.g., 1)                                | চওড়া-উচ্চতার অনুপাত         |

---

## 🔵 `sns.stripplot()`

```python
sns.stripplot(data=tips, x="day", y="total_bill", jitter=True, hue="sex", dodge=True)
```

### 📌 প্যারামিটার:

| Parameter | মান                          | কাজ                            |
| --------- | ---------------------------- | ------------------------------ |
| `jitter`  | True/False                   | পয়েন্টগুলো overlap না করতে    |
| `dodge`   | True/False                   | hue ভিত্তিক আলাদা কলামে দেখাতে |
| `hue`     | ক্যাটাগরিকাল ভেরিয়েবল        | গ্রুপ অনুযায়ী আলাদা রঙ         |
| `palette` | palette নাম (e.g., `'Set2'`) | কালার সেট                      |
| `alpha`   | 0 থেকে 1                     | ট্রান্সপারেন্সি নিয়ন্ত্রণ      |
| `size`    | সংখ্যা                       | পয়েন্টের সাইজ                 |

---

## 🟠 `sns.swarmplot()`

```python
sns.swarmplot(data=tips, x="day", y="total_bill", hue="sex")
```

### 📌 প্যারামিটার:

| Parameter | কাজ                              |
| --------- | -------------------------------- |
| `dodge`   | hue-এর জন্য পয়েন্ট সরিয়ে সাজায় |
| `hue`     | ক্যাটাগরির ভিত্তিতে আলাদা        |
| `size`    | পয়েন্টের সাইজ                   |

⚠️ **বি.দ্র:** বড় ডেটার জন্য `swarmplot()` ধীর হতে পারে।

---

## 🟡 `sns.boxplot()`

```python
sns.boxplot(data=tips, x="day", y="total_bill", hue="sex")
```

### 📌 প্যারামিটার:

| Parameter   | কাজ                                |
| ----------- | ---------------------------------- |
| `notch`     | মিডিয়ান-এর কাছাকাছি ব্যবধান ছোটায় |
| `width`     | বক্সের চওড়া নিয়ন্ত্রণ করে         |
| `showmeans` | গড় মান দেখায়                       |
| `hue`       | গ্রুপিং করে বক্সপ্লট               |

---

## 🟢 `sns.violinplot()`

```python
sns.violinplot(data=tips, x="day", y="total_bill", hue="sex", split=True)
```

### 📌 প্যারামিটার:

| Parameter           | কাজ                                                        |
| ------------------- | ---------------------------------------------------------- |
| `inner`             | `'box'`, `'point'`, `'stick'`, `None` – ভিতরের স্ট্যাটস    |
| `split`             | True হলে hue অনুযায়ী একসাথে দেখায়                         |
| `scale`             | `'area'`, `'count'`, `'width'` – চওড়া কীভাবে নির্ধারণ হবে |
| `bw` or `bw_method` | bandwidth control (KDE smoothness)                         |

---

## 🔴 `sns.boxenplot()`

```python
sns.boxenplot(data=tips, x="day", y="total_bill", hue="sex")
```

### 📌 প্যারামিটার:

| Parameter      | কাজ                                             |
| -------------- | ----------------------------------------------- |
| `k_depth`      | কতটা deep quantiles দেখাবে (e.g., `'profound'`) |
| `outlier_prop` | outlier বাদ দেওয়ার অনুপাত                       |
| `hue`          | আলাদা রঙে গ্রুপ দেখাতে                          |

---

## 🟤 `sns.pointplot()`

```python
sns.pointplot(data=tips, x="day", y="total_bill", hue="sex", capsize=0.2)
```

### 📌 প্যারামিটার:

| Parameter   | কাজ                                     |
| ----------- | --------------------------------------- |
| `estimator` | গড় ছাড়া অন্য কিছু যেমন `np.median`     |
| `ci`        | confidence interval (default 95)        |
| `capsize`   | বারগুলোর শেষে cap দেখাতে                |
| `join`      | পয়েন্ট গুলোকে লাইনে জোড়া (True/False) |

---

## 🟣 `sns.barplot()`

```python
sns.barplot(data=tips, x="day", y="total_bill", hue="sex", ci="sd")
```

### 📌 প্যারামিটার:

| Parameter   | কাজ                                  |
| ----------- | ------------------------------------ |
| `estimator` | গড় বাদে অন্য কিছু হিসেব করতে         |
| `ci`        | `"sd"` দিলে standard deviation দেখায় |
| `errwidth`  | error bar-এর প্রস্থ                  |
| `capsize`   | error bar cap-এর সাইজ                |

---

## ⚫ `sns.countplot()`

```python
sns.countplot(data=tips, x="day", hue="sex")
```

### 📌 প্যারামিটার:

| Parameter | কাজ                                |
| --------- | ---------------------------------- |
| `hue`     | ক্যাটাগরি অনুযায়ী count আলাদা করে |
| `order`   | ক্যাটাগরি কীভাবে সাজানো হবে        |
| `palette` | রঙের সেট                           |

---

## ✅ সারাংশ (Parameter Reference)

| Function       | Key Parameters                                           |
| -------------- | -------------------------------------------------------- |
| `catplot()`    | `kind`, `hue`, `col`, `row`, `order`, `height`, `aspect` |
| `stripplot()`  | `jitter`, `dodge`, `hue`, `palette`, `size`, `alpha`     |
| `swarmplot()`  | `hue`, `dodge`, `size`                                   |
| `boxplot()`    | `notch`, `showmeans`, `width`, `hue`                     |
| `violinplot()` | `inner`, `split`, `scale`, `bw`                          |
| `boxenplot()`  | `k_depth`, `outlier_prop`, `hue`                         |
| `pointplot()`  | `estimator`, `ci`, `capsize`, `join`, `hue`              |
| `barplot()`    | `estimator`, `ci`, `errwidth`, `capsize`, `hue`          |
| `countplot()`  | `hue`, `order`, `palette`                                |

---


import seaborn as sns
import matplotlib.pyplot as plt
import streamlit as st

# Load dataset
tips = sns.load_dataset("tips")

st.title("📊 Seaborn Categorical and Distribution Plots Dashboard")
st.write("Visualize both categorical and distribution plots using the 'tips' dataset.")

# ---------------- Distribution Plots ----------------
st.header("📈 Distribution Plots")

# 1. displot (Histogram)
fig1 = sns.displot(data=tips, x="total_bill", kind="hist", bins=20)
st.pyplot(fig1)

# 2. displot (KDE)
fig2 = sns.displot(data=tips, x="total_bill", kind="kde", fill=True)
st.pyplot(fig2)

# 3. displot (ECDF)
fig3 = sns.displot(data=tips, x="total_bill", kind="ecdf")
st.pyplot(fig3)

# 4. histplot
fig4, ax4 = plt.subplots()
sns.histplot(data=tips, x="total_bill", bins=20, kde=True, ax=ax4)
st.pyplot(fig4)

# 5. kdeplot
fig5, ax5 = plt.subplots()
sns.kdeplot(data=tips, x="total_bill", fill=True, ax=ax5)
st.pyplot(fig5)

# 6. ecdfplot
fig6, ax6 = plt.subplots()
sns.ecdfplot(data=tips, x="total_bill", ax=ax6)
st.pyplot(fig6)

# 7. rugplot
fig7, ax7 = plt.subplots()
sns.rugplot(data=tips, x="total_bill", ax=ax7)
st.pyplot(fig7)

# 8. violinplot (used here in distribution context)
fig8, ax8 = plt.subplots()
sns.violinplot(data=tips, x="day", y="total_bill", ax=ax8)
st.pyplot(fig8)

# 9. distplot (Deprecated)
fig9, ax9 = plt.subplots()
sns.distplot(tips['total_bill'], bins=20, kde=True, ax=ax9)
st.pyplot(fig9)

# ---------------- Categorical Plots ----------------
st.header("📊 Categorical Plots")

# 1. catplot - general interface (boxplot kind)
# বিভিন্ন ক্যাটাগরি অনুসারে boxplot তৈরি করে
fig10 = sns.catplot(data=tips, x="day", y="total_bill", kind="box")
st.pyplot(fig10)

# 2. stripplot - প্রতিটি ডেটা পয়েন্ট দেখায় jitter সহ
fig11, ax11 = plt.subplots()
sns.stripplot(data=tips, x="day", y="total_bill", jitter=True, ax=ax11)
st.pyplot(fig11)

# 3. swarmplot - stripplot এর মতো কিন্তু overlap ছাড়াই সাজায়
fig12, ax12 = plt.subplots()
sns.swarmplot(data=tips, x="day", y="total_bill", ax=ax12)
st.pyplot(fig12)

# 4. boxplot - পাঁচটি পরিসংখ্যান মান (min, Q1, median, Q3, max)
fig13, ax13 = plt.subplots()
sns.boxplot(data=tips, x="day", y="total_bill", ax=ax13)
st.pyplot(fig13)

# 5. violinplot - boxplot + KDE, distribution ও statistics একসাথে
fig14, ax14 = plt.subplots()
sns.violinplot(data=tips, x="day", y="total_bill", ax=ax14)
st.pyplot(fig14)

# 6. boxenplot - বড় ডেটার distribution দেখানোর জন্য উপযুক্ত
fig15, ax15 = plt.subplots()
sns.boxenplot(data=tips, x="day", y="total_bill", ax=ax15)
st.pyplot(fig15)

# 7. pointplot - প্রতিটি ক্যাটাগরির mean ও CI দেখায়
fig16, ax16 = plt.subplots()
sns.pointplot(data=tips, x="day", y="total_bill", capsize=0.2, ax=ax16)
st.pyplot(fig16)

# 8. barplot - bar আকারে mean ও confidence interval দেখায়
fig17, ax17 = plt.subplots()
sns.barplot(data=tips, x="day", y="total_bill", ci="sd", ax=ax17)
st.pyplot(fig17)

# 9. countplot - প্রতিটি ক্যাটাগরির ডেটা পয়েন্টের সংখ্যা দেখায়
fig18, ax18 = plt.subplots()
sns.countplot(data=tips, x="day", ax=ax18)
st.pyplot(fig18)






## 📈 **Distribution Plots**

* `sns.displot()` – Histogram, KDE, ECDF, and rug in one interface
* `sns.histplot()` – Histogram plot
* `sns.kdeplot()` – Kernel density estimate plot
* `sns.ecdfplot()` – Empirical cumulative distribution function
* `sns.rugplot()` – Marginal tick marks
* `sns.violinplot()` – Also visualizes distributions with stats
* `sns.distplot()` – **Deprecated** since 0.11 (use `displot()` instead)

---


---

## 📈 **Distribution Plots – ডেটার ছড়ানো ও গঠন দেখাতে ব্যবহার হয়**

ডিস্ট্রিবিউশন প্লট দিয়ে মূলত **ডেটা কিভাবে ছড়ানো আছে**, সেটা দেখা হয়। নিচে প্রতিটি ফাংশন আলোচনা করা হলো।

---

### 🔹 1. `sns.displot()`

✅ **কাজ:**
Figure-level interface যা একসাথে Histogram, KDE, ECDF, rug—all-in-one দেয়।

✅ **ব্যবহার:**
যখন বিভিন্ন ধরণের distribution plot চাই একসাথে বা সাবপ্লট সহ।

✅ **সিনট্যাক্স:**

```python
sns.displot(data=tips, x="total_bill", kind="hist", bins=20)
sns.displot(data=tips, x="total_bill", kind="kde", fill=True)
sns.displot(data=tips, x="total_bill", kind="ecdf")
```

✅ **মুখ্য প্যারামিটার:**

| Parameter    | কাজ                                |
| ------------ | ---------------------------------- |
| `data`       | ডেটাসেট                            |
| `x`, `y`     | কোন কলামের উপর ভিত্তি করে প্লট হবে |
| `kind`       | `hist`, `kde`, `ecdf`, `rug`       |
| `bins`       | histogram-এর জন্য bin সংখ্যা       |
| `col`, `row` | faceting - subplot এ ভাগ করতে      |
| `hue`        | গ্রুপভেদে কালার আলাদা করতে         |

---

### 🔹 2. `sns.histplot()`

✅ **কাজ:**
Histogram — data কে bins এ ভাগ করে কতবার ঘটেছে দেখায়।

✅ **ব্যবহার:**
Numeric ডেটা কতোটা কোথায় বেশি/কম আছে দেখতে চাইলে।

✅ **সিনট্যাক্স:**

```python
sns.histplot(data=tips, x="total_bill", bins=20, kde=True)
```

✅ **মুখ্য প্যারামিটার:**

| Parameter  | কাজ                              |
| ---------- | -------------------------------- |
| `bins`     | কতটা range ভাগ করা হবে           |
| `kde=True` | KDE যোগ করতে                     |
| `color`    | বারগুলোর রঙ পরিবর্তন করতে        |
| `multiple` | `stack`, `dodge`, `fill` ইত্যাদি |

---

### 🔹 3. `sns.kdeplot()`

✅ **কাজ:**
Kernel Density Estimate — একটি smooth curve যা দেখায় ডেটার সম্ভাব্য distribution।

✅ **ব্যবহার:**
ডেটা কোথায় most dense (গুচ্ছাকারে) সেটা বুঝতে।

✅ **সিনট্যাক্স:**

```python
sns.kdeplot(data=tips, x="total_bill", fill=True)
```

✅ **মুখ্য প্যারামিটার:**

| Parameter   | কাজ                                         |
| ----------- | ------------------------------------------- |
| `bw_adjust` | bandwidth নিয়ন্ত্রণ করে — বেশি মান = smooth |
| `fill=True` | নিচের অংশ রঙ করে                            |
| `hue`       | আলাদা গ্রুপ রঙে আলাদা                       |

---

### 🔹 4. `sns.ecdfplot()`

✅ **কাজ:**
Empirical Cumulative Distribution Function — cumulative probability কেমন সেটা দেখায়।

✅ **ব্যবহার:**
যেমন: কত শতাংশ গ্রাহকের বিল ২০ ডলারের কম — সেটা জানতে।

✅ **সিনট্যাক্স:**

```python
sns.ecdfplot(data=tips, x="total_bill")
```

✅ **মুখ্য প্যারামিটার:**

| Parameter    | কাজ                  |
| ------------ | -------------------- |
| `hue`        | আলাদা গ্রুপ দেখাতে   |
| `complement` | 1 − CDF দেখাতে চাইলে |

---

### 🔹 5. `sns.rugplot()`

✅ **কাজ:**
ডেটা পয়েন্ট কোথায় কোথায় আছে, তা মার্কার (tick) দিয়ে দেখায়।

✅ **ব্যবহার:**
KDE বা Histogram এর নিচে মার্জিনাল পয়েন্ট দেখানোর জন্য।

✅ **সিনট্যাক্স:**

```python
sns.rugplot(data=tips, x="total_bill")
```

✅ **মুখ্য প্যারামিটার:**

| Parameter | কাজ                              |
| --------- | -------------------------------- |
| `height`  | টিক মার্কের উচ্চতা নিয়ন্ত্রণ করে |
| `hue`     | গ্রুপভেদে আলাদা কালার            |

---

### 🔹 6. `sns.violinplot()` (উভয় Distribution ও Categorical ফাংশনে পড়ে)

✅ **কাজ:**
একটি ক্যাটাগরির distribution কেমন সেটার আকার দেখায় (KDE+Box)।

✅ **ব্যবহার:**
যখন distribution ও summary statistics (mean, median) একসাথে দরকার।

✅ **সিনট্যাক্স:**

```python
sns.violinplot(data=tips, x="day", y="total_bill")
```

✅ **মুখ্য প্যারামিটার:**

| Parameter    | কাজ                          |
| ------------ | ---------------------------- |
| `inner`      | `"box"` দিলে boxplot সহ আসে  |
| `split=True` | দুই গ্রুপ এক violin-এ দেখাতে |

---

### 🔹 7. `sns.distplot()` (**Deprecated**)

❌ এটি পুরনো ভার্সনে ছিল। এখন `displot()` বা `histplot()` দিয়ে সব কিছু করা যায়। তবে যদি পুরনো কোড দেখো:

```python
sns.distplot(tips['total_bill'], bins=20, kde=True)
```

---

## ✅ কোন ফাংশন কবে ব্যবহার করবো?

| ফাংশন          | কবে ব্যবহার করবো                       |
| -------------- | -------------------------------------- |
| `displot()`    | একাধিক টাইপের প্লট, subplot দরকার হলে  |
| `histplot()`   | কেবল histogram দরকার হলে               |
| `kdeplot()`    | smooth density curve দরকার হলে         |
| `ecdfplot()`   | cumulative distribution দরকার হলে      |
| `rugplot()`    | নিচে tick দিয়ে পয়েন্টের অবস্থান দেখাতে |
| `violinplot()` | distribution + stats দেখতে হলে         |
| `distplot()`   | ❌ পুরনো, এখন আর ব্যবহার না করাই ভালো   |

---
import seaborn as sns
import matplotlib.pyplot as plt
import streamlit as st

# Load dataset
tips = sns.load_dataset("tips")

st.title("📊 Seaborn Categorical and Distribution Plots Dashboard")
st.write("Visualize both categorical and distribution plots using the 'tips' dataset.")

# ---------------- Distribution Plots with Comments ----------------
st.header("📈 Distribution Plots with Detailed Comments")

# displot() - Histogram
# 👉 ডেটার ফ্রিকোয়েন্সি দেখতে bin ভাগ করে histogram দেখায়
fig1 = sns.displot(data=tips, x="total_bill", kind="hist", bins=20)
st.pyplot(fig1)

# displot() - KDE
# 👉 histogram-এর পরিবর্তে smooth distribution curve দেখায়
fig2 = sns.displot(data=tips, x="total_bill", kind="kde", fill=True)
st.pyplot(fig2)

# displot() - ECDF
# 👉 cumulative distribution function দেখায়
fig3 = sns.displot(data=tips, x="total_bill", kind="ecdf")
st.pyplot(fig3)

# histplot()
# 👉 শুধুমাত্র histogram দেখানোর জন্য, optionally kde যোগ করা যায়
fig4, ax4 = plt.subplots()
sns.histplot(data=tips, x="total_bill", bins=20, kde=True, ax=ax4)
st.pyplot(fig4)

# kdeplot()
# 👉 kernel density estimate - smooth probability distribution curve
fig5, ax5 = plt.subplots()
sns.kdeplot(data=tips, x="total_bill", fill=True, ax=ax5)
st.pyplot(fig5)

# ecdfplot()
# 👉 empirical CDF দেখায়, যা cumulative probability বোঝায়
fig6, ax6 = plt.subplots()
sns.ecdfplot(data=tips, x="total_bill", ax=ax6)
st.pyplot(fig6)

# rugplot()
# 👉 এক্স-অ্যাক্সিসে প্রতিটি ডেটা পয়েন্টের টিক মার্ক দেখায়
fig7, ax7 = plt.subplots()
sns.rugplot(data=tips, x="total_bill", ax=ax7)
st.pyplot(fig7)

# violinplot() - categorized distribution
# 👉 প্রতিটি ক্যাটাগরির distribution ও summary stats দেখায়
fig8, ax8 = plt.subplots()
sns.violinplot(data=tips, x="day", y="total_bill", ax=ax8)
st.pyplot(fig8)

# distplot() - deprecated
# 👉 পুরনো ফাংশন যা histogram ও kde একত্রে দেখাতো (deprecated)
fig9, ax9 = plt.subplots()
sns.distplot(tips['total_bill'], bins=20, kde=True, ax=ax9)
st.pyplot(fig9)

# ---------------- Categorical Plots ----------------
st.header("📊 Categorical Plots")

# 1. catplot - general interface (boxplot kind)
# বিভিন্ন ক্যাটাগরি অনুসারে boxplot তৈরি করে
fig10 = sns.catplot(data=tips, x="day", y="total_bill", kind="box")
st.pyplot(fig10)

# 2. stripplot - প্রতিটি ডেটা পয়েন্ট দেখায় jitter সহ
fig11, ax11 = plt.subplots()
sns.stripplot(data=tips, x="day", y="total_bill", jitter=True, ax=ax11)
st.pyplot(fig11)

# 3. swarmplot - stripplot এর মতো কিন্তু overlap ছাড়াই সাজায়
fig12, ax12 = plt.subplots()
sns.swarmplot(data=tips, x="day", y="total_bill", ax=ax12)
st.pyplot(fig12)

# 4. boxplot - পাঁচটি পরিসংখ্যান মান (min, Q1, median, Q3, max)
fig13, ax13 = plt.subplots()
sns.boxplot(data=tips, x="day", y="total_bill", ax=ax13)
st.pyplot(fig13)

# 5. violinplot - boxplot + KDE, distribution ও statistics একসাথে
fig14, ax14 = plt.subplots()
sns.violinplot(data=tips, x="day", y="total_bill", ax=ax14)
st.pyplot(fig14)

# 6. boxenplot - বড় ডেটার distribution দেখানোর জন্য উপযুক্ত
fig15, ax15 = plt.subplots()
sns.boxenplot(data=tips, x="day", y="total_bill", ax=ax15)
st.pyplot(fig15)

# 7. pointplot - প্রতিটি ক্যাটাগরির mean ও CI দেখায়
fig16, ax16 = plt.subplots()
sns.pointplot(data=tips, x="day", y="total_bill", capsize=0.2, ax=ax16)
st.pyplot(fig16)

# 8. barplot - bar আকারে mean ও confidence interval দেখায়
fig17, ax17 = plt.subplots()
sns.barplot(data=tips, x="day", y="total_bill", ci="sd", ax=ax17)
st.pyplot(fig17)

# 9. countplot - প্রতিটি ক্যাটাগরির ডেটা পয়েন্টের সংখ্যা দেখায়
fig18, ax18 = plt.subplots()
sns.countplot(data=tips, x="day", ax=ax18)
st.pyplot(fig18)





## 📉 **Regression & Relationship Plots**

* `sns.lmplot()` – Faceted regression plot
* `sns.regplot()` – Regression fit plot
* `sns.residplot()` – Residuals of regression
* `sns.relplot()` – General relational plot (line, scatter)
* `sns.scatterplot()` – Scatterplot
* `sns.lineplot()` – Lineplot with confidence intervals

---


---

## 📉 **Regression & Relationship Plots**

এই প্লটগুলো মূলতঃ **দুই বা ততোধিক চলক (variables)** এর মধ্যে সম্পর্ক এবং তাদের মধ্যকার **trend বা pattern** দেখাতে ব্যবহৃত হয়।

---

### 🔹 `sns.lmplot()`

✅ **কাজ:**
Regression লাইন সহ scatter plot তৈরি করে, এবং subplot (facet) করা যায় `row`, `col`, `hue` দিয়ে।

✅ **সিনট্যাক্স:**

```python
sns.lmplot(data=tips, x='total_bill', y='tip', hue='sex', col='time')
```

✅ **গুরুত্বপূর্ণ প্যারামিটার:**

| Parameter    | মান           | কাজ                          |
| ------------ | ------------- | ---------------------------- |
| `data`       | DataFrame     | কোন ডেটাসেট ব্যবহার হবে      |
| `x`, `y`     | কলাম নাম      | নির্ভরশীল ও স্বতন্ত্র চলক    |
| `hue`        | ক্যাটাগরিকাল  | আলাদা রঙে আলাদা গ্রুপ        |
| `col`, `row` | ক্যাটাগরিকাল  | subplot তৈরি করে             |
| `markers`    | e.g. 'o', 'x' | গ্রুপভিত্তিক মার্কার         |
| `height`     | সংখ্যা        | subplot-এর উচ্চতা            |
| `aspect`     | সংখ্যা        | চওড়ার অনুপাত (width/height) |

✅ **ব্যবহার:**
👉 subgroup-wise regression দেখতে চাইলে (`time`, `sex` ইত্যাদি দিয়ে facet করে)

---

### 🔹 `sns.regplot()`

✅ **কাজ:**
Simple scatter + linear regression fit (একটি Axes-এ)।

✅ **সিনট্যাক্স:**

```python
sns.regplot(data=tips, x='total_bill', y='tip')
```

✅ **গুরুত্বপূর্ণ প্যারামিটার:**

| Parameter     | মান              | কাজ                               |
| ------------- | ---------------- | --------------------------------- |
| `x`, `y`      | কলাম             | সম্পর্কিত চলক                     |
| `fit_reg`     | True/False       | রিগ্রেশন লাইন দেখাবে কি না        |
| `ci`          | int (e.g. 95)    | Confidence interval (% তে)        |
| `marker`      | 'o', 'x' ইত্যাদি | পয়েন্ট মার্কার                   |
| `line_kws`    | dict             | লাইন কাস্টমাইজ (color, linewidth) |
| `scatter_kws` | dict             | scatter কাস্টমাইজ (alpha, size)   |

✅ **ব্যবহার:**
👉 Quick regression plot; subplot দরকার নেই।

---

### 🔹 `sns.residplot()`

✅ **কাজ:**
Regression model-এর **residuals (ভুল মান)** প্লট করে।

✅ **সিনট্যাক্স:**

```python
sns.residplot(data=tips, x='total_bill', y='tip')
```

✅ **গুরুত্বপূর্ণ প্যারামিটার:**

| Parameter     | মান         | কাজ                       |
| ------------- | ----------- | ------------------------- |
| `lowess`      | True/False  | Local regression smoother |
| `x`, `y`      | চলক         | x অনুযায়ী y residual     |
| `color`       | e.g. 'blue' | রঙ                        |
| `scatter_kws` | dict        | marker কাস্টমাইজ          |

✅ **ব্যবহার:**
👉 Regression model-এর fit কতটা ভালো, তা যাচাই করতে।

---

### 🔹 `sns.relplot()`

✅ **কাজ:**
General interface for relational plots — scatter অথবা line plot তৈরি করে।

✅ **সিনট্যাক্স:**

```python
sns.relplot(data=tips, x='total_bill', y='tip', kind='scatter', hue='sex')
```

✅ **গুরুত্বপূর্ণ প্যারামিটার:**

| Parameter    | মান               | কাজ                   |
| ------------ | ----------------- | --------------------- |
| `kind`       | 'scatter', 'line' | কোন টাইপের প্লট হবে   |
| `col`, `row` | ক্যাটাগরি         | subplot তৈরি          |
| `style`      | marker style      | মার্কার আলাদা করতে    |
| `size`       | numeric var       | point size আলাদা করতে |
| `palette`    | রঙ পছন্দ করতে     |                       |

✅ **ব্যবহার:**
👉 Faceted scatter বা line plot করতে চাইলে (flexible structure)

---

### 🔹 `sns.scatterplot()`

✅ **কাজ:**
Simple scatter plot, সম্পর্ক বোঝাতে ব্যবহার হয়।

✅ **সিনট্যাক্স:**

```python
sns.scatterplot(data=tips, x='total_bill', y='tip', hue='sex')
```

✅ **গুরুত্বপূর্ণ প্যারামিটার:**

| Parameter | মান                                 | কাজ             |
| --------- | ----------------------------------- | --------------- |
| `hue`     | ক্যাটাগরি                           | আলাদা রঙে গ্রুপ |
| `style`   | ক্যাটাগরি                           | আলাদা marker    |
| `size`    | ক্যাটাগরি বা সংখ্যার উপর ভিত্তি করে | point এর আকার   |
| `palette` | রঙ                                  | রঙ নির্বাচন     |
| `alpha`   | 0-1                                 | transparency    |

✅ **ব্যবহার:**
👉 দুই চলকের মধ্যে raw সম্পর্ক দেখতে চাইলে।

---

### 🔹 `sns.lineplot()`

✅ **কাজ:**
লাইন আঁকে দুই চলকের মধ্যে পরিবর্তন দেখাতে।

✅ **সিনট্যাক্স:**

```python
sns.lineplot(data=tips, x='size', y='tip', hue='sex')
```

✅ **গুরুত্বপূর্ণ প্যারামিটার:**

| Parameter | মান                 | কাজ                       |
| --------- | ------------------- | ------------------------- |
| `ci`      | confidence interval | default 95                |
| `markers` | True/False          | point marker দেখাবে কি না |
| `dashes`  | True/False          | dashed line               |
| `sort`    | True/False          | x sort করবে কিনা          |
| `style`   | ক্যাটাগরি           | linestyle বা marker       |

✅ **ব্যবহার:**
👉 trends বা সময়ক্রমে মানের পরিবর্তন দেখাতে।

---

## ✅ কোনটি কবে ব্যবহার করবো?

| Function        | ব্যবহার করুন যখন...                        |
| --------------- | ------------------------------------------ |
| `lmplot()`      | একাধিক facet-সহ regression দরকার           |
| `regplot()`     | Simple regression line ও scatter দেখতে চাও |
| `residplot()`   | Model fit ভাল না খারাপ বুঝতে চাও           |
| `relplot()`     | Facet সহ general scatter/line করতে চাও     |
| `scatterplot()` | Raw point-to-point সম্পর্ক দেখতে           |
| `lineplot()`    | Continuous trend বা টাইম-সিরিজ data        |

---


import seaborn as sns
import matplotlib.pyplot as plt
import streamlit as st

# Load dataset
tips = sns.load_dataset("tips")

st.title("📊 Seaborn Categorical, Distribution, and Regression Plots Dashboard")
st.write("Visualize categorical, distribution, and regression/relationship plots using the 'tips' dataset.")

# ---------------- Distribution Plots ----------------
st.header("📈 Distribution Plots")

# displot() - Histogram
fig1 = sns.displot(data=tips, x="total_bill", kind="hist", bins=20)
st.pyplot(fig1)

# displot() - KDE
fig2 = sns.displot(data=tips, x="total_bill", kind="kde", fill=True)
st.pyplot(fig2)

# displot() - ECDF
fig3 = sns.displot(data=tips, x="total_bill", kind="ecdf")
st.pyplot(fig3)

# histplot()
fig4, ax4 = plt.subplots()
sns.histplot(data=tips, x="total_bill", bins=20, kde=True, ax=ax4)
st.pyplot(fig4)

# kdeplot()
fig5, ax5 = plt.subplots()
sns.kdeplot(data=tips, x="total_bill", fill=True, ax=ax5)
st.pyplot(fig5)

# ecdfplot()
fig6, ax6 = plt.subplots()
sns.ecdfplot(data=tips, x="total_bill", ax=ax6)
st.pyplot(fig6)

# rugplot()
fig7, ax7 = plt.subplots()
sns.rugplot(data=tips, x="total_bill", ax=ax7)
st.pyplot(fig7)

# violinplot()
fig8, ax8 = plt.subplots()
sns.violinplot(data=tips, x="day", y="total_bill", ax=ax8)
st.pyplot(fig8)

# distplot() - deprecated
fig9, ax9 = plt.subplots()
sns.distplot(tips['total_bill'], bins=20, kde=True, ax=ax9)
st.pyplot(fig9)

# ---------------- Categorical Plots ----------------
st.header("📊 Categorical Plots")

# catplot()
fig10 = sns.catplot(data=tips, x="day", y="total_bill", kind="box")
st.pyplot(fig10)

# stripplot()
fig11, ax11 = plt.subplots()
sns.stripplot(data=tips, x="day", y="total_bill", jitter=True, ax=ax11)
st.pyplot(fig11)

# swarmplot()
fig12, ax12 = plt.subplots()
sns.swarmplot(data=tips, x="day", y="total_bill", ax=ax12)
st.pyplot(fig12)

# boxplot()
fig13, ax13 = plt.subplots()
sns.boxplot(data=tips, x="day", y="total_bill", ax=ax13)
st.pyplot(fig13)

# violinplot()
fig14, ax14 = plt.subplots()
sns.violinplot(data=tips, x="day", y="total_bill", ax=ax14)
st.pyplot(fig14)

# boxenplot()
fig15, ax15 = plt.subplots()
sns.boxenplot(data=tips, x="day", y="total_bill", ax=ax15)
st.pyplot(fig15)

# pointplot()
fig16, ax16 = plt.subplots()
sns.pointplot(data=tips, x="day", y="total_bill", capsize=0.2, ax=ax16)
st.pyplot(fig16)

# barplot()
fig17, ax17 = plt.subplots()
sns.barplot(data=tips, x="day", y="total_bill", ci="sd", ax=ax17)
st.pyplot(fig17)

# countplot()
fig18, ax18 = plt.subplots()
sns.countplot(data=tips, x="day", ax=ax18)
st.pyplot(fig18)

# ---------------- Regression & Relationship Plots ----------------
st.header("📉 Regression & Relationship Plots")

# lmplot()
fig19 = sns.lmplot(data=tips, x="total_bill", y="tip", hue="sex", col="time")
st.pyplot(fig19)

# regplot()
fig20, ax20 = plt.subplots()
sns.regplot(data=tips, x="total_bill", y="tip", ax=ax20)
st.pyplot(fig20)

# residplot()
fig21, ax21 = plt.subplots()
sns.residplot(data=tips, x="total_bill", y="tip", ax=ax21)
st.pyplot(fig21)

# relplot() - scatter
fig22 = sns.relplot(data=tips, x="total_bill", y="tip", kind="scatter", hue="sex")
st.pyplot(fig22)

# scatterplot()
fig23, ax23 = plt.subplots()
sns.scatterplot(data=tips, x="total_bill", y="tip", hue="sex", ax=ax23)
st.pyplot(fig23)

# lineplot()
fig24, ax24 = plt.subplots()
sns.lineplot(data=tips, x="size", y="tip", hue="sex", ax=ax24)
st.pyplot(fig24)



## 📚 **Matrix / Heatmaps & Grids**

* `sns.heatmap()` – 2D matrix with color encoding
* `sns.clustermap()` – Clustered heatmap
* `sns.PairGrid()` – Flexible pairwise grid
* `sns.JointGrid()` – Bivariate grid
* `sns.FacetGrid()` – General purpose multi-plot grid
* `sns.pairplot()` – Pairwise plot grid
* `sns.jointplot()` – Joint and marginal plot

---

## 🧰 **Themes, Palettes, and Aesthetic Control**

* `sns.set_theme()` – Set overall theme
* `sns.set_style()` – Set plot style (whitegrid, darkgrid, etc.)
* `sns.set_context()` – Resize elements for context (talk, paper…)
* `sns.set_palette()` – Set default color palette
* `sns.color_palette()` – Return list of colors from palette
* `sns.palplot()` – Visualize a palette
* `sns.choose_diverging_palette()` – GUI tool for diverging palettes
* `sns.choose_colorbrewer_palette()` – GUI for ColorBrewer palettes
* `sns.choose_cubehelix_palette()` – GUI for cubehelix palettes
* `sns.cubehelix_palette()` – Cubehelix palette
* `sns.dark_palette()` – Dark-themed palette
* `sns.light_palette()` – Light-themed palette
* `sns.diverging_palette()` – Diverging color palette
* `sns.xkcd_palette()` – XKCD color names
* `sns.husl_palette()` – Husl color space
* `sns.hls_palette()` – HLS color space
* `sns.mpl_palette()` – Matplotlib-compatible palette

---

## 📌 **Figure Utilities**

* `sns.despine()` – Remove axes spines
* `sns.move_legend()` – Reposition the legend
* `sns.plotting_context()` – Temporarily set context
* `sns.axes_style()` – Temporarily set style
* `sns.set()` – Quick set style/palette/context
* `sns.reset_defaults()` – Restore Seaborn defaults
* `sns.reset_orig()` – Restore Matplotlib defaults
* `sns.get_dataset_names()` – List built-in datasets
* `sns.load_dataset()` – Load a sample dataset
* `sns.get_data_home()` – Path for datasets
* `sns.set_color_codes()` – Color codes for matplotlib

---


---

## 📌 **Figure Utility Functions – ব্যাকগ্রাউন্ড, context, legend, dataset নিয়ন্ত্রণের টুল**

---

### 1. 🔹 `sns.despine()`

✅ **কাজ:**
Plot-এর চারপাশের অতিরিক্ত border (spines) সরিয়ে দেয়।

✅ **সিনট্যাক্স:**

```python
import matplotlib.pyplot as plt
sns.boxplot(data=tips, x='day', y='total_bill')
sns.despine()  # removes right and top border
plt.show()
```

✅ **প্যারামিটার:**

| Parameter        | মান        | কাজ                                   |
| ---------------- | ---------- | ------------------------------------- |
| `top`            | True/False | top spine রাখবে কি না                 |
| `right`          | True/False | right spine রাখবে কি না               |
| `left`, `bottom` | True/False | প্রয়োজনে নিচ বা বামটাও বাদ দিতে পারো |

---

### 2. 🔹 `sns.move_legend()`

✅ **কাজ:**
Legend-এর অবস্থান পরিবর্তন করতে সাহায্য করে (v0.11+).

✅ **সিনট্যাক্স:**

```python
fig, ax = plt.subplots()
sns.scatterplot(data=tips, x='total_bill', y='tip', hue='sex', ax=ax)
sns.move_legend(ax, 'upper left')  # moves legend
```

✅ **প্যারামিটার:**

| Parameter | মান                         | কাজ                          |
| --------- | --------------------------- | ---------------------------- |
| `obj`     | Axes object                 | কোন plot-এর legend সরানো হবে |
| `loc`     | string (e.g., 'upper left') | নতুন অবস্থান                 |
| `title`   | str                         | নতুন legend title            |

---

### 3. 🔹 `sns.plotting_context()`

✅ **কাজ:**
Plot context (text size, line thickness) সাময়িকভাবে পরিবর্তন।

✅ **সিনট্যাক্স:**

```python
with sns.plotting_context(\"talk\"):  # paper, notebook, talk, poster
    sns.boxplot(data=tips, x='day', y='total_bill')
    plt.show()
```

✅ **ব্যবহার:**
👉 Report, presentation বা article এর জন্য visualization scale পরিবর্তন।

---

### 4. 🔹 `sns.axes_style()`

✅ **কাজ:**
Plot-এর background style সাময়িকভাবে পরিবর্তন।

✅ **সিনট্যাক্স:**

```python
with sns.axes_style(\"whitegrid\"):  # darkgrid, white, ticks, etc.
    sns.histplot(data=tips, x=\"total_bill\")
    plt.show()
```

✅ **style options:**

* `"whitegrid"` (default)
* `"darkgrid"`
* `"white"`
* `"dark"`
* `"ticks"`

---

### 5. 🔹 `sns.set()`

✅ **কাজ:**
একসাথে style, context, palette সেট করে দেয় — shortcut ফাংশন।

✅ **সিনট্যাক্স:**

```python
sns.set(style=\"whitegrid\", context=\"talk\", palette=\"pastel\")
```

✅ **ব্যবহার:**
👉 Fast setup for plots — one-liner to style all plots.

---

### 6. 🔹 `sns.reset_defaults()`

✅ **কাজ:**
Seaborn-এর ডিফল্ট setting-এ ফিরে যায়।

✅ **সিনট্যাক্স:**

```python
sns.reset_defaults()
```

✅ **ব্যবহার:**
👉 অনেক কাস্টমাইজেশনের পর সব কিছু আবার default-এ আনতে।

---

### 7. 🔹 `sns.reset_orig()`

✅ **কাজ:**
Matplotlib-এর একদম মূল (original) settings পুনরুদ্ধার করে।

✅ **সিনট্যাক্স:**

```python
sns.reset_orig()
```

✅ **ব্যবহার:**
👉 Plot দেখতে Matplotlib style এ ফিরতে।

---

### 8. 🔹 `sns.get_dataset_names()`

✅ **কাজ:**
Seaborn-এর বিল্ট-ইন dataset গুলোর নামের তালিকা দেয়।

✅ **সিনট্যাক্স:**

```python
print(sns.get_dataset_names())
```

✅ **ব্যবহার:**
👉 কোণ dataset আছে সেটা জানার জন্য।

---

### 9. 🔹 `sns.load_dataset()`

✅ **কাজ:**
Seaborn-এর বিল্ট-ইন dataset লোড করে `pandas.DataFrame` আকারে।

✅ **সিনট্যাক্স:**

```python
tips = sns.load_dataset(\"tips\")
```

✅ **ব্যবহার:**
👉 Quick practice বা ডেমো visualization এর জন্য।

---

### 10. 🔹 `sns.get_data_home()`

✅ **কাজ:**
যে path-এ Seaborn dataset ক্যাশ হয় সেটা জানায়।

✅ **সিনট্যাক্স:**

```python
print(sns.get_data_home())
```

---

### 11. 🔹 `sns.set_color_codes()`

✅ **কাজ:**
Matplotlib-এর জন্য seaborn-style color codes সক্রিয় করে।

✅ **সিনট্যাক্স:**

```python
sns.set_color_codes(\"pastel\")  # dark, muted, bright, pastel, colorblind, deep
```

---

## ✅ উপসংহার

| Function              | কাজ                          | কবে ব্যবহার করবেন        |
| --------------------- | ---------------------------- | ------------------------ |
| `despine()`           | অপ্রয়োজনীয় border সরাতে      | Cleaner look             |
| `move_legend()`       | legend-এর অবস্থান বদলাতে     | Text overlap এড়াতে      |
| `plotting_context()`  | text scale সাময়িক পরিবর্তন  | report/presentation      |
| `axes_style()`        | background style বদলাতে      | dark/light theme         |
| `set()`               | সব একসাথে সেট করতে           | দ্রুত styling            |
| `reset_defaults()`    | Seaborn default-এ ফেরার জন্য | reset দরকার হলে          |
| `reset_orig()`        | Matplotlib default-এ ফিরতে   | সম্পূর্ণ reset           |
| `get_dataset_names()` | dataset দেখতে                | কোনটা আছে বোঝার জন্য     |
| `load_dataset()`      | dataset লোড করতে             | ডেমো বা practice এর জন্য |
| `get_data_home()`     | ক্যাশ লোকেশন জানতে           | advanced config          |
| `set_color_codes()`   | matplotlib রঙ কন্ট্রোল       | custom plots এ           |

---
import seaborn as sns
import matplotlib.pyplot as plt
import streamlit as st

# Load dataset
tips = sns.load_dataset("tips")

st.title("📊 Seaborn All-in-One Plots Dashboard")
st.write("Visualize categorical, distribution, regression, and utility functions using the 'tips' dataset.")

# ---------------- Distribution Plots ----------------
st.header("📈 Distribution Plots")
fig1 = sns.displot(data=tips, x="total_bill", kind="hist", bins=20)
st.pyplot(fig1)
fig2 = sns.displot(data=tips, x="total_bill", kind="kde", fill=True)
st.pyplot(fig2)
fig3 = sns.displot(data=tips, x="total_bill", kind="ecdf")
st.pyplot(fig3)
fig4, ax4 = plt.subplots()
sns.histplot(data=tips, x="total_bill", bins=20, kde=True, ax=ax4)
st.pyplot(fig4)
fig5, ax5 = plt.subplots()
sns.kdeplot(data=tips, x="total_bill", fill=True, ax=ax5)
st.pyplot(fig5)
fig6, ax6 = plt.subplots()
sns.ecdfplot(data=tips, x="total_bill", ax=ax6)
st.pyplot(fig6)
fig7, ax7 = plt.subplots()
sns.rugplot(data=tips, x="total_bill", ax=ax7)
st.pyplot(fig7)
fig8, ax8 = plt.subplots()
sns.violinplot(data=tips, x="day", y="total_bill", ax=ax8)
st.pyplot(fig8)
fig9, ax9 = plt.subplots()
sns.distplot(tips['total_bill'], bins=20, kde=True, ax=ax9)
st.pyplot(fig9)

# ---------------- Categorical Plots ----------------
st.header("📊 Categorical Plots")
fig10 = sns.catplot(data=tips, x="day", y="total_bill", kind="box")
st.pyplot(fig10)
fig11, ax11 = plt.subplots()
sns.stripplot(data=tips, x="day", y="total_bill", jitter=True, ax=ax11)
st.pyplot(fig11)
fig12, ax12 = plt.subplots()
sns.swarmplot(data=tips, x="day", y="total_bill", ax=ax12)
st.pyplot(fig12)
fig13, ax13 = plt.subplots()
sns.boxplot(data=tips, x="day", y="total_bill", ax=ax13)
st.pyplot(fig13)
fig14, ax14 = plt.subplots()
sns.violinplot(data=tips, x="day", y="total_bill", ax=ax14)
st.pyplot(fig14)
fig15, ax15 = plt.subplots()
sns.boxenplot(data=tips, x="day", y="total_bill", ax=ax15)
st.pyplot(fig15)
fig16, ax16 = plt.subplots()
sns.pointplot(data=tips, x="day", y="total_bill", capsize=0.2, ax=ax16)
st.pyplot(fig16)
fig17, ax17 = plt.subplots()
sns.barplot(data=tips, x="day", y="total_bill", ci="sd", ax=ax17)
st.pyplot(fig17)
fig18, ax18 = plt.subplots()
sns.countplot(data=tips, x="day", ax=ax18)
st.pyplot(fig18)

# ---------------- Regression & Relationship Plots ----------------
st.header("📉 Regression & Relationship Plots")
fig19 = sns.lmplot(data=tips, x="total_bill", y="tip", hue="sex", col="time")
st.pyplot(fig19)
fig20, ax20 = plt.subplots()
sns.regplot(data=tips, x="total_bill", y="tip", ax=ax20)
st.pyplot(fig20)
fig21, ax21 = plt.subplots()
sns.residplot(data=tips, x="total_bill", y="tip", ax=ax21)
st.pyplot(fig21)
fig22 = sns.relplot(data=tips, x="total_bill", y="tip", kind="scatter", hue="sex")
st.pyplot(fig22)
fig23, ax23 = plt.subplots()
sns.scatterplot(data=tips, x="total_bill", y="tip", hue="sex", ax=ax23)
st.pyplot(fig23)
fig24, ax24 = plt.subplots()
sns.lineplot(data=tips, x="size", y="tip", hue="sex", ax=ax24)
st.pyplot(fig24)

# ---------------- Figure Utilities ----------------
st.header("🧰 Figure Utility Examples")

# despine
fig25, ax25 = plt.subplots()
sns.boxplot(data=tips, x="day", y="total_bill", ax=ax25)
sns.despine(ax=ax25)
st.pyplot(fig25)

# move_legend
fig26, ax26 = plt.subplots()
sns.scatterplot(data=tips, x="total_bill", y="tip", hue="sex", ax=ax26)
sns.move_legend(ax26, "upper left")
st.pyplot(fig26)

# plotting_context
with sns.plotting_context("poster"):
    fig27, ax27 = plt.subplots()
    sns.boxplot(data=tips, x="day", y="total_bill", ax=ax27)
    st.pyplot(fig27)

# axes_style
with sns.axes_style("darkgrid"):
    fig28, ax28 = plt.subplots()
    sns.histplot(data=tips, x="total_bill", ax=ax28)
    st.pyplot(fig28)

# set
sns.set(style="whitegrid", context="talk", palette="pastel")
fig29, ax29 = plt.subplots()
sns.violinplot(data=tips, x="day", y="tip", ax=ax29)
st.pyplot(fig29)

# reset_defaults
sns.reset_defaults()

# reset_orig
sns.reset_orig()

# get_dataset_names
dataset_names = sns.get_dataset_names()
st.write("### Available Seaborn Datasets:", dataset_names)

# load_dataset
iris = sns.load_dataset("iris")
st.write("### Preview of 'iris' dataset:")
st.dataframe(iris.head())

# get_data_home
data_home = sns.get_data_home()
st.write("### Seaborn Data Home Path:", data_home)

# set_color_codes
sns.set_color_codes("muted")
fig30, ax30 = plt.subplots()
sns.boxplot(data=tips, x="sex", y="total_bill", ax=ax30)
st.pyplot(fig30)



## 🔢 **Seaborn Objects Interface (`seaborn.objects`)**

This is Seaborn’s new object-oriented interface for fine-tuned visualizations. These are *building blocks*:

### **Plot Component**

* `sns.objects.Plot()` – Main object for building layered plots

### **Marks (visual representations)**

* `Dot()`, `Dots()` – Single or multiple dot markers
* `Line()`, `Lines()` – Line(s) connecting data
* `Path()`, `Paths()` – Flexible point connections
* `Dash()` – Dashed line segments
* `Bar()`, `Bars()` – Bar charts
* `Range()` – Vertical or horizontal ranges
* `Area()` – Area under a line
* `Band()` – Confidence bands or ranges
* `Text()` – Text annotations


---

## 🔢 **Plot Object (`sns.objects.Plot`)**

**কাজ:**
Plot তৈরির মূল কাঠামো (foundation)। `.add()` বা `+` দিয়ে বিভিন্ন visual mark যোগ করা হয়।

**সাধারণ সিনট্যাক্স:**

```python
from seaborn.objects import Plot, Dot
Plot(data=df, x='col1', y='col2').add(Dot())
```

### 🧾 Key Parameters:

| Parameter                                  | মান         | কাজ                           |
| ------------------------------------------ | ----------- | ----------------------------- |
| `data`                                     | DataFrame   | প্লটে ব্যবহৃত ডেটাসেট         |
| `x`, `y`, `color`, `label`, `size`, `fill` | column name | aesthetics mapping            |
| `group`                                    | column      | plot গ্রুপভিত্তিক বিভাজন করতে |
| `title`                                    | str         | plot-এর টাইটেল                |
| `xlim`, `ylim`                             | tuple       | axis সীমা নির্ধারণ করতে       |

---

## 🎯 **Marks – Visual Representations**

### 1. 🔵 `Dot()`

**কাজ:** Individual scatter point দেখাতে ব্যবহৃত।

```python
Plot(data=df, x='x', y='y').add(Dot())
```

| Parameter | মান           | কাজ          |
| --------- | ------------- | ------------ |
| `color`   | column/str    | point color  |
| `alpha`   | 0–1           | transparency |
| `size`    | number/column | পয়েন্ট সাইজ |

---

### 2. 🔵 `Dots()`

**কাজ:** গ্রুপ করা ডেটা একসাথে দেখায় (like stripplot/swarmplot এর বিকল্প)।

```python
Plot(df, x='category', y='value').add(Dots())
```

| Parameter        | মান             | কাজ                          |
| ---------------- | --------------- | ---------------------------- |
| `dodge`          | True/False      | আলাদা গ্রুপ আলাদা করে সাজানো |
| `alpha`, `color` | যেমন Dot এর মতই | স্টাইলিং                     |

---

### 3. 🔷 `Line()`

**কাজ:** ডেটা পয়েন্টের মধ্যে line আঁকে — সাধারণত ট্রেন্ড বোঝাতে।

```python
Plot(df, x='x', y='y').add(Line())
```

| Parameter   | মান                  | কাজ                |
| ----------- | -------------------- | ------------------ |
| `linestyle` | '-', '--', '-.', ':' | line স্টাইল        |
| `linewidth` | সংখ্যা               | line-এর মোটা/পাতলা |
| `color`     | str/column           | line color         |

---

### 4. 🔷 `Lines()`

**কাজ:** গ্রুপভিত্তিক একাধিক line আঁকে।

```python
Plot(df, x='x', y='y', color='group').add(Lines())
```

| Parameter                 | মান    | কাজ                         |
| ------------------------- | ------ | --------------------------- |
| `group`, `color`, `style` | column | গ্রুপ অনুযায়ী line styling |

---

### 5. 🔶 `Path()` & `Paths()`

**কাজ:** custom order অনুযায়ী point connect করা।

```python
Plot(df, x='x', y='y').add(Path())
```

| Parameter            | মান    | কাজ        |
| -------------------- | ------ | ---------- |
| `group`              | column | আলাদা path |
| `alpha`, `linewidth` | সংখ্যা | স্টাইলিং   |

---

### 6. 🔻 `Dash()`

**কাজ:** dashed line segment তৈরি করে।

```python
Plot(df, x='x', y='y').add(Dash())
```

| Parameter   | মান                    | কাজ              |
| ----------- | ---------------------- | ---------------- |
| `dashes`    | pattern (e.g., (4, 2)) | ড্যাশ স্টাইল     |
| `linewidth` | সংখ্যা                 | ড্যাশ মোটা/পাতলা |

---

### 7. 🟥 `Bar()` & `Bars()`

**কাজ:** Bar chart তৈরি করে — একক বা গ্রুপ অনুযায়ী।

```python
Plot(df, x='category', y='value').add(Bars())
```

| Parameter | মান          | কাজ                              |
| --------- | ------------ | -------------------------------- |
| `fill`    | color/column | bar রঙ                           |
| `width`   | সংখ্যা       | bar-এর প্রস্থ                    |
| `dodge`   | True/False   | গ্রুপভিত্তিক বর আলাদা করে সাজানো |

---

### 8. 🔺 `Range()`

**কাজ:** একটি নির্দিষ্ট x বা y range দেখায় — error bar বা ইন্টারভ্যালের জন্য।

```python
Plot(df, x='x', y='low', y2='high').add(Range())
```

| Parameter | মান    | কাজ          |
| --------- | ------ | ------------ |
| `y2`      | column | upper limit  |
| `alpha`   | 0–1    | transparency |

---

### 9. 🟩 `Area()`

**কাজ:** line এর নিচে area fill করে — cumulative/stacked প্লটের জন্য।

```python
Plot(df, x='x', y='y').add(Area())
```

| Parameter | মান          | কাজ                 |
| --------- | ------------ | ------------------- |
| `fill`    | color        | area রঙ             |
| `alpha`   | transparency | fill কতটা হালকা/গাঢ় |

---

### 10. 🟦 `Band()`

**কাজ:** Confidence band বা uncertainty range দেখাতে।

```python
Plot(df, x='x', y='y').add(Band(), alpha=0.3).add(Line())
```

| Parameter | মান   | কাজ          |
| --------- | ----- | ------------ |
| `fill`    | color | ব্যান্ড রঙ   |
| `alpha`   | 0–1   | transparency |

---

### 11. 📝 `Text()`

**কাজ:** পয়েন্টের পাশে লেবেল বা annotation দেখায়।

```python
Plot(df, x='x', y='y', label='label_column').add(Dot()).add(Text())
```

| Parameter       | মান        | কাজ                   |
| --------------- | ---------- | --------------------- |
| `offset`        | tuple      | টেক্সট একটু সরে থাকবে |
| `color`, `size` | str/number | স্টাইল কাস্টমাইজ      |

---

## ✅ উপসংহার (Summary Table)

| Mark      | কাজ                                | প্রধান Parameters                 |
| --------- | ---------------------------------- | --------------------------------- |
| `Dot()`   | Individual points                  | `color`, `alpha`, `size`          |
| `Dots()`  | Grouped points (strip/swarm style) | `dodge`, `alpha`                  |
| `Line()`  | Simple connected line              | `linestyle`, `linewidth`, `color` |
| `Lines()` | Groupwise multiple lines           | `group`, `style`, `color`         |
| `Path()`  | Custom order path                  | `group`, `linewidth`              |
| `Dash()`  | Dashed segments                    | `dashes`, `linewidth`             |
| `Bars()`  | Bar charts                         | `fill`, `dodge`, `width`          |
| `Range()` | y/y2 বা x/x2 এর range              | `y2`, `alpha`                     |
| `Area()`  | Fill area under curve              | `fill`, `alpha`                   |
| `Band()`  | Confidence intervals               | `fill`, `alpha`                   |
| `Text()`  | Labels/annotations                 | `label`, `offset`, `color`        |

---


import seaborn as sns
import matplotlib.pyplot as plt
import streamlit as st
from seaborn.objects import Plot, Dot, Dots, Line, Lines, Path, Paths, Dash, Bar, Bars, Range, Area, Band, Text

# Load dataset
tips = sns.load_dataset("tips")

st.title("📊 Seaborn All-in-One Plots Dashboard")
st.write("Visualize categorical, distribution, regression, utility, and object interface plots using the 'tips' dataset.")

# ---------------- Seaborn Objects Interface ----------------
st.header("🔢 Seaborn Objects Interface Examples")

# Dot()
st.subheader("Dot() - Single data points")
p1 = Plot(data=tips, x="total_bill", y="tip").add(Dot())
st.pyplot(p1.figure)

# Dots()
st.subheader("Dots() - Grouped dot markers")
p2 = Plot(data=tips, x="day", y="total_bill").add(Dots())
st.pyplot(p2.figure)

# Line()
st.subheader("Line() - Line through points")
p3 = Plot(data=tips, x="total_bill", y="tip").add(Line())
st.pyplot(p3.figure)

# Lines()
st.subheader("Lines() - Multiple grouped lines")
p4 = Plot(data=tips, x="total_bill", y="tip", color="sex").add(Lines())
st.pyplot(p4.figure)

# Path()
st.subheader("Path() - Custom connected path")
p5 = Plot(data=tips, x="total_bill", y="tip").add(Path())
st.pyplot(p5.figure)

# Dash()
st.subheader("Dash() - Dashed segments")
p6 = Plot(data=tips, x="total_bill", y="tip").add(Dash())
st.pyplot(p6.figure)

# Bars()
st.subheader("Bars() - Bar chart")
bar_data = tips.groupby("day")["total_bill"].mean().reset_index()
p7 = Plot(bar_data, x="day", y="total_bill").add(Bars())
st.pyplot(p7.figure)

# Range()
st.subheader("Range() - Low/High Range Display")
import pandas as pd
range_data = pd.DataFrame({
    "x": ["A", "B", "C"],
    "y": [5, 7, 6],
    "y2": [8, 10, 9]
})
p8 = Plot(range_data, x="x", y="y", y2="y2").add(Range())
st.pyplot(p8.figure)

# Area()
st.subheader("Area() - Filled area under line")
area_data = tips.groupby("size")["tip"].mean().reset_index()
p9 = Plot(area_data, x="size", y="tip").add(Area())
st.pyplot(p9.figure)

# Band()
st.subheader("Band() - Confidence band with line")
band_data = tips.groupby("size")["tip"].agg(["mean", "std"]).reset_index()
band_data.columns = ["size", "mean", "std"]
band_data["low"] = band_data["mean"] - band_data["std"]
band_data["high"] = band_data["mean"] + band_data["std"]
p10 = Plot(band_data, x="size", y="mean", y2="high").add(Band()).add(Line())
st.pyplot(p10.figure)

# Text()
st.subheader("Text() - Labels on points")
p11 = Plot(tips.head(10), x="total_bill", y="tip", label="day").add(Dot()).add(Text())
st.pyplot(p11.figure)


✅ অন্তর্ভুক্ত উদাহরণ:
Dot() – সাধারণ scatter point

Dots() – গুচ্ছাকারে ডট (strip/swarm style)

Line() – একক রেখা (trend)

Lines() – গ্রুপ অনুযায়ী অনেক রেখা

Path() – custom point connection

Dash() – dashed segments

Bars() – Bar chart (day vs mean)

Range() – একটি range (low/high)

Area() – Line-এর নিচের এলাকা পূরণ

Band() – Confidence interval (mean ± std)

Text() – পয়েন্টের উপর লেবেল


### **Statistical Transforms**

* `Agg()` – Aggregation
* `Est()` – Estimation
* `Hist()` – Histogram binning
* `KDE()` – Kernel density estimation
* `Count()` – Count occurrences
* `Perc()` – Percentile transform
* `PolyFit()` – Polynomial fitting


---

## 🎯 **Statistical Transforms – কী করে ও কবে ব্যবহার করব**

Stat transforms মূলত raw data কে উপযোগী **summary / shape**-এ রূপান্তর করে, যেমনঃ average, count, histogram bin, density ইত্যাদি।

---

### 1. 🔹 `Agg()` – Aggregation (গড়, median, sum, ইত্যাদি)

✅ **কাজ:**
একটি বা একাধিক ক্যাটাগরির উপর ডেটা **summarize** করে (যেমন গড়/মোট)। `Bars()` বা `Dots()` এর সাথে বেশি ব্যবহৃত হয়।

✅ **সিনট্যাক্স:**

```python
from seaborn.objects import Plot, Bars, Agg
Plot(data=tips, x=\"day\", y=\"total_bill\").add(Bars(), Agg())
```

### 📌 প্যারামিটার:

| Parameter | মান                                      | কাজ                          |
| --------- | ---------------------------------------- | ---------------------------- |
| `stat`    | `'mean'`, `'sum'`, `'median'`, `'count'` | কোন aggregation হবে          |
| `error`   | `'ci'`, `'sd'`, `'se'`                   | error bar কী ভিত্তিতে দেখাবে |
| `ci`      | int (e.g., 95)                           | confidence interval          |

---

### 2. 🔹 `Est()` – Estimation over continuous variables

✅ **কাজ:**
Line বা trend plot তৈরির জন্য, **x** অনুযায়ী কিছু **estimate** করে (যেমন mean, sum)।

✅ **সিনট্যাক্স:**

```python
Plot(tips, x=\"total_bill\", y=\"tip\").add(Line(), Est(stat=\"mean\"))
```

### 📌 প্যারামিটার:

| Parameter | মান                           | কাজ                     |
| --------- | ----------------------------- | ----------------------- |
| `stat`    | `'mean'`, `'sum'`, `'median'` | নির্দিষ্ট estimate      |
| `n_bins`  | সংখ্যা                        | কতটি bin-এ x ভাগ হবে    |
| `ci`      | সংখ্যা (e.g., 95)             | error bar হিসেবে দেখাবে |

---

### 3. 🔹 `Hist()` – Histogram Binning

✅ **কাজ:**
x অক্ষের ভ্যালুগুলোকে **bin** করে তাদের ফ্রিকোয়েন্সি দেখায়।

✅ **সিনট্যাক্স:**

```python
Plot(tips, x=\"total_bill\").add(Bars(), Hist())
```

### 📌 প্যারামিটার:

| Parameter   | মান                                     | কাজ                       |
| ----------- | --------------------------------------- | ------------------------- |
| `bins`      | সংখ্যা বা list                          | কতোটি bin বা bin এর range |
| `stat`      | `'count'`, `'density'`, `'probability'` | y-axis কী দেখাবে          |
| `normalize` | bool                                    | বার নর্মালাইজ করব কিনা    |

---

### 4. 🔹 `KDE()` – Kernel Density Estimation

✅ **কাজ:**
একটি smooth curve আঁকে যা ডেটার distribution বোঝায়।

✅ **সিনট্যাক্স:**

```python
Plot(tips, x=\"total_bill\").add(Line(), KDE())
```

### 📌 প্যারামিটার:

| Parameter    | মান        | কাজ                          |
| ------------ | ---------- | ---------------------------- |
| `bw`         | সংখ্যা     | bandwidth (curve smoothness) |
| `cut`        | সংখ্যা     | কতদূর পর্যন্ত extend করবে    |
| `cumulative` | True/False | cumulative KDE দেখাবে কি না  |

---

### 5. 🔹 `Count()` – Frequency Count

✅ **কাজ:**
প্রতিটি x category-তে **কতবার ডেটা** আছে তা দেখায়।

✅ **সিনট্যাক্স:**

```python
Plot(tips, x=\"day\").add(Bars(), Count())
```

### 📌 প্যারামিটার:

| Parameter   | মান        | কাজ                             |
| ----------- | ---------- | ------------------------------- |
| `normalize` | True/False | পার্সেন্টেজ হিসেবে দেখাবে কি না |

---

### 6. 🔹 `Perc()` – Percentile Transformation

✅ **কাজ:**
y-এর **percentile rank** (e.g., 25th, 50th, 75th) হিসাব করে।

✅ **সিনট্যাক্স:**

```python
Plot(tips, x=\"total_bill\", y=\"tip\").add(Line(), Perc(q=50))
```

### 📌 প্যারামিটার:

| Parameter | মান   | কাজ                                            |
| --------- | ----- | ---------------------------------------------- |
| `q`       | 0–100 | কোন percentile (e.g. q=25 for 25th percentile) |

---

### 7. 🔹 `PolyFit()` – Polynomial Fit

✅ **কাজ:**
ডেটার উপর polynomial regression fit করে (line বা curve)।

✅ **সিনট্যাক্স:**

```python
Plot(tips, x=\"total_bill\", y=\"tip\").add(Line(), PolyFit(degree=2))
```

### 📌 প্যারামিটার:

| Parameter | মান | কাজ                                                    |
| --------- | --- | ------------------------------------------------------ |
| `degree`  | int | কোন ডিগ্রির polynomial হবে (1 = linear, 2 = quadratic) |

---

## ✅ উপসংহার (Summary Table)

| Stat Transform | কাজ                       | গুরুত্বপূর্ণ প্যারামিটার    |
| -------------- | ------------------------- | --------------------------- |
| `Agg()`        | ক্যাটাগরির গড়/মোট/median  | `stat`, `error`, `ci`       |
| `Est()`        | Continuous estimation     | `stat`, `n_bins`, `ci`      |
| `Hist()`       | Histogram bin & count     | `bins`, `stat`, `normalize` |
| `KDE()`        | Smooth distribution curve | `bw`, `cut`, `cumulative`   |
| `Count()`      | Category-wise count       | `normalize`                 |
| `Perc()`       | Percentile line           | `q`                         |
| `PolyFit()`    | Polynomial regression fit | `degree`                    |

---
import seaborn as sns
import matplotlib.pyplot as plt
import streamlit as st
from seaborn.objects import Plot, Dot, Dots, Line, Lines, Path, Paths, Dash, Bar, Bars, Range, Area, Band, Text
from seaborn.objects import Agg, Est, Hist, KDE, Count, Perc, PolyFit
import pandas as pd

# Load dataset
tips = sns.load_dataset("tips")

st.title("📊 Seaborn All-in-One Plots Dashboard")
st.write("Visualize categorical, distribution, regression, utility, object-oriented, and stat transform plots using the 'tips' dataset.")

# ---------------- Seaborn Statistical Transforms ----------------
st.header("🔢 Seaborn Statistical Transforms Examples")

# Agg() - Category-wise mean using Bars
st.subheader("Agg() - Aggregation (mean)")
p1 = Plot(tips, x="day", y="total_bill").add(Bars(), Agg(stat="mean"))
st.pyplot(p1.figure)

# Est() - Continuous estimation with mean
st.subheader("Est() - Estimation over bins")
p2 = Plot(tips, x="total_bill", y="tip").add(Line(), Est(stat="mean", n_bins=20))
st.pyplot(p2.figure)

# Hist() - Histogram binning on continuous variable
st.subheader("Hist() - Histogram binning")
p3 = Plot(tips, x="total_bill").add(Bars(), Hist(bins=15, stat="count"))
st.pyplot(p3.figure)

# KDE() - Kernel density estimation (smooth distribution curve)
st.subheader("KDE() - Kernel density estimate")
p4 = Plot(tips, x="total_bill").add(Line(), KDE(bw=1.5))
st.pyplot(p4.figure)

# Count() - Count occurrences in each category
st.subheader("Count() - Frequency count")
p5 = Plot(tips, x="day").add(Bars(), Count())
st.pyplot(p5.figure)

# Perc() - Percentile line
st.subheader("Perc() - Percentile (50th)")
p6 = Plot(tips, x="total_bill", y="tip").add(Line(), Perc(q=50))
st.pyplot(p6.figure)

# PolyFit() - Polynomial regression (degree 2)
st.subheader("PolyFit() - Polynomial fitting")
p7 = Plot(tips, x="total_bill", y="tip").add(Line(), PolyFit(degree=2))
st.pyplot(p7.figure)

✅ অন্তর্ভুক্ত উদাহরণসমূহ:
Agg() – ক্যাটাগরি অনুযায়ী mean aggregation (Bars() সহ)

Est() – Continuous bin estimate (e.g., mean of y over x bins)

Hist() – Histogram binning using Bars() (like histplot)

KDE() – Kernel Density estimation (smooth curve)

Count() – প্রতিটি ক্যাটাগরিতে কতবার মান এসেছে তা গণনা

Perc() – Percentile (e.g. median line)

PolyFit() – Polynomial regression fit (e.g. degree=2 for curve)


### **Position Adjustments**

* `Jitter()` – Add random noise to prevent overlap
* `Dodge()` – Offset elements to avoid overlap
* `Norm()` – Normalize
* `Shift()` – Shift plot elements
* `Stack()` – Stack elements

### **Scales**

* `Continuous()`, `Nominal()`, `Temporal()`, `Boolean()` – Used for axis scaling

---
নিচে **Seaborn’s Object-Oriented Interface (`seaborn.objects`)**-এর **Position Adjustments** ও **Scales** এর প্রতিটি উপাদানের বিস্তারিত ব্যাখ্যা দেওয়া হলো — প্রতিটির **কাজ (task)**, **প্যারামিটার (parameter)**, এবং **প্যারামিটার ভ্যালু কী বোঝায়** সবকিছু বাংলায়:

---

## 🎯 **Position Adjustments**

`Plot().add(<Mark>(), <PositionTransform>)`
এগুলি plot-এর মধ্যে overlapping বা সাজানোর সমস্যাগুলো সমাধানে ব্যবহৃত হয়।

---

### 1. 🔹 `Jitter()`

✅ **কাজ:**
Categorical axis-এ একাধিক ডেটা পয়েন্ট **একই অবস্থানে থাকলে** overlapping হয়। `Jitter()` এলোমেলোভাবে সেগুলিকে **অল্প একটু সরিয়ে** দেখায়।

✅ **সিনট্যাক্স:**

```python
from seaborn.objects import Plot, Dot, Jitter
Plot(data=tips, x='day', y='total_bill').add(Dot(), Jitter(width=0.3))
```

📌 **প্যারামিটার:**

| Parameter | মান                    | কাজ                             |
| --------- | ---------------------- | ------------------------------- |
| `width`   | সংখ্যা (e.g. 0.2, 0.5) | X-অক্ষ বরাবর কতটা সরানো হবে     |
| `height`  | সংখ্যা                 | Y-অক্ষ বরাবর jitter করার পরিমাণ |

---

### 2. 🔹 `Dodge()`

✅ **কাজ:**
Categorical ভ্যালু যদি **multiple hue/group** থাকে, তাহলে `Dodge()` তাদের **একই category-র মধ্যে আলাদা করে** side-by-side সাজায়।

✅ **সিনট্যাক্স:**

```python
from seaborn.objects import Plot, Bars, Dodge
Plot(tips, x='day', y='total_bill', color='sex').add(Bars(), Dodge())
```

📌 **প্যারামিটার:**

| Parameter | মান    | কাজ                                     |
| --------- | ------ | --------------------------------------- |
| `amount`  | সংখ্যা | এক গ্রুপকে আরেকটির থেকে কতটা দূরে সরাবে |

---

### 3. 🔹 `Norm()`

✅ **কাজ:**
Data values কে **normalize (0 থেকে 1)** স্কেলে রূপান্তর করে। সাধারণত size/color/map জন্য ব্যবহৃত হয়।

✅ **সিনট্যাক্স:**

```python
from seaborn.objects import Plot, Dots, Norm
Plot(tips, x='day', y='total_bill', size='tip').add(Dots(), Norm())
```

📌 **প্যারামিটার:**

| Parameter | মান                    | কাজ                        |
| --------- | ---------------------- | -------------------------- |
| `axis`    | `'x'`, `'y'`, `'size'` | কোন axis normalize হবে     |
| `scale`   | Tuple (min, max)       | normalize value এর পরিসীমা |

---

### 4. 🔹 `Shift()`

✅ **কাজ:**
Plot elements-কে নির্দিষ্টভাবে **এক্স-অক্ষ বা ওয়াই-অক্ষ বরাবর সরিয়ে** দেয়।

✅ **সিনট্যাক্স:**

```python
from seaborn.objects import Plot, Dots, Shift
Plot(tips, x='day', y='total_bill').add(Dots(), Shift(x=0.2))
```

📌 **প্যারামিটার:**

| Parameter | মান    | কাজ                        |
| --------- | ------ | -------------------------- |
| `x`       | সংখ্যা | X-অক্ষ বরাবর কত দূরে সরাবে |
| `y`       | সংখ্যা | Y-অক্ষ বরাবর সরাবে কি না   |

---

### 5. 🔹 `Stack()`

✅ **কাজ:**
Elements যেমন bar/area কে **stack** করে, অর্থাৎ একটির ওপর আরেকটি।

✅ **সিনট্যাক্স:**

```python
from seaborn.objects import Plot, Bars, Stack
Plot(tips, x='day', y='total_bill', color='sex').add(Bars(), Stack())
```

📌 **প্যারামিটার:**

| Parameter | মান              | কাজ                              |
| --------- | ---------------- | -------------------------------- |
| `order`   | callable or list | stacking-এর অর্ডার নির্ধারণ করতে |

---

## 🧮 **Scales**

Scales নির্ধারণ করে **axis বা aesthetic mapping** কিভাবে কাজ করবে।

---

### 1. 🔸 `Continuous()`

✅ **কাজ:**
X বা Y axis এ **continuous numeric values** এর জন্য।

📌 উদাহরণ:

```python
from seaborn.objects import Plot, Line
from seaborn.objects.scales import Continuous
Plot(tips, x='total_bill', y='tip', xscale=Continuous()).add(Line())
```

---

### 2. 🔸 `Nominal()`

✅ **কাজ:**
Categorical (non-numeric) ডেটার জন্য।

📌 উদাহরণ:

```python
from seaborn.objects import Plot, Bars
from seaborn.objects.scales import Nominal
Plot(tips, x='day', y='total_bill', xscale=Nominal()).add(Bars())
```

---

### 3. 🔸 `Temporal()`

✅ **কাজ:**
Date/time-based axis scaling (e.g., timestamps, dates)।

📌 উদাহরণ:

```python
from seaborn.objects import Plot, Line
from seaborn.objects.scales import Temporal
Plot(df, x='timestamp', y='value', xscale=Temporal()).add(Line())
```

---

### 4. 🔸 `Boolean()`

✅ **কাজ:**
True/False টাইপ ডেটার জন্য axis scale।

📌 উদাহরণ:

```python
from seaborn.objects import Plot, Dot
from seaborn.objects.scales import Boolean
Plot(data, x='active', y='value', xscale=Boolean()).add(Dot())
```

---

## ✅ Summary Table

| Component      | কাজ                         | মূল Parameter     |
| -------------- | --------------------------- | ----------------- |
| `Jitter()`     | Overlap ঠেকাতে random সরানো | `width`, `height` |
| `Dodge()`      | Group-wise offset           | `amount`          |
| `Norm()`       | Scaling (0–1)               | `axis`, `scale`   |
| `Shift()`      | Manual shift                | `x`, `y`          |
| `Stack()`      | Elements stack করা          | `order`           |
| `Continuous()` | Continuous axis scale       | —                 |
| `Nominal()`    | Categorical scale           | —                 |
| `Temporal()`   | Date/time scale             | —                 |
| `Boolean()`    | True/False scale            | —                 |

---

import seaborn as sns
import matplotlib.pyplot as plt
import streamlit as st
from seaborn.objects import Plot, Dot, Dots, Line, Lines, Path, Paths, Dash, Bar, Bars, Range, Area, Band, Text
from seaborn.objects import Agg, Est, Hist, KDE, Count, Perc, PolyFit
from seaborn.objects import Jitter, Dodge, Norm, Shift, Stack
from seaborn.objects.scales import Continuous, Nominal, Temporal, Boolean
import pandas as pd

# Load dataset
tips = sns.load_dataset("tips")

st.title("📊 Seaborn All-in-One Plots Dashboard")
st.write("Visualize categorical, distribution, regression, utility, object-oriented, stat transform, position adjustment and scale-based plots using the 'tips' dataset.")

# ---------------- Position Adjustments ----------------
st.header("🧲 Position Adjustments")

# Jitter()
st.subheader("Jitter() - Add random noise to reduce overlap")
p1 = Plot(data=tips, x="day", y="total_bill").add(Dot(), Jitter(width=0.3, height=0.1))
st.pyplot(p1.figure)

# Dodge()
st.subheader("Dodge() - Offset elements to avoid overlap")
p2 = Plot(data=tips, x="day", y="total_bill", color="sex").add(Bars(), Dodge())
st.pyplot(p2.figure)

# Norm()
st.subheader("Norm() - Normalize size or color")
p3 = Plot(data=tips, x="day", y="total_bill", size="tip").add(Dots(), Norm())
st.pyplot(p3.figure)

# Shift()
st.subheader("Shift() - Move plot elements by amount")
p4 = Plot(data=tips, x="day", y="total_bill").add(Dots(), Shift(x=0.2))
st.pyplot(p4.figure)

# Stack()
st.subheader("Stack() - Stack overlapping elements")
p5 = Plot(data=tips, x="day", y="total_bill", color="sex").add(Bars(), Stack())
st.pyplot(p5.figure)

# ---------------- Scales ----------------
st.header("📐 Axis Scales")

# Continuous()
st.subheader("Continuous() - Numeric scaling")
p6 = Plot(data=tips, x="total_bill", y="tip", xscale=Continuous()).add(Line())
st.pyplot(p6.figure)

# Nominal()
st.subheader("Nominal() - Categorical scaling")
p7 = Plot(data=tips, x="day", y="total_bill", xscale=Nominal()).add(Bars())
st.pyplot(p7.figure)

# Temporal()
st.subheader("Temporal() - Time-based scaling")
time_df = pd.DataFrame({
    "date": pd.date_range("2023-01-01", periods=5),
    "value": [5, 7, 6, 9, 8]
})
p8 = Plot(time_df, x="date", y="value", xscale=Temporal()).add(Line())
st.pyplot(p8.figure)

# Boolean()
st.subheader("Boolean() - True/False scaling")
bool_df = pd.DataFrame({"active": [True, False, True, False], "value": [5, 7, 6, 9]})
p9 = Plot(bool_df, x="active", y="value", xscale=Boolean()).add(Dot())
st.pyplot(p9.figure)


✅ অন্তর্ভুক্ত উদাহরণ:
📍 Position Adjustments
Jitter() – Overlapping পয়েন্ট সরিয়ে দেয়

Dodge() – আলাদা গ্রুপকে side-by-side করে

Norm() – Size বা color কে 0–1 স্কেলে normalize করে

Shift() – X বা Y-এ প্লট এলিমেন্ট সরিয়ে নেয়

Stack() – Bar/area কে একটার ওপর আরেকটা রাখে

🧭 Scales
Continuous() – Numeric axis scale (default)

Nominal() – Categorical scaling

Temporal() – Date/time-based scaling

Boolean() – True/False binary axis

