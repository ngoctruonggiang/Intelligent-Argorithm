# PHƯƠNG ÁN 1: GIẢI THÍCH ĐƠN GIẢN

# HỒI QUY TUYẾN TÍNH (LINEAR REGRESSION)

---

## 📚 MỤC LỤC

1. [Giới thiệu tổng quan](#1-giới-thiệu-tổng-quan)
2. [Hồi quy tuyến tính là gì?](#2-hồi-quy-tuyến-tính-là-gì)
3. [Hàm giả thuyết (Hypothesis)](#3-hàm-giả-thuyết-hypothesis)
4. [Hàm chi phí (Cost Function)](#4-hàm-chi-phí-cost-function)
5. [Gradient Descent](#5-gradient-descent)
6. [Ví dụ minh họa từng bước](#6-ví-dụ-minh-họa-từng-bước)
7. [Phương trình chuẩn (Normal Equation)](#7-phương-trình-chuẩn-normal-equation)
8. [Hồi quy đa biến](#8-hồi-quy-đa-biến)
9. [Các vấn đề thường gặp](#9-các-vấn-đề-thường-gặp)
10. [Tổng kết](#10-tổng-kết)

---

# 1. GIỚI THIỆU TỔNG QUAN

## 1.1. Bài toán dự đoán là gì?

Trong cuộc sống, chúng ta thường muốn **dự đoán** một giá trị dựa trên các thông tin đã biết.

**Ví dụ thực tế:**

| Bài toán          | Đầu vào (Input)             | Đầu ra cần dự đoán (Output) |
| ----------------- | --------------------------- | --------------------------- |
| Dự đoán giá nhà   | Diện tích, vị trí, số phòng | Giá bán                     |
| Dự đoán điểm thi  | Số giờ học, điểm danh       | Điểm số                     |
| Dự đoán doanh thu | Chi phí quảng cáo           | Doanh thu                   |
| Dự đoán nhiệt độ  | Tháng, độ ẩm                | Nhiệt độ                    |

**Đặc điểm chung:** Đầu ra là một **giá trị liên tục** (continuous) - nghĩa là có thể là 3.5, 100.25, 1500000, v.v.

## 1.2. Tại sao cần học máy?

**Cách truyền thống:** Viết quy tắc thủ công

```
Nếu diện tích < 50m² → giá = 500 triệu
Nếu 50 ≤ diện tích < 100m² → giá = 1 tỷ
Nếu diện tích ≥ 100m² → giá = 2 tỷ
```

**Vấn đề:** Quá đơn giản, không chính xác, không linh hoạt.

**Cách học máy:** Cho máy tự học từ dữ liệu

```
Đưa cho máy 1000 căn nhà với giá thực tế
→ Máy tự tìm ra quy luật
→ Dự đoán giá nhà mới
```

**Ưu điểm:** Chính xác hơn, tự động, linh hoạt.

## 1.3. Phân loại bài toán học máy

### 1.3.1. Hồi quy (Regression)

- **Đầu ra:** Giá trị liên tục
- **Ví dụ:** Dự đoán giá nhà (100 triệu, 500 triệu, 1.2 tỷ...)

### 1.3.2. Phân loại (Classification)

- **Đầu ra:** Nhãn rời rạc
- **Ví dụ:** Phân loại email (Spam / Không spam)

**Hồi quy tuyến tính thuộc loại HỒI QUY** - dự đoán giá trị liên tục.

---

# 2. HỒI QUY TUYẾN TÍNH LÀ GÌ?

## 2.1. Định nghĩa đơn giản

**Hồi quy tuyến tính** là phương pháp tìm **đường thẳng** "khớp" nhất với tập dữ liệu, sau đó dùng đường thẳng đó để dự đoán.

```
      y (giá nhà)
      |           *
   15 |         *   /
   10 |       *   /     ← Đường thẳng dự đoán
    5 |     *   /
    0 |   * /
      +------------------→ x (diện tích)
         20  40  60  80
```

## 2.2. Tại sao gọi là "tuyến tính"?

**"Tuyến tính" = "Đường thẳng"**

Mối quan hệ giữa đầu vào (x) và đầu ra (y) được biểu diễn bằng một **đường thẳng**.

**Phương trình đường thẳng:** y = ax + b

Trong học máy, ta viết: **h(x) = θ₁x + θ₀**

## 2.3. Ví dụ trực quan

**Bài toán:** Bạn bán trà sữa. Bạn nhận thấy:

| Nhiệt độ (°C) | Số ly bán được |
| ------------- | -------------- |
| 25            | 50             |
| 30            | 70             |
| 35            | 90             |
| 40            | 110            |

**Đồ thị:**

```
Số ly |
 120  |               *
 100  |           *
  80  |       *
  60  |   *
  40  |
      +-------------------
         25  30  35  40  Nhiệt độ
```

**Nhận xét:** Các điểm gần như thẳng hàng!

→ Có thể dùng **đường thẳng** để mô tả mối quan hệ này.

**Câu hỏi:** Nếu mai trời 32°C, dự đoán bán được bao nhiêu ly?

**Giải pháp:** Tìm phương trình đường thẳng, rồi thay x = 32.

---

# 3. HÀM GIẢ THUYẾT (HYPOTHESIS)

## 3.1. Khái niệm

**Hàm giả thuyết** (Hypothesis Function) là **công thức dự đoán** mà chúng ta xây dựng.

**Ký hiệu:** h(x) hoặc hθ(x)

**Công thức:**

```
h(x) = θ₀ + θ₁x
```

Trong đó:

- **x**: Đầu vào (feature/input)
- **h(x)**: Giá trị dự đoán
- **θ₀** (theta-0): Hệ số chặn (intercept/bias)
- **θ₁** (theta-1): Hệ số góc (slope/weight)

## 3.2. Ý nghĩa của các tham số

### 3.2.1. θ₀ - Hệ số chặn (Intercept)

- Là giá trị của h(x) khi x = 0
- Điểm mà đường thẳng cắt trục y

```
      y
      |
   θ₀ |*
      | \
      |  \
      |   \
      +-------→ x
```

### 3.2.2. θ₁ - Hệ số góc (Slope)

- Cho biết đường thẳng dốc như thế nào
- θ₁ > 0: Đường đi lên (x tăng → y tăng)
- θ₁ < 0: Đường đi xuống (x tăng → y giảm)
- θ₁ = 0: Đường nằm ngang

```
θ₁ > 0:     θ₁ < 0:     θ₁ = 0:
    /           \         ───────
   /             \
```

## 3.3. Ví dụ tính toán

**Cho:** h(x) = 2 + 3x

**Tính h(x) khi x = 4:**

```
h(4) = 2 + 3×4
     = 2 + 12
     = 14
```

**Bảng giá trị:**

| x   | h(x) = 2 + 3x |
| --- | ------------- |
| 0   | 2 + 3×0 = 2   |
| 1   | 2 + 3×1 = 5   |
| 2   | 2 + 3×2 = 8   |
| 3   | 2 + 3×3 = 11  |
| 4   | 2 + 3×4 = 14  |

## 3.4. Vấn đề cốt lõi

**Câu hỏi:** Làm sao tìm được θ₀ và θ₁ tốt nhất?

**Trả lời:** Sử dụng:

1. **Hàm chi phí (Cost Function)** - đo độ sai
2. **Gradient Descent** - tìm θ tối ưu

---

# 4. HÀM CHI PHÍ (COST FUNCTION)

## 4.1. Ý tưởng

Trước khi tìm đường thẳng tốt nhất, ta cần cách **đo xem một đường thẳng tệ cỡ nào**.

**Ý tưởng:** So sánh giá trị dự đoán với giá trị thực tế.

```
      y
      |
   12 |         *(thực tế)
      |        /
   10 |      ○(dự đoán)
      |     /
      |    /
      +------------→ x

Sai số = |12 - 10| = 2
```

## 4.2. Định nghĩa hàm chi phí

**Hàm chi phí J(θ)** đo **tổng bình phương sai số** của tất cả các điểm dữ liệu.

**Công thức:**

```
J(θ₀, θ₁) = (1/2m) × Σᵢ₌₁ᵐ [h(xⁱ) - yⁱ]²
```

Trong đó:

- **m**: Số điểm dữ liệu
- **xⁱ**: Đầu vào của điểm thứ i
- **yⁱ**: Giá trị thực của điểm thứ i
- **h(xⁱ)**: Giá trị dự đoán của điểm thứ i
- **[h(xⁱ) - yⁱ]**: Sai số của điểm thứ i

## 4.3. Tại sao bình phương?

**Lý do 1:** Loại bỏ dấu âm

- Sai số có thể dương hoặc âm
- Bình phương luôn dương

**Ví dụ:**

```
Điểm 1: dự đoán = 10, thực tế = 12 → sai số = -2
Điểm 2: dự đoán = 8, thực tế = 6 → sai số = +2

Tổng sai số = -2 + 2 = 0  ← SAI! (vì thực tế có sai)
Tổng bình phương = 4 + 4 = 8  ← ĐÚNG!
```

**Lý do 2:** Phạt sai số lớn nhiều hơn

- Sai 1 đơn vị: 1² = 1
- Sai 2 đơn vị: 2² = 4
- Sai 3 đơn vị: 3² = 9

→ Sai số lớn bị "phạt" nặng hơn.

## 4.4. Tại sao chia 2m?

**Chia m:** Để lấy trung bình (không phụ thuộc vào số lượng dữ liệu)

**Chia 2:** Để thuận tiện khi lấy đạo hàm (số 2 sẽ triệt tiêu)

## 4.5. Ví dụ tính hàm chi phí

**Dữ liệu (m = 3):**

| i   | xⁱ  | yⁱ (thực tế) |
| --- | --- | ------------ |
| 1   | 1   | 1            |
| 2   | 2   | 2            |
| 3   | 3   | 3            |

**Giả sử:** θ₀ = 0, θ₁ = 1 → h(x) = 0 + 1×x = x

**Tính h(xⁱ) và sai số:**

| i   | xⁱ  | yⁱ  | h(xⁱ) = xⁱ | h(xⁱ) - yⁱ | [h(xⁱ) - yⁱ]² |
| --- | --- | --- | ---------- | ---------- | ------------- |
| 1   | 1   | 1   | 1          | 0          | 0             |
| 2   | 2   | 2   | 2          | 0          | 0             |
| 3   | 3   | 3   | 3          | 0          | 0             |

**Tính J(θ):**

```
J(θ) = (1/2×3) × (0 + 0 + 0)
     = (1/6) × 0
     = 0
```

**Nhận xét:** J = 0 nghĩa là đường thẳng "khớp" hoàn hảo với dữ liệu!

---

**Ví dụ khác:** θ₀ = 1, θ₁ = 0 → h(x) = 1

| i   | xⁱ  | yⁱ  | h(xⁱ) = 1 | h(xⁱ) - yⁱ | [h(xⁱ) - yⁱ]² |
| --- | --- | --- | --------- | ---------- | ------------- |
| 1   | 1   | 1   | 1         | 0          | 0             |
| 2   | 2   | 2   | 1         | -1         | 1             |
| 3   | 3   | 3   | 1         | -2         | 4             |

**Tính J(θ):**

```
J(θ) = (1/6) × (0 + 1 + 4)
     = (1/6) × 5
     = 5/6 ≈ 0.833
```

**Nhận xét:** J > 0 nghĩa là đường thẳng h(x) = 1 không tốt.

## 4.6. Mục tiêu

**MỤC TIÊU:** Tìm θ₀, θ₁ sao cho J(θ₀, θ₁) **nhỏ nhất** (minimum).

---

# 5. GRADIENT DESCENT

## 5.1. Ý tưởng

**Gradient Descent** (Hạ gradient) là phương pháp tìm giá trị nhỏ nhất của hàm chi phí bằng cách "đi xuống dốc".

**Ví dụ đời thường:**

Tưởng tượng bạn đang đứng trên một ngọn đồi trong sương mù. Bạn muốn đi xuống điểm thấp nhất nhưng không thấy xa được.

**Cách làm:**

1. Nhìn xung quanh, xác định hướng dốc nhất
2. Bước một bước về hướng đó
3. Lặp lại cho đến khi đến đáy

```
     *  ← Bạn đang ở đây
      \
       \
        \
         \_____* ← Điểm thấp nhất
```

## 5.2. Công thức Gradient Descent

**Công thức cập nhật:**

```
θⱼ := θⱼ - α × (∂J/∂θⱼ)
```

Trong đó:

- **θⱼ**: Tham số cần cập nhật
- **α** (alpha): Tốc độ học (learning rate)
- **∂J/∂θⱼ**: Đạo hàm riêng của J theo θⱼ (cho biết hướng dốc)
- **:=**: Gán giá trị mới

## 5.3. Giải thích từng thành phần

### 5.3.1. Đạo hàm (∂J/∂θⱼ)

**Đạo hàm cho biết:**

- Hướng đi lên hay đi xuống
- Độ dốc như thế nào

```
Đạo hàm > 0: Đang đi lên → cần giảm θ
Đạo hàm < 0: Đang đi xuống → cần tăng θ
Đạo hàm = 0: Đã ở đáy → DỪNG
```

### 5.3.2. Learning rate (α)

**α cho biết:** Bước đi lớn hay nhỏ

```
α nhỏ:                    α lớn:
    *                         *
     \                         \
      \                         \
       \                         +---*  ← Nhảy qua đáy!
        \_____                      \
              \_____*                 \_____*
```

**Chọn α như thế nào?**

- α quá nhỏ: Hội tụ rất chậm
- α quá lớn: Có thể không hội tụ (nhảy qua đáy)
- Giá trị thường dùng: 0.01, 0.1, 0.001

### 5.3.3. Tại sao trừ đi?

```
θ_mới = θ_cũ - α × đạo_hàm
```

- Nếu đạo hàm > 0: θ_mới < θ_cũ (giảm θ)
- Nếu đạo hàm < 0: θ_mới > θ_cũ (tăng θ)

→ Luôn đi **ngược hướng** với đạo hàm = đi xuống dốc!

## 5.4. Đạo hàm của hàm chi phí

### Đạo hàm theo θ₀:

```
∂J/∂θ₀ = (1/m) × Σᵢ₌₁ᵐ [h(xⁱ) - yⁱ]
```

### Đạo hàm theo θ₁:

```
∂J/∂θ₁ = (1/m) × Σᵢ₌₁ᵐ [h(xⁱ) - yⁱ] × xⁱ
```

## 5.5. Công thức cập nhật đầy đủ

Lặp lại cho đến khi hội tụ:

```
θ₀ := θ₀ - α × (1/m) × Σᵢ₌₁ᵐ [h(xⁱ) - yⁱ]

θ₁ := θ₁ - α × (1/m) × Σᵢ₌₁ᵐ [h(xⁱ) - yⁱ] × xⁱ
```

**LƯU Ý QUAN TRỌNG:** Phải cập nhật θ₀ và θ₁ **đồng thời** (simultaneous update)!

```
ĐÚNG:                           SAI:
temp0 = θ₀ - α × (...)          θ₀ = θ₀ - α × (...)
temp1 = θ₁ - α × (...)          θ₁ = θ₁ - α × (...)
θ₀ = temp0                      (Dùng θ₀ mới để tính θ₁)
θ₁ = temp1
```

---

# 6. VÍ DỤ MINH HỌA TỪNG BƯỚC

## 6.1. Đề bài

**Cho tập dữ liệu (m = 3):**

| xⁱ  | yⁱ  |
| --- | --- |
| 1   | 1   |
| 2   | 2   |
| 3   | 3   |

**Yêu cầu:** Thực hiện 2 vòng lặp Gradient Descent với:

- θ₀ ban đầu = 0
- θ₁ ban đầu = 0
- α = 0.1

---

## 6.2. Vòng lặp 1

### Bước 1: Tính h(xⁱ) với θ hiện tại

Với θ₀ = 0, θ₁ = 0:

```
h(x) = θ₀ + θ₁x = 0 + 0×x = 0
```

| i   | xⁱ  | yⁱ  | h(xⁱ) |
| --- | --- | --- | ----- |
| 1   | 1   | 1   | 0     |
| 2   | 2   | 2   | 0     |
| 3   | 3   | 3   | 0     |

### Bước 2: Tính sai số

| i   | xⁱ  | yⁱ  | h(xⁱ) | h(xⁱ) - yⁱ |
| --- | --- | --- | ----- | ---------- |
| 1   | 1   | 1   | 0     | 0 - 1 = -1 |
| 2   | 2   | 2   | 0     | 0 - 2 = -2 |
| 3   | 3   | 3   | 0     | 0 - 3 = -3 |

### Bước 3: Tính đạo hàm riêng

**Đạo hàm theo θ₀:**

```
∂J/∂θ₀ = (1/m) × Σ[h(xⁱ) - yⁱ]
       = (1/3) × [(-1) + (-2) + (-3)]
       = (1/3) × (-6)
       = -2
```

**Đạo hàm theo θ₁:**

```
∂J/∂θ₁ = (1/m) × Σ[h(xⁱ) - yⁱ] × xⁱ
       = (1/3) × [(-1)×1 + (-2)×2 + (-3)×3]
       = (1/3) × [-1 + (-4) + (-9)]
       = (1/3) × (-14)
       = -14/3 ≈ -4.667
```

### Bước 4: Cập nhật θ

```
θ₀_mới = θ₀_cũ - α × (∂J/∂θ₀)
       = 0 - 0.1 × (-2)
       = 0 + 0.2
       = 0.2

θ₁_mới = θ₁_cũ - α × (∂J/∂θ₁)
       = 0 - 0.1 × (-14/3)
       = 0 + 1.4/3
       = 0.467 (làm tròn)
```

**Kết quả sau Vòng 1:** θ₀ = 0.2, θ₁ = 0.467

---

## 6.3. Vòng lặp 2

### Bước 1: Tính h(xⁱ) với θ mới

Với θ₀ = 0.2, θ₁ = 0.467:

```
h(x) = 0.2 + 0.467x
```

| i   | xⁱ  | yⁱ  | h(xⁱ) = 0.2 + 0.467xⁱ |
| --- | --- | --- | --------------------- |
| 1   | 1   | 1   | 0.2 + 0.467×1 = 0.667 |
| 2   | 2   | 2   | 0.2 + 0.467×2 = 1.134 |
| 3   | 3   | 3   | 0.2 + 0.467×3 = 1.601 |

### Bước 2: Tính sai số

| i   | xⁱ  | yⁱ  | h(xⁱ) | h(xⁱ) - yⁱ |
| --- | --- | --- | ----- | ---------- |
| 1   | 1   | 1   | 0.667 | -0.333     |
| 2   | 2   | 2   | 1.134 | -0.866     |
| 3   | 3   | 3   | 1.601 | -1.399     |

### Bước 3: Tính đạo hàm riêng

**Đạo hàm theo θ₀:**

```
∂J/∂θ₀ = (1/3) × [(-0.333) + (-0.866) + (-1.399)]
       = (1/3) × (-2.598)
       = -0.866
```

**Đạo hàm theo θ₁:**

```
∂J/∂θ₁ = (1/3) × [(-0.333)×1 + (-0.866)×2 + (-1.399)×3]
       = (1/3) × [-0.333 + (-1.732) + (-4.197)]
       = (1/3) × (-6.262)
       = -2.087
```

### Bước 4: Cập nhật θ

```
θ₀_mới = 0.2 - 0.1 × (-0.866)
       = 0.2 + 0.0866
       = 0.287

θ₁_mới = 0.467 - 0.1 × (-2.087)
       = 0.467 + 0.209
       = 0.676
```

**Kết quả sau Vòng 2:** θ₀ = 0.287, θ₁ = 0.676

---

## 6.4. Tổng kết quá trình học

| Vòng        | θ₀    | θ₁    | h(x)           |
| ----------- | ----- | ----- | -------------- |
| 0 (ban đầu) | 0     | 0     | 0              |
| 1           | 0.2   | 0.467 | 0.2 + 0.467x   |
| 2           | 0.287 | 0.676 | 0.287 + 0.676x |
| ...         | ...   | ...   | ...            |
| Cuối cùng   | 0     | 1     | x              |

**Nhận xét:** Qua mỗi vòng, θ₀ và θ₁ dần tiến về giá trị tối ưu (θ₀ = 0, θ₁ = 1).

---

## 6.5. Kiểm tra kết quả

**Đường thẳng lý tưởng:** h(x) = x (vì y = x trong dữ liệu)

| x   | y thực | h(x) = x |
| --- | ------ | -------- |
| 1   | 1      | 1 ✓      |
| 2   | 2      | 2 ✓      |
| 3   | 3      | 3 ✓      |

**Kết luận:** Nếu chạy đủ vòng lặp, θ₀ → 0 và θ₁ → 1.

---

# 7. PHƯƠNG TRÌNH CHUẨN (NORMAL EQUATION)

## 7.1. Ý tưởng

Thay vì dùng Gradient Descent (lặp nhiều lần), có thể tính **trực tiếp** θ tối ưu bằng công thức toán học.

## 7.2. Công thức

```
θ = (XᵀX)⁻¹ × Xᵀy
```

Trong đó:

- **X**: Ma trận đầu vào (thêm cột 1 cho θ₀)
- **Xᵀ**: Ma trận chuyển vị của X
- **(XᵀX)⁻¹**: Ma trận nghịch đảo của XᵀX
- **y**: Vector đầu ra

## 7.3. Ví dụ

**Dữ liệu:**

| x   | y   |
| --- | --- |
| 1   | 1   |
| 2   | 2   |
| 3   | 3   |

**Bước 1: Xây dựng ma trận X (thêm cột 1)**

```
X = | 1  1 |
    | 1  2 |
    | 1  3 |
```

**Bước 2: Xây dựng vector y**

```
y = | 1 |
    | 2 |
    | 3 |
```

**Bước 3: Tính θ = (XᵀX)⁻¹ × Xᵀy**

(Các bước tính toán chi tiết - thường dùng máy tính)

**Kết quả:** θ₀ = 0, θ₁ = 1

## 7.4. So sánh Gradient Descent và Normal Equation

| Tiêu chí          | Gradient Descent | Normal Equation |
| ----------------- | ---------------- | --------------- |
| Cần chọn α        | Có               | Không           |
| Cần lặp nhiều lần | Có               | Không           |
| Tốc độ với n nhỏ  | Chậm hơn         | Nhanh hơn       |
| Tốc độ với n lớn  | Nhanh hơn        | Chậm hơn        |
| Độ phức tạp       | O(kn²)           | O(n³)           |

**Khi nào dùng gì?**

- **n < 10,000**: Normal Equation
- **n > 10,000**: Gradient Descent

---

# 8. HỒI QUY ĐA BIẾN

## 8.1. Khái niệm

Khi có **nhiều đầu vào** (features), ta gọi là **hồi quy đa biến** (Multiple Linear Regression).

**Ví dụ:** Dự đoán giá nhà dựa trên:

- x₁: Diện tích
- x₂: Số phòng ngủ
- x₃: Số tầng
- x₄: Tuổi nhà

## 8.2. Công thức

```
h(x) = θ₀ + θ₁x₁ + θ₂x₂ + θ₃x₃ + ... + θₙxₙ
```

Hoặc dạng vector:

```
h(x) = θᵀx
```

## 8.3. Gradient Descent cho đa biến

```
θⱼ := θⱼ - α × (1/m) × Σᵢ₌₁ᵐ [h(xⁱ) - yⁱ] × xⱼⁱ
```

Với j = 0, 1, 2, ..., n (cập nhật đồng thời tất cả θ)

## 8.4. Feature Scaling

**Vấn đề:** Các feature có phạm vi khác nhau

```
x₁ (diện tích): 50 - 500 m²
x₂ (số phòng): 1 - 5 phòng
```

→ Gradient Descent hội tụ chậm.

**Giải pháp:** Chuẩn hóa về cùng phạm vi

```
xⱼ_mới = (xⱼ - μⱼ) / sⱼ
```

Trong đó:

- μⱼ: Trung bình của feature j
- sⱼ: Độ lệch chuẩn (hoặc max - min)

---

# 9. CÁC VẤN ĐỀ THƯỜNG GẶP

## 9.1. Gradient Descent không hội tụ

**Nguyên nhân:**

1. α quá lớn
2. Bug trong code
3. Feature chưa được scale

**Giải pháp:**

1. Giảm α
2. Kiểm tra lại công thức
3. Áp dụng feature scaling

## 9.2. Underfitting (Thiếu khớp)

**Triệu chứng:** Đường thẳng không khớp tốt với dữ liệu

**Nguyên nhân:** Mô hình quá đơn giản

**Giải pháp:** Thêm features hoặc dùng mô hình phức tạp hơn

## 9.3. Overfitting (Quá khớp)

**Triệu chứng:** Khớp tốt với dữ liệu huấn luyện nhưng dự đoán kém trên dữ liệu mới

**Nguyên nhân:** Mô hình quá phức tạp

**Giải pháp:**

- Dùng regularization
- Thu thập thêm dữ liệu
- Giảm số features

---

# 10. TỔNG KẾT

## 10.1. Những điều cần nhớ

1. **Hồi quy tuyến tính** dự đoán giá trị liên tục bằng đường thẳng

2. **Hàm giả thuyết:**

   ```
   h(x) = θ₀ + θ₁x
   ```

3. **Hàm chi phí (MSE):**

   ```
   J(θ) = (1/2m) × Σ[h(xⁱ) - yⁱ]²
   ```

4. **Gradient Descent:**

   ```
   θⱼ := θⱼ - α × (∂J/∂θⱼ)
   ```

5. **Đạo hàm:**
   ```
   ∂J/∂θ₀ = (1/m) × Σ[h(xⁱ) - yⁱ]
   ∂J/∂θ₁ = (1/m) × Σ[h(xⁱ) - yⁱ] × xⁱ
   ```

## 10.2. Quy trình làm bài

1. **Xác định** h(x) = θ₀ + θ₁x
2. **Tính** h(xⁱ) cho mỗi điểm
3. **Tính sai số** [h(xⁱ) - yⁱ]
4. **Tính đạo hàm** riêng theo θ₀ và θ₁
5. **Cập nhật** θ₀ và θ₁
6. **Lặp lại** cho đến khi hội tụ hoặc đủ vòng

## 10.3. Bài tập tự luyện

**Bài 1:** Cho dữ liệu:
| x | y |
|---|---|
| 1 | 2 |
| 2 | 4 |
| 3 | 6 |

Thực hiện 1 vòng Gradient Descent với θ₀ = 0, θ₁ = 0, α = 0.1.

**Bài 2:** Với h(x) = 3 + 2x, tính J(θ) khi dữ liệu là:
| x | y |
|---|---|
| 1 | 5 |
| 2 | 7 |
| 3 | 9 |

---

# 11. CÔNG THỨC TÍNH TRỰC TIẾP θ (QUAN TRỌNG CHO THI!)

> **⚠️ QUAN TRỌNG:** Đề thi thường yêu cầu tính θ₀, θ₁ rồi dự đoán, **KHÔNG phải lặp Gradient Descent nhiều vòng**. Phần này là **BẮT BUỘC phải biết**!

## 11.1. Công thức Least Squares (Bình phương tối thiểu)

### Công thức tính θ₁ (hệ số góc):

$$\theta_1 = \frac{n \sum x_i y_i - \sum x_i \sum y_i}{n \sum x_i^2 - (\sum x_i)^2}$$

### Công thức tính θ₀ (hệ số chặn):

$$\theta_0 = \bar{y} - \theta_1 \bar{x} = \frac{\sum y_i - \theta_1 \sum x_i}{n}$$

Trong đó:

- **n**: Số điểm dữ liệu
- **x̄**: Trung bình của x
- **ȳ**: Trung bình của y

## 11.2. Công thức thay thế (dễ nhớ hơn)

$$\theta_1 = \frac{\sum (x_i - \bar{x})(y_i - \bar{y})}{\sum (x_i - \bar{x})^2}$$

$$\theta_0 = \bar{y} - \theta_1 \times \bar{x}$$

---

# 12. BÀI MẪU: GIẢI ĐỀ THI THỰC TẾ (Linear Regression)

## 📝 ĐỀ BÀI (Giống Bài tập 4)

Một trường Đại học khảo sát số giờ học ở nhà và điểm đạt được:

| Hours (x) | Scores (y) |
| :-------: | :--------: |
|    2.0    |    4.1     |
|    4.6    |    6.7     |
|    2.5    |    4.7     |
|    8.0    |    8.2     |
|    3.0    |    5.0     |
|    1.0    |    3.2     |
|    8.7    |    9.3     |
|    5.0    |    7.0     |

**Yêu cầu:** Dùng hồi quy tuyến tính dự đoán điểm khi x = 6.5 giờ.

---

## 🔷 GIẢI CHI TIẾT

### Bước 1: Lập bảng tính các tổng cần thiết

|   i   |    xᵢ    |    yᵢ    |    xᵢ²     |    xᵢyᵢ    |
| :---: | :------: | :------: | :--------: | :--------: |
|   1   |   2.0    |   4.1    |    4.00    |    8.20    |
|   2   |   4.6    |   6.7    |   21.16    |   30.82    |
|   3   |   2.5    |   4.7    |    6.25    |   11.75    |
|   4   |   8.0    |   8.2    |   64.00    |   65.60    |
|   5   |   3.0    |   5.0    |    9.00    |   15.00    |
|   6   |   1.0    |   3.2    |    1.00    |    3.20    |
|   7   |   8.7    |   9.3    |   75.69    |   80.91    |
|   8   |   5.0    |   7.0    |   25.00    |   35.00    |
| **Σ** | **34.8** | **48.2** | **206.10** | **250.48** |

**Số điểm:** n = 8

### Bước 2: Tính θ₁

$$\theta_1 = \frac{n \sum x_i y_i - \sum x_i \sum y_i}{n \sum x_i^2 - (\sum x_i)^2}$$

```
θ₁ = [8 × 250.48 - 34.8 × 48.2] / [8 × 206.10 - (34.8)²]
   = [2003.84 - 1677.36] / [1648.80 - 1211.04]
   = 326.48 / 437.76
   = 0.7457 ≈ 0.75
```

### Bước 3: Tính θ₀

```
x̄ = Σxᵢ / n = 34.8 / 8 = 4.35
ȳ = Σyᵢ / n = 48.2 / 8 = 6.025

θ₀ = ȳ - θ₁ × x̄
   = 6.025 - 0.7457 × 4.35
   = 6.025 - 3.244
   = 2.781 ≈ 2.78
```

### Bước 4: Viết phương trình hồi quy

$$h(x) = 2.78 + 0.75x$$

### Bước 5: Dự đoán khi x = 6.5

```
h(6.5) = 2.78 + 0.75 × 6.5
       = 2.78 + 4.875
       = 7.655 ≈ 7.66
```

### ✅ KẾT LUẬN

Sinh viên học 6.5 giờ tại nhà dự đoán đạt **khoảng 7.66 điểm**.

---

## 📋 TEMPLATE LÀM BÀI (Copy để dùng)

```
BƯỚC 1: Lập bảng
┌────┬────────┬────────┬────────┬────────┐
│ i  │  xᵢ   │  yᵢ   │  xᵢ²  │ xᵢyᵢ  │
├────┼────────┼────────┼────────┼────────┤
│ 1  │        │        │        │        │
│ 2  │        │        │        │        │
│... │        │        │        │        │
├────┼────────┼────────┼────────┼────────┤
│ Σ  │        │        │        │        │
└────┴────────┴────────┴────────┴────────┘

n = _____

BƯỚC 2: Tính θ₁
θ₁ = [n×Σxᵢyᵢ - Σxᵢ×Σyᵢ] / [n×Σxᵢ² - (Σxᵢ)²]
   = [___ × ___ - ___ × ___] / [___ × ___ - (___)²]
   = [___ - ___] / [___ - ___]
   = ___ / ___
   = ___

BƯỚC 3: Tính θ₀
x̄ = Σxᵢ / n = ___ / ___ = ___
ȳ = Σyᵢ / n = ___ / ___ = ___

θ₀ = ȳ - θ₁ × x̄
   = ___ - ___ × ___
   = ___

BƯỚC 4: Phương trình hồi quy
h(x) = ___ + ___x

BƯỚC 5: Dự đoán
h(___) = ___ + ___ × ___
       = ___
```

---

# 13. SO SÁNH 2 PHƯƠNG PHÁP

| Tiêu chí         | Gradient Descent      | Công thức trực tiếp |
| ---------------- | --------------------- | ------------------- |
| **Dùng khi nào** | Lặp nhiều vòng (code) | Tính tay 1 lần      |
| **Đề thi**       | Ít gặp (1-2 vòng)     | **THƯỜNG GẶP**      |
| **Độ phức tạp**  | O(iterations × n)     | O(n)                |
| **Cần chọn α**   | Có                    | Không               |

**⚠️ TRONG ĐỀ THI:** 99% sẽ dùng **công thức trực tiếp**!

---

_Hết phần Linear Regression - Phương án 1: Giải thích đơn giản_

**Bài 3:** Giải thích tại sao learning rate α quá lớn có thể khiến Gradient Descent không hội tụ?

---

_Hết phần Linear Regression - Phương án 1: Giải thích đơn giản_
