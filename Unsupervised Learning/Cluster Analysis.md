---

# 📘 Cluster Analysis: বিস্তারিত ব্যাখ্যা

---

## 📌 1. What is a Cluster?

একটি **Cluster** হলো ডেটার এমন একটি গুচ্ছ (set), যেখানে একই গুচ্ছের ডেটাগুলো পরস্পরের সঙ্গে বেশি **similar (সাদৃশ্যপূর্ণ)** এবং অন্য গুচ্ছের ডেটার থেকে তুলনামূলকভাবে **dissimilar (বিচ্ছিন্ন/অসাদৃশ্যপূর্ণ)**।

---

## 🔍 2. What is Cluster Analysis?

**Cluster Analysis** (বা **Clustering**) হলো এমন একটি পদ্ধতি যা unlabeled ডেটা গুলোকে একই বৈশিষ্ট্যের ভিত্তিতে বিভাজন করে। এটি unsupervised learning-এর অন্তর্ভুক্ত।

---

## 🧠 3. Unsupervised Learning

Unsupervised Learning-এ মডেলকে এমন ডেটা দেওয়া হয় যার কোনো নির্দিষ্ট লেবেল থাকে না। Clustering এই শ্রেণির অন্তর্গত।

---

## 💡 4. Applications of Clustering

| Sector           | Example                      |
| ---------------- | ---------------------------- |
| Marketing        | Customer segmentation        |
| E-commerce       | Product recommendation       |
| Healthcare       | Disease type classification  |
| Image Processing | Object or color segmentation |

---

## 🧪 প্র্যাকটিক্যাল উদাহরণ: প্রোডাক্ট কাস্টারিং

| Products | Quantity | Price(K) |
| -------- | -------- | -------- |
| FaceWash | 3        | 7        |
| Cream    | 5        | 4        |
| Shoes    | 4        | 3        |
| Bags     | 4        | 8        |
| Jacket   | 6        | 3        |
| Shirt    | 3        | 8        |

---

### 📌 Step 1: Initial Centroids

* C₁ = (3, 7) → FaceWash
* C₂ = (5, 4) → Cream

---

### ✏️ Step 2: Distance Calculation (Using Euclidean Distance)

**FaceWash** → (3,7)

* Distance from C₁: 0 → Assign to C₁
* Distance from C₂: √\[(5−3)² + (4−7)²] = √(4 + 9) = √13 ≈ 3.6

**Cream** → (5,4)

* Distance from C₁: √\[(5−3)² + (4−7)²] = √13 ≈ 3.6
* Distance from C₂: 0 → Assign to C₂

**Shoes** → (4,3)

* Distance from C₁: √\[(4−3)² + (3−7)²] = √(1 + 16) = √17 ≈ 4.12
* Distance from C₂: √\[(4−5)² + (3−4)²] = √(1 + 1) = √2 ≈ 1.41 → C₂

🔄 **New Centroid C₂** = \[(5+4)/2, (4+3)/2] = (4.5, 3.5)

---

### 🔁 Step 3: Bags → (4, 8)

* C₁ = (3, 7), C₂ = (4.5, 3.5)
* Distance from C₁ = √\[(4−3)² + (8−7)²] = √2 ≈ 1.41 → C₁
* Distance from C₂ = √\[(4−4.5)² + (8−3.5)²] = √20.5 ≈ 4.53

📌 New C₁ = \[(3+4)/2, (7+8)/2] = (3.5, 7.5)

---

### 🧠 Step 4: Jacket → (6, 3)

* Distance from C₁: √\[(6−3.5)² + (3−7.5)²] = √26.5 ≈ 5.15
* Distance from C₂: √\[(6−4.5)² + (3−3.5)²] = √2.5 ≈ 1.58 → C₂

📌 New C₂ = \[(5+4+6)/3, (4+3+3)/3] = (5, 3.33)

---

### 👕 Step 5: Shirt → (3, 8)

* Distance from C₁: √\[(3−3.5)² + (8−7.5)²] = √0.5 ≈ 0.70 → C₁
* Distance from C₂: √\[(3−5)² + (8−3.33)²] = √25.78 ≈ 5.08

📌 New C₁ = \[(3+4+3)/3, (7+8+8)/3] = (3.33, 7.67)

---

## 📈 Elbow Method

### 📌 লক্ষ্য:

সঠিক K (ক্লাস্টারের সংখ্যা) নির্ধারণ করা যেখানে WCSS (Within Cluster Sum of Squares) হঠাৎ কমে যাওয়া বন্ধ করে দেয়। Elbow method ব্যবহার করে এই K নির্ধারণ করা হয়।

