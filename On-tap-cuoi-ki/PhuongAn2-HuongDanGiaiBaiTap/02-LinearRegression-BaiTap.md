# PHƯƠNG ÁN 2: HƯỚNG DẪN GIẢI BÀI TẬP TỪNG BƯỚC
# BÀI TẬP HỒI QUY TUYẾN TÍNH (LINEAR REGRESSION)

---

## 📚 MỤC LỤC

1. [Dạng bài tập thường gặp](#1-dạng-bài-tập-thường-gặp)
2. [Bài tập 1: Tính giá trị dự đoán](#2-bài-tập-1-tính-giá-trị-dự-đoán)
3. [Bài tập 2: Gradient Descent 1 vòng](#3-bài-tập-2-gradient-descent-1-vòng)
4. [Bài tập 3: Gradient Descent nhiều vòng](#4-bài-tập-3-gradient-descent-nhiều-vòng)
5. [Bài tập thực tế: Dự đoán điểm thi](#5-bài-tập-thực-tế-dự-đoán-điểm-thi)
6. [Mẹo làm bài](#6-mẹo-làm-bài)

---

# 1. DẠNG BÀI TẬP THƯỜNG GẶP

## 1.1. Các dạng đề phổ biến

| Dạng | Mô tả | Độ khó |
|------|-------|--------|
| Dạng 1 | Tính $\hat{y}$ cho trước $w, b$ | ⭐ |
| Dạng 2 | Tính Loss cho từng điểm dữ liệu | ⭐⭐ |
| Dạng 3 | Thực hiện 1 vòng Gradient Descent | ⭐⭐⭐ |
| Dạng 4 | Thực hiện nhiều vòng GD | ⭐⭐⭐⭐ |

## 1.2. Công thức cần nhớ (Theo Slide)

### Hàm dự đoán:
$$\hat{y} = w \cdot x + b$$

### Hàm Loss (cho 1 điểm dữ liệu):
$$L = (\hat{y}_i - y_i)^2$$

### Công thức đạo hàm:
$$\frac{\partial L}{\partial w} = 2 \cdot x_i \cdot (\hat{y}_i - y_i)$$
$$\frac{\partial L}{\partial b} = 2 \cdot (\hat{y}_i - y_i)$$

### Công thức cập nhật (Gradient Descent):
$$w_{new} = w - \eta \cdot \frac{\partial L}{\partial w}$$
$$b_{new} = b - \eta \cdot \frac{\partial L}{\partial b}$$

---

# 2. BÀI TẬP 1: TÍNH GIÁ TRỊ DỰ ĐOÁN

## 2.1. Đề bài

Cho hàm dự đoán $\hat{y} = w \cdot x + b$ với $w = 10$, $b = 5$.

**Tính:**
a) $\hat{y}$ khi $x = 3$
b) $\hat{y}$ khi $x = 7$
c) $\hat{y}$ khi $x = 0$

---

## 2.2. Lời giải chi tiết

### Bước 1: Xác định công thức
$$\hat{y} = w \cdot x + b = 10x + 5$$

### Bước 2: Thay giá trị

**a) x = 3:**
$$\hat{y} = 10 \times 3 + 5 = 30 + 5 = 35$$

**b) x = 7:**
$$\hat{y} = 10 \times 7 + 5 = 70 + 5 = 75$$

**c) x = 0:**
$$\hat{y} = 10 \times 0 + 5 = 0 + 5 = 5$$

---

## 2.3. Đáp án

| x | $\hat{y} = 10x + 5$ |
|---|---------------------|
| 3 | 35 |
| 7 | 75 |
| 0 | 5 |

---

# 3. BÀI TẬP 2: GRADIENT DESCENT 1 VÒNG

## 3.1. Đề bài

Cho tập dữ liệu huấn luyện:

| Index | $x$ (Kinh nghiệm) | $y$ (Lương - triệu) |
|:---:|:---:|:---:|
| 0 | 3 | 60 |
| 1 | 4 | 55 |
| 2 | 5 | 66 |
| 3 | 6 | 93 |

**Yêu cầu:** Thực hiện **1 iteration** Gradient Descent với:
- $w$ ban đầu = 10
- $b$ ban đầu = 5
- Learning rate $\eta$ = 0.01
- Sử dụng **mẫu đầu tiên** ($x_0 = 3$, $y_0 = 60$)

---

## 3.2. Phân tích đề

- Tham số: $w = 10$, $b = 5$, $\eta = 0.01$
- Dữ liệu mẫu 0: $x_0 = 3$, $y_0 = 60$

