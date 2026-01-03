# 📚 HƯỚNG DẪN GIẢI BÀI TẬP: K-NEAREST NEIGHBOR (KNN)

## Phương án 2: Bài tập từng bước chi tiết

---

> **Lời dặn của Giảng viên:**
>
> Các bạn ơi, phần này tập trung vào việc **giải bài tập KNN từng bước**. Đây là dạng bài **100% sẽ có trong đề thi**.
>
> Mỗi bài tập mình sẽ giải **rất chi tiết**, từng phép tính một. Các bạn cứ theo dõi và làm theo nhé!

---

## 📋 DẠNG BÀI TẬP KNN THƯỜNG GẶP

|    Dạng    | Mô tả                           |     Độ khó      |
| :--------: | ------------------------------- | :-------------: |
| **Dạng 1** | Cho tọa độ, tính khoảng cách    |      ⭐ Dễ      |
| **Dạng 2** | Phân loại với K cho trước       | ⭐⭐ Trung bình |
| **Dạng 3** | So sánh kết quả với K khác nhau |   ⭐⭐⭐ Khó    |

---

# 🔷 DẠNG 1: TÍNH KHOẢNG CÁCH EUCLIDEAN

## Bài tập 1.1 (Cơ bản - 2D)

**Đề bài:** Cho hai điểm A(2, 3) và B(5, 7). Tính khoảng cách Euclid giữa A và B.

### Lời giải chi tiết

**Bước 1: Xác định tọa độ**

- A: x₁ = 2, y₁ = 3
- B: x₂ = 5, y₂ = 7

**Bước 2: Áp dụng công thức**

```
d(A, B) = √[(x₂ - x₁)² + (y₂ - y₁)²]
        = √[(5 - 2)² + (7 - 3)²]
        = √[3² + 4²]
        = √[9 + 16]
        = √25
        = 5
```

**✅ Đáp án:** d(A, B) = **5**

---

## Bài tập 1.2 (Nâng cao - 3D)

**Đề bài:** Cho hai điểm trong không gian 3 chiều: P(1, 2, 3) và Q(4, 6, 3). Tính khoảng cách giữa P và Q.

### Lời giải chi tiết

**Bước 1: Xác định tọa độ**

- P: x₁ = 1, y₁ = 2, z₁ = 3
- Q: x₂ = 4, y₂ = 6, z₂ = 3

**Bước 2: Áp dụng công thức 3D**

```
d(P, Q) = √[(x₂-x₁)² + (y₂-y₁)² + (z₂-z₁)²]
        = √[(4-1)² + (6-2)² + (3-3)²]
        = √[3² + 4² + 0²]
        = √[9 + 16 + 0]
        = √25
        = 5
```

**✅ Đáp án:** d(P, Q) = **5**

---

# 🔷 DẠNG 2: PHÂN LOẠI VỚI K CHO TRƯỚC

## Bài tập 2.1 (Đề thi thường gặp)

**Đề bài:** Cho tập dữ liệu huấn luyện:

| Điểm |  x  |  y  | Nhãn |
| :--: | :-: | :-: | :--: |
|  A   |  1  |  1  |  Đỏ  |
|  B   |  2  |  1  |  Đỏ  |
|  C   |  1  |  2  |  Đỏ  |
|  D   |  5  |  5  | Xanh |
|  E   |  5  |  6  | Xanh |
|  F   |  6  |  5  | Xanh |

**Hỏi:** Với **K = 3**, điểm mới **P(3, 3)** thuộc lớp nào?

### Lời giải chi tiết

**📍 Bước 1: Tính khoảng cách từ P(3,3) đến tất cả các điểm**

|  Điểm  |    Công thức     | Tính toán |    Kết quả     |
| :----: | :--------------: | :-------: | :------------: |
| d(P,A) | √[(3-1)²+(3-1)²] |  √[4+4]   | √8 ≈ **2.83**  |
| d(P,B) | √[(3-2)²+(3-1)²] |  √[1+4]   | √5 ≈ **2.24**  |
| d(P,C) | √[(3-1)²+(3-2)²] |  √[4+1]   | √5 ≈ **2.24**  |
| d(P,D) | √[(3-5)²+(3-5)²] |  √[4+4]   | √8 ≈ **2.83**  |
| d(P,E) | √[(3-5)²+(3-6)²] |  √[4+9]   | √13 ≈ **3.61** |
| d(P,F) | √[(3-6)²+(3-5)²] |  √[9+4]   | √13 ≈ **3.61** |

**📍 Bước 2: Sắp xếp theo khoảng cách tăng dần**

| Thứ tự | Điểm | Khoảng cách |  Nhãn   |
| :----: | :--: | :---------: | :-----: |
|   1    |  B   |  √5 ≈ 2.24  |  🔴 Đỏ  |
|   2    |  C   |  √5 ≈ 2.24  |  🔴 Đỏ  |
|   3    |  A   |  √8 ≈ 2.83  |  🔴 Đỏ  |
|   4    |  D   |  √8 ≈ 2.83  | 🔵 Xanh |
|   5    |  E   | √13 ≈ 3.61  | 🔵 Xanh |
|   6    |  F   | √13 ≈ 3.61  | 🔵 Xanh |

