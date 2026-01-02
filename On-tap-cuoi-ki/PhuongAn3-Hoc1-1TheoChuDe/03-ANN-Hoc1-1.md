# PHƯƠNG ÁN 3: HỌC 1-1 THEO CHỦ ĐỀ
# MẠNG NƠ-RON NHÂN TẠO - TỪ CƠ BẢN ĐẾN NÂNG CAO

---

## 🎯 MỤC TIÊU BÀI HỌC

Sau bài học này, bạn sẽ:
1. Hiểu cấu trúc mạng nơ-ron
2. Thành thạo hàm Sigmoid
3. Tính Forward Propagation
4. Thực hiện Backpropagation

---

# PHẦN 1: KHÁI NIỆM CƠ BẢN

## 1.1. Nơ-ron nhân tạo là gì?

**So sánh với não người:**
- Não: Tỷ nơ-ron kết nối với nhau
- Mạng: Nhiều node kết nối bằng trọng số

## 1.2. Cấu trúc 1 node

```
x₁ ──w₁──┐
          ↘
           [Σ+b] ──→ [σ] ──→ y
          ↗
x₂ ──w₂──┘
```

**Công thức:**
```
z = w₁x₁ + w₂x₂ + b
y = σ(z)
```

---

## ✅ KIỂM TRA HIỂU BIẾT 1

**Câu hỏi:** Trong mạng nơ-ron, "weight" (trọng số) đại diện cho điều gì?

<details>
<summary>👉 Xem đáp án</summary>

**Weight** đại diện cho **độ mạnh của kết nối** giữa hai node.
- w lớn → kết nối mạnh
- w nhỏ → kết nối yếu
- w âm → kết nối ức chế

</details>

---

# PHẦN 2: HÀM SIGMOID

## 2.1. Công thức

```
σ(z) = 1 / (1 + e⁻ᶻ)
```

## 2.2. Đặc điểm

- Output: luôn trong (0, 1)
- σ(0) = 0.5
- z → +∞ thì σ(z) → 1
- z → -∞ thì σ(z) → 0

## 2.3. Đạo hàm

```
σ'(z) = σ(z) × (1 - σ(z))
```

**Mẹo:** Nếu biết a = σ(z), thì σ'(z) = a × (1-a)

---

## ✅ KIỂM TRA HIỂU BIẾT 2

**Bài tập:** Tính σ(0) và σ'(0).

<details>
<summary>👉 Xem đáp án</summary>

```
σ(0) = 1/(1 + e⁰) = 1/(1+1) = 0.5

σ'(0) = σ(0) × (1-σ(0)) = 0.5 × 0.5 = 0.25
```

</details>

---

# PHẦN 3: FORWARD PROPAGATION

## 3.1. Quy trình

Tính output từ **trái sang phải** (input → output):

1. Tính z = Σwᵢxᵢ + b
2. Tính a = σ(z)
3. Lặp lại cho layer tiếp theo

## 3.2. Ví dụ

**Cho:** x = 1, w = 0.5, b = 0.2

```
z = 0.5×1 + 0.2 = 0.7
y = σ(0.7) = 1/(1 + e⁻⁰·⁷) ≈ 0.668
```

---

## ✅ KIỂM TRA HIỂU BIẾT 3

**Bài tập:** x₁=0.5, x₂=0.3, w₁=0.4, w₂=0.6, b=0.1. Tính output.

<details>
<summary>👉 Xem đáp án</summary>

```
z = 0.4×0.5 + 0.6×0.3 + 0.1
  = 0.2 + 0.18 + 0.1 = 0.48

y = σ(0.48) = 1/(1 + e⁻⁰·⁴⁸)
  = 1/(1 + 0.619) ≈ 0.618
```

</details>

---

# PHẦN 4: BACKPROPAGATION

## 4.1. Ý tưởng

Sau khi tính output, **lan truyền ngược** sai số để cập nhật trọng số.

## 4.2. Công thức

**Delta output:**
```
δ = (ŷ - y) × ŷ × (1 - ŷ)
```

**Cập nhật trọng số:**
```
w_mới = w_cũ - α × δ × input
b_mới = b_cũ - α × δ
```

## 4.3. Quy trình

1. Tính sai số: ŷ - y
2. Tính delta: δ = (ŷ-y) × ŷ × (1-ŷ)
3. Cập nhật w và b

---

## ✅ KIỂM TRA HIỂU BIẾT 4

**Bài tập:** ŷ = 0.7, y = 1. Tính δ.

<details>
<summary>👉 Xem đáp án</summary>

```
δ = (ŷ - y) × ŷ × (1 - ŷ)
  = (0.7 - 1) × 0.7 × (1 - 0.7)
  = (-0.3) × 0.7 × 0.3
  = -0.063
```

</details>

---

# PHẦN 5: VÍ DỤ HOÀN CHỈNH

## Đề bài

Mạng 1 node: x=1, w=0.5, b=0.2, y_thực=1, α=0.5

## Lời giải

**Forward:**
```
z = 0.5×1 + 0.2 = 0.7
ŷ = σ(0.7) ≈ 0.668
```

**Backward:**
```
δ = (0.668-1) × 0.668 × (1-0.668)
  = (-0.332) × 0.668 × 0.332 ≈ -0.074

w_mới = 0.5 - 0.5×(-0.074)×1 = 0.537
b_mới = 0.2 - 0.5×(-0.074) = 0.237
```

---

# PHẦN 6: BẢNG TRA CỨU

## Giá trị Sigmoid

| z | σ(z) | σ'(z) |
|---|------|-------|
| -2 | 0.12 | 0.11 |
| -1 | 0.27 | 0.20 |
| 0 | 0.50 | 0.25 |
| 1 | 0.73 | 0.20 |
| 2 | 0.88 | 0.11 |

## Giá trị e⁻ᶻ

| z | e⁻ᶻ |
|---|-----|
| 0 | 1.00 |
| 0.5 | 0.61 |
| 1 | 0.37 |
| 2 | 0.14 |

---

# PHẦN 7: TỔNG KẾT

## Công thức quan trọng

| Tên | Công thức |
|-----|-----------|
| Sigmoid | σ(z) = 1/(1+e⁻ᶻ) |
| Đạo hàm | σ'(z) = a(1-a) |
| Forward | z = Σwx+b, a = σ(z) |
| Delta | δ = (ŷ-y)×ŷ×(1-ŷ) |
| Cập nhật w | w := w - α×δ×x |
| Cập nhật b | b := b - α×δ |

---

*Hết bài học ANN - Phương án 3*