**Quy trình (theo Slide):**
1. Tính Output $\hat{y}$
2. Tính Loss $L$
3. Tính đạo hàm $\frac{\partial L}{\partial w}$ và $\frac{\partial L}{\partial b}$
4. Cập nhật $w$ và $b$

---

## 3.3. Lời giải chi tiết

### Bước 1: Tính Output
$$\hat{y}_0 = w \cdot x_0 + b = 10 \times 3 + 5 = 35$$

### Bước 2: Tính Loss
$$L = (\hat{y}_0 - y_0)^2 = (35 - 60)^2 = (-25)^2 = 625$$

> [!WARNING]
> Loss = 625 là cao! Mô hình dự đoán 35 triệu nhưng thực tế là 60 triệu.

### Bước 3: Tính đạo hàm

**Đạo hàm theo w:**
$$\frac{\partial L}{\partial w} = 2 \times x_0 \times (\hat{y}_0 - y_0)$$
$$= 2 \times 3 \times (35 - 60)$$
$$= 6 \times (-25) = -150$$

**Đạo hàm theo b:**
$$\frac{\partial L}{\partial b} = 2 \times (\hat{y}_0 - y_0)$$
$$= 2 \times (-25) = -50$$

### Bước 4: Cập nhật tham số

**Cập nhật w:**
$$w_{new} = w - \eta \cdot \frac{\partial L}{\partial w}$$
$$= 10 - 0.01 \times (-150)$$
$$= 10 + 1.5 = 11.5$$

**Cập nhật b:**
$$b_{new} = b - \eta \cdot \frac{\partial L}{\partial b}$$
$$= 5 - 0.01 \times (-50)$$
$$= 5 + 0.5 = 5.5$$

---

## 3.4. Kết quả

