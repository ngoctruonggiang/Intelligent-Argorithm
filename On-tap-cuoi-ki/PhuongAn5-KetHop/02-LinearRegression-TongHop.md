# PHƯƠNG ÁN 5: KẾT HỢP NHIỀU PHƯƠNG PHÁP
# HỒI QUY TUYẾN TÍNH - TÀI LIỆU TỔNG HỢP

---

# PHẦN A: LÝ THUYẾT ĐƠN GIẢN

## 1. Hồi quy tuyến tính là gì?

**Định nghĩa:** Tìm đường thẳng "khớp" nhất với dữ liệu để dự đoán.

**Ví dụ:** Dự đoán doanh thu dựa trên chi phí quảng cáo.

## 2. Công thức quan trọng

| Tên | Công thức |
|-----|-----------|
| Giả thuyết | h(x) = θ₀ + θ₁x |
| Chi phí | J = (1/2m)×Σ[h(x)-y]² |
| Cập nhật θ₀ | θ₀ := θ₀ - α×(1/m)×Σ[h(x)-y] |
| Cập nhật θ₁ | θ₁ := θ₁ - α×(1/m)×Σ[h(x)-y]×x |

## 3. Gradient Descent

```
1. Khởi tạo θ₀ = 0, θ₁ = 0
2. Tính h(xⁱ) cho mỗi điểm
3. Tính sai số [h(xⁱ) - yⁱ]
4. Tính đạo hàm
5. Cập nhật θ
6. Lặp lại đến khi hội tụ
```

---

# PHẦN B: BÀI TẬP MẪU CHI TIẾT

## Đề bài

Dữ liệu: (1,1), (2,2), (3,3)
θ₀ = 0, θ₁ = 0, α = 0.1
Thực hiện 1 vòng Gradient Descent.

## Lời giải

### Bước 1: Tính h(xⁱ)

h(x) = 0 + 0×x = 0

| i | x | y | h(x) |
|---|---|---|------|
| 1 | 1 | 1 | 0 |
| 2 | 2 | 2 | 0 |
| 3 | 3 | 3 | 0 |

### Bước 2: Tính sai số

| i | h(x)-y | [h(x)-y]×x |
|---|--------|------------|
| 1 | -1 | -1 |
| 2 | -2 | -4 |
| 3 | -3 | -9 |
| Σ | -6 | -14 |

### Bước 3: Tính đạo hàm

```
∂J/∂θ₀ = (1/3)×(-6) = -2
∂J/∂θ₁ = (1/3)×(-14) = -4.67
```

### Bước 4: Cập nhật

```
θ₀ = 0 - 0.1×(-2) = 0.2
θ₁ = 0 - 0.1×(-4.67) = 0.467
```

**Kết quả:** h(x) = 0.2 + 0.467x

---

# PHẦN C: CÂU HỎI TỰ KIỂM TRA

**Q1:** h(x) = 2 + 3x. Tính h(4)?
<details><summary>Đáp án</summary>h(4) = 2 + 3×4 = 14</details>

**Q2:** Hàm chi phí J đo điều gì?
<details><summary>Đáp án</summary>Tổng bình phương sai số giữa dự đoán và thực tế</details>

**Q3:** Tại sao cần Gradient Descent?
<details><summary>Đáp án</summary>Để tìm θ₀, θ₁ sao cho J(θ) nhỏ nhất</details>

---

# PHẦN D: SƠ ĐỒ MINH HỌA

```
TRƯỚC (θ₀=0, θ₁=0):           SAU:

      y                             y
    4 |     ●                     4 |     ●/
    3 |   ●                       3 |   ●/
    2 | ●   ────── h(x)=0         2 | ●/  h(x)≈x
    1 |                           1 |/
    0 +─────────→ x               0 +─────────→ x

    J(θ) cao                      J(θ) thấp
```

---

# PHẦN E: BẢNG TÍNH MẪU

```
┌───┬────┬────┬──────┬─────────┬────────────┐
│ i │ xⁱ │ yⁱ │ h(xⁱ)│ h(xⁱ)-yⁱ│[h(xⁱ)-yⁱ]×xⁱ│
├───┼────┼────┼──────┼─────────┼────────────┤
│ 1 │    │    │      │         │            │
│ 2 │    │    │      │         │            │
│ 3 │    │    │      │         │            │
├───┼────┼────┼──────┼─────────┼────────────┤
│ Σ │  - │  - │   -  │    ?    │     ?      │
└───┴────┴────┴──────┴─────────┴────────────┘

∂J/∂θ₀ = (1/m) × Σ[h(xⁱ)-yⁱ]
∂J/∂θ₁ = (1/m) × Σ[h(xⁱ)-yⁱ]×xⁱ
```

---

# PHẦN F: CHECKLIST LÀM BÀI

- [ ] Xác định m, θ₀, θ₁, α
- [ ] Tính h(xⁱ) = θ₀ + θ₁xⁱ
- [ ] Tính sai số h(xⁱ) - yⁱ
- [ ] Lập tổng Σ[sai số] và Σ[sai số × x]
- [ ] Tính đạo hàm chia cho m
- [ ] Cập nhật: θ := θ - α × đạo hàm

---

*Hết Linear Regression - Phương án 5: Kết hợp*