**📍 Bước 3: Chọn K = 3 điểm gần nhất**

3 điểm gần nhất: **B, C, A**

**📍 Bước 4: Bỏ phiếu**

|  Nhãn   | Số phiếu |  Điểm   |
| :-----: | :------: | :-----: |
|  🔴 Đỏ  |    3     | B, C, A |
| 🔵 Xanh |    0     |    -    |

**✅ Kết luận:** Với K = 3, điểm P(3, 3) được phân loại là **🔴 ĐỎ** (tỷ lệ 3-0)

---

## Bài tập 2.2 (Trường hợp phức tạp hơn)

**Đề bài:** Vẫn dữ liệu trên, nếu **K = 5** thì kết quả thay đổi thế nào?

### Lời giải chi tiết

**📍 Bước 1:** (Đã có từ bài trước)

**📍 Bước 2: Chọn K = 5 điểm gần nhất**

5 điểm gần nhất: **B, C, A, D, E** (hoặc F thay E vì bằng nhau)

**📍 Bước 3: Bỏ phiếu**

|  Nhãn   | Số phiếu |  Điểm   |
| :-----: | :------: | :-----: |
|  🔴 Đỏ  |    3     | B, C, A |
| 🔵 Xanh |    2     |  D, E   |

**✅ Kết luận:** Với K = 5, điểm P(3, 3) vẫn được phân loại là **🔴 ĐỎ** (tỷ lệ 3-2)

---

# 🔷 DẠNG 3: SO SÁNH KẾT QUẢ VỚI K KHÁC NHAU

## Bài tập 3.1

**Đề bài:** Cho tập dữ liệu sau:

| Điểm |  x  |  y  |   Nhãn   |
| :--: | :-: | :-: | :------: |
|  A   |  0  |  0  |  ⬛ Đen  |
|  B   |  1  |  0  | ⬜ Trắng |
|  C   |  0  |  1  | ⬜ Trắng |
|  D   |  2  |  0  |  ⬛ Đen  |
|  E   |  0  |  2  |  ⬛ Đen  |

**Hỏi:** Điểm mới **Q(0.5, 0.5)** thuộc lớp nào với K=1, K=3, K=5?

### Lời giải chi tiết

**📍 Bước 1: Tính khoảng cách**

|  Điểm  |     Công thức     |     Kết quả     |
| :----: | :---------------: | :-------------: |
| d(Q,A) | √[(0.5)²+(0.5)²]  | √0.5 ≈ **0.71** |
| d(Q,B) | √[(-.5)²+(0.5)²]  | √0.5 ≈ **0.71** |
| d(Q,C) | √[(0.5)²+(-.5)²]  | √0.5 ≈ **0.71** |
| d(Q,D) | √[(-1.5)²+(0.5)²] | √2.5 ≈ **1.58** |
| d(Q,E) | √[(0.5)²+(-1.5)²] | √2.5 ≈ **1.58** |

**📍 Bước 2: Sắp xếp**

| Thứ tự |  Điểm   | Khoảng cách |  Nhãn  |
| :----: | :-----: | :---------: | :----: |
|  1-3   | A, B, C |    0.71     | ⬛⬜⬜ |
|  4-5   |  D, E   |    1.58     |  ⬛⬛  |

**📍 Bước 3: Phân tích theo K**

### Với K = 1:

- Lấy 1 điểm gần nhất: A hoặc B hoặc C (bằng nhau)
- Nếu chọn A → ⬛ Đen
- Nếu chọn B hoặc C → ⬜ Trắng
- **⚠️ Kết quả không xác định rõ ràng** (cần quy tắc phá tie)

### Với K = 3:

- Lấy 3 điểm: A, B, C
- Đếm: ⬛ Đen = 1, ⬜ Trắng = 2
- **✅ Kết quả: ⬜ TRẮNG** (tỷ lệ 2-1)

### Với K = 5:

- Lấy 5 điểm: A, B, C, D, E
- Đếm: ⬛ Đen = 3 (A, D, E), ⬜ Trắng = 2 (B, C)
- **✅ Kết quả: ⬛ ĐEN** (tỷ lệ 3-2)

### 📊 Tổng kết

|  K  |      Kết quả      | Lý do                      |
| :-: | :---------------: | -------------------------- |
|  1  | ⚠️ Không xác định | Có 3 điểm cùng khoảng cách |
|  3  |     ⬜ Trắng      | 2 Trắng > 1 Đen            |
|  5  |      ⬛ Đen       | 3 Đen > 2 Trắng            |

**💡 Bài học:** Việc chọn K có ảnh hưởng LỚN đến kết quả!

---

# 📝 BẢNG TRA CỨU CĂN BẬC 2