```
┌─────────────────────────────────────────────────────────┐
│         KẾT QUẢ SAU 1 ITERATION GRADIENT DESCENT        │
├─────────────────────────────────────────────────────────┤
│                                                         │
│   w = 11.5                                              │
│   b = 5.5                                               │
│                                                         │
│   Hàm mới: ŷ = 11.5x + 5.5                              │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

---

# 4. BÀI TẬP 3: GRADIENT DESCENT NHIỀU VÒNG

## 4.1. Đề bài

*Tiếp tục Bài tập 2*

Thực hiện thêm **1 iteration** nữa với **mẫu dữ liệu thứ 1** ($x_1 = 4$, $y_1 = 55$).

---

## 4.2. Lời giải

**Trạng thái:** $w = 11.5$, $b = 5.5$, $\eta = 0.01$
**Dữ liệu:** $x_1 = 4$, $y_1 = 55$

### Bước 1: Tính Output
$$\hat{y}_1 = 11.5 \times 4 + 5.5 = 46 + 5.5 = 51.5$$

### Bước 2: Tính Loss
$$L = (51.5 - 55)^2 = (-3.5)^2 = 12.25$$

> [!NOTE]
> Loss giảm từ 625 xuống còn 12.25! Mô hình đang học tốt.

### Bước 3: Tính đạo hàm

$$\frac{\partial L}{\partial w} = 2 \times 4 \times (51.5 - 55) = 8 \times (-3.5) = -28$$
$$\frac{\partial L}{\partial b} = 2 \times (-3.5) = -7$$

### Bước 4: Cập nhật

$$w_{new} = 11.5 - 0.01 \times (-28) = 11.5 + 0.28 = 11.78$$
$$b_{new} = 5.5 - 0.01 \times (-7) = 5.5 + 0.07 = 5.57$$

---

## 4.3. Tổng kết tiến trình

| Iteration | Mẫu dùng | $w$ | $b$ | Loss |
|:---:|:---:|:---:|:---:|:---:|
| 0 (Ban đầu) | - | 10 | 5 | - |
| 1 | ($x_0=3, y_0=60$) | 11.5 | 5.5 | 625 |
| 2 | ($x_1=4, y_1=55$) | 11.78 | 5.57 | 12.25 |

**Nhận xét:** Qua mỗi iteration, $w$ và $b$ dần tiến về giá trị tối ưu.

---

# 5. BÀI TẬP THỰC TẾ: DỰ ĐOÁN ĐIỂM THI

## 5.1. Đề bài

> **Bài tập 4:**
> 
> Một trường Đại học khảo sát số giờ học ở nhà trong tuần sinh viên giành môn học Giải tích 1 và kết quả đạt được sau khi kết thúc môn học, thống kê được như sau:
> 
> | Hours | Scores |
> |:---:|:---:|
> | 2.0 | 4.1 |
> | 4.6 | 6.7 |
> | 2.5 | 4.7 |
> | 8.0 | 8.2 |
> | 3.0 | 5.0 |
> | 1.0 | 3.2 |
> | 8.7 | 9.3 |
> | 5.0 | 7.0 |
> 
> Sử dụng phương pháp hồi quy tuyến tính để dự đoán một sinh viên có giờ học tại nhà là **6.5 giờ** thì điểm đạt được là bao nhiêu.


---

## 5.2. Lời giải (Thực hiện 8 iterations - mỗi mẫu 1 lần)

### Iteration 1: Mẫu ($x=2.0$, $y=4.1$)

**Output:** $\hat{y} = 0.5 \times 2.0 + 2 = 3.0$
**Loss:** $L = (3.0 - 4.1)^2 = 1.21$
**Đạo hàm:** $\frac{\partial L}{\partial w} = 2 \times 2.0 \times (-1.1) = -4.4$, $\frac{\partial L}{\partial b} = -2.2$
**Cập nhật:** $w = 0.5 + 0.044 = 0.544$, $b = 2 + 0.022 = 2.022$

### Iteration 2: Mẫu ($x=4.6$, $y=6.7$)

**Output:** $\hat{y} = 0.544 \times 4.6 + 2.022 = 4.524$
**Loss:** $L = (4.524 - 6.7)^2 = 4.73$
**Đạo hàm:** $\frac{\partial L}{\partial w} = 2 \times 4.6 \times (-2.176) = -20.02$, $\frac{\partial L}{\partial b} = -4.35$
**Cập nhật:** $w = 0.544 + 0.200 = 0.744$, $b = 2.022 + 0.044 = 2.066$

*(Tiếp tục tương tự cho các mẫu còn lại...)*

---

## 5.3. Kết quả sau khi huấn luyện

Sau khi duyệt qua tất cả 8 mẫu dữ liệu, giả sử ta được:
- $w \approx 0.75$
- $b \approx 2.78$

**Phương trình hồi quy:** $\hat{y} = 0.75x + 2.78$

### Dự đoán cho sinh viên học 6.5 giờ:
$$\hat{y} = 0.75 \times 6.5 + 2.78 = 4.875 + 2.78 = 7.655$$

**✅ Kết luận:** Sinh viên học 6.5 giờ dự kiến đạt khoảng **7.6 điểm**.

---

## 5.4. 🚀 MỞ RỘNG: Phương pháp Bình phương tối thiểu (Nhanh hơn!)

> [!CAUTION]
> **Lưu ý:** Phương pháp này **KHÔNG có trong slide bài giảng**, nhưng là cách giải NHANH và CHÍNH XÁC cho bài toán hồi quy tuyến tính.

### Công thức:
$$w = \frac{n\sum xy - \sum x \sum y}{n\sum x^2 - (\sum x)^2}$$
$$b = \bar{y} - w \cdot \bar{x}$$

### Các bước thực hiện:

**Bước 1: Lập bảng tính**

| STT | $x$ | $y$ | $x^2$ | $xy$ |
|:---:|:---:|:---:|:---:|:---:|
| 1 | 2.0 | 4.1 | 4.00 | 8.20 |
| 2 | 4.6 | 6.7 | 21.16 | 30.82 |
| 3 | 2.5 | 4.7 | 6.25 | 11.75 |
| 4 | 8.0 | 8.2 | 64.00 | 65.60 |
| 5 | 3.0 | 5.0 | 9.00 | 15.00 |
| 6 | 1.0 | 3.2 | 1.00 | 3.20 |
| 7 | 8.7 | 9.3 | 75.69 | 80.91 |
| 8 | 5.0 | 7.0 | 25.00 | 35.00 |
| **Σ** | **34.8** | **48.2** | **206.1** | **250.48** |

**Bước 2: Tính các giá trị**

- $n = 8$
- $\bar{x} = 34.8 / 8 = 4.35$
- $\bar{y} = 48.2 / 8 = 6.025$

**Bước 3: Tính $w$**
$$w = \frac{8 \times 250.48 - 34.8 \times 48.2}{8 \times 206.1 - 34.8^2}$$
$$= \frac{2003.84 - 1677.36}{1648.8 - 1211.04}$$
$$= \frac{326.48}{437.76} \approx 0.7458$$

**Bước 4: Tính $b$**
$$b = 6.025 - 0.7458 \times 4.35 = 6.025 - 3.244 = 2.781$$

**Phương trình hồi quy:** $\hat{y} = 0.75x + 2.78$

**Bước 5: Dự đoán**
$$\hat{y} = 0.75 \times 6.5 + 2.78 = 7.655 \approx \textbf{7.6 điểm}$$

> [!TIP]
> **So sánh:** Phương pháp Least Squares cho **đáp án chính xác** chỉ với 5 bước tính đơn giản, không cần lặp như Gradient Descent!

---

## 5.5. 📱 MẸO: Bấm máy Casio 580VNX (SIÊU NHANH!)

> [!NOTE]
> Casio 580VNX có chế độ **Statistics** tính hồi quy tuyến tính **TỰ ĐỘNG**. Chỉ mất ~1 phút thay vì 10+ phút tính tay!

---

### 📌 Bước 1: Vào chế độ Statistics (Thống kê)

**Thao tác:**
1. Bấm phím `MENU` (góc trái trên màn hình)
2. Màn hình hiện menu chính, bấm số `6` để chọn **Statistics**
3. Màn hình hỏi chọn loại hồi quy, bấm số `2` để chọn **y = a + bx** (hồi quy tuyến tính)

```
MENU → 6 → 2
```

**Giải thích:** Chế độ này cho phép máy tự tính các hệ số $a$ và $b$ trong phương trình $y = a + bx$ từ dữ liệu bạn nhập.

---

### 📌 Bước 2: Nhập dữ liệu vào máy

**Màn hình sẽ hiện bảng có 2 cột: X và Y**

**Cách nhập:**
- Nhập giá trị $x$ → bấm `=` → nhập giá trị $y$ → bấm `=`
- Sau mỗi cặp, con trỏ tự động xuống dòng mới

**Ví dụ với bài toán dự đoán điểm thi:**

| Lần nhập | Bấm phím | Kết quả trên màn hình |
|:---:|:---|:---|
| 1 | `2.0` `=` `4.1` `=` | X₁ = 2.0, Y₁ = 4.1 |
| 2 | `4.6` `=` `6.7` `=` | X₂ = 4.6, Y₂ = 6.7 |
| 3 | `2.5` `=` `4.7` `=` | X₃ = 2.5, Y₃ = 4.7 |
| 4 | `8.0` `=` `8.2` `=` | X₄ = 8.0, Y₄ = 8.2 |
| 5 | `3.0` `=` `5.0` `=` | X₅ = 3.0, Y₅ = 5.0 |
| 6 | `1.0` `=` `3.2` `=` | X₆ = 1.0, Y₆ = 3.2 |
| 7 | `8.7` `=` `9.3` `=` | X₇ = 8.7, Y₇ = 9.3 |
| 8 | `5.0` `=` `7.0` `=` | X₈ = 5.0, Y₈ = 7.0 |

> [!TIP]
> **Mẹo:** Nếu nhập sai, dùng phím mũi tên để di chuyển đến ô cần sửa và nhập lại.

---

### 📌 Bước 3: Xem kết quả hệ số a và b

**Thao tác:**
1. Bấm `AC` (xóa màn hình nhập, quay về chế độ tính)
2. Bấm `SHIFT` → `1` (vào menu STAT)
3. Bấm `5` để chọn **Reg** (Regression - Hồi quy)
4. Chọn hệ số cần xem:
   - Bấm `1` → Hiện giá trị **a** = **2.7808** (đây là bias $b$)
   - Bấm `2` → Hiện giá trị **b** = **0.7458** (đây là weight $w$)

```
AC → SHIFT → 1 → 5 → 1 (xem a)
AC → SHIFT → 1 → 5 → 2 (xem b)
```

> [!WARNING]
> **⚠️ CHÚ Ý KÝ HIỆU RẤT QUAN TRỌNG:**
> 
> | Máy Casio | Slide bài giảng | Ý nghĩa |
> |:---:|:---:|:---|
> | $a$ | $b$ | Hệ số tự do (bias) |
> | $b$ | $w$ | Hệ số góc (weight) |
> 
> **Công thức Casio:** $y = a + bx$
> **Công thức Slide:** $\hat{y} = wx + b$
> 
> → **Đọc ngược:** $a_{casio} = b_{slide}$, $b_{casio} = w_{slide}$

---

### 📌 Bước 4: Dự đoán giá trị $\hat{y}$ cho x mới

**Bài toán:** Dự đoán điểm cho sinh viên học **6.5 giờ**?

**Thao tác:**
1. Bấm giá trị x cần dự đoán: `6.5`
2. Bấm `SHIFT` → `1` → `5` → `5` để chọn **ŷ** (y-predicted)
3. Bấm `=` để tính kết quả

```
6.5 → SHIFT → 1 → 5 → 5 → =
```

**Kết quả:** Màn hình hiện **7.6285** → Sinh viên dự kiến đạt **~7.6 điểm** ✓

---

### 📌 Bước 5 (Tùy chọn): Xem thêm các thông số khác

Sau khi vào `SHIFT → 1 → 5`, bạn có thể xem:

| Phím | Ký hiệu | Ý nghĩa |
|:---:|:---:|:---|
| 1 | a | Hệ số chặn (bias) |
| 2 | b | Hệ số góc (weight) |
| 3 | r | Hệ số tương quan (correlation) |
| 4 | x̂ | Dự đoán x khi biết y |
| 5 | ŷ | Dự đoán y khi biết x |

---

### ⚡ BẢNG TÓM TẮT PHÍM BẤM NHANH

| Thao tác | Phím bấm | Kết quả |
|:---|:---|:---|
| **Vào chế độ thống kê** | `MENU → 6 → 2` | Mở bảng nhập X, Y |
| **Nhập dữ liệu** | `x = y =` (lặp lại) | Thêm từng cặp dữ liệu |
| **Xem hệ số a (bias)** | `AC → SHIFT → 1 → 5 → 1` | Hiện giá trị a |
| **Xem hệ số b (weight)** | `AC → SHIFT → 1 → 5 → 2` | Hiện giá trị b |
| **Dự đoán ŷ** | `x_mới → SHIFT → 1 → 5 → 5 → =` | Hiện giá trị dự đoán |
| **Xóa và thoát** | `MENU → 1` | Quay về chế độ Calculate |

> [!IMPORTANT]
> **Lợi ích:** Với 8 điểm dữ liệu, bấm máy mất ~1 phút, trong khi tính tay (Gradient Descent hoặc Least Squares) mất 10-15 phút!

---


# 6. MẸO LÀM BÀI

## 6.1. Quy trình làm bài

```
┌─────────────────────────────────────────────────────────┐
│               QUY TRÌNH GRADIENT DESCENT                │
├─────────────────────────────────────────────────────────┤
│                                                         │
│   1. Xác định: w, b ban đầu, η, dữ liệu (x, y)         │
│                       ↓                                 │
│   2. Tính Output: ŷ = w × x + b                        │
│                       ↓                                 │
│   3. Tính Loss: L = (ŷ - y)²                           │
│                       ↓                                 │
│   4. Tính đạo hàm: dL/dw = 2x(ŷ-y), dL/db = 2(ŷ-y)    │
│                       ↓                                 │
│   5. Cập nhật: w = w - η×dL/dw, b = b - η×dL/db       │
│                       ↓                                 │
│   6. Lặp lại với mẫu dữ liệu tiếp theo                 │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

