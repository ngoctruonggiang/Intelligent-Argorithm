# PHƯƠNG ÁN 3: HỌC 1-1 THEO CHỦ ĐỀ
# HỒI QUY TUYẾN TÍNH - TỪ CƠ BẢN ĐẾN NÂNG CAO

---

## 🎯 MỤC TIÊU BÀI HỌC

Sau bài học này, bạn sẽ:
1. Hiểu được hồi quy tuyến tính dùng để làm gì
2. Nắm vững hàm giả thuyết và hàm chi phí
3. Thành thạo Gradient Descent
4. Tự tin giải bài tập tính θ

---

# PHẦN 1: KHÁI NIỆM CƠ BẢN

## 1.1. Bài toán dự đoán

**Giảng viên hỏi:** Bạn bán nước. Bạn nhận thấy trời nóng thì bán được nhiều. Làm sao dự đoán số ly bán được ngày mai nếu biết nhiệt độ?

**Suy nghĩ:**
- Có mối quan hệ giữa nhiệt độ và số ly bán
- Cần tìm ra "quy luật" từ dữ liệu quá khứ
- Dùng quy luật đó để dự đoán

→ Đây là bài toán **hồi quy**!

## 1.2. Tại sao gọi là "tuyến tính"?

**"Tuyến tính" = "Đường thẳng"**

Mối quan hệ giữa x và y được biểu diễn bằng đường thẳng:
```
y = ax + b
```

---

## ✅ KIỂM TRA HIỂU BIẾT 1

**Câu hỏi:** Hồi quy tuyến tính dự đoán loại giá trị nào?
- A) Nhãn rời rạc (Có/Không)
- B) Giá trị liên tục (100, 150.5, 200...)
- C) Cả hai

<details>
<summary>👉 Xem đáp án</summary>

**Đáp án: B) Giá trị liên tục**

Ví dụ: giá nhà, điểm số, doanh thu...

</details>

---

# PHẦN 2: HÀM GIẢ THUYẾT

## 2.1. Công thức

```
h(x) = θ₀ + θ₁x
```

- **θ₀**: Hệ số chặn (giá trị y khi x=0)
- **θ₁**: Hệ số góc (độ dốc)

## 2.2. Ví dụ tính toán

**Cho:** θ₀ = 2, θ₁ = 3

**Tính h(x) khi x = 4:**
```
h(4) = 2 + 3×4 = 2 + 12 = 14
```

---

## ✅ KIỂM TRA HIỂU BIẾT 2

**Bài tập:** Với h(x) = 5 + 2x, tính h(3).

<details>
<summary>👉 Xem đáp án</summary>

```
h(3) = 5 + 2×3 = 5 + 6 = 11
```

</details>

---

# PHẦN 3: HÀM CHI PHÍ

## 3.1. Ý tưởng

**Đo xem đường thẳng "sai" bao nhiêu** so với dữ liệu thực.

## 3.2. Công thức

```
J(θ) = (1/2m) × Σᵢ₌₁ᵐ [h(xⁱ) - yⁱ]²
```

## 3.3. Các bước tính J(θ)

1. Tính h(xⁱ) cho mỗi điểm
2. Tính sai số: h(xⁱ) - yⁱ
3. Bình phương sai số
4. Cộng tổng và chia 2m

---

## ✅ KIỂM TRA HIỂU BIẾT 3

**Bài tập:** Dữ liệu (1,2), (2,4). Với h(x) = 2x, tính J(θ).

<details>
<summary>👉 Xem đáp án</summary>

| x | y | h(x) | h(x)-y | [h(x)-y]² |
|---|---|------|--------|-----------|
| 1 | 2 | 2 | 0 | 0 |
| 2 | 4 | 4 | 0 | 0 |

```
J(θ) = (1/4) × (0 + 0) = 0
```

**Nhận xét:** J = 0 → đường thẳng khớp hoàn hảo!

</details>

---

# PHẦN 4: GRADIENT DESCENT

## 4.1. Ý tưởng

**"Đi xuống đồi"** để tìm điểm thấp nhất (J nhỏ nhất).

## 4.2. Công thức cập nhật

```
θ₀ := θ₀ - α × (1/m) × Σ[h(xⁱ) - yⁱ]
θ₁ := θ₁ - α × (1/m) × Σ[h(xⁱ) - yⁱ] × xⁱ
```

## 4.3. Quy trình từng bước

**Bước 1:** Tính h(xⁱ) cho mỗi điểm

**Bước 2:** Tính sai số [h(xⁱ) - yⁱ]

**Bước 3:** Tính đạo hàm:
- ∂J/∂θ₀ = (1/m) × Σ(sai số)
- ∂J/∂θ₁ = (1/m) × Σ(sai số × x)

**Bước 4:** Cập nhật θ:
- θ₀_mới = θ₀_cũ - α × ∂J/∂θ₀
- θ₁_mới = θ₁_cũ - α × ∂J/∂θ₁

---

## ✅ KIỂM TRA HIỂU BIẾT 4

**Bài tập:** Dữ liệu (1,1), (2,2), (3,3). Với θ₀=0, θ₁=0, α=0.1.
Tính ∂J/∂θ₀ sau vòng 1.

<details>
<summary>👉 Xem đáp án</summary>

**h(x) = 0 + 0×x = 0**

| x | y | h(x) | h(x)-y |
|---|---|------|--------|
| 1 | 1 | 0 | -1 |
| 2 | 2 | 0 | -2 |
| 3 | 3 | 0 | -3 |

```
∂J/∂θ₀ = (1/3) × [(-1) + (-2) + (-3)]
       = (1/3) × (-6)
       = -2
```

</details>

---

# PHẦN 5: VÍ DỤ HOÀN CHỈNH

## Đề bài

Dữ liệu: (1,1), (2,2), (3,3)
θ₀ = 0, θ₁ = 0, α = 0.1
Thực hiện 1 vòng Gradient Descent.

## Lời giải

**Bước 1-2:** Tính h(xⁱ) và sai số

| x | y | h(x)=0 | sai số |
|---|---|--------|--------|
| 1 | 1 | 0 | -1 |
| 2 | 2 | 0 | -2 |
| 3 | 3 | 0 | -3 |

**Bước 3:** Tính đạo hàm
```
∂J/∂θ₀ = (1/3)×(-6) = -2
∂J/∂θ₁ = (1/3)×[(-1)×1 + (-2)×2 + (-3)×3]
       = (1/3)×(-14) = -4.67
```

**Bước 4:** Cập nhật
```
θ₀ = 0 - 0.1×(-2) = 0.2
θ₁ = 0 - 0.1×(-4.67) = 0.467
```

**Kết quả:** θ₀ = 0.2, θ₁ = 0.467

---

# PHẦN 6: TỔNG KẾT

## Công thức quan trọng

| Tên | Công thức |
|-----|-----------|
| Giả thuyết | h(x) = θ₀ + θ₁x |
| Chi phí | J = (1/2m)×Σ[h(x)-y]² |
| Đạo hàm θ₀ | (1/m)×Σ[h(x)-y] |
| Đạo hàm θ₁ | (1/m)×Σ[h(x)-y]×x |
| Cập nhật | θ := θ - α×đạo hàm |

---

*Hết bài học Linear Regression - Phương án 3*