| Số  | Căn bậc 2 | Ghi chú |
| :-: | :-------: | ------- |
|  1  |   1.00    |         |
|  2  |   1.41    | ≈ √2    |
|  3  |   1.73    |         |
|  4  |   2.00    |         |
|  5  |   2.24    |         |
|  6  |   2.45    |         |
|  7  |   2.65    |         |
|  8  |   2.83    | = 2√2   |
|  9  |   3.00    |         |
| 10  |   3.16    |         |
| 13  |   3.61    |         |
| 16  |   4.00    |         |
| 17  |   4.12    |         |
| 18  |   4.24    | = 3√2   |
| 20  |   4.47    |         |
| 25  |   5.00    |         |

---

# � DẠNG 4: ĐỀ THI THỰC TẾ (k=5, 12 ĐIỂM, 3 LỚP)

## Bài tập 4.1 - GIỐNG ĐỀ THI BÀI 2

**Đề bài:** Cho tập huấn luyện gồm **12 điểm** thuộc **3 lớp A, B, C**:

| STT | Tọa độ | Lớp |     | STT | Tọa độ | Lớp |
| :-: | :----: | :-: | :-: | :-: | :----: | :-: |
|  1  | (1, 2) |  A  |     |  7  | (3, 2) |  B  |
|  2  | (2, 1) |  A  |     |  8  | (4, 3) |  B  |
|  3  | (1, 4) |  A  |     |  9  | (6, 6) |  C  |
|  4  | (2, 5) |  A  |     | 10  | (5, 7) |  C  |
|  5  | (3, 4) |  B  |     | 11  | (7, 5) |  C  |
|  6  | (4, 2) |  B  |     | 12  | (6, 4) |  C  |

**Yêu cầu:** Với **K = 5**, phân loại các điểm:

- **Q₁(3, 3)**
- **Q₂(5, 5)**

---

### 📍 GIẢI CHI TIẾT CHO Q₁(3, 3)

**BƯỚC 1: Tính khoảng cách d² (để tránh căn bậc 2)**

| Điểm | (x, y) | Lớp |       d² = (x-3)² + (y-3)²        |  d  |
| :--: | :----: | :-: | :-------------------------------: | :-: |
|  1   | (1, 2) |  A  |  (1-3)² + (2-3)² = 4 + 1 = **5**  | √5  |
|  2   | (2, 1) |  A  |  (2-3)² + (1-3)² = 1 + 4 = **5**  | √5  |
|  3   | (1, 4) |  A  |  (1-3)² + (4-3)² = 4 + 1 = **5**  | √5  |
|  4   | (2, 5) |  A  |  (2-3)² + (5-3)² = 1 + 4 = **5**  | √5  |
|  5   | (3, 4) |  B  |  (3-3)² + (4-3)² = 0 + 1 = **1**  |  1  |
|  6   | (4, 2) |  B  |  (4-3)² + (2-3)² = 1 + 1 = **2**  | √2  |
|  7   | (3, 2) |  B  |  (3-3)² + (2-3)² = 0 + 1 = **1**  |  1  |
|  8   | (4, 3) |  B  |  (4-3)² + (3-3)² = 1 + 0 = **1**  |  1  |
|  9   | (6, 6) |  C  | (6-3)² + (6-3)² = 9 + 9 = **18**  | √18 |
|  10  | (5, 7) |  C  | (5-3)² + (7-3)² = 4 + 16 = **20** | √20 |
|  11  | (7, 5) |  C  | (7-3)² + (5-3)² = 16 + 4 = **20** | √20 |
|  12  | (6, 4) |  C  | (6-3)² + (4-3)² = 9 + 1 = **10**  | √10 |

**BƯỚC 2: Sắp xếp theo d² tăng dần**

| Hạng | Điểm |  Lớp  | d²  |
| :--: | :--: | :---: | :-: |
|  1   |  5   | **B** |  1  |
|  2   |  7   | **B** |  1  |
|  3   |  8   | **B** |  1  |
|  4   |  6   | **B** |  2  |
|  5   |  1   | **A** |  5  |
|  6   |  2   |   A   |  5  |
|  7   |  3   |   A   |  5  |
|  8   |  4   |   A   |  5  |
|  9   |  12  |   C   | 10  |
|  10  |  9   |   C   | 18  |
|  11  |  10  |   C   | 20  |
|  12  |  11  |   C   | 20  |

**BƯỚC 3: Chọn k=5 láng giềng gần nhất**

5 điểm gần nhất: **5, 7, 8, 6, 1**

| Điểm | Lớp |
| :--: | :-: |
|  5   |  B  |
|  7   |  B  |
|  8   |  B  |
|  6   |  B  |
|  1   |  A  |

**BƯỚC 4: Bỏ phiếu**

|  Lớp  |    Số phiếu    |
| :---: | :------------: |
| **B** | **4** ⬅️ THẮNG |
|   A   |       1        |
|   C   |       0        |

### ✅ KẾT QUẢ: Q₁(3, 3) thuộc lớp **B** (tỷ lệ 4:1:0)

---

### 📍 GIẢI CHI TIẾT CHO Q₂(5, 5)

**BƯỚC 1: Tính khoảng cách d²**

