# 📚 TỔNG HỢP KIẾN THỨC: CÂY QUYẾT ĐỊNH (ID3)
## Phương án 5: Kết hợp tất cả - Tài liệu in ấn

---

# 📌 PHẦN 1: TÓM TẮT LÝ THUYẾT

## 1.1. Định nghĩa
**Cây quyết định** là cấu trúc cây dùng để phân loại bằng cách đặt các câu hỏi liên tiếp. Thuật toán **ID3** xây dựng cây bằng cách chọn thuộc tính có **Gain cao nhất** làm nút.

## 1.2. Thành phần
| Thành phần | Ý nghĩa |
|------------|---------|
| **Root Node** | Câu hỏi đầu tiên (Gain cao nhất) |
| **Internal Node** | Câu hỏi tiếp theo |
| **Leaf Node** | Kết luận cuối cùng |
| **Branch** | Câu trả lời/điều kiện |

---

# 📌 PHẦN 2: CÔNG THỨC QUAN TRỌNG

## 2.1. Entropy (Độ hỗn loạn)

$$Entropy(S) = -\sum_{i} p_i \times \log_2(p_i)$$

**Trường hợp 2 lớp (Yes/No):**
$$E(S) = -p_{+}\log_2(p_{+}) - p_{-}\log_2(p_{-})$$

## 2.2. Information Gain

$$Gain(S, A) = E(S) - \sum_{v} \frac{|S_v|}{|S|} \times E(S_v)$$

---

# 📌 PHẦN 3: BẢNG TRA LOG₂ (QUAN TRỌNG!)

## 3.1. Giá trị log₂

| p | log₂(p) | | p | log₂(p) |
|:-:|:-------:|:-:|:-:|:-------:|
| 1/2 | -1.00 | | 3/4 | -0.42 |
| 1/3 | -1.58 | | 4/5 | -0.32 |
| 2/3 | -0.58 | | 1/5 | -2.32 |
| 1/4 | -2.00 | | 2/5 | -1.32 |

## 3.2. Giá trị Entropy thường gặp

| Tỷ lệ (+/-) | Entropy |
|:-----------:|:-------:|
| 10/0 hoặc 0/10 | **0.00** |
| 9/1 | 0.47 |
| 8/2 | 0.72 |
| 7/3 | 0.88 |
| 6/4 | 0.97 |
| 5/5 | **1.00** |

---

# 📌 PHẦN 4: QUY TRÌNH LÀM BÀI

## ✅ Checklist từng bước

- [ ] **Bước 1:** Đếm số Yes/No của tập gốc
- [ ] **Bước 2:** Tính **Entropy(S)** gốc
- [ ] **Bước 3:** Với MỖI thuộc tính:
  - [ ] Chia theo từng giá trị
  - [ ] Tính Entropy nhánh con
  - [ ] Tính **Gain**
- [ ] **Bước 4:** Chọn thuộc tính có **Gain MAX**
- [ ] **Bước 5:** Vẽ cây, lặp lại với nhánh chưa thuần nhất

---

# 📌 PHẦN 5: VÍ DỤ MẪU (ĐỀ THI)

**Đề:** S = [9 Yes, 5 No]. Thuộc tính "Gió" chia thành:
- Yếu: [6 Yes, 2 No]
- Mạnh: [3 Yes, 3 No]

Tính Gain(S, Gió).

**Giải:**

**B1: Entropy(S)**
```
E(S) = -(9/14)log(9/14) - (5/14)log(5/14) ≈ 0.94
```

**B2: Entropy nhánh**
```
E(Yếu) = -(6/8)log(6/8) - (2/8)log(2/8) ≈ 0.81
E(Mạnh) = -(3/6)log(3/6) - (3/6)log(3/6) = 1
```

**B3: Entropy trung bình**
```
E_tb = (8/14)×0.81 + (6/14)×1 ≈ 0.89
```

**B4: Gain**
```
Gain = 0.94 - 0.89 = 0.05 ✅
```

---

# 📌 PHẦN 6: LƯU Ý QUAN TRỌNG

> ⚠️ **Entropy = 0** → DỪNG (tạo lá)
> 
> ⚠️ **Entropy = 1** → Hỗn loạn nhất (50-50)
> 
> ⚠️ **Gain CAO** → Chọn làm nút
> 
> ⚠️ **0 × log(0) = 0** (quy ước)

---

# 📌 PHẦN 7: CÔNG THỨC TÍNH NHANH

**Entropy tỷ lệ đơn giản:**
- 1:0 hoặc 0:1 → E = 0
- 1:1 → E = 1
- 3:1 hoặc 1:3 → E ≈ 0.81
- 2:1 hoặc 1:2 → E ≈ 0.92

---

*Hết tổng hợp Decision Tree - In mang vào phòng thi*
