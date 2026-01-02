# TÀI LIỆU ÔN TẬP CUỐI KỲ
## Môn: Một số Thuật toán Thông minh - Chương 6: Học Máy

---

# PHẦN 1: PHÂN CỤM K-MEANS

## 1.1. Giới thiệu
K-means là thuật toán học không giám sát (unsupervised learning) dùng để phân cụm dữ liệu thành K nhóm dựa trên độ tương đồng.

## 1.2. Các bước thuật toán K-means

```
Bước 1: Chọn K điểm làm tâm cụm ban đầu (centroids)
Bước 2: Gán mỗi điểm dữ liệu vào cụm có tâm gần nhất
Bước 3: Tính lại tâm cụm mới = trung bình các điểm trong cụm
Bước 4: Lặp lại Bước 2-3 cho đến khi hội tụ (tâm cụm không đổi)
```

## 1.3. Công thức quan trọng

### Khoảng cách Euclidean (2 chiều):
```
d(A, B) = √[(x₂ - x₁)² + (y₂ - y₁)²]
```

### Khoảng cách Euclidean (n chiều):
```
d(A, B) = √[Σᵢ₌₁ⁿ (aᵢ - bᵢ)²]
```

### Tính tâm cụm (Centroid):
```
Centroid = (x̄, ȳ) = (Σxᵢ/n, Σyᵢ/n)
```
Với n là số điểm trong cụm.

---

## 1.4. BÀI TẬP MẪU K-MEANS

### Bài tập 1: Phân cụm K=2

**Cho tập dữ liệu:**
| Điểm | x | y |
|------|---|---|
| A | 1 | 1 |
| B | 2 | 1 |
| C | 4 | 3 |
| D | 5 | 4 |

**Tâm cụm ban đầu:** C₁ = A(1,1), C₂ = C(4,3)

---

**VÒNG LẶP 1:**

**Bước 1: Tính khoảng cách từ mỗi điểm đến các tâm cụm**

| Điểm | d(điểm, C₁) | d(điểm, C₂) | Gán vào cụm |
|------|-------------|-------------|-------------|
| A(1,1) | √[(1-1)²+(1-1)²] = 0 | √[(4-1)²+(3-1)²] = √13 ≈ 3.61 | **C₁** |
| B(2,1) | √[(2-1)²+(1-1)²] = 1 | √[(4-2)²+(3-1)²] = √8 ≈ 2.83 | **C₁** |
| C(4,3) | √[(4-1)²+(3-1)²] = √13 ≈ 3.61 | √[(4-4)²+(3-3)²] = 0 | **C₂** |
| D(5,4) | √[(5-1)²+(4-1)²] = √25 = 5 | √[(5-4)²+(4-3)²] = √2 ≈ 1.41 | **C₂** |

**Kết quả vòng 1:**
- Cụm 1: {A, B}
- Cụm 2: {C, D}

**Bước 2: Tính tâm cụm mới**
```
C₁_mới = ((1+2)/2, (1+1)/2) = (1.5, 1)
C₂_mới = ((4+5)/2, (3+4)/2) = (4.5, 3.5)
```

---

**VÒNG LẶP 2:**

**Tính khoảng cách với tâm mới:**

| Điểm | d(điểm, C₁) | d(điểm, C₂) | Gán vào cụm |
|------|-------------|-------------|-------------|
| A(1,1) | √[(1.5-1)²+(1-1)²] = 0.5 | √[(4.5-1)²+(3.5-1)²] = √18.5 ≈ 4.30 | **C₁** |
| B(2,1) | √[(2-1.5)²+(1-1)²] = 0.5 | √[(4.5-2)²+(3.5-1)²] = √12.5 ≈ 3.54 | **C₁** |
| C(4,3) | √[(4-1.5)²+(3-1)²] = √10.25 ≈ 3.20 | √[(4.5-4)²+(3.5-3)²] = √0.5 ≈ 0.71 | **C₂** |
| D(5,4) | √[(5-1.5)²+(4-1)²] = √21.25 ≈ 4.61 | √[(5-4.5)²+(4-3.5)²] = √0.5 ≈ 0.71 | **C₂** |

**Kết quả:** Phân cụm không đổi → **HỘI TỤ**

**Kết quả cuối cùng:**
- **Cụm 1:** {A(1,1), B(2,1)} với tâm (1.5, 1)
- **Cụm 2:** {C(4,3), D(5,4)} với tâm (4.5, 3.5)

---

# PHẦN 2: HỒI QUY TUYẾN TÍNH (LINEAR REGRESSION)

## 2.1. Giới thiệu
Hồi quy tuyến tính dùng để dự đoán giá trị đầu ra liên tục dựa trên các đặc trưng đầu vào.

## 2.2. Hàm giả thuyết (Hypothesis Function)

### Hồi quy đơn biến:
```
h(x) = θ₀ + θ₁x
```

### Hồi quy đa biến:
```
h(x) = θ₀ + θ₁x₁ + θ₂x₂ + ... + θₙxₙ
```

Hoặc dạng vector:
```
h(x) = θᵀx
```

## 2.3. Hàm chi phí (Cost Function) - MSE