| Điểm | (x, y) | Lớp |       d² = (x-5)² + (y-5)²        |
| :--: | :----: | :-: | :-------------------------------: |
|  1   | (1, 2) |  A  | (1-5)² + (2-5)² = 16 + 9 = **25** |
|  2   | (2, 1) |  A  | (2-5)² + (1-5)² = 9 + 16 = **25** |
|  3   | (1, 4) |  A  | (1-5)² + (4-5)² = 16 + 1 = **17** |
|  4   | (2, 5) |  A  |  (2-5)² + (5-5)² = 9 + 0 = **9**  |
|  5   | (3, 4) |  B  |  (3-5)² + (4-5)² = 4 + 1 = **5**  |
|  6   | (4, 2) |  B  | (4-5)² + (2-5)² = 1 + 9 = **10**  |
|  7   | (3, 2) |  B  | (3-5)² + (2-5)² = 4 + 9 = **13**  |
|  8   | (4, 3) |  B  |  (4-5)² + (3-5)² = 1 + 4 = **5**  |
|  9   | (6, 6) |  C  |  (6-5)² + (6-5)² = 1 + 1 = **2**  |
|  10  | (5, 7) |  C  |  (5-5)² + (7-5)² = 0 + 4 = **4**  |
|  11  | (7, 5) |  C  |  (7-5)² + (5-5)² = 4 + 0 = **4**  |
|  12  | (6, 4) |  C  |  (6-5)² + (4-5)² = 1 + 1 = **2**  |

**BƯỚC 2: Sắp xếp theo d²**

| Hạng | Điểm |  Lớp  | d²  |
| :--: | :--: | :---: | :-: |
|  1   |  9   | **C** |  2  |
|  2   |  12  | **C** |  2  |
|  3   |  10  | **C** |  4  |
|  4   |  11  | **C** |  4  |
|  5   |  5   | **B** |  5  |
|  6   |  8   |   B   |  5  |
|  7   |  4   |   A   |  9  |
| ...  | ...  |  ...  | ... |

**BƯỚC 3: Chọn k=5 láng giềng**

5 điểm gần nhất: **9, 12, 10, 11, 5**

**BƯỚC 4: Bỏ phiếu**

|  Lớp  |    Số phiếu    |
| :---: | :------------: |
| **C** | **4** ⬅️ THẮNG |
|   B   |       1        |
|   A   |       0        |

### ✅ KẾT QUẢ: Q₂(5, 5) thuộc lớp **C** (tỷ lệ 4:1:0)

---

## 📊 TỔNG KẾT BÀI 4.1

| Điểm test | 5 láng giềng gần nhất | Phân bố phiếu |  Kết quả  |
| :-------: | :-------------------: | :-----------: | :-------: |
| Q₁(3, 3)  |     5, 7, 8, 6, 1     | B:4, A:1, C:0 | **Lớp B** |
| Q₂(5, 5)  |   9, 12, 10, 11, 5    | C:4, B:1, A:0 | **Lớp C** |

---

# 🔷 DẠNG 5: XỬ LÝ TRƯỜNG HỢP HÒA (TIE-BREAKING)

## Bài tập 5.1

**Đề bài:** Cho 6 điểm:

| Điểm | Tọa độ | Lớp |
| :--: | :----: | :-: |
|  1   | (0, 0) |  A  |
|  2   | (1, 0) |  B  |
|  3   | (0, 1) |  B  |
|  4   | (2, 2) |  A  |
|  5   | (3, 1) |  C  |
|  6   | (1, 3) |  C  |

Với **K = 3**, phân loại **P(1, 1)**.

### 📍 GIẢI CHI TIẾT

**Bước 1: Tính d²**

| Điểm | Lớp |  d² = (x-1)² + (y-1)²   |
| :--: | :-: | :---------------------: |
|  1   |  A  | (0-1)² + (0-1)² = **2** |
|  2   |  B  | (1-1)² + (0-1)² = **1** |
|  3   |  B  | (0-1)² + (1-1)² = **1** |
|  4   |  A  | (2-1)² + (2-1)² = **2** |
|  5   |  C  | (3-1)² + (1-1)² = **4** |
|  6   |  C  | (1-1)² + (3-1)² = **4** |

**Bước 2: Sắp xếp**

| Hạng | Điểm | Lớp  | d²  |
| :--: | :--: | :--: | :-: |
| 1-2  | 2, 3 | B, B |  1  |
| 3-4  | 1, 4 | A, A |  2  |
| 5-6  | 5, 6 | C, C |  4  |

**Bước 3: Chọn k=3**

3 điểm gần nhất: **2, 3, và 1 hoặc 4** (vì d²=2 có 2 điểm cùng khoảng cách)

**Bước 4: Bỏ phiếu**

Nếu chọn 2, 3, 1:
| Lớp | Số phiếu |
|:---:|:--------:|
| B | 2 |
| A | 1 |

Nếu chọn 2, 3, 4: → Kết quả giống (B vẫn thắng)

### ✅ KẾT QUẢ: P(1, 1) thuộc lớp **B**

