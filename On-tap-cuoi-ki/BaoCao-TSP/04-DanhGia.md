# PHẦN 4: ĐỘ ĐO VÀ ĐÁNH GIÁ ĐỘ PHỨC TẠP
# (Tiêu chí đánh giá chất lượng thuật toán TSP)

---

## 📚 MỤC LỤC

1. [Độ đo chất lượng nghiệm](#1-độ-đo-chất-lượng-nghiệm)
2. [Đánh giá độ phức tạp thuật toán](#2-đánh-giá-độ-phức-tạp-thuật-toán)
3. [Tiêu chí so sánh các thuật toán](#3-tiêu-chí-so-sánh-các-thuật-toán)

---

# 1. ĐỘ ĐO CHẤT LƯỢNG NGHIỆM

## 1.1. Tổng chi phí đường đi (Tour Cost)

### 📌 Định nghĩa

$$\text{Tour Cost} = \sum_{i=1}^{n-1} D[p_i][p_{i+1}] + D[p_n][p_1]$$

Với $(p_1, p_2, ..., p_n)$ là thứ tự thăm các thành phố.

### 📌 Ý nghĩa

- **Đây là mục tiêu chính** cần tối thiểu hóa
- Đơn vị: km, m, hoặc đơn vị khoảng cách tùy bài toán

### 📌 Ví dụ

Tour: 0 → 3 → 2 → 1 → 4 → 0
Chi phí: D[0][3] + D[3][2] + D[2][1] + D[1][4] + D[4][0]
       = 3 + 3 + 5 + 3 + 4 = **18**

---

## 1.2. Gap so với nghiệm tối ưu

### 📌 Định nghĩa

$$\text{Gap (\%)} = \frac{\text{Cost}_{found} - \text{Cost}_{optimal}}{\text{Cost}_{optimal}} \times 100\%$$

### 📌 Ý nghĩa

- Đo **độ chênh lệch** giữa nghiệm tìm được và nghiệm tối ưu
- Gap = 0% → Nghiệm tìm được **chính xác tối ưu**
- Gap = 10% → Nghiệm tìm được **tệ hơn 10%** so với tối ưu

### 📌 Ví dụ

| Thuật toán | Chi phí tìm được | Nghiệm tối ưu | Gap |
|:---|:---:|:---:|:---:|
| Brute Force | 80 | 80 | **0%** |
| Nearest Neighbor | 95 | 80 | 18.75% |
| Genetic Algorithm | 82 | 80 | 2.5% |

> [!NOTE]
> Gap chỉ tính được khi **biết nghiệm tối ưu** (từ Brute Force hoặc TSPLIB).

---

## 1.3. Độ lệch chuẩn (Standard Deviation)

### 📌 Định nghĩa

Với các thuật toán ngẫu nhiên (như GA), chạy nhiều lần sẽ cho kết quả khác nhau.

$$\sigma = \sqrt{\frac{1}{N}\sum_{i=1}^{N}(x_i - \bar{x})^2}$$

### 📌 Ý nghĩa

- Đánh giá **độ ổn định** của thuật toán
- σ nhỏ → Kết quả **nhất quán** qua nhiều lần chạy
- σ lớn → Kết quả **dao động nhiều**, không đáng tin cậy

---

# 2. ĐÁNH GIÁ ĐỘ PHỨC TẠP THUẬT TOÁN

## 2.1. Độ phức tạp thời gian

| Thuật toán | Độ phức tạp | Giải thích |
|:---|:---:|:---|
| **Brute Force** | O(n!) | Duyệt tất cả (n-1)! hoán vị |
| **Nearest Neighbor** | O(n²) | n bước × tìm min trong n phần tử |
| **Genetic Algorithm** | O(g × p × n) | g thế hệ × p cá thể × n thao tác |

### 📊 So sánh bằng số liệu

| n | Brute Force | Nearest Neighbor | GA (g=100, p=50) |
|:---:|:---:|:---:|:---:|
| 10 | 362,880 | 100 | 50,000 |
| 20 | 1.2 × 10¹⁷ | 400 | 100,000 |
| 50 | Không khả thi | 2,500 | 250,000 |
| 100 | Không khả thi | 10,000 | 500,000 |

---

## 2.2. Độ phức tạp bộ nhớ

| Thuật toán | Bộ nhớ | Giải thích |
|:---|:---:|:---|
| **Brute Force** | O(n) | Lưu 1 tour tại mỗi thời điểm |
| **Nearest Neighbor** | O(n) | Lưu visited set + tour |
| **Genetic Algorithm** | O(p × n) | Lưu p cá thể, mỗi cá thể n phần tử |

---

## 2.3. Thời gian chạy thực tế

| n | Brute Force | Nearest Neighbor | GA |
|:---:|:---:|:---:|:---:|
| 10 | 0.01s | < 0.001s | 0.1s |
| 15 | 10s | < 0.001s | 0.2s |
| 20 | Không khả thi | 0.001s | 0.5s |
| 50 | - | 0.01s | 2s |
| 100 | - | 0.05s | 10s |

---

# 3. TIÊU CHÍ SO SÁNH CÁC THUẬT TOÁN

## 3.1. Ma trận đánh giá

| Tiêu chí | Trọng số | Brute Force | Nearest Neighbor | Genetic Algorithm |
|:---|:---:|:---:|:---:|:---:|
| Chất lượng nghiệm | 40% | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐⭐ |
| Tốc độ | 30% | ⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ |
| Khả năng mở rộng | 20% | ⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ |
| Dễ cài đặt | 10% | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ |

## 3.2. Trade-off: Chất lượng vs Thời gian

```
Chất lượng nghiệm
     ^
100% │ ● Brute Force
     │
 95% │           ● Genetic Algorithm
     │
 80% │                    ● Nearest Neighbor
     │
     +─────────────────────────────────────> Thời gian
            Nhanh                  Chậm
```

## 3.3. Kết luận đánh giá

| Thuật toán | Phù hợp cho | Không phù hợp cho |
|:---|:---|:---|
| **Brute Force** | n ≤ 12, cần nghiệm chính xác | Bài toán lớn |
| **Nearest Neighbor** | Ước lượng nhanh, n lớn | Cần kết quả chính xác |
| **Genetic Algorithm** | Cân bằng chất lượng/tốc độ | Hạn chế thời gian rất ngắn |

---

*Hết Phần 4 - Độ đo và đánh giá độ phức tạp*
