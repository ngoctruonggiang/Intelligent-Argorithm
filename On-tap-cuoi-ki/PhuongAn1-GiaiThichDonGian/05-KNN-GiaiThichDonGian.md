# 📚 TÀI LIỆU ÔN TẬP: K-NEAREST NEIGHBOR (KNN)

## Phương án 1: Giải thích đơn giản + HƯỚNG DẪN GIẢI BÀI THI

---

> **⚠️ LƯU Ý QUAN TRỌNG:**
>
> Tài liệu này được thiết kế để bạn có thể **GIẢI ĐƯỢC BÀI THI** sau khi đọc xong.
> Mọi lý thuyết đều hướng đến việc **làm bài tập thực tế**.

---

# 📑 MỤC LỤC

1. [KNN là gì? (30 giây)](#1-knn-là-gì)
2. [Công thức khoảng cách (PHẢI THUỘC)](#2-công-thức-khoảng-cách)
3. [Quy trình giải bài KNN - 5 bước](#3-quy-trình-giải-bài-knn)
4. [BÀI MẪU: Giải đề thi thực tế](#4-bài-mẫu-giải-đề-thi-thực-tế)
5. [Bảng tra căn bậc 2](#5-bảng-tra-căn-bậc-2)
6. [Các trường hợp đặc biệt](#6-các-trường-hợp-đặc-biệt)
7. [Bài tập tự luyện](#7-bài-tập-tự-luyện)

---

# 1️⃣ KNN LÀ GÌ?

## 1.1. Định nghĩa (30 giây đọc hiểu)

**KNN = K-Nearest Neighbors = K láng giềng gần nhất**

> **Nguyên lý:** Để phân loại điểm mới, tìm K điểm gần nhất trong tập training, rồi **bỏ phiếu** - nhãn nào nhiều hơn thì gán nhãn đó.

**Ví dụ thực tế:** Bạn chuyển đến khu phố mới, muốn biết quán nào ngon:

- Hỏi 5 người hàng xóm gần nhất (K=5)
- 3 người nói quán A ngon, 2 người nói quán B
- → Kết luận: Quán A ngon (vì 3 > 2)

## 1.2. Đặc điểm quan trọng

| Đặc điểm           | Giải thích                      |
| ------------------ | ------------------------------- |
| **K là số lẻ**     | Tránh hòa phiếu (2 vs 2)        |
| **Lazy Learning**  | Không "học" gì, chỉ lưu dữ liệu |
| **Instance-based** | Dựa vào từng điểm cụ thể        |

---

# 2️⃣ CÔNG THỨC KHOẢNG CÁCH (PHẢI THUỘC!)

## 2.1. Khoảng cách Euclidean 2D

Cho 2 điểm **A(x₁, y₁)** và **B(x₂, y₂)**:

$$d(A, B) = \sqrt{(x_2 - x_1)^2 + (y_2 - y_1)^2}$$

### Ví dụ nhanh:

```
A(1, 2) và B(4, 6)

d = √[(4-1)² + (6-2)²]
  = √[3² + 4²]
  = √[9 + 16]
  = √25
  = 5
```

## 2.2. Mẹo tính nhanh

**Nhận dạng tam giác vuông đặc biệt:**

- 3² + 4² = 5² → d = 5
- 5² + 12² = 13² → d = 13
- 6² + 8² = 10² → d = 10

**Nếu không phải số đẹp:** Để nguyên √ hoặc tra bảng

---

# 3️⃣ QUY TRÌNH GIẢI BÀI KNN - 5 BƯỚC

```
┌─────────────────────────────────────────────────────────────┐
│  BƯỚC 1: Xác định K và điểm cần phân loại                   │
│                        ↓                                    │
│  BƯỚC 2: Lập bảng tính khoảng cách từ điểm mới              │
│          đến TẤT CẢ điểm trong tập training                 │
│                        ↓                                    │
│  BƯỚC 3: Sắp xếp khoảng cách từ BÉ → LỚN                    │
│                        ↓                                    │
│  BƯỚC 4: Chọn K điểm có khoảng cách NHỎ NHẤT               │
│                        ↓                                    │
│  BƯỚC 5: Đếm nhãn, gán theo ĐA SỐ                           │
└─────────────────────────────────────────────────────────────┘
```

---

# 4️⃣ BÀI MẪU: GIẢI ĐỀ THI THỰC TẾ

## 📝 ĐỀ BÀI (Giống đề thi SE313)

Cho bảng dữ liệu training:

|  #  |  X  |  Y  | Label |
| :-: | :-: | :-: | :---: |
|  1  |  2  |  8  |   A   |
|  2  |  3  |  2  |   B   |
|  3  |  4  |  1  |   C   |
|  4  | 11  |  5  |   A   |
|  5  |  5  |  6  |   A   |
|  6  |  6  |  7  |   C   |
|  7  |  7  |  3  |   C   |
|  8  |  2  |  0  |   B   |
|  9  |  4  |  1  |   B   |
| 10  |  2  |  2  |   A   |
| 11  |  8  |  6  |   B   |
| 12  |  9  |  4  |   C   |

**Yêu cầu:** Dùng KNN với **k = 5** để tìm nhãn cho:

- Điểm Q₁(1, 7)
- Điểm Q₂(6, 4)
- Điểm Q₃(2, 1)

---

## 🔷 GIẢI CHI TIẾT ĐIỂM Q₁(1, 7)

### Bước 1: Xác định

- K = 5
- Điểm cần phân loại: Q₁(1, 7)

### Bước 2: Lập bảng tính khoảng cách

|  #  | Điểm (X,Y) | Label | Công thức d = √[(X-1)² + (Y-7)²] | d²  |       d        |
| :-: | :--------: | :---: | :------------------------------: | :-: | :------------: |
|  1  |   (2, 8)   |   A   |   √[(2-1)² + (8-7)²] = √[1+1]    |  2  | **√2 ≈ 1.41**  |
|  2  |   (3, 2)   |   B   |   √[(3-1)² + (2-7)²] = √[4+25]   | 29  |   √29 ≈ 5.39   |
|  3  |   (4, 1)   |   C   |   √[(4-1)² + (1-7)²] = √[9+36]   | 45  |   √45 ≈ 6.71   |
|  4  |  (11, 5)   |   A   |  √[(11-1)² + (5-7)²] = √[100+4]  | 104 |  √104 ≈ 10.20  |
|  5  |   (5, 6)   |   A   |   √[(5-1)² + (6-7)²] = √[16+1]   | 17  | **√17 ≈ 4.12** |
|  6  |   (6, 7)   |   C   |   √[(6-1)² + (7-7)²] = √[25+0]   | 25  |  **√25 = 5**   |
|  7  |   (7, 3)   |   C   |  √[(7-1)² + (3-7)²] = √[36+16]   | 52  |   √52 ≈ 7.21   |
|  8  |   (2, 0)   |   B   |   √[(2-1)² + (0-7)²] = √[1+49]   | 50  |   √50 ≈ 7.07   |
|  9  |   (4, 1)   |   B   |   √[(4-1)² + (1-7)²] = √[9+36]   | 45  |   √45 ≈ 6.71   |
| 10  |   (2, 2)   |   A   |   √[(2-1)² + (2-7)²] = √[1+25]   | 26  |   √26 ≈ 5.10   |
| 11  |   (8, 6)   |   B   |   √[(8-1)² + (6-7)²] = √[49+1]   | 50  |   √50 ≈ 7.07   |
| 12  |   (9, 4)   |   C   |   √[(9-1)² + (4-7)²] = √[64+9]   | 73  |   √73 ≈ 8.54   |

**💡 MẸO:** Tính d² trước, so sánh d² thay vì d để tránh tính căn!

### Bước 3: Sắp xếp theo d² (tăng dần)

| Thứ tự |  #  | d²  |  d   | Label |
| :----: | :-: | :-: | :--: | :---: |
|   1    |  1  |  2  | 1.41 | **A** |
|   2    |  5  | 17  | 4.12 | **A** |
|   3    |  6  | 25  | 5.00 | **C** |
|   4    | 10  | 26  | 5.10 | **A** |
|   5    |  2  | 29  | 5.39 | **B** |
|   6    |  3  | 45  | 6.71 |   C   |
|  ...   | ... | ... | ...  |  ...  |

### Bước 4: Chọn K = 5 điểm gần nhất

5 điểm gần nhất: **#1(A), #5(A), #6(C), #10(A), #2(B)**

### Bước 5: Đếm và kết luận

| Label | Số phiếu |    Điểm     |
| :---: | :------: | :---------: |
| **A** |  **3**   | #1, #5, #10 |
|   B   |    1     |     #2      |
|   C   |    1     |     #6      |

### ✅ KẾT LUẬN: Q₁(1, 7) thuộc lớp **A** (vì 3 > 1 = 1)

---

## 🔷 GIẢI CHI TIẾT ĐIỂM Q₂(6, 4)

### Bước 2: Lập bảng tính khoảng cách

|  #  |  Điểm  | Label | (X-6)² | (Y-4)² |  d²   |    d     |
| :-: | :----: | :---: | :----: | :----: | :---: | :------: |
|  1  | (2,8)  |   A   |   16   |   16   |  32   |   5.66   |
|  2  | (3,2)  |   B   |   9    |   4    |  13   |   3.61   |
|  3  | (4,1)  |   C   |   4    |   9    |  13   |   3.61   |
|  4  | (11,5) |   A   |   25   |   1    |  26   |   5.10   |
|  5  | (5,6)  |   A   |   1    |   4    | **5** | **2.24** |
|  6  | (6,7)  |   C   |   0    |   9    | **9** | **3.00** |
|  7  | (7,3)  |   C   |   1    |   1    | **2** | **1.41** |
|  8  | (2,0)  |   B   |   16   |   16   |  32   |   5.66   |
|  9  | (4,1)  |   B   |   4    |   9    |  13   |   3.61   |
| 10  | (2,2)  |   A   |   16   |   4    |  20   |   4.47   |
| 11  | (8,6)  |   B   |   4    |   4    | **8** | **2.83** |
| 12  | (9,4)  |   C   |   9    |   0    | **9** | **3.00** |

### Bước 3 & 4: Sắp xếp và chọn K=5

| Thứ tự |  #  | d²  | Label |
| :----: | :-: | :-: | :---: |
|   1    |  7  |  2  | **C** |
|   2    |  5  |  5  | **A** |
|   3    | 11  |  8  | **B** |
|   4    |  6  |  9  | **C** |
|   5    | 12  |  9  | **C** |

### Bước 5: Đếm

| Label | Số phiếu |
| :---: | :------: |
| **C** |  **3**   |
|   A   |    1     |
|   B   |    1     |

### ✅ KẾT LUẬN: Q₂(6, 4) thuộc lớp **C**

---

## 🔷 GIẢI CHI TIẾT ĐIỂM Q₃(2, 1)

### Bước 2: Lập bảng (tính nhanh)

|  #  |  Điểm  | Label | d² = (X-2)² + (Y-1)² |
| :-: | :----: | :---: | :------------------: |
|  1  | (2,8)  |   A   |     0 + 49 = 49      |
|  2  | (3,2)  |   B   |    1 + 1 = **2**     |
|  3  | (4,1)  |   C   |    4 + 0 = **4**     |
|  4  | (11,5) |   A   |     81 + 16 = 97     |
|  5  | (5,6)  |   A   |     9 + 25 = 34      |
|  6  | (6,7)  |   C   |     16 + 36 = 52     |
|  7  | (7,3)  |   C   |     25 + 4 = 29      |
|  8  | (2,0)  |   B   |    0 + 1 = **1**     |
|  9  | (4,1)  |   B   |    4 + 0 = **4**     |
| 10  | (2,2)  |   A   |    0 + 1 = **1**     |
| 11  | (8,6)  |   B   |     36 + 25 = 61     |
| 12  | (9,4)  |   C   |     49 + 9 = 58      |

### Bước 3 & 4: 5 điểm gần nhất (d² nhỏ nhất)

| Thứ tự |  #  | d²  | Label |
| :----: | :-: | :-: | :---: |
|   1    |  8  |  1  | **B** |
|   2    | 10  |  1  | **A** |
|   3    |  2  |  2  | **B** |
|   4    |  3  |  4  | **C** |
|   5    |  9  |  4  | **B** |

### Bước 5: Đếm

| Label | Số phiếu |
| :---: | :------: |
| **B** |  **3**   |
|   A   |    1     |
|   C   |    1     |

### ✅ KẾT LUẬN: Q₃(2, 1) thuộc lớp **B**

---

## 📊 TỔNG KẾT BÀI GIẢI

|   Điểm   |  K  | Kết quả | Lý do          |
| :------: | :-: | :-----: | -------------- |
| Q₁(1, 7) |  5  |  **A**  | 3A vs 1B vs 1C |
| Q₂(6, 4) |  5  |  **C**  | 3C vs 1A vs 1B |
| Q₃(2, 1) |  5  |  **B**  | 3B vs 1A vs 1C |

---

# 5️⃣ BẢNG TRA CĂN BẬC 2

## 5.1. Giá trị chính xác (THUỘC!)

|  n  |    √n    |     |  n  |  √n  |
| :-: | :------: | :-: | :-: | :--: |
|  1  |   1.00   |     | 17  | 4.12 |
|  2  | **1.41** |     | 18  | 4.24 |
|  3  |   1.73   |     | 19  | 4.36 |
|  4  |   2.00   |     | 20  | 4.47 |
|  5  | **2.24** |     | 25  | 5.00 |
|  6  |   2.45   |     | 26  | 5.10 |
|  7  |   2.65   |     | 29  | 5.39 |
|  8  | **2.83** |     | 32  | 5.66 |
|  9  |   3.00   |     | 36  | 6.00 |
| 10  | **3.16** |     | 45  | 6.71 |
| 13  | **3.61** |     | 49  | 7.00 |
| 16  |   4.00   |     | 50  | 7.07 |

## 5.2. MẸO: Không cần tính căn!

**So sánh d² thay vì d:**

Vì √a < √b ⟺ a < b (với a, b ≥ 0)

→ **Chỉ cần so sánh d², không cần tính √**

Ví dụ: d² = 17 và d² = 25

- So sánh: 17 < 25
- → √17 < √25
- → Không cần biết √17 = bao nhiêu!

---

# 6️⃣ CÁC TRƯỜNG HỢP ĐẶC BIỆT

## 6.1. Hòa phiếu (Tie)

**Tình huống:** K=4, kết quả 2A vs 2B

**Cách xử lý:**

1. Chọn lớp của điểm **gần nhất** trong số hòa
2. Hoặc giảm K đi 1 (K=3)
3. Hoặc theo quy định đề bài

**Ví dụ:**

```
K=4: Điểm #1(A, d=1), #2(B, d=2), #3(A, d=3), #4(B, d=4)
Đếm: 2A vs 2B → Hòa!
Giải quyết: Điểm gần nhất là #1(A) → Chọn A
```

## 6.2. Nhiều điểm cùng khoảng cách

**Tình huống:** K=3, nhưng điểm thứ 3 và 4 có cùng khoảng cách

**Cách xử lý:**

1. Lấy tất cả các điểm cùng khoảng cách
2. Hoặc theo thứ tự xuất hiện trong bảng

## 6.3. K quá lớn hoặc quá nhỏ

|   K   | Vấn đề                       |
| :---: | ---------------------------- |
| K = 1 | Rất nhạy với nhiễu           |
| K = N | Mọi điểm đều thuộc lớp đa số |

**Khuyến nghị:** K = √N (N là số điểm training)

---

# 7️⃣ BÀI TẬP TỰ LUYỆN

## Bài 1: Cơ bản (K=3, 2 lớp)

Cho dữ liệu:

| Điểm |  X  |  Y  | Label |
| :--: | :-: | :-: | :---: |
|  A   |  1  |  1  |  Đỏ   |
|  B   |  2  |  2  |  Đỏ   |
|  C   |  5  |  5  | Xanh  |
|  D   |  6  |  6  | Xanh  |

Với K=3, điểm P(3, 3) thuộc lớp nào?

<details>
<summary>📝 Xem lời giải</summary>

**Tính d² từ P(3,3):**

- d²(P,A) = (3-1)² + (3-1)² = 4 + 4 = 8
- d²(P,B) = (3-2)² + (3-2)² = 1 + 1 = 2 ← Nhỏ nhất
- d²(P,C) = (3-5)² + (3-5)² = 4 + 4 = 8
- d²(P,D) = (3-6)² + (3-6)² = 9 + 9 = 18

**Sắp xếp:** B(2) < A(8) = C(8) < D(18)

**K=3:** B(Đỏ), A(Đỏ), C(Xanh)

**Đếm:** Đỏ = 2, Xanh = 1

**→ P thuộc lớp ĐỎ**

</details>

---

## Bài 2: Nâng cao (K=5, 3 lớp)

Cho dữ liệu:

|  #  |  X  |  Y  | Label |
| :-: | :-: | :-: | :---: |
|  1  |  0  |  0  |   A   |
|  2  |  1  |  0  |   A   |
|  3  |  0  |  1  |   B   |
|  4  |  1  |  1  |   B   |
|  5  |  3  |  0  |   C   |
|  6  |  3  |  1  |   C   |
|  7  |  2  |  2  |   B   |

Với K=5, điểm Q(1.5, 0.5) thuộc lớp nào?

<details>
<summary>📝 Xem lời giải</summary>

**Tính d² từ Q(1.5, 0.5):**

- #1: (1.5)² + (0.5)² = 2.25 + 0.25 = 2.5
- #2: (0.5)² + (0.5)² = 0.25 + 0.25 = **0.5** ← Nhỏ nhất
- #3: (1.5)² + (0.5)² = 2.25 + 0.25 = 2.5
- #4: (0.5)² + (0.5)² = 0.25 + 0.25 = **0.5** ← Nhỏ nhất
- #5: (1.5)² + (0.5)² = 2.25 + 0.25 = 2.5
- #6: (1.5)² + (0.5)² = 2.25 + 0.25 = 2.5
- #7: (0.5)² + (1.5)² = 0.25 + 2.25 = 2.5

**Sắp xếp:** #2(0.5), #4(0.5), #1(2.5), #3(2.5), #5(2.5)...

**K=5:** #2(A), #4(B), #1(A), #3(B), #5(C)

**Đếm:** A=2, B=2, C=1

**Hòa A vs B!** → Xét điểm gần nhất: #2(A) hoặc #4(B) cùng d²=0.5

**→ Cần quy tắc tie-breaking (ví dụ: theo thứ tự) → A**

</details>

---

## Bài 3: Thử thách (Giống đề thi)

Cho dữ liệu như Bài mẫu ở trên. Với **K=3**, phân loại lại Q₁(1,7), Q₂(6,4), Q₃(2,1).

<details>
<summary>📝 Xem lời giải</summary>

Sử dụng bảng d² đã tính, lấy 3 điểm gần nhất:

**Q₁(1,7) với K=3:**

- 3 điểm gần nhất: #1(A), #5(A), #6(C)
- Đếm: A=2, C=1 → **A**

**Q₂(6,4) với K=3:**

- 3 điểm gần nhất: #7(C), #5(A), #11(B)
- Đếm: C=1, A=1, B=1 → **Hòa!** → Chọn #7(C) gần nhất → **C**

**Q₃(2,1) với K=3:**

- 3 điểm gần nhất: #8(B), #10(A), #2(B)
- Đếm: B=2, A=1 → **B**
</details>

---

# 📋 CHECKLIST LÀM BÀI THI KNN

- [ ] Đọc đề: Xác định **K** và **điểm cần phân loại**
- [ ] Lập bảng: Liệt kê TẤT CẢ điểm training
- [ ] Tính: (X - x)² và (Y - y)² cho mỗi điểm
- [ ] Cộng: d² = (X-x)² + (Y-y)²
- [ ] Sắp xếp: d² từ bé đến lớn
- [ ] Chọn: K điểm có d² nhỏ nhất
- [ ] Đếm: Số lượng mỗi nhãn trong K điểm
- [ ] Kết luận: Nhãn có số phiếu cao nhất

---

> **💡 LỜI KHUYÊN:**
>
> 1. **Tính d² thay vì d** để tiết kiệm thời gian
> 2. **Lập bảng có hệ thống** để tránh sai sót
> 3. **Kiểm tra lại** việc đếm nhãn
> 4. **K lẻ** để tránh hòa phiếu

---

# 📟 MẸO THI: TÍNH NHANH VỚI CASIO

## 1️⃣ Dùng MODE TABLE

### 🟢 Casio fx-580VNX (Model mới - Khuyên dùng!)

**Bước setup:**

```
Bước 1: Nhấn MODE → 3:TABLE
Bước 2: Nhập công thức: (X-Qx)²+(Y-Qy)²
        Ví dụ: (X-1)²+(Y-7)²

Bước 3: Chọn chế độ nhập:
        • f(x): Chỉ 1 biến (cho KNN 1D)
        • f(x,y): 2 biến (cho KNN 2D) ← CHỌN CÁI NÀY

Bước 4: Nhập dữ liệu:
        X? → Nhập 2 (điểm đầu tiên), nhấn =
        Y? → Nhập 8, nhấn =
        → Máy hiển thị: f(2,8) = 2

        Nhấn = tiếp → Nhập điểm thứ 2...
```

**✨ Ưu điểm fx-580VNX:**

- Màn hình LCD lớn, dễ đọc
- Hỗ trợ QR Code (có thể bỏ qua)
- TABLE mode ổn định hơn

---

### 🟡 Casio fx-570VN PLUS (Model cũ)

**Bước setup:**

```
Bước 1: Nhấn MODE → 3 (TABLE)
Bước 2: Nhập công thức: (X-Qx)²+(Y-Qy)²
        Ví dụ: (X-1)²+(Y-7)²
Bước 3: Nhấn =
Bước 4: Nhập Start, End, Step
        HOẶC nhập từng điểm thủ công (giống 580VNX)
```

---

**🎯 Ưu điểm chung:**

- Máy tự động tính hết 12 giá trị d²
- Chỉ cần nhìn và chọn 5 số nhỏ nhất
- Tiết kiệm 70% thời gian!

**⚠️ Lưu ý:** Cần chuẩn bị sẵn tọa độ theo thứ tự trong bảng riêng

---

## 2️⃣ Kỹ thuật LOẠI TRỪ NHANH (không cần máy)

### Nhận dạng điểm "quá xa" bằng mắt

**Quy tắc nhanh:**

- Nếu **|Δx| > 5 HOẶC |Δy| > 5** → Có thể loại (d² > 25)
- Ưu tiên tính điểm có **Δx, Δy đều nhỏ**

### Ví dụ với Q₁(1, 7) - Đề thi thật:

```
┌────┬─────────┬──────┬──────┬─────────────┐
│ #  │ (X, Y)  │ Δx   │ Δy   │ Quyết định  │
├────┼─────────┼──────┼──────┼─────────────┤
│ 1  │ (2, 8)  │  1   │  1   │ ✅ Tính ngay│
│ 2  │ (3, 2)  │  2   │ -5   │ ⚠️ Có thể xa│
│ 3  │ (4, 1)  │  3   │ -6   │ ❌ LOẠI (>5)│
│ 4  │ (11,5)  │ 10   │ -2   │ ❌ LOẠI (>5)│
│ 5  │ (5, 6)  │  4   │ -1   │ ✅ Tính     │
│ 6  │ (6, 7)  │  5   │  0   │ ✅ Tính     │
│ 7  │ (7, 3)  │  6   │ -4   │ ❌ LOẠI (>5)│
│ 8  │ (2, 0)  │  1   │ -7   │ ❌ LOẠI (>5)│
│ 9  │ (4, 1)  │  3   │ -6   │ ❌ LOẠI     │
│ 10 │ (2, 2)  │  1   │ -5   │ ⚠️ Biên giới│
│ 11 │ (8, 6)  │  7   │ -1   │ ❌ LOẠI (>5)│
│ 12 │ (9, 4)  │  8   │ -3   │ ❌ LOẠI (>5)│
└────┴─────────┴──────┴──────┴─────────────┘

→ Chỉ cần tính 5-6 điểm thay vì 12!
```

**Quy trình tối ưu:**

```
1. Quét nhanh bảng → Loại điểm |Δx|>5 hoặc |Δy|>5
2. Tính d² cho ~6-7 điểm còn lại
3. Chọn 5 điểm nhỏ nhất
4. Đếm nhãn → Kết luận
```

**⏱️ Thời gian:** Từ 5-7 phút xuống còn **2-3 phút/câu**!

---

## 3️⃣ Thủ thuật tính d² KHÔNG CẦN GHI RA

**Pattern thường gặp:**

```
Δx  Δy  →  d²
 1   1  →   2  ← NHỚ!
 1   2  →   5
 2   2  →   8
 1   3  →  10
 2   3  →  13
 3   3  →  18
 1   4  →  17
 2   4  →  20
 3   4  →  25  ← Ngưỡng loại
```

**Thuộc lòng:**

- d² ≤ 10: Chắc chắn trong top 5 (với 12 điểm)
- d² > 30: Hầu như chắc chắn bị loại
- Khoảng 10-30: Cần so sánh

---

## 4️⃣ CHECKLIST THI NHANH

```
□ Bước 0: Vẽ nhanh sơ đồ vị trí (nếu có thời gian)
          → Nhận dạng cụm điểm gần

□ Bước 1: LOẠI TRỪ bằng mắt
          Gạch bỏ điểm có |Δx|>5 hoặc |Δy|>5

□ Bước 2: Tính d² cho ~6-7 điểm "khả nghi"
          Dùng Casio MODE TABLE hoặc tính tay

□ Bước 3: Sắp xếp tìm 5 giá trị nhỏ nhất
          Không cần sắp tất cả, chỉ tìm top 5

□ Bước 4: Đếm nhãn → Ghi đáp án
```

---

## 💡 MẸO VÀNG

### 1. Với Casio fx-580VNX / fx-570VN PLUS:

- **MODE 3 (TABLE)** là công cụ mạnh nhất
- Lưu công thức: `(X-[số])²+(Y-[số])²`
- Thay [số] cho từng câu hỏi
- **580VNX:** Chọn f(x,y) khi máy hỏi
- **570VN:** Nhập công thức rồi chọn Start/End

### 2. Không có Casio TABLE:

- **M+ (Memory)** để cộng dồn:
  ```
  (x-Qx)² M+
  (y-Qy)² M+
  MR (xem kết quả) → Ghi lại
  AC → Làm điểm tiếp theo
  ```

### 3. Chiến thuật thời gian:

- Câu dễ (Q gần góc): 2 phút
- Câu trung bình: 3-4 phút
- Câu khó (Q ở giữa): 5 phút

### 4. Khi không chắc:

- Nếu hòa phiếu → Chọn lớp của điểm **gần nhất** trong top K
- Nếu có 2 điểm cùng d² (tie) → Lấy cả 2 vào top K

---

_Hết tài liệu KNN - Phương án 1_
_Cập nhật: 2026 | Cho kỳ thi SE313_