---

## 💡 QUY TẮC XỬ LÝ HÒA (TIE-BREAKING)

### Khi nhiều điểm cùng khoảng cách (để vào top K):

1. **Lấy tất cả** các điểm cùng khoảng cách
2. **Hoặc** lấy theo thứ tự xuất hiện trong dữ liệu

### Khi bỏ phiếu có tỷ lệ bằng nhau:

1. **Giảm K** (bỏ điểm xa nhất, tính lại)
2. **Hoặc** chọn lớp của điểm gần nhất
3. **Hoặc** chọn ngẫu nhiên (đề thi thường tránh)

---

# 📌 BÀI TẬP TỰ LUYỆN

## Bài 1: Tính khoảng cách

Cho A(0, 0), B(3, 0), C(0, 4). Điểm P(1, 1) gần điểm nào nhất?

<details>
<summary>📝 Đáp án</summary>

- d²(P,A) = 1² + 1² = 2
- d²(P,B) = 2² + 1² = 5
- d²(P,C) = 1² + 3² = 10

→ **A gần nhất** (d² = 2)

</details>

---

## Bài 2: K=3 với 2 lớp

Cho dữ liệu:

- Đỏ: (0,0), (1,1), (2,0)
- Xanh: (4,4), (5,5), (6,4)

Với K=3, điểm (2,2) thuộc lớp nào?

<details>
<summary>📝 Đáp án</summary>

Tính d² từ (2,2):

- (0,0): 4+4 = 8, Đỏ
- (1,1): 1+1 = 2, Đỏ ⬅️
- (2,0): 0+4 = 4, Đỏ ⬅️
- (4,4): 4+4 = 8, Xanh
- (5,5): 9+9 = 18, Xanh
- (6,4): 16+4 = 20, Xanh

3 gần nhất: (1,1), (2,0), (0,0) hoặc (4,4)
→ **Đỏ** (ít nhất 2 Đỏ)

</details>

---

## Bài 3: K=5 với 3 lớp

Cho 9 điểm:

| Điểm | Tọa độ | Lớp |
| :--: | :----: | :-: |
|  1   | (1, 1) |  X  |
|  2   | (2, 1) |  X  |
|  3   | (1, 2) |  X  |
|  4   | (4, 1) |  Y  |
|  5   | (5, 1) |  Y  |
|  6   | (4, 2) |  Y  |
|  7   | (7, 7) |  Z  |
|  8   | (8, 7) |  Z  |
|  9   | (7, 8) |  Z  |

Với K=5, phân loại P(3, 1).

<details>
<summary>📝 Đáp án</summary>

Tính d² từ (3,1):

- 1: 4+0=4, X
- 2: 1+0=1, X ⬅️
- 3: 4+1=5, X
- 4: 1+0=1, Y ⬅️
- 5: 4+0=4, Y
- 6: 1+1=2, Y ⬅️
- 7: 16+36=52, Z
- 8: 25+36=61, Z
- 9: 16+49=65, Z

5 gần nhất: 2(X), 4(Y), 6(Y), 1(X), 5(Y)

→ **Y** (3 phiếu Y > 2 phiếu X)

</details>

---

# 📋 CHECKLIST LÀM BÀI THI KNN

- [ ] **Bước 1:** Tính d² (bình phương khoảng cách) cho tất cả điểm
- [ ] **Bước 2:** Sắp xếp theo d² tăng dần
- [ ] **Bước 3:** Chọn K điểm đầu tiên
- [ ] **Bước 4:** Đếm số phiếu mỗi lớp
- [ ] **Bước 5:** Lớp có nhiều phiếu nhất → Kết quả
- [ ] **⚠️ Nếu hòa:** Áp dụng quy tắc tie-breaking

---

> **💡 MẸO LÀM NHANH:**
>
> 1. **Dùng d² thay vì d** để tránh tính căn
> 2. **Lập bảng có cột Lớp** để dễ đếm phiếu
> 3. **Gạch chân/tô màu** K điểm gần nhất
> 4. **Với 3 lớp**, cần K ≥ 3 để có nghĩa

---

# 🔷 DẠNG 4: KỸ THUẬT THI CASIO (BẮT BUỘC PHẢI BIẾT!)

## Bài tập 4.1: Dùng MODE TABLE

**Đề bài:** Cho 8 điểm sau:

|  #  |  X  |  Y  | Nhãn |
| :-: | :-: | :-: | :--: |
|  1  |  1  |  1  |  A   |
|  2  |  2  |  3  |  A   |
|  3  |  3  |  1  |  B   |
|  4  |  5  |  4  |  B   |
|  5  |  6  |  2  |  B   |
|  6  |  7  |  5  |  C   |
|  7  |  8  |  3  |  C   |
|  8  |  9  |  1  |  C   |

Với K=3, phân loại điểm P(4, 2) bằng **Casio MODE TABLE**.

### Lời giải với Casio fx-580VNX (Khuyên dùng!)

**📟 Bước 1: Vào MODE TABLE**

