# PHƯƠNG ÁN 3: HỌC 1-1 THEO CHỦ ĐỀ
# K-MEANS CLUSTERING - TỪ CƠ BẢN ĐẾN NÂNG CAO

---

## 🎯 MỤC TIÊU BÀI HỌC

Sau bài học này, bạn sẽ:
1. Hiểu được K-means dùng để làm gì
2. Nắm vững các bước của thuật toán
3. Thành thạo công thức tính toán
4. Tự tin giải các dạng bài tập

---

# PHẦN 1: KHÁI NIỆM CƠ BẢN

## 1.1. Phân cụm là gì?

**Giảng viên hỏi:** Nếu có 100 học sinh, bạn sẽ chia thành các nhóm như thế nào?

**Suy nghĩ:**
- Theo điểm số? (Giỏi, Khá, Trung bình)
- Theo sở thích? (Thể thao, Âm nhạc, Học thuật)
- Theo địa lý? (Cùng khu vực)

→ Đây chính là **phân cụm** - chia dữ liệu thành các nhóm có đặc điểm tương tự!

## 1.2. K-means giải quyết vấn đề gì?

**Bài toán:** Chia m điểm dữ liệu thành K nhóm sao cho các điểm trong cùng nhóm **gần nhau** nhất có thể.

**Ví dụ trực quan:**
```
Trước:                 Sau (K=2):
    •  •                   ○  ○   ← Cụm 1
  •  •  •                ○  ○  ○
     •                      ○
                         
  •  •  •                △  △  △  ← Cụm 2
    •  •                   △  △
```

---

## ✅ KIỂM TRA HIỂU BIẾT 1

**Câu hỏi:** K-means thuộc loại học máy nào?
- A) Học có giám sát
- B) Học không giám sát
- C) Học tăng cường

<details>
<summary>👉 Xem đáp án</summary>

**Đáp án: B) Học không giám sát**

Vì dữ liệu đầu vào KHÔNG có nhãn sẵn. Thuật toán tự tìm ra cấu trúc nhóm.

</details>

---

# PHẦN 2: THUẬT TOÁN K-MEANS

## 2.1. Tổng quan 4 bước

```
┌────────────────────────────────────────────┐
│         THUẬT TOÁN K-MEANS                 │
├────────────────────────────────────────────┤
│                                            │
│  BƯỚC 1: Chọn K tâm cụm ban đầu           │
│              ↓                             │
│  BƯỚC 2: Gán mỗi điểm vào cụm gần nhất    │
│              ↓                             │
│  BƯỚC 3: Tính lại tâm cụm                 │
│              ↓                             │
│  BƯỚC 4: Nếu thay đổi → Về BƯỚC 2         │
│          Nếu không → DỪNG                  │
│                                            │
└────────────────────────────────────────────┘
```

## 2.2. Chi tiết từng bước

### BƯỚC 1: Khởi tạo

**Làm gì:** Chọn K điểm làm tâm cụm ban đầu.

**Cách chọn:**
- Chọn ngẫu nhiên từ dữ liệu
- Hoặc đề bài cho sẵn

### BƯỚC 2: Gán điểm

**Làm gì:** Với mỗi điểm, tính khoảng cách đến TẤT CẢ tâm cụm, gán vào cụm có tâm gần nhất.

**Công thức khoảng cách Euclidean:**
```
d(A, B) = √[(x₂-x₁)² + (y₂-y₁)²]
```

### BƯỚC 3: Tính tâm mới

**Làm gì:** Tính trung bình tọa độ của các điểm trong cùng cụm.

**Công thức:**
```
Tâm = (Σxᵢ/n, Σyᵢ/n)
```

### BƯỚC 4: Kiểm tra hội tụ

**Làm gì:** So sánh phân cụm mới với phân cụm cũ.

**Hội tụ khi:** Không có điểm nào đổi cụm.

---

## ✅ KIỂM TRA HIỂU BIẾT 2

**Câu hỏi:** Trong bước nào của K-means ta sử dụng công thức khoảng cách Euclidean?

<details>
<summary>👉 Xem đáp án</summary>

**Đáp án: BƯỚC 2 - Gán điểm vào cụm**

Công thức được dùng để tính khoảng cách từ mỗi điểm đến các tâm cụm.

</details>

---

# PHẦN 3: THỰC HÀNH TÍNH TOÁN

## 3.1. Ví dụ mẫu

**Đề bài:** Cho 4 điểm A(1,1), B(2,1), C(4,3), D(5,4). Phân cụm K=2 với tâm ban đầu C₁=A, C₂=C.

---

### VÒNG 1 - Hướng dẫn chi tiết

**Bước 2.1: Tính khoảng cách cho điểm A(1,1)**

