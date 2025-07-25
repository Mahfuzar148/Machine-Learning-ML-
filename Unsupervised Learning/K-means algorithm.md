
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