```
Nhấn: MODE → 3:TABLE
```

**📟 Bước 2: Chọn chế độ và nhập công thức**

```
Máy hỏi: f(x) hay f(x,y)? → Chọn f(x,y)

Nhập công thức:
(  X  -  4  )  x²  +  (  Y  -  2  )  x²  =
```

**📟 Bước 3: Nhập dữ liệu từng điểm**

```
Máy hỏi: X? → Nhập 1, nhấn =
Máy hỏi: Y? → Nhập 1, nhấn =
Máy hiển thị: f(1,1) = 10

Nhấn = tiếp → Nhập điểm 2...
```

---

### Lời giải với Casio fx-570VN PLUS (Model cũ)

**📟 Các bước tương tự:**

```
1. MODE → 3 (TABLE)
2. Nhập công thức: (X-4)²+(Y-2)²
3. Nhập từng điểm khi máy hỏi X?, Y?
```

**📊 Kết quả từ máy:**

|  #  |  X  |  Y  | **f(X,Y) = d²** |    Nhãn    |
| :-: | :-: | :-: | :-------------: | :--------: |
|  1  |  1  |  1  |       10        |     A      |
|  2  |  2  |  3  |        5        |     A      |
|  3  |  3  |  1  |        2        | **B** ← #1 |
|  4  |  5  |  4  |        5        |     B      |
|  5  |  6  |  2  |        4        | **B** ← #2 |
|  6  |  7  |  5  |       18        |     C      |
|  7  |  8  |  3  |       17        |     C      |
|  8  |  9  |  1  |       26        |     C      |

**📍 Top 3 (K=3):**

- d²=2 → B
- d²=4 → B
- d²=5 → A (hoặc B, có 2 điểm cùng d²=5)

**✅ Đáp án:** Lớp **B** (2 phiếu B, 1 phiếu A)

**⏱️ Thời gian:** ~90 giây (thay vì 4-5 phút tính tay)

---

## Bài tập 4.2: Kỹ thuật LOẠI TRỪ nhanh (không máy)

**Đề bài:** Với dữ liệu bài 4.1, tìm nhãn cho Q(8, 4) với K=3 bằng cách **loại trừ điểm xa trước**.

### Lời giải

**📍 Bước 1: Phân tích Δx, Δy**

```
Q = (8, 4)

┌───┬───────┬──────┬──────┬──────────────────┐
│ # │ (X,Y) │  Δx  │  Δy  │ Nhận xét         │
├───┼───────┼──────┼──────┼──────────────────┤
│ 1 │ (1,1) │  -7  │  -3  │ ❌ |Δx|>5 → LOẠI │
│ 2 │ (2,3) │  -6  │  -1  │ ❌ |Δx|>5 → LOẠI │
│ 3 │ (3,1) │  -5  │  -3  │ ⚠️ Biên giới     │
│ 4 │ (5,4) │  -3  │   0  │ ✅ Gần!         │
│ 5 │ (6,2) │  -2  │  -2  │ ✅ Gần!         │
│ 6 │ (7,5) │  -1  │   1  │ ✅ Rất gần!     │
│ 7 │ (8,3) │   0  │  -1  │ ✅ Rất gần!     │
│ 8 │ (9,1) │   1  │  -3  │ ✅ Gần!         │
└───┴───────┴──────┴──────┴──────────────────┘

→ Loại #1, #2 → Chỉ cần tính 6 điểm!
```

**📍 Bước 2: Tính d² cho 6 điểm còn lại**

|  #  | Δx  | Δy  | d² = Δx² + Δy²  | Nhãn |
| :-: | :-: | :-: | :-------------: | :--: |
|  3  | -5  | -3  | 25 + 9 = **34** |  B   |
|  4  | -3  |  0  |  9 + 0 = **9**  |  B   |
|  5  | -2  | -2  |  4 + 4 = **8**  |  B   |
|  6  | -1  |  1  |  1 + 1 = **2**  |  C   |
|  7  |  0  | -1  |  0 + 1 = **1**  |  C   |
|  8  |  1  | -3  | 1 + 9 = **10**  |  C   |

**📍 Bước 3: Top 3**

| Hạng | d²  | Nhãn  |
| :--: | :-: | :---: |
|  1   |  1  | **C** |
|  2   |  2  | **C** |
|  3   |  8  | **B** |

**✅ Đáp án:** Lớp **C** (2 phiếu C, 1 phiếu B)

**⏱️ Thời gian:** ~2 phút (tiết kiệm 60%!)

---

## 💡 QUY TẮC LOẠI TRỪ VÀNG

### Với K=3 (12 điểm training):

```
|Δx| hoặc |Δy| > 6  →  Chắc chắn LOẠI
|Δx| hoặc |Δy| = 5-6  →  Nghi ngờ
|Δx| và |Δy| < 4     →  Chắc chắn TÍNH
```

### Với K=5 (12 điểm training):

```
|Δx| hoặc |Δy| > 5  →  Có thể LOẠI
|Δx| hoặc |Δy| = 4-5  →  Nên tính
|Δx| và |Δy| < 3     →  Bắt buộc TÍNH
```