```
d(A, C₁) = √[(1-1)² + (1-1)²]  ← Thay tọa độ
         = √[0² + 0²]          ← Tính hiệu
         = √[0 + 0]            ← Bình phương
         = √0 = 0              ← Kết quả

d(A, C₂) = √[(4-1)² + (3-1)²]
         = √[3² + 2²]
         = √[9 + 4]
         = √13 ≈ 3.61
```

**So sánh:** 0 < 3.61 → **A thuộc Cụm 1**

---

**Bước 2.2: Tính cho điểm B(2,1)**

```
d(B, C₁) = √[(2-1)² + (1-1)²]
         = √[1 + 0] = 1

d(B, C₂) = √[(4-2)² + (3-1)²]
         = √[4 + 4] = √8 ≈ 2.83
```

**So sánh:** 1 < 2.83 → **B thuộc Cụm 1**

---

**Bước 2.3: Tính cho điểm C(4,3)**

```
d(C, C₁) = √13 ≈ 3.61
d(C, C₂) = √0 = 0
```

**So sánh:** 3.61 > 0 → **C thuộc Cụm 2**

---

**Bước 2.4: Tính cho điểm D(5,4)**

```
d(D, C₁) = √[(5-1)² + (4-1)²] = √[16+9] = √25 = 5
d(D, C₂) = √[(5-4)² + (4-3)²] = √[1+1] = √2 ≈ 1.41
```

**So sánh:** 5 > 1.41 → **D thuộc Cụm 2**

---

**Kết quả Vòng 1:**
- Cụm 1: {A, B}
- Cụm 2: {C, D}

---

**Bước 3: Tính tâm mới**

**Cụm 1:** {A(1,1), B(2,1)}
```
C₁_mới = ((1+2)/2, (1+1)/2) = (1.5, 1)
```

**Cụm 2:** {C(4,3), D(5,4)}
```
C₂_mới = ((4+5)/2, (3+4)/2) = (4.5, 3.5)
```

---

### VÒNG 2

*(Tính lại với tâm mới, phân cụm không đổi)*

→ **HỘI TỤ!**

---

## ✅ KIỂM TRA HIỂU BIẾT 3

**Bài tập:** Cho 3 điểm: P(0,0), Q(1,0), R(10,10). 
- K = 2
- Tâm ban đầu: C₁ = P, C₂ = R

**Hãy:**
1. Tính khoảng cách từ Q đến C₁ và C₂
2. Q thuộc cụm nào?

<details>
<summary>👉 Xem đáp án</summary>

**1. Tính khoảng cách:**
```
d(Q, C₁) = √[(1-0)² + (0-0)²] = √1 = 1
d(Q, C₂) = √[(1-10)² + (0-10)²] = √[81+100] = √181 ≈ 13.45
```

**2. So sánh:** 1 < 13.45 → **Q thuộc Cụm 1**

</details>

---

# PHẦN 4: CÁC DẠNG BÀI TẬP

## Dạng 1: Phân cụm cơ bản (K=2)
- Cho tâm ban đầu
- Thực hiện 1-2 vòng lặp

## Dạng 2: Phân cụm K=3
- Tính khoảng cách đến 3 tâm
- Chọn tâm gần nhất

## Dạng 3: Xác định hội tụ
- So sánh phân cụm giữa các vòng
- Hội tụ khi không đổi

## Dạng 4: Dữ liệu 3 chiều
- Dùng công thức: d = √[(x₂-x₁)² + (y₂-y₁)² + (z₂-z₁)²]

---

# PHẦN 5: TỔNG KẾT

## 5.1. Công thức cần nhớ

| Tên | Công thức |
|-----|-----------|
| Khoảng cách 2D | d = √[(x₂-x₁)² + (y₂-y₁)²] |
| Khoảng cách 3D | d = √[(x₂-x₁)² + (y₂-y₁)² + (z₂-z₁)²] |
| Tâm cụm | C = (Σxᵢ/n, Σyᵢ/n) |

## 5.2. Quy trình làm bài

1. Vẽ hình (nếu có thể)
2. Lập bảng khoảng cách
3. So sánh và gán cụm
4. Tính tâm mới
5. Kiểm tra hội tụ

## 5.3. Căn bậc 2 thường gặp

| Biểu thức | Giá trị |
|-----------|---------|
| √2 | 1.41 |
| √5 | 2.24 |
| √8 | 2.83 |
| √10 | 3.16 |
| √13 | 3.61 |

---

## 🎯 BÀI TẬP CUỐI BÀI

**Bài tập:** Cho 5 điểm: (1,1), (2,2), (8,8), (9,9), (10,10).
K = 2, Tâm ban đầu: C₁ = (1,1), C₂ = (8,8).

Hãy thực hiện thuật toán K-means đến khi hội tụ.

---

*Hết bài học K-means - Phương án 3*
