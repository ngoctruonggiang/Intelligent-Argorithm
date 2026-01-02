# PHƯƠNG ÁN 2: HƯỚNG DẪN GIẢI BÀI TẬP TỪNG BƯỚC
# BÀI TẬP MẠNG NƠ-RON NHÂN TẠO (ANN)

---

## 📚 MỤC LỤC

1. [Dạng bài tập thường gặp](#1-dạng-bài-tập-thường-gặp)
2. [Bài tập 1: Tính Sigmoid](#2-bài-tập-1-tính-sigmoid)
3. [Bài tập 2: Forward Propagation đơn giản](#3-bài-tập-2-forward-propagation-đơn-giản)
4. [Bài tập 3: Forward Propagation mạng 2 lớp](#4-bài-tập-3-forward-propagation-mạng-2-lớp)
5. [Bài tập 4: Backpropagation 1 vòng](#5-bài-tập-4-backpropagation-1-vòng)
6. [Bài tập 5: Forward + Backward hoàn chỉnh](#6-bài-tập-5-forward--backward-hoàn-chỉnh)
7. [Bài tập tự luyện](#7-bài-tập-tự-luyện)
8. [Bảng tra cứu và mẹo](#8-bảng-tra-cứu-và-mẹo)

---

# 1. DẠNG BÀI TẬP THƯỜNG GẶP

## 1.1. Các dạng đề phổ biến

| Dạng | Mô tả | Độ khó |
|------|-------|--------|
| Dạng 1 | Tính hàm sigmoid và đạo hàm | ⭐ |
| Dạng 2 | Forward propagation 1 node | ⭐⭐ |
| Dạng 3 | Forward propagation nhiều lớp | ⭐⭐⭐ |
| Dạng 4 | Backpropagation cập nhật trọng số | ⭐⭐⭐⭐ |
| Dạng 5 | Kết hợp Forward + Backward | ⭐⭐⭐⭐⭐ |

## 1.2. Công thức cần nhớ

### Sigmoid:
```
σ(z) = 1 / (1 + e⁻ᶻ)
σ'(z) = σ(z) × (1 - σ(z)) = a × (1 - a)
```

### Forward Propagation:
```
z = Σwᵢxᵢ + b
a = σ(z)
```

### Backpropagation:
```
δ_output = (ŷ - y) × ŷ × (1 - ŷ)
δ_hidden = (w × δ_next) × a × (1 - a)
w_mới = w_cũ - α × δ × input
b_mới = b_cũ - α × δ
```

---

# 2. BÀI TẬP 1: TÍNH SIGMOID

## 2.1. Đề bài

**Tính giá trị hàm sigmoid và đạo hàm tại:**
a) z = 0
b) z = 1
c) z = -1
d) z = 2

---

## 2.2. Lời giải chi tiết

### a) z = 0

**Tính σ(0):**
```
σ(0) = 1 / (1 + e⁻⁰)
     = 1 / (1 + e⁰)
     = 1 / (1 + 1)
     = 1 / 2
     = 0.5
```

**Tính σ'(0):**
```
σ'(0) = σ(0) × (1 - σ(0))
      = 0.5 × (1 - 0.5)
      = 0.5 × 0.5
      = 0.25
```

---

### b) z = 1

**Tính σ(1):**
```
e⁻¹ ≈ 0.368

σ(1) = 1 / (1 + e⁻¹)
     = 1 / (1 + 0.368)
     = 1 / 1.368
     ≈ 0.731
```

**Tính σ'(1):**
```
σ'(1) = 0.731 × (1 - 0.731)
      = 0.731 × 0.269
      ≈ 0.197
```

---

### c) z = -1

**Tính σ(-1):**
```
e⁻⁽⁻¹⁾ = e¹ ≈ 2.718

σ(-1) = 1 / (1 + e¹)
      = 1 / (1 + 2.718)
      = 1 / 3.718
      ≈ 0.269
```

**Tính σ'(-1):**
```
σ'(-1) = 0.269 × (1 - 0.269)
       = 0.269 × 0.731
       ≈ 0.197
```

---

### d) z = 2

**Tính σ(2):**
```
e⁻² ≈ 0.135

σ(2) = 1 / (1 + e⁻²)
     = 1 / (1 + 0.135)
     = 1 / 1.135
     ≈ 0.881
```

**Tính σ'(2):**
```
σ'(2) = 0.881 × (1 - 0.881)
      = 0.881 × 0.119
      ≈ 0.105
```

---

## 2.3. Bảng tổng hợp

| z | e⁻ᶻ | σ(z) | σ'(z) |
|---|-----|------|-------|
| 0 | 1 | 0.500 | 0.250 |
| 1 | 0.368 | 0.731 | 0.197 |
| -1 | 2.718 | 0.269 | 0.197 |
| 2 | 0.135 | 0.881 | 0.105 |

---

# 3. BÀI TẬP 2: FORWARD PROPAGATION ĐƠN GIẢN

## 3.1. Đề bài

Cho mạng nơ-ron 1 node với:
- Input: x₁ = 0.5, x₂ = 0.3
- Trọng số: w₁ = 0.4, w₂ = 0.6
- Bias: b = 0.1
- Hàm kích hoạt: Sigmoid

**Yêu cầu:** Tính output của node.

---

## 3.2. Sơ đồ mạng

```
x₁ = 0.5 ────(w₁=0.4)────┐
                          ↘
                           [Σ + b=0.1] ──→ [σ] ──→ y = ?
                          ↗
x₂ = 0.3 ────(w₂=0.6)────┘
```

---

## 3.3. Lời giải chi tiết

### Bước 1: Tính tổng có trọng số z

**Công thức:**
```
z = w₁×x₁ + w₂×x₂ + b
```

**Tính:**
```
z = 0.4 × 0.5 + 0.6 × 0.3 + 0.1
  = 0.20 + 0.18 + 0.1
  = 0.48
```

### Bước 2: Áp dụng hàm sigmoid

**Công thức:**
```
y = σ(z) = 1 / (1 + e⁻ᶻ)
```

**Tính e⁻⁰·⁴⁸:**
```
e⁻⁰·⁴⁸ ≈ 0.619
```

**Tính σ(0.48):**
```
y = 1 / (1 + 0.619)
  = 1 / 1.619
  ≈ 0.618
```

---

## 3.4. Kết quả

```
┌─────────────────────────────────────────────────────────┐
│                        KẾT QUẢ                          │
├─────────────────────────────────────────────────────────┤
│                                                         │
│   z = 0.48                                             │
│   y = σ(0.48) ≈ 0.618                                  │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

---

# 4. BÀI TẬP 3: FORWARD PROPAGATION MẠNG 2 LỚP

## 4.1. Đề bài

Cho mạng nơ-ron:
- **Input layer:** x₁ = 1, x₂ = 0
- **Hidden layer (1 node h):**
  - w₁ = 0.5, w₂ = 0.3, b₁ = 0.1
- **Output layer (1 node y):**
  - w₃ = 0.7, b₂ = 0.2
- **Hàm kích hoạt:** Sigmoid

**Yêu cầu:** Tính output ŷ.

---

## 4.2. Sơ đồ mạng

```
         Hidden              Output
x₁=1 ──(w₁=0.5)──┐
                  ↘
                   [h] ──(w₃=0.7)──→ [y]
                  ↗         b₁=0.1           b₂=0.2
x₂=0 ──(w₂=0.3)──┘
```

---

## 4.3. Lời giải chi tiết

### BƯỚC 1: Tính Hidden Layer

**Tính z₁:**
```
z₁ = w₁×x₁ + w₂×x₂ + b₁
   = 0.5×1 + 0.3×0 + 0.1
   = 0.5 + 0 + 0.1
   = 0.6
```

**Tính a₁ = σ(z₁):**
```
e⁻⁰·⁶ ≈ 0.549

a₁ = 1 / (1 + 0.549)
   = 1 / 1.549
   ≈ 0.646
```

### BƯỚC 2: Tính Output Layer

**Tính z₂:**
```
z₂ = w₃×a₁ + b₂
   = 0.7×0.646 + 0.2
   = 0.452 + 0.2
   = 0.652
```

**Tính ŷ = σ(z₂):**
```
e⁻⁰·⁶⁵² ≈ 0.521

ŷ = 1 / (1 + 0.521)
  = 1 / 1.521
  ≈ 0.658
```

---

## 4.4. Kết quả

```
┌─────────────────────────────────────────────────────────┐
│                        KẾT QUẢ                          │
├─────────────────────────────────────────────────────────┤
│                                                         │
│   Hidden layer:                                         │
│   - z₁ = 0.6                                           │
│   - a₁ = 0.646                                         │
│                                                         │
│   Output layer:                                         │
│   - z₂ = 0.652                                         │
│   - ŷ = 0.658                                          │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

---

# 5. BÀI TẬP 4: BACKPROPAGATION 1 VÒNG

## 5.1. Đề bài

*Tiếp tục Bài tập 3*

Cho:
- y (giá trị thực) = 1
- Learning rate α = 0.5

**Yêu cầu:** Thực hiện 1 vòng Backpropagation để cập nhật trọng số.

---

## 5.2. Thông tin từ Forward Pass

```
x₁ = 1, x₂ = 0
z₁ = 0.6, a₁ = 0.646
z₂ = 0.652, ŷ = 0.658
y = 1
```

---

## 5.3. Lời giải chi tiết

### BƯỚC 1: Tính sai số tại Output

**Sai số thô:**
```
Error = ŷ - y = 0.658 - 1 = -0.342
```

**Tính delta output (δ₂):**
```
δ₂ = (ŷ - y) × σ'(z₂)
   = (ŷ - y) × ŷ × (1 - ŷ)
   = (-0.342) × 0.658 × (1 - 0.658)
   = (-0.342) × 0.658 × 0.342
   = -0.077
```

### BƯỚC 2: Cập nhật trọng số Output Layer

**Cập nhật w₃:**
```
w₃_mới = w₃_cũ - α × δ₂ × a₁
       = 0.7 - 0.5 × (-0.077) × 0.646
       = 0.7 - (-0.025)
       = 0.7 + 0.025
       = 0.725
```

**Cập nhật b₂:**
```
b₂_mới = b₂_cũ - α × δ₂
       = 0.2 - 0.5 × (-0.077)
       = 0.2 + 0.039
       = 0.239
```

### BƯỚC 3: Tính delta Hidden Layer

**Tính δ₁:**
```
δ₁ = (w₃ × δ₂) × σ'(z₁)
   = (w₃ × δ₂) × a₁ × (1 - a₁)
   = (0.7 × (-0.077)) × 0.646 × (1 - 0.646)
   = (-0.054) × 0.646 × 0.354
   = -0.012
```

### BƯỚC 4: Cập nhật trọng số Hidden Layer

**Cập nhật w₁:**
```
w₁_mới = w₁_cũ - α × δ₁ × x₁
       = 0.5 - 0.5 × (-0.012) × 1
       = 0.5 + 0.006
       = 0.506
```

**Cập nhật w₂:**
```
w₂_mới = w₂_cũ - α × δ₁ × x₂
       = 0.3 - 0.5 × (-0.012) × 0
       = 0.3 - 0
       = 0.3  (không đổi vì x₂ = 0)
```

**Cập nhật b₁:**
```
b₁_mới = b₁_cũ - α × δ₁
       = 0.1 - 0.5 × (-0.012)
       = 0.1 + 0.006
       = 0.106
```

---

## 5.4. Bảng tổng hợp kết quả

| Tham số | Giá trị cũ | Giá trị mới | Thay đổi |
|---------|------------|-------------|----------|
| w₁ | 0.500 | 0.506 | +0.006 |
| w₂ | 0.300 | 0.300 | 0 |
| b₁ | 0.100 | 0.106 | +0.006 |
| w₃ | 0.700 | 0.725 | +0.025 |
| b₂ | 0.200 | 0.239 | +0.039 |

**Nhận xét:** 
- Tất cả trọng số **tăng** (ngoại trừ w₂) vì δ âm và ŷ < y
- w₂ không đổi vì x₂ = 0

---

# 6. BÀI TẬP 5: FORWARD + BACKWARD HOÀN CHỈNH

## 6.1. Đề bài

Cho mạng 1 node:
- Input: x = 1
- Trọng số: w = 0.5, b = 0.2
- Hàm kích hoạt: Sigmoid
- Giá trị thực: y = 1
- Learning rate: α = 0.5

**Yêu cầu:** 
1. Forward propagation
2. Backpropagation để cập nhật w và b

---

## 6.2. Lời giải

### FORWARD PROPAGATION

**Tính z:**
```
z = w×x + b = 0.5×1 + 0.2 = 0.7
```

**Tính ŷ:**
```
e⁻⁰·⁷ ≈ 0.497

ŷ = 1/(1 + 0.497) = 1/1.497 ≈ 0.668
```

### BACKPROPAGATION

**Tính δ:**
```
δ = (ŷ - y) × ŷ × (1 - ŷ)
  = (0.668 - 1) × 0.668 × (1 - 0.668)
  = (-0.332) × 0.668 × 0.332
  = -0.074
```

**Cập nhật w:**
```
w_mới = w - α × δ × x
      = 0.5 - 0.5 × (-0.074) × 1
      = 0.5 + 0.037
      = 0.537
```

**Cập nhật b:**
```
b_mới = b - α × δ
      = 0.2 - 0.5 × (-0.074)
      = 0.2 + 0.037
      = 0.237
```

---

## 6.3. Kết quả

| Tham số | Cũ | Mới |
|---------|-----|-----|
| w | 0.5 | 0.537 |
| b | 0.2 | 0.237 |

---

# 7. BÀI TẬP TỰ LUYỆN

## 7.1. Dạng Sigmoid

**Bài 1:** Tính σ(0.5) và σ'(0.5).

**Bài 2:** Nếu σ(z) = 0.8, tính σ'(z).

## 7.2. Dạng Forward

**Bài 3:** x = 2, w = 0.3, b = 0.1. Tính output với sigmoid.

**Bài 4:** x₁ = 1, x₂ = 1, w₁ = 0.5, w₂ = 0.5, b = 0. Tính output.

## 7.3. Dạng Backpropagation

**Bài 5:** Cho ŷ = 0.7, y = 1, a = 0.6, α = 0.5. Tính δ và cập nhật w nếu w_cũ = 0.4.

**Bài 6:** Thực hiện 2 vòng forward + backward cho mạng 1 node.

---

# 8. BẢNG TRA CỨU VÀ MẸO

## 8.1. Bảng giá trị e⁻ᶻ

| z | e⁻ᶻ |
|---|-----|
| 0 | 1.000 |
| 0.5 | 0.607 |
| 1 | 0.368 |
| 1.5 | 0.223 |
| 2 | 0.135 |
| -0.5 | 1.649 |
| -1 | 2.718 |
| -2 | 7.389 |

## 8.2. Bảng giá trị σ(z)

| z | σ(z) | σ'(z) |
|---|------|-------|
| -2 | 0.119 | 0.105 |
| -1 | 0.269 | 0.197 |
| -0.5 | 0.378 | 0.235 |
| 0 | 0.500 | 0.250 |
| 0.5 | 0.622 | 0.235 |
| 1 | 0.731 | 0.197 |
| 2 | 0.881 | 0.105 |

## 8.3. Mẹo tính nhanh

### Tính σ(z) khi biết e⁻ᶻ:
```
σ(z) = 1 / (1 + e⁻ᶻ)
```

### Tính σ'(z) khi biết a = σ(z):
```
σ'(z) = a × (1 - a)
```

### Dấu của δ:
```
ŷ > y → δ > 0 → w giảm
ŷ < y → δ < 0 → w tăng
```

## 8.4. Quy trình làm bài

```
┌─────────────────────────────────────────────────────────┐
│                    QUY TRÌNH LÀM BÀI                    │
├─────────────────────────────────────────────────────────┤
│  FORWARD:                                               │
│  1. z = Σwᵢxᵢ + b                                      │
│  2. a = σ(z)                                           │
│  (Lặp lại cho mỗi layer từ trái → phải)               │
├─────────────────────────────────────────────────────────┤
│  BACKWARD:                                              │
│  1. δ_output = (ŷ-y) × ŷ × (1-ŷ)                      │
│  2. δ_hidden = (w×δ_next) × a × (1-a)                  │
│  3. w := w - α × δ × input                             │
│  4. b := b - α × δ                                     │
│  (Lặp lại từ phải → trái)                              │
└─────────────────────────────────────────────────────────┘
```

---

*Hết phần Bài tập ANN - Phương án 2*
