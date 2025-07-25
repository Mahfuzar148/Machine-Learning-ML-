### 🧠 **Unsupervised Learning** – বিস্তারিত ব্যাখ্যা (With Examples)

---

## 🔍 কী হলো Unsupervised Learning?

**Unsupervised Learning** হলো Machine Learning-এর একটি গুরুত্বপূর্ণ শাখা যেখানে:

* ডেটা-তে **কোনো label বা category দেওয়া থাকে না**।
* এলগরিদম নিজে নিজে ডেটা থেকে **pattern বা structure** বের করে।
* এটি মূলত **observation বা similarity**-র উপর ভিত্তি করে কাজ করে।

📌 **মুখ্য উদ্দেশ্য**:

> ডেটার গঠন (structure) বা লুকানো সম্পর্ক (hidden patterns) আবিষ্কার করা।

---

## 🆚 Supervised vs. Unsupervised Learning

| বিষয়     | Supervised Learning                 | Unsupervised Learning                    |
| -------- | ----------------------------------- | ---------------------------------------- |
| Data     | Labeled data                        | Unlabeled data                           |
| Aim      | Prediction                          | Pattern discovery                        |
| Output   | Class or value                      | Cluster or structure                     |
| Examples | Email spam detection, Loan approval | Customer segmentation, Anomaly detection |

---

## 🧱 কিভাবে কাজ করে?

Unsupervised Learning এলগরিদম **ডেটার ফিচার/characteristics** বিশ্লেষণ করে তাদের মধ্যে সাদৃশ্য খোঁজে। যারা পরস্পরের মতো, তাদের একত্র করে বা অন্যদের থেকে আলাদা করে।

---

## 🔍 গুরুত্বপূর্ণ Unsupervised Learning Techniques

### 1. **Clustering (ক্লাস্টারিং)**

ডেটাকে **গ্রুপে ভাগ** করা যাতে গ্রুপের ভেতরের আইটেমগুলো একে অপরের সাথে বেশি মিল রাখে।

* 📌 Algorithm: **K-Means, DBSCAN, Hierarchical Clustering**
* 🧠 Example: গ্রাহকদের তাদের ব্যয় করার ধরণ অনুযায়ী ভাগ করা।

---

### 2. **Dimensionality Reduction (মাত্রা হ্রাস)**

ডেটার ফিচার সংখ্যা কমিয়ে **visualization** বা **performance** বাড়ানো।

* 📌 Algorithm: **PCA (Principal Component Analysis), t-SNE**
* 🧠 Example: 100-dimensional ডেটাকে 2D/3D-তে আনিয়ে গ্রাফে দেখানো।

---

### 3. **Anomaly Detection (ব্যতিক্রম চিহ্নিতকরণ)**

সাধারণ ডেটার তুলনায় **বিচিত্র বা অস্বাভাবিক** প্যাটার্ন খোঁজা।

* 📌 Algorithm: **Isolation Forest, One-Class SVM**
* 🧠 Example: Online ব্যাংকিং-এ fraud ট্রানজ্যাকশন খোঁজা।

---

## ✅ বাস্তব উদাহরণ

### 🎯 Example 1: Customer Segmentation

একটি ই-কমার্স কোম্পানি বিভিন্ন গ্রাহকের বয়স ও খরচের ইতিহাস বিশ্লেষণ করে তাদের সেগমেন্ট করে:

* **Cluster 1**: Student buyers (কম বয়স, কম খরচ)
* **Cluster 2**: Working professionals (মধ্যবয়সী, মাঝারি খরচ)
* **Cluster 3**: High-spenders (উচ্চ আয়, বেশি খরচ)

📌 K-Means এলগরিদম ব্যবহার করে করা যায়।

---

### 🎯 Example 2: Document Topic Modeling

একটি নিউজ ওয়েবসাইটের হাজার হাজার আর্টিকেলের মধ্যে থেকে স্বয়ংক্রিয়ভাবে তাদের **কোন টপিকের ওপর লেখা তা খুঁজে বের করা**।

📌 Latent Dirichlet Allocation (LDA) ব্যবহার করে করা যায়।

---

## 💻 Python Code (K-Means Clustering)

```python
from sklearn.cluster import KMeans
import matplotlib.pyplot as plt
import pandas as pd

# Sample data
data = {'Feature1': [1, 2, 3, 8, 9, 10], 'Feature2': [2, 1, 3, 9, 8, 10]}
df = pd.DataFrame(data)

# KMeans clustering
kmeans = KMeans(n_clusters=2)
df['Cluster'] = kmeans.fit_predict(df)

# Plot
plt.scatter(df['Feature1'], df['Feature2'], c=df['Cluster'], cmap='rainbow')
plt.title("Simple K-Means Clustering (Unsupervised Learning)")
plt.xlabel("Feature1")
plt.ylabel("Feature2")
plt.show()
```

---

## 📦 কোথায় ব্যবহার হয় (Real-Life Use Cases)

| Sectors          | Use Case                     |
| ---------------- | ---------------------------- |
| মার্কেটিং        | গ্রাহক বিভাজন (Segmentation) |
| ব্যাংকিং         | ফ্রড ডিটেকশন                 |
| ই-কমার্স         | রিকমেন্ডেশন সিস্টেম          |
| চিকিৎসা          | রোগ নির্ণয়ের ক্লাস্টারিং     |
| সাইবার সিকিউরিটি | অস্বাভাবিক প্রবণতা শনাক্ত    |

---

## 🔚 উপসংহার

Unsupervised Learning ডেটার অজানা কাঠামো বুঝে **জ্ঞান আহরণে শক্তিশালী** একটি পদ্ধতি। এটি যেখানে লেবেল না থাকলেও আমরা ডেটা থেকে ইনসাইট পেতে চাই, সেখানে সবচেয়ে বেশি কার্যকর।

---

