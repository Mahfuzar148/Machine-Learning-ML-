---

# 📊 K-Means Clustering Step-by-Step Example with Euclidean Distance

---

## 🧮 Dataset

আমরা নিচের 6টি পয়েন্ট নিয়ে K-Means clustering প্রয়োগ করবো যেখানে $K=2$।

| x   | y  |
| --- | -- |
| 185 | 72 |
| 170 | 56 |
| 168 | 60 |
| 179 | 68 |
| 182 | 72 |
| 188 | 77 |

Initial centroids:

* $C_1 = (185, 72)$
* $C_2 = (170, 56)$

---

## 📐 Euclidean Distance Formula:

$$
D = \sqrt{(x - x_c)^2 + (y - y_c)^2}
$$

---

## 🔁 Iteration 1: Distance Calculation & Cluster Assignment

| Point (x,y) | Distance to C1 | Distance to C2 | Assigned Cluster |
| ----------- | -------------- | -------------- | ---------------- |
| (185,72)    | 0              | 21.03          | C1               |
| (170,56)    | 21.03          | 0              | C2               |
| (168,60)    | 20.81          | 4.47           | C2               |
| (179,68)    | 7.21           | 15.00          | C1               |
| (182,72)    | 3.00           | 20.00          | C1               |
| (188,77)    | 5.83           | 27.66          | C1               |

### 📌 Assigned Clusters:

* **C1**: (185,72), (179,68), (182,72), (188,77)
* **C2**: (170,56), (168,60)

---

## 🧲 New Centroid Calculation:

### ✅ For C1:

* $X = \frac{185 + 179 + 182 + 188}{4} = 183.5$
* $Y = \frac{72 + 68 + 72 + 77}{4} = 72.25$
* ⏩ New C1 = (183.5, 72.25)

### ✅ For C2:

* $X = \frac{170 + 168}{2} = 169$
* $Y = \frac{56 + 60}{2} = 58$
* ⏩ New C2 = (169, 58)

---

## 🔁 Iteration 2: Updated Distance and Assignment

| Point (x,y) | Distance to C1 | Distance to C2 | Assigned Cluster |
| ----------- | -------------- | -------------- | ---------------- |
| (185,72)    | 1.52           | 21.26          | C1               |
| (170,56)    | 21.13          | 2.24           | C2               |
| (168,60)    | 19.76          | 2.24           | C2               |
| (179,68)    | 6.19           | 14.14          | C1               |
| (182,72)    | 1.52           | 19.10          | C1               |
| (188,77)    | 6.54           | 26.87          | C1               |

✅ **Final Clusters Stable, No Change. Algorithm Converged.**

---

## 📍 Final Clusters:

* **C1** = (185,72), (179,68), (182,72), (188,77)
* **C2** = (170,56), (168,60)
* Final centroids:

  * C1 = (183.5, 72.25)
  * C2 = (169, 58)

---

## ✅ উপসংহার

* K-Means ক্লাস্টারিং ধাপে ধাপে Euclidean Distance ব্যবহার করে পয়েন্টগুলোকে নির্ধারিত ক্লাস্টারে ভাগ করে
* প্রতিবার centroid হালনাগাদ হয় এবং শেষ পর্যন্ত যখন পরিবর্তন হয় না, তখন এলগরিদম থামে
* এই উদাহরণটি খুব সহজ ও পরিষ্কারভাবে K-Means প্রক্রিয়াটি বোঝায়


---

## 🔄 K-Means Clustering: Full Process Overview

### 🎯 উদ্দেশ্য

একটি dataset-এর ডেটা পয়েন্টগুলোকে এমনভাবে ক্লাস্টারে ভাগ করা যাতে:

* একই ক্লাস্টারের পয়েন্টগুলো একে অপরের কাছাকাছি হয়।
* এক ক্লাস্টার থেকে অন্য ক্লাস্টারের দূরত্ব হয় অনেক বেশি।

---

### 📌 Step-by-Step Process

#### 1. **Initialization (Centroid নির্ধারণ)**

* প্রথমে আমরা **K মান ঠিক করি** (এখানে K=2)
* এলোমেলোভাবে 2টি পয়েন্টকে **initial centroid** ধরা হয়।

  * C1 = (185,72)
  * C2 = (170,56)

#### 2. **Distance Calculation (Iteration 1)**

* প্রতিটি পয়েন্ট থেকে C1 এবং C2-এর **Euclidean Distance** বের করা হয়।
* পয়েন্টটি যেটা কাছাকাছি, সেটিকে তার ক্লাস্টারে অন্তর্ভুক্ত করা হয়।

#### 3. **Cluster Assignment**

* প্রতিটি ডেটা পয়েন্টকে সবচেয়ে কাছের centroid অনুযায়ী **C1 অথবা C2** তে অ্যাসাইন করা হয়।

#### 4. **New Centroid Calculation**

* প্রতিটি ক্লাস্টারের নতুন centroid বের করা হয়:

  * C1-এর জন্য: ক্লাস্টারের সব x ও y গড়
  * C2-এর জন্য: ক্লাস্টারের সব x ও y গড়

#### 5. **Repeat**

* আবার নতুন centroid ব্যবহার করে distance বের করা হয়।
* যদি আগের ক্লাস্টারের সাথে নতুন ক্লাস্টার **একই থাকে** → অ্যালগরিদম থেমে যায়।
* না হলে: পুনরায় iteration চালানো হয়।

#### 6. **Convergence**

* যখন কোনো ক্লাস্টার চেঞ্জ হয় না, তখন আমরা বলি **converged** হয়েছে।

---

## 🧪 Final Result

* Iteration ২-এ কোনো ক্লাস্টার পরিবর্তন হয়নি → ✅ Converged!
* Final Centroids:

  * C1 = (183.5, 72.25)
  * C2 = (169, 58)

---

## 🧑‍💻 Python Code Implementation

```python
import numpy as np
from sklearn.cluster import KMeans
import matplotlib.pyplot as plt

# Dataset
X = np.array([
    [185, 72],
    [170, 56],
    [168, 60],
    [179, 68],
    [182, 72],
    [188, 77]
])

# Apply KMeans with 2 clusters
kmeans = KMeans(n_clusters=2, init=np.array([[185, 72], [170, 56]]), n_init=1)
kmeans.fit(X)

# Cluster assignment
labels = kmeans.labels_
centroids = kmeans.cluster_centers_

# Print outputs
print("Final Centroids:")
print(centroids)

print("\nCluster Assignments:")
for i, point in enumerate(X):
    print(f"Point {point} → Cluster {labels[i]}")

# Plotting
plt.scatter(X[:, 0], X[:, 1], c=labels, s=100, cmap='viridis')
plt.scatter(centroids[:, 0], centroids[:, 1], c='red', s=200, marker='X')
plt.title("K-Means Clustering (K=2)")
plt.xlabel("X")
plt.ylabel("Y")
plt.grid(True)
plt.show()
```

---

## ✅ Output Summary

* কোডটি আমাদের বাস্তব উদাহরণের মতোই একই ক্লাস্টারে ভাগ করবে।
* এটি দেখতে পারবে visually কোন পয়েন্ট কোন ক্লাস্টারে গেছে।
* প্রক্রিয়াটি চলবে যতক্ষণ পর্যন্ত centroid পরিবর্তন না হয়।

---

## ❓ Iteration কতবার চলে?

* এটা নির্ভর করে dataset আর initial centroid-এর উপর।
* সাধারণত 2-10 iteration এর মধ্যেই কনভার্জ করে।
* এখানে ২বার iteration হয় এবং এরপর থেমে যায়।

---

