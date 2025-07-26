---

# 📘 Cluster Analysis: বিস্তারিত ব্যাখ্যা

---

## 📌 1. What is a Cluster?

একটি **Cluster** হলো ডেটার এমন একটি গুচ্ছ (set), যেখানে একই গুচ্ছের ডেটাগুলো পরস্পরের সঙ্গে বেশি **similar (সাদৃশ্যপূর্ণ)** এবং অন্য গুচ্ছের ডেটার থেকে তুলনামূলকভাবে **dissimilar (বিচ্ছিন্ন/অসাদৃশ্যপূর্ণ)**।

* উদাহরণস্বরূপ: যদি কিছু গ্রাহকের বয়স ও আয় অনুযায়ী তাদের শ্রেণিবদ্ধ করি, তাহলে ছাত্র, চাকুরিজীবী এবং অবসরপ্রাপ্তদের মধ্যে স্বাভাবিকভাবে আলাদা গ্রুপ তৈরি হবে।

---

## 🔍 2. What is Cluster Analysis?

**Cluster Analysis** (বা **Clustering**, **Data Segmentation**) হলো এমন একটি পদ্ধতি যা:

* ডেটার মধ্যে **সাদৃশ্য (similarity)** নির্ধারণ করে।
* সেই ভিত্তিতে ডেটাগুলোকে **অটো ক্লাস্টারে ভাগ করে**।
* এটি **Unsupervised Learning**-এর একটি অংশ, যেখানে **লেবেল (labels)** দেওয়া থাকে না।

📌 লক্ষ্য: ডেটার ভেতরের লুকানো গঠন (structure) বুঝতে সাহায্য করা।

---

## 🧠 3. Unsupervised Learning

* এখানে কোনো **predefined class বা label** নেই।
* মেশিন **observation-এর মাধ্যমে শেখে**।
* Clustering হলো এই ধরনের শেখার একটি গুরুত্বপূর্ণ উদাহরণ।

---

## 💡 4. Typical Applications of Clustering

| Application Area | Example                                                 |
| ---------------- | ------------------------------------------------------- |
| Marketing        | Customer Segmentation (বিভিন্ন ধরনের গ্রাহক শনাক্ত করা) |
| Retail           | Market Basket Analysis (একসাথে কোন পণ্য কেনা হয়)        |
| Healthcare       | Patient Disease Grouping                                |
| Image Processing | Pixel-based image compression                           |
| Biology          | Genetic sequence clustering                             |

---

## 🧪 উদাহরণ: Customer Segmentation using K-Means

আমরা একটি উদাহরণ নিচ্ছি যেখানে একটি কোম্পানি গ্রাহকদের বয়স ও বার্ষিক আয় অনুযায়ী সেগমেন্ট করতে চায়।

### ✅ Python Code (Using K-Means)

```python
import pandas as pd
import matplotlib.pyplot as plt
from sklearn.cluster import KMeans

# Sample Data
data = {
    'Age': [22, 25, 47, 52, 46, 56, 55, 60, 26, 30],
    'Income': [15000, 18000, 60000, 80000, 62000, 70000, 72000, 85000, 20000, 25000]
}
df = pd.DataFrame(data)

# Apply KMeans with 3 clusters
kmeans = KMeans(n_clusters=3)
df['Cluster'] = kmeans.fit_predict(df)

# Plotting
plt.scatter(df['Age'], df['Income'], c=df['Cluster'], cmap='viridis', s=100)
plt.scatter(kmeans.cluster_centers_[:, 0], kmeans.cluster_centers_[:, 1], color='red', marker='X', s=200)
plt.xlabel('Age')
plt.ylabel('Annual Income')
plt.title('Customer Segmentation using K-Means')
plt.show()
```

### 🔍 ফলাফল বিশ্লেষণ:

* Cluster 0: তরুণ গ্রাহক, কম আয়
* Cluster 1: মধ্যবয়সী গ্রাহক, বেশি আয়
* Cluster 2: সিনিয়র গ্রাহক, মাঝারি থেকে বেশি আয়

---

## 🎯 উপসংহার

**Cluster Analysis** হলো ডেটাকে শ্রেণিবিন্যাস করার একটি অসাধারণ কৌশল, যেখানে মেশিন নিজেই ডেটার গঠন বিশ্লেষণ করে ক্লাস্টার তৈরি করে। এটি বিশেষভাবে সহায়ক যখন আমাদের কাছে পূর্বনির্ধারিত ক্লাস বা ট্যাগ থাকে না।

---

## 🧠 ১. Algorithm (KMeans)

### ✅ সংজ্ঞা:

K-Means একটি **Unsupervised Learning Algorithm**, যা ডেটাকে স্বয়ংক্রিয়ভাবে *K* সংখ্যক ক্লাস্টারে বিভক্ত করে দেয়, যেখানে প্রতিটি ক্লাস্টার মানে একরকম বৈশিষ্ট্যের ডেটা পয়েন্ট।

### 🔁 ধাপসমূহ:

1. K মান নির্ধারণ (যেমন: 3 ক্লাস্টার চাইলে K = 3)
2. K সংখ্যক **initial centroids** এলোমেলোভাবে বেছে নেওয়া
3. প্রতিটি পয়েন্টকে তার সবচেয়ে কাছের centroid অনুযায়ী ক্লাস্টারে যুক্ত করা
4. প্রতিটি ক্লাস্টারের গড় ব্যবহার করে নতুন centroid নির্ধারণ
5. যতক্ষণ না centroid পরিবর্তন হয়, ধাপ ৩ ও ৪ পুনরাবৃত্তি হয়

### 🌍 বাস্তব উদাহরণ:

**কাস্টমার সেগমেন্টেশন:**
একটি সুপারশপ তার ক্রেতাদের বয়স এবং খরচের পরিমাণের উপর ভিত্তি করে ৩ ধরনের গ্রুপে ভাগ করতে চায়:

* Cluster 1: ছাত্র (অল্প খরচ)
* Cluster 2: মধ্যবয়সী পরিবার (মাঝারি খরচ)
* Cluster 3: ধনী কাস্টমার (বেশি খরচ)

---

## 📏 ২. Metrics

### 🔹 ১. Euclidean Distance

#### ➕ সংজ্ঞা:

দুটি পয়েন্টের সরলরেখার দূরত্ব।
**Formula:**

$$
\sqrt{(x_2 - x_1)^2 + (y_2 - y_1)^2}
$$

#### 🛠️ বাস্তব উদাহরণ:

Customer A: (age 25, spending 400)
Customer B: (age 30, spending 420)

Euclidean distance:

$$
\sqrt{(30-25)^2 + (420-400)^2} = \sqrt{25 + 400} = \sqrt{425} \approx 20.61
$$

এই দূরত্ব কম হলে, তারা একই ক্লাস্টারে যাবে।

---

### 🔹 ২. Manhattan Distance

#### ➕ সংজ্ঞা:

দুটি পয়েন্টের মধ্যে **অনুভূমিক ও উল্লম্ব** দূরত্বের যোগফল।
**Formula:**

$$
|x_2 - x_1| + |y_2 - y_1|
$$

#### 🛠️ বাস্তব উদাহরণ:

Customer A: (25, 400)
Customer B: (30, 420)

Manhattan Distance:

$$
|30-25| + |420-400| = 5 + 20 = 25
$$

📌 এটি আউটলায়ার সেনসিটিভ নয় এবং জটিল শহুরে গ্রিডে কার্যকর।

---

## 📉 ৩. Elbow Method

### 🔍 উদ্দেশ্য:

উত্তম K মান (কতটি ক্লাস্টার নেবেন) নির্ধারণ করা।

### 🪜 ধাপসমূহ:

1. বিভিন্ন K মান (1 থেকে 10) দিয়ে KMeans চালানো
2. প্রতিটি K-তে **Within-Cluster-Sum-of-Squares (WCSS)** হিসাব করা
3. WCSS বনাম K-এর গ্রাফ আঁকা
4. যেখানে হঠাৎ করে WCSS কমার হার কমে যায়, সেই পয়েন্টে “elbow” দেখা যায় → এটিই সেরা K

### 📊 বাস্তব উদাহরণ:

কোনো ই-কমার্স সাইটে ৫০০ কাস্টমার আছে। তারা K=1 থেকে K=10 পর্যন্ত চেষ্টা করে দেখে:

* K=1: WCSS = 12000
* K=2: 7000
* K=3: 3500
* K=4: 1800
* K=5: 1700

এখানে Elbow point K=4, কারণ তার পর WCSS খুব কম হারে কমছে।

📌 **Python Implementation:**

```python
from sklearn.cluster import KMeans
import matplotlib.pyplot as plt

wcss = []
for i in range(1, 11):
    kmeans = KMeans(n_clusters=i, random_state=0)
    kmeans.fit(data)
    wcss.append(kmeans.inertia_)

plt.plot(range(1, 11), wcss, marker='o')
plt.title('Elbow Method')
plt.xlabel('Clusters (K)')
plt.ylabel('WCSS')
plt.show()
```

---

## 🎯 সারাংশ টেবিল:

| বিষয়              | ব্যাখ্যা                           | বাস্তব উদাহরণ                         |
| ------------------ | ---------------------------------- | ------------------------------------- |
| Algorithm          | ডেটাকে K সংখ্যক ক্লাস্টারে ভাগ করা | কাস্টমার গ্রুপিং                      |
| Euclidean Distance | সরলরেখার দূরত্ব                    | বয়স ও খরচের ভিত্তিতে কাস্টমার দূরত্ব |
| Manhattan Distance | অনুভূমিক ও উল্লম্ব দূরত্বের যোগ    | শহরের রাস্তায় নেভিগেশন               |
| Elbow Method       | সঠিক K নির্ধারণ                    | সুপারশপে কত ধরনের গ্রাহক আছে বুঝতে    |

---
