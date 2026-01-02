# PHƯƠNG ÁN 5: KẾT HỢP NHIỀU PHƯƠNG PHÁP
# K-MEANS CLUSTERING - TÀI LIỆU TỔNG HỢP

---

# PHẦN A: LÝ THUYẾT ĐƠN GIẢN

## 1. K-means là gì?

**Định nghĩa:** Thuật toán phân cụm chia m điểm thành K nhóm dựa trên khoảng cách.

**Ví dụ đời thường:** Chia 100 khách hàng thành 3 nhóm (VIP, Thường, Mới) dựa trên hành vi mua sắm.

## 2. Các bước thuật toán

```
BƯỚC 1: Chọn K tâm ban đầu
    ↓
BƯỚC 2: Gán mỗi điểm vào cụm gần nhất
    ↓
BƯỚC 3: Tính lại tâm cụm (trung bình)
    ↓
BƯỚC 4: Nếu thay đổi → Về bước 2
        Nếu không → DỪNG
```

## 3. Công thức quan trọng

| Công thức | Ý nghĩa |
|-----------|---------|
| d = √[(x₂-x₁)² + (y₂-y₁)²] | Khoảng cách 2D |
| C = (Σxᵢ/n, Σyᵢ/n) | Tâm cụm |

---

# PHẦN B: BÀI TẬP MẪU CHI TIẾT

## Đề bài

Cho 4 điểm: A(1,1), B(2,1), C(4,3), D(5,4)
K = 2, Tâm ban đầu: C₁ = A, C₂ = C

## Lời giải

### Vòng 1 - Bước 2: Gán cụm

**Điểm A(1,1):**
```
d(A,C₁) = √[(1-1)² + (1-1)²] = 0
d(A,C₂) = √[(4-1)² + (3-1)²] = √13 ≈ 3.61
→ A vào Cụm 1
```

**Điểm B(2,1):**
```
d(B,C₁) = √[(2-1)² + (1-1)²] = 1
d(B,C₂) = √[(4-2)² + (3-1)²] = √8 ≈ 2.83
→ B vào Cụm 1
```

**Điểm C(4,3):**
```
d(C,C₁) = √13 ≈ 3.61
d(C,C₂) = 0
→ C vào Cụm 2
```

**Điểm D(5,4):**
```
d(D,C₁) = √[(5-1)² + (4-1)²] = √25 = 5
d(D,C₂) = √[(5-4)² + (4-3)²] = √2 ≈ 1.41
→ D vào Cụm 2
```

**Bảng tổng hợp:**

| Điểm | d(C₁) | d(C₂) | Gán |
|------|-------|-------|-----|
| A | 0 | 3.61 | Cụm 1 |
| B | 1 | 2.83 | Cụm 1 |
| C | 3.61 | 0 | Cụm 2 |
| D | 5 | 1.41 | Cụm 2 |

### Vòng 1 - Bước 3: Tính tâm mới

```
C₁_mới = ((1+2)/2, (1+1)/2) = (1.5, 1)
C₂_mới = ((4+5)/2, (3+4)/2) = (4.5, 3.5)
```

### Vòng 2: Kiểm tra hội tụ

*(Tính lại với tâm mới - phân cụm không đổi)*

**Kết quả:** HỘI TỤ sau 2 vòng!

---

# PHẦN C: CÂU HỎI TỰ KIỂM TRA

**Q1:** K-means thuộc loại học máy nào?
<details><summary>Đáp án</summary>Học không giám sát (Unsupervised Learning)</details>

**Q2:** Công thức tính tâm cụm?
<details><summary>Đáp án</summary>C = (Σxᵢ/n, Σyᵢ/n) - trung bình tọa độ</details>

**Q3:** Khi nào thuật toán hội tụ?
<details><summary>Đáp án</summary>Khi phân cụm không thay đổi giữa 2 vòng liên tiếp</details>

---

# PHẦN D: SƠ ĐỒ MINH HỌA

```
TRƯỚC:                    SAU (K=2):
    ●  ●                      ○  ○   Cụm 1
  ● ●    ●                  ○ ○    
    ●  ●                        △  △  Cụm 2
      ●  ●                    △  △

Không cấu trúc            Có 2 nhóm rõ ràng
```

---

# PHẦN E: BẢNG TRA CỨU NHANH

## Căn bậc 2 thường gặp

| √ | Giá trị |
|---|---------|
| √2 | 1.41 |
| √5 | 2.24 |
| √8 | 2.83 |
| √10 | 3.16 |
| √13 | 3.61 |
| √18 | 4.24 |
| √25 | 5 |

## Checklist làm bài

- [ ] Xác định K và tâm ban đầu
- [ ] Tính khoảng cách từng điểm
- [ ] Lập bảng và gán cụm
- [ ] Tính tâm mới
- [ ] Kiểm tra hội tụ

---

*Hết K-means - Phương án 5: Kết hợp*