### Công thức ước lượng nhanh:

```
d² ≈ (|Δx| + |Δy|)²/2  (ước lượng trên)

Ví dụ: Δx=3, Δy=4
→ d² ước lượng ≈ (3+4)²/2 = 49/2 ≈ 24
→ d² thực tế = 9+16 = 25 ✓ (sai số nhỏ)
```

---

## 📋 BẢNG THAM KHẢO: CASIO MODE TABLE

### Setup cho các dạng bài thường gặp:

**1. KNN cơ bản (2D):**

```
🟢 fx-580VNX:
   MODE → 3:TABLE → Chọn f(x,y) → (X-a)²+(Y-b)²

🟡 fx-570VN PLUS:
   MODE → 3 (TABLE) → f(X,Y) = (X-a)²+(Y-b)²
```

**2. KNN 1D (chỉ có X):**

```
🟢 fx-580VNX:
   MODE → 3:TABLE → Chọn f(x) → (X-a)²

🟡 fx-570VN PLUS:
   MODE → 3 (TABLE) → f(X) = (X-a)²
```

**3. KNN 3D (nâng cao):**

```
Cả 2 model đều tương tự 2D, nhưng:
f(X,Y,Z) = (X-a)²+(Y-b)²+(Z-c)²

⚠️ fx-580VNX không có sẵn f(x,y,z)
→ Dùng f(x,y) và tính Z riêng, hoặc
→ Tính tay cho trục Z
```

---

### 🔧 Khắc phục sự cố:

| Vấn đề                 | Giải pháp                             |
| :--------------------- | :------------------------------------ |
| Máy không có TABLE     | Dùng kỹ thuật loại trừ (xem phần 4.2) |
| Nhầm f(x) thành f(x,y) | AC → MODE 3 lại từ đầu                |
| Quên công thức         | Xem lại: (X-Qx)²+(Y-Qy)²              |
| Nhập sai tọa độ        | SHIFT → CLR → 2 (TABLE) → Nhập lại    |

---

## 🎯 CHIẾN LƯỢC LÀM BÀI THI

### Với 3 câu hỏi (như đề mẫu):

**⏱️ Phân bổ thời gian (tổng 15 phút):**

```
┌─────────┬───────────┬──────────────────────┐
│ Câu     │ Thời gian │ Chiến thuật          │
├─────────┼───────────┼──────────────────────┤
│ Câu 1   │ 4 phút    │ Làm đầy đủ, cẩn thận │
│ Câu 2   │ 5 phút    │ Dùng Casio/Loại trừ  │
│ Câu 3   │ 4 phút    │ Nhanh, ưu tiên đáp án│
│ Kiểm tra│ 2 phút    │ Check top K, đếm lại │
└─────────┴───────────┴──────────────────────┘
```

### Thứ tự ưu tiên:

**1. Nếu có Casio MODE TABLE:**

---

# 🔷 DẠNG 5: GIẢI ĐỀ THI THỰC TẾ (BÀI TẬP 2)

![Bài tập 2](../Bai-tap-tham-khao/Bài%20tập-1,Bài%20tập-2,Bài%20tập-3/Bài%20tập-2.png)

## 📝 ĐỀ BÀI
Cho bảng dữ liệu train (như hình trên) và yêu cầu tìm nhãn cho 3 điểm kiểm tra với **K = 5**:
1. **$P_1(1, 7)$**
2. **$P_2(6, 4)$**
3. **$P_3(2, 1)$**

---

## 🟢 LỜI GIẢI CHI TIẾT

### 1. Phân loại điểm $P_1(1, 7)$

**Bước 1: Tính bình phương khoảng cách ($d^2$) từ $P_1(1, 7)$ đến các điểm training**

| ID | Data Point | Label | $d^2 = (x-1)^2 + (y-7)^2$ | Kết quả |
|:--:|:----------:|:-----:|:-------------------------:|:-------:|
| 1 | (2, 8) | A | $(2-1)^2 + (8-7)^2$ | $1+1 = \mathbf{2}$ |
| 2 | (3, 2) | B | $(3-1)^2 + (2-7)^2$ | $4+25 = 29$ |
| 3 | (4, 1) | C | $(4-1)^2 + (1-7)^2$ | $9+36 = 45$ |
| 4 | (11, 5) | A | $(11-1)^2 + (5-7)^2$ | $100+4 = 104$ |
| 5 | (5, 6) | A | $(5-1)^2 + (6-7)^2$ | $16+1 = \mathbf{17}$ |
| 6 | (6, 7) | C | $(6-1)^2 + (7-7)^2$ | $25+0 = 25$ |
| 7 | (7, 3) | C | $(7-1)^2 + (3-7)^2$ | $36+16 = 52$ |
| 8 | (2, 0) | B | $(2-1)^2 + (0-7)^2$ | $1+49 = 50$ |
| 9 | (4, 1) | B | $(4-1)^2 + (1-7)^2$ | $9+36 = 45$ |
| 10 | (2, 2) | A | $(2-1)^2 + (2-7)^2$ | $1+25 = 26$ |
| 11 | (8, 6) | B | $(8-1)^2 + (6-7)^2$ | $49+1 = 50$ |
| 12 | (9, 4) | C | $(9-1)^2 + (4-7)^2$ | $64+9 = 73$ |

