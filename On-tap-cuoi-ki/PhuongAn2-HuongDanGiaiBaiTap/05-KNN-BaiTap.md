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

| Dạng | Mô tả | Độ khó |
|:----:|-------|:------:|
| **Dạng 1** | Cho tọa độ, tính khoảng cách | ⭐ Dễ |
| **Dạng 2** | Phân loại với K cho trước | ⭐⭐ Trung bình |
| **Dạng 3** | So sánh kết quả với K khác nhau | ⭐⭐⭐ Khó |

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

| Điểm | x | y | Nhãn |
|:----:|:-:|:-:|:----:|
| A | 1 | 1 | Đỏ |
| B | 2 | 1 | Đỏ |
| C | 1 | 2 | Đỏ |
| D | 5 | 5 | Xanh |
| E | 5 | 6 | Xanh |
| F | 6 | 5 | Xanh |

**Hỏi:** Với **K = 3**, điểm mới **P(3, 3)** thuộc lớp nào?

### Lời giải chi tiết

**📍 Bước 1: Tính khoảng cách từ P(3,3) đến tất cả các điểm**

| Điểm | Công thức | Tính toán | Kết quả |
|:----:|:---------:|:---------:|:-------:|
| d(P,A) | √[(3-1)²+(3-1)²] | √[4+4] | √8 ≈ **2.83** |
| d(P,B) | √[(3-2)²+(3-1)²] | √[1+4] | √5 ≈ **2.24** |
| d(P,C) | √[(3-1)²+(3-2)²] | √[4+1] | √5 ≈ **2.24** |
| d(P,D) | √[(3-5)²+(3-5)²] | √[4+4] | √8 ≈ **2.83** |
| d(P,E) | √[(3-5)²+(3-6)²] | √[4+9] | √13 ≈ **3.61** |
| d(P,F) | √[(3-6)²+(3-5)²] | √[9+4] | √13 ≈ **3.61** |

**📍 Bước 2: Sắp xếp theo khoảng cách tăng dần**

| Thứ tự | Điểm | Khoảng cách | Nhãn |
|:------:|:----:|:-----------:|:----:|
| 1 | B | √5 ≈ 2.24 | 🔴 Đỏ |
| 2 | C | √5 ≈ 2.24 | 🔴 Đỏ |
| 3 | A | √8 ≈ 2.83 | 🔴 Đỏ |
| 4 | D | √8 ≈ 2.83 | 🔵 Xanh |
| 5 | E | √13 ≈ 3.61 | 🔵 Xanh |
| 6 | F | √13 ≈ 3.61 | 🔵 Xanh |

**📍 Bước 3: Chọn K = 3 điểm gần nhất**

3 điểm gần nhất: **B, C, A**

**📍 Bước 4: Bỏ phiếu**

| Nhãn | Số phiếu | Điểm |
|:----:|:--------:|:----:|
| 🔴 Đỏ | 3 | B, C, A |
| 🔵 Xanh | 0 | - |

**✅ Kết luận:** Với K = 3, điểm P(3, 3) được phân loại là **🔴 ĐỎ** (tỷ lệ 3-0)

---

## Bài tập 2.2 (Trường hợp phức tạp hơn)

**Đề bài:** Vẫn dữ liệu trên, nếu **K = 5** thì kết quả thay đổi thế nào?

### Lời giải chi tiết

**📍 Bước 1:** (Đã có từ bài trước)

**📍 Bước 2: Chọn K = 5 điểm gần nhất**

5 điểm gần nhất: **B, C, A, D, E** (hoặc F thay E vì bằng nhau)

**📍 Bước 3: Bỏ phiếu**

| Nhãn | Số phiếu | Điểm |
|:----:|:--------:|:----:|
| 🔴 Đỏ | 3 | B, C, A |
| 🔵 Xanh | 2 | D, E |

**✅ Kết luận:** Với K = 5, điểm P(3, 3) vẫn được phân loại là **🔴 ĐỎ** (tỷ lệ 3-2)

---

# 🔷 DẠNG 3: SO SÁNH KẾT QUẢ VỚI K KHÁC NHAU

## Bài tập 3.1

**Đề bài:** Cho tập dữ liệu sau:

| Điểm | x | y | Nhãn |
|:----:|:-:|:-:|:----:|
| A | 0 | 0 | ⬛ Đen |
| B | 1 | 0 | ⬜ Trắng |
| C | 0 | 1 | ⬜ Trắng |
| D | 2 | 0 | ⬛ Đen |
| E | 0 | 2 | ⬛ Đen |

**Hỏi:** Điểm mới **Q(0.5, 0.5)** thuộc lớp nào với K=1, K=3, K=5?

### Lời giải chi tiết

**📍 Bước 1: Tính khoảng cách**

| Điểm | Công thức | Kết quả |
|:----:|:---------:|:-------:|
| d(Q,A) | √[(0.5)²+(0.5)²] | √0.5 ≈ **0.71** |
| d(Q,B) | √[(-.5)²+(0.5)²] | √0.5 ≈ **0.71** |
| d(Q,C) | √[(0.5)²+(-.5)²] | √0.5 ≈ **0.71** |
| d(Q,D) | √[(-1.5)²+(0.5)²] | √2.5 ≈ **1.58** |
| d(Q,E) | √[(0.5)²+(-1.5)²] | √2.5 ≈ **1.58** |

**📍 Bước 2: Sắp xếp**

| Thứ tự | Điểm | Khoảng cách | Nhãn |
|:------:|:----:|:-----------:|:----:|
| 1-3 | A, B, C | 0.71 | ⬛⬜⬜ |
| 4-5 | D, E | 1.58 | ⬛⬛ |

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

| K | Kết quả | Lý do |
|:-:|:-------:|-------|
| 1 | ⚠️ Không xác định | Có 3 điểm cùng khoảng cách |
| 3 | ⬜ Trắng | 2 Trắng > 1 Đen |
| 5 | ⬛ Đen | 3 Đen > 2 Trắng |

**💡 Bài học:** Việc chọn K có ảnh hưởng LỚN đến kết quả!

---

# 📝 BẢNG TRA CỨU CĂN BẬC 2

| Số | Căn bậc 2 | Ghi chú |
|:--:|:---------:|---------|
| 1 | 1.00 | |
| 2 | 1.41 | ≈ √2 |
| 3 | 1.73 | |
| 4 | 2.00 | |
| 5 | 2.24 | |
| 6 | 2.45 | |
| 7 | 2.65 | |
| 8 | 2.83 | = 2√2 |
| 9 | 3.00 | |
| 10 | 3.16 | |
| 13 | 3.61 | |
| 16 | 4.00 | |
| 17 | 4.12 | |
| 18 | 4.24 | = 3√2 |
| 20 | 4.47 | |
| 25 | 5.00 | |

---

# 📌 BÀI TẬP TỰ LUYỆN

**Bài 1:** Cho A(0, 0), B(3, 0), C(0, 4). Điểm P(1, 1) gần điểm nào nhất?

**Bài 2:** Cho dữ liệu:
- Đỏ: (0,0), (1,1), (2,0)
- Xanh: (4,4), (5,5), (6,4)

Với K=3, điểm (2,2) thuộc lớp nào?

**Bài 3:** Trong bài 2, nếu K=5 thì sao?

---

*Hết tài liệu bài tập KNN - Phương án 2*