```
J(θ) = (1/2m) × Σᵢ₌₁ᵐ [h(xⁱ) - yⁱ]²
```

Trong đó:
- m = số mẫu huấn luyện
- h(xⁱ) = giá trị dự đoán
- yⁱ = giá trị thực

## 2.4. Gradient Descent (Hạ gradient)

### Công thức cập nhật tham số:
```
θⱼ := θⱼ - α × (∂J/∂θⱼ)
```

### Đạo hàm riêng:
```
∂J/∂θⱼ = (1/m) × Σᵢ₌₁ᵐ [h(xⁱ) - yⁱ] × xⱼⁱ
```

### Công thức cập nhật cụ thể:
```
θ₀ := θ₀ - α × (1/m) × Σᵢ₌₁ᵐ [h(xⁱ) - yⁱ]
θ₁ := θ₁ - α × (1/m) × Σᵢ₌₁ᵐ [h(xⁱ) - yⁱ] × xⁱ
```

Trong đó: **α** = learning rate (tốc độ học)

## 2.5. Normal Equation (Phương trình chuẩn)

```
θ = (XᵀX)⁻¹ × Xᵀy
```

---

## 2.6. BÀI TẬP MẪU HỒI QUY TUYẾN TÍNH

### Bài tập: Gradient Descent 1 vòng lặp

**Cho dữ liệu:**
| x | y |
|---|---|
| 1 | 1 |
| 2 | 2 |
| 3 | 3 |

**Tham số ban đầu:** θ₀ = 0, θ₁ = 0, α = 0.1

---

**BƯỚC 1: Tính h(x) với θ₀=0, θ₁=0**
```
h(x) = θ₀ + θ₁x = 0 + 0×x = 0
```

| xⁱ | yⁱ | h(xⁱ) | h(xⁱ) - yⁱ |
|----|----|----|------------|
| 1 | 1 | 0 | 0 - 1 = -1 |
| 2 | 2 | 0 | 0 - 2 = -2 |
| 3 | 3 | 0 | 0 - 3 = -3 |

**BƯỚC 2: Tính đạo hàm riêng**

```
∂J/∂θ₀ = (1/3) × [(-1) + (-2) + (-3)] = (1/3) × (-6) = -2

∂J/∂θ₁ = (1/3) × [(-1)×1 + (-2)×2 + (-3)×3]
       = (1/3) × [-1 - 4 - 9] = (1/3) × (-14) = -14/3 ≈ -4.67
```

**BƯỚC 3: Cập nhật θ**
```
θ₀_mới = θ₀ - α × (∂J/∂θ₀) = 0 - 0.1 × (-2) = 0.2
θ₁_mới = θ₁ - α × (∂J/∂θ₁) = 0 - 0.1 × (-14/3) = 14/30 ≈ 0.467
```

**Kết quả sau 1 vòng lặp:**
- **θ₀ = 0.2**
- **θ₁ ≈ 0.467**

---

# PHẦN 3: MẠNG NƠ-RON NHÂN TẠO (ANN)

## 3.1. Cấu trúc mạng nơ-ron

```
Input Layer → Hidden Layer(s) → Output Layer
   (x)              (a)              (ŷ)
```

## 3.2. Hàm kích hoạt (Activation Functions)

### Sigmoid:
```
σ(z) = 1 / (1 + e⁻ᶻ)
```

Đạo hàm: `σ'(z) = σ(z) × (1 - σ(z))`

### ReLU:
```
ReLU(z) = max(0, z)
```

### Tanh:
```
tanh(z) = (eᶻ - e⁻ᶻ) / (eᶻ + e⁻ᶻ)
```

## 3.3. Forward Propagation (Lan truyền tiến)

**Tính output của mỗi node:**
```
z = Σ(wᵢ × xᵢ) + b = w₁x₁ + w₂x₂ + ... + wₙxₙ + b
a = σ(z)   (hoặc hàm kích hoạt khác)
```

Trong đó:
- wᵢ = trọng số (weight)
- xᵢ = đầu vào
- b = bias
- a = activation (đầu ra sau khi qua hàm kích hoạt)

## 3.4. Backpropagation (Lan truyền ngược)

### Tính sai số (error) tại output layer:
```
δ_output = (ŷ - y) × σ'(z)
```

### Tính sai số tại hidden layer:
```
δ_hidden = (Σ wⱼ × δⱼ) × σ'(z)
```

### Cập nhật trọng số:
```
w_mới = w_cũ - α × δ × x
b_mới = b_cũ - α × δ
```

---

## 3.5. BÀI TẬP MẪU MẠNG NƠ-RON

### Bài tập: Forward Propagation

**Cho mạng nơ-ron:**
- Input: x₁ = 0.5, x₂ = 0.3
- Hidden layer: 1 node với w₁ = 0.4, w₂ = 0.6, b₁ = 0.1
- Output layer: 1 node với w₃ = 0.5, b₂ = 0.2
- Hàm kích hoạt: Sigmoid

---