## 6.2. Bảng tính mẫu

| Iteration | $x$ | $y$ | $\hat{y}$ | $\hat{y}-y$ | $\frac{\partial L}{\partial w}$ | $\frac{\partial L}{\partial b}$ | $w_{new}$ | $b_{new}$ |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| 1 | | | | | | | | |
| 2 | | | | | | | | |
| 3 | | | | | | | | |

## 6.3. Công thức nhanh

| Bước | Công thức |
|:---|:---|
| **Output** | $\hat{y} = w \times x + b$ |
| **Loss** | $L = (\hat{y} - y)^2$ |
| **Đạo hàm w** | $2 \times x \times (\hat{y} - y)$ |
| **Đạo hàm b** | $2 \times (\hat{y} - y)$ |
| **Cập nhật** | Giá trị cũ $-$ $\eta$ $\times$ Đạo hàm |

## 6.4. Lưu ý quan trọng

1. **Dấu trừ:** Công thức cập nhật luôn có dấu **TRỪ** (để "xuống đồi").
2. **Thứ tự:** Tính hết đạo hàm rồi mới cập nhật (không cập nhật w trước khi tính đạo hàm b).
3. **Làm tròn:** Giữ 2-3 chữ số thập phân để tránh sai số tích lũy.
4. **Kiểm tra:** Loss phải **giảm dần** qua các iteration.

---

*Hết phần Bài tập Linear Regression - Phương án 2*