### 📖 বিস্তারিত ব্যাখ্যা:

Elbow Method হল একটি গ্রাফিক্যাল টুল যা K-Means clustering-এ ব্যবহার করা হয়। এখানে আমরা বিভিন্ন K মানের জন্য WCSS হিসাব করি এবং তা গ্রাফে উপস্থাপন করি। K এর মান বৃদ্ধির সঙ্গে সঙ্গে WCSS কমতে থাকে, কারণ প্রতিটি ক্লাস্টারে পয়েন্ট কম থাকায় তাদের mean-এর সাথে দূরত্ব কমে যায়।

তবে একটি পর্যায়ে গিয়ে WCSS কমার হার হঠাৎ কমে যায়—এই পরিবর্তনের স্থানটিকে বলা হয় **"Elbow point"** এবং সেখানেই আমরা কাকে Optimal number of clusters ধরে নিই।

### 📐 সূত্র:

WCSS(k) = ∑(j=1 থেকে k) ∑(xi ∈ cluster j) || xi − x̄j ||²
যেখানে xi হলো cluster-এর প্রতিটি পয়েন্ট এবং x̄j হলো সেই cluster-এর mean।

### 📊 গ্রাফ বিশ্লেষণ:

* **X-axis:** number of clusters (K)
* **Y-axis:** WCSS
* **Elbow Point:** যেখানে গ্রাফে হঠাৎ বাঁক আসে (elbow-এর মতো), সেখানেই Optimal K

### 🔍 উদাহরণ:

### 📌 WCSS হিসাব করার বাস্তব উদাহরণ:

ধরা যাক আমাদের কাছে K = 2 ক্লাস্টার আছে:

* Cluster 1: Points → (3,7), (4,8), (3,8)
* Cluster 2: Points → (5,4), (4,3), (6,3)

Centroid C₁ = (3.33, 7.67)
Centroid C₂ = (5, 3.33)

**WCSS = Cluster 1 এর WCSS + Cluster 2 এর WCSS**

### 🧮 Cluster 1 WCSS Calculation:

1. Distance² for (3,7):
   $(3−3.33)² + (7−7.67)² = 0.1089 + 0.4489 = 0.5578$
2. Distance² for (4,8):
   $(4−3.33)² + (8−7.67)² = 0.4489 + 0.1089 = 0.5578$
3. Distance² for (3,8):
   $(3−3.33)² + (8−7.67)² = 0.1089 + 0.1089 = 0.2178$

📌 Cluster 1 WCSS = 0.5578 + 0.5578 + 0.2178 = **1.3334**

---

### 🧮 Cluster 2 WCSS Calculation:

1. (5,4): (5−5)² + (4−3.33)² = 0 + 0.4489 = 0.4489
2. (4,3): (4−5)² + (3−3.33)² = 1 + 0.1089 = 1.1089
3. (6,3): (6−5)² + (3−3.33)² = 1 + 0.1089 = 1.1089

📌 Cluster 2 WCSS = 0.4489 + 1.1089 + 1.1089 = **2.6667**

---

✅ **Total WCSS = 1.3334 + 2.6667 = 4.0001**

এভাবে বিভিন্ন K মানের জন্য একইভাবে WCSS হিসাব করা হয় এবং Elbow Graph আঁকা হয়।
K = 1 → WCSS = 8000
K = 2 → WCSS = 3000
K = 3 → WCSS = 1000 ← ⬅️ Elbow point
K = 4 → WCSS = 850
K = 5 → WCSS = 830

এখানে K = 3 তে WCSS কমে যাওয়ার হার হঠাৎ কমে যায়, তাই 3 হলো Optimal cluster সংখ্যা।

---

## 📊 Scatter Plot Code (Python)

```python
plt.xlabel('Quantity')
plt.ylabel('Price in Thousand (Taka)')
plt.scatter(dataframe['Quantity'], dataframe['Price(K)'], marker='+', color='blue')
```

📌 এটি প্রোডাক্টগুলোর Quantity ও Price এর ভিত্তিতে distribution দেখায়।

---

## ✅ সারসংক্ষেপ

| বিষয়              | ব্যাখ্যা                         |
| ------------------ | -------------------------------- |
| Algorithm          | K-Means Clustering               |
| Distance Metric    | Euclidean Distance (Mostly Used) |
| Cluster Evaluation | Elbow Method                     |
| Visualization      | Scatter Plot                     |

---