**BƯỚC 1: Tính giá trị tại Hidden Layer**
```
z₁ = w₁×x₁ + w₂×x₂ + b₁
z₁ = 0.4×0.5 + 0.6×0.3 + 0.1
z₁ = 0.2 + 0.18 + 0.1 = 0.48

a₁ = σ(z₁) = 1/(1 + e⁻⁰·⁴⁸)
a₁ = 1/(1 + 0.6188) = 1/1.6188 ≈ 0.618
```

**BƯỚC 2: Tính giá trị tại Output Layer**
```
z₂ = w₃×a₁ + b₂
z₂ = 0.5×0.618 + 0.2
z₂ = 0.309 + 0.2 = 0.509

ŷ = σ(z₂) = 1/(1 + e⁻⁰·⁵⁰⁹)
ŷ = 1/(1 + 0.601) = 1/1.601 ≈ 0.625
```

**Kết quả:** Output = **0.625**

---

### Bài tập: Backpropagation 1 vòng

**Tiếp theo bài trên, giả sử:**
- y (giá trị thực) = 1
- Learning rate α = 0.5

---

**BƯỚC 1: Tính sai số tại Output**
```
δ₂ = (ŷ - y) × σ'(z₂)
   = (ŷ - y) × ŷ × (1 - ŷ)
   = (0.625 - 1) × 0.625 × (1 - 0.625)
   = (-0.375) × 0.625 × 0.375
   = -0.0879
```

**BƯỚC 2: Cập nhật trọng số output layer**
```
w₃_mới = w₃ - α × δ₂ × a₁
       = 0.5 - 0.5 × (-0.0879) × 0.618
       = 0.5 + 0.0272 = 0.527

b₂_mới = b₂ - α × δ₂
       = 0.2 - 0.5 × (-0.0879)
       = 0.2 + 0.044 = 0.244
```

**BƯỚC 3: Tính sai số tại Hidden Layer**
```
δ₁ = δ₂ × w₃ × σ'(z₁)
   = δ₂ × w₃ × a₁ × (1 - a₁)
   = (-0.0879) × 0.5 × 0.618 × (1 - 0.618)
   = (-0.0879) × 0.5 × 0.618 × 0.382
   = -0.0104
```

**BƯỚC 4: Cập nhật trọng số hidden layer**
```
w₁_mới = w₁ - α × δ₁ × x₁
       = 0.4 - 0.5 × (-0.0104) × 0.5
       = 0.4 + 0.0026 = 0.4026

w₂_mới = w₂ - α × δ₁ × x₂
       = 0.6 - 0.5 × (-0.0104) × 0.3
       = 0.6 + 0.0016 = 0.6016

b₁_mới = b₁ - α × δ₁
       = 0.1 - 0.5 × (-0.0104)
       = 0.1 + 0.0052 = 0.1052
```

**Kết quả sau 1 vòng Backpropagation:**
| Tham số | Giá trị cũ | Giá trị mới |
|---------|------------|-------------|
| w₁ | 0.4 | 0.4026 |
| w₂ | 0.6 | 0.6016 |
| b₁ | 0.1 | 0.1052 |
| w₃ | 0.5 | 0.527 |
| b₂ | 0.2 | 0.244 |

---

# PHẦN 4: BẢNG TRA CỨU NHANH

## Giá trị Sigmoid thường dùng:

| z | σ(z) |
|---|------|
| 0 | 0.5 |
| 1 | 0.731 |
| 2 | 0.881 |
| -1 | 0.269 |
| -2 | 0.119 |
| 0.5 | 0.622 |
| -0.5 | 0.378 |

## Giá trị e thường dùng:
```
e ≈ 2.718
e⁻¹ ≈ 0.368
e⁻² ≈ 0.135
e⁻⁰·⁵ ≈ 0.607
e⁰·⁵ ≈ 1.649
e¹ ≈ 2.718
e² ≈ 7.389
```

## Căn bậc hai thường dùng:
```
√2 ≈ 1.414
√3 ≈ 1.732
√5 ≈ 2.236
√8 ≈ 2.828
√10 ≈ 3.162
√13 ≈ 3.606
```

---

# PHẦN 5: TÓM TẮT CÔNG THỨC

## K-MEANS:
```
Khoảng cách: d = √[Σ(aᵢ - bᵢ)²]
Tâm cụm:     C = (Σxᵢ/n, Σyᵢ/n)
```

## HỒI QUY TUYẾN TÍNH:
```
Giả thuyết:  h(x) = θ₀ + θ₁x
Chi phí:     J(θ) = (1/2m)Σ[h(xⁱ) - yⁱ]²
Cập nhật:    θⱼ := θⱼ - α(1/m)Σ[h(xⁱ) - yⁱ]xⱼⁱ
```

## MẠNG NƠ-RON:
```
Forward:     z = Σwᵢxᵢ + b; a = σ(z)
Sigmoid:     σ(z) = 1/(1 + e⁻ᶻ)
Đạo hàm:     σ'(z) = σ(z)(1 - σ(z))
Error:       δ = (ŷ - y) × σ'(z)
Cập nhật:    w := w - α × δ × x
```

---

*Tài liệu được tạo cho mục đích ôn tập cuối kỳ*
*Môn: Một số Thuật toán Thông minh*
