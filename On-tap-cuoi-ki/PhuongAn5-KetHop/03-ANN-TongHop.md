# PHƯƠNG ÁN 5: KẾT HỢP NHIỀU PHƯƠNG PHÁP
# MẠNG NƠ-RON NHÂN TẠO - TÀI LIỆU TỔNG HỢP

---

# PHẦN A: LÝ THUYẾT ĐƠN GIẢN

## 1. Mạng nơ-ron là gì?

**Định nghĩa:** Mô hình tính toán mô phỏng não người, gồm nhiều node kết nối bằng trọng số.

**Cấu trúc:** Input → Hidden → Output

## 2. Công thức quan trọng

| Tên | Công thức |
|-----|-----------|
| Sigmoid | σ(z) = 1/(1+e⁻ᶻ) |
| Đạo hàm sigmoid | σ'(z) = a×(1-a) |
| Forward | z = Σwx+b, a = σ(z) |
| Delta | δ = (ŷ-y)×ŷ×(1-ŷ) |
| Cập nhật w | w := w - α×δ×input |
| Cập nhật b | b := b - α×δ |

## 3. Quy trình

```
FORWARD:  Input → z = Σwx+b → a = σ(z) → Output
BACKWARD: Output ← δ ← Cập nhật w, b ← Input
```

---

# PHẦN B: BÀI TẬP MẪU CHI TIẾT

## Đề bài

Mạng 1 node: x=1, w=0.5, b=0.2, y_thực=1, α=0.5

## Lời giải

### Forward Propagation

```
z = w×x + b = 0.5×1 + 0.2 = 0.7
ŷ = σ(0.7) = 1/(1+e⁻⁰·⁷) ≈ 0.668
```

### Backpropagation

```
δ = (ŷ-y) × ŷ × (1-ŷ)
  = (0.668-1) × 0.668 × (1-0.668)
  = -0.332 × 0.668 × 0.332
  = -0.074
```

### Cập nhật

```
w_mới = 0.5 - 0.5×(-0.074)×1 = 0.537
b_mới = 0.2 - 0.5×(-0.074) = 0.237
```

---

# PHẦN C: CÂU HỎI TỰ KIỂM TRA

**Q1:** σ(0) = ?
<details><summary>Đáp án</summary>σ(0) = 1/(1+1) = 0.5</details>

**Q2:** Nếu a = σ(z) = 0.7, thì σ'(z) = ?
<details><summary>Đáp án</summary>σ'(z) = 0.7×(1-0.7) = 0.7×0.3 = 0.21</details>

**Q3:** Khi ŷ < y, δ âm hay dương?
<details><summary>Đáp án</summary>δ âm (vì ŷ-y < 0), do đó w sẽ tăng</details>

---

# PHẦN D: SƠ ĐỒ MINH HỌA

## Cấu trúc 1 node

```
x₁ ──w₁──┐
          ↘
           [Σ+b] ──► [σ] ──► y
          ↗
x₂ ──w₂──┘
```

## Flowchart

```
┌─────────────┐
│ Forward     │
│ z = Σwx+b   │
│ a = σ(z)    │
└──────┬──────┘
       ↓
┌─────────────┐
│ Tính Loss   │
│ L = (ŷ-y)²  │
└──────┬──────┘
       ↓
┌─────────────┐
│ Backward    │
│ δ = (ŷ-y)×..│
│ w := w-α×δ×x│
└─────────────┘
```

---

# PHẦN E: BẢNG TRA CỨU NHANH

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

# PHẦN F: CHECKLIST LÀM BÀI

## Forward

- [ ] z = Σwᵢxᵢ + b
- [ ] a = σ(z) = 1/(1+e⁻ᶻ)
- [ ] Lặp lại cho mỗi layer

## Backward

- [ ] δ_output = (ŷ-y) × ŷ × (1-ŷ)
- [ ] δ_hidden = (w×δ_next) × a × (1-a)
- [ ] w := w - α × δ × input
- [ ] b := b - α × δ

---

*Hết ANN - Phương án 5: Kết hợp*