**Bước 2: Tìm 5 điểm gần nhất (có $d^2$ nhỏ nhất)**
1. ID **1** (A) - $d^2=2$
2. ID **5** (A) - $d^2=17$
3. ID **6** (C) - $d^2=25$
4. ID **10** (A) - $d^2=26$
5. ID **2** (B) - $d^2=29$

**Bước 3: Bầu chọn (K=5)**
- **A**: 3 phiếu (ID 1, 5, 10)
- **B**: 1 phiếu (ID 2)
- **C**: 1 phiếu (ID 6)

👉 **Kết luận: $P_1(1, 7)$ thuộc lớp A**

---

### 2. Phân loại điểm $P_2(6, 4)$

**Bước 1: Tính $d^2$ từ $P_2(6, 4)$**

| ID | Point | Label | $d^2 = (x-6)^2 + (y-4)^2$ | Kết quả | Gần nhất? |
|:--:|:-----:|:-----:|:-------------------------:|:-------:|:---------:|
| 7 | (7, 3) | C | $1^2 + (-1)^2$ | $\mathbf{2}$ | ✅ #1 |
| 5 | (5, 6) | A | $(-1)^2 + 2^2$ | $\mathbf{5}$ | ✅ #2 |
| 11 | (8, 6) | B | $2^2 + 2^2$ | $\mathbf{8}$ | ✅ #3 |
| 6 | (6, 7) | C | $0^2 + 3^2$ | $\mathbf{9}$ | ✅ #4 (tie) |
| 12 | (9, 4) | C | $3^2 + 0^2$ | $\mathbf{9}$ | ✅ #5 (tie) |
| 9 | (4, 1) | B | $(-2)^2 + (-3)^2$ | 13 | |
| 2 | (3, 2) | B | $(-3)^2 + (-2)^2$ | 13 | |
| 3 | (4, 1) | C | $(-2)^2 + (-3)^2$ | 13 | |
| 4 | (11, 5) | A | $5^2 + 1^2$ | 26 | |
| ... | ... | ... | (Các điểm khác > 13) | | |

**Bước 2: Tìm 5 điểm gần nhất**
- ID 7 (C), ID 5 (A), ID 11 (B), ID 6 (C), ID 12 (C)

**Bước 3: Bầu chọn**
- **C**: 3 phiếu (ID 7, 6, 12)
- **A**: 1 phiếu
- **B**: 1 phiếu

👉 **Kết luận: $P_2(6, 4)$ thuộc lớp C**

---

### 3. Phân loại điểm $P_3(2, 1)$

**Bước 1: Tính $d^2$ từ $P_3(2, 1)$**

| ID | Point | Label | $d^2 = (x-2)^2 + (y-1)^2$ | Kết quả | Gần nhất? |
|:--:|:-----:|:-----:|:-------------------------:|:-------:|:---------:|
| 8 | (2, 0) | B | $0^2 + (-1)^2$ | $\mathbf{1}$ | ✅ #1 (tie) |
| 10 | (2, 2) | A | $0^2 + 1^2$ | $\mathbf{1}$ | ✅ #2 (tie) |
| 2 | (3, 2) | B | $1^2 + 1^2$ | $\mathbf{2}$ | ✅ #3 |
| 3 | (4, 1) | C | $2^2 + 0^2$ | $\mathbf{4}$ | ✅ #4 (tie) |
| 9 | (4, 1) | B | $2^2 + 0^2$ | $\mathbf{4}$ | ✅ #5 (tie) |
| ... | ... | ... | Các điểm khác xa hơn | | |

**Bước 2: Tìm 5 điểm gần nhất**
- ID 8 (B), ID 10 (A), ID 2 (B), ID 3 (C), ID 9 (B)

**Bước 3: Bầu chọn**
- **B**: 3 phiếu (ID 8, 2, 9)
- **A**: 1 phiếu (ID 10)
- **C**: 1 phiếu (ID 3)

👉 **Kết luận: $P_3(2, 1)$ thuộc lớp B**

---

- Dùng cho CẢ 3 câu
- Thời gian: 8-10 phút (rất dư thời gian check)

**2. Nếu KHÔNG có TABLE:**

- Câu 1: Loại trừ + tính tay (4 phút)
- Câu 2: Loại trừ + tính tay (5 phút)
- Câu 3: Nếu không kịp, dùng "ước lượng mắt" chọn cụm gần nhất

**3. Backup plan (khẩn cấp):**

- Vẽ sơ đồ tọa độ → Nhìn điểm Q gần cụm nào → Chọn lớp đó
- Độ chính xác: ~70% (tốt hơn bỏ trắng!)

---

_Hết tài liệu bài tập KNN - Phương án 2_
