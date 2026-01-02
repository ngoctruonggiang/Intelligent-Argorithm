# 📚 HƯỚNG DẪN GIẢI BÀI TẬP: CÂY QUYẾT ĐỊNH (ID3)
## Phương án 2: Bài tập từng bước chi tiết

---

> **Lời dặn của Giảng viên:**
> 
> Bài tập Decision Tree yêu cầu tính toán **Entropy** và **Information Gain**. Đây là phần nhiều bạn hay sai vì công thức log₂ khá phức tạp.
> 
> Mình sẽ giải từng bài **rất chi tiết**, kèm theo bảng tra cứu để các bạn làm bài thi nhanh hơn!

---

## 📋 DẠNG BÀI TẬP DECISION TREE THƯỜNG GẶP

| Dạng | Mô tả | Độ khó |
|:----:|-------|:------:|
| **Dạng 1** | Tính Entropy của một tập dữ liệu | ⭐ Dễ |
| **Dạng 2** | Tính Information Gain cho một thuộc tính | ⭐⭐ Trung bình |
| **Dạng 3** | Xây dựng toàn bộ cây quyết định | ⭐⭐⭐ Khó |

---

# 🔷 DẠNG 1: TÍNH ENTROPY

## Bài tập 1.1 (Trường hợp đơn giản nhất)

**Đề bài:** Cho tập dữ liệu S có 10 mẫu, trong đó:
- 10 mẫu thuộc lớp "Có"
- 0 mẫu thuộc lớp "Không"

Tính Entropy(S).

### Lời giải chi tiết

**Bước 1: Xác định tỷ lệ**
- p(Có) = 10/10 = 1
- p(Không) = 0/10 = 0

**Bước 2: Áp dụng công thức**

⚠️ **Quy ước:** 0 × log₂(0) = 0 (vì lim x→0 của x·log(x) = 0)

```
Entropy(S) = -p(Có)×log₂(p(Có)) - p(Không)×log₂(p(Không))
           = -1 × log₂(1) - 0 × log₂(0)
           = -1 × 0 - 0
           = 0
```

**✅ Đáp án:** Entropy(S) = **0**

**💡 Giải thích:** Entropy = 0 vì dữ liệu hoàn toàn thuần nhất (tất cả đều "Có").

---

## Bài tập 1.2 (Trường hợp 50-50)

**Đề bài:** Cho tập S có 8 mẫu: 4 "Có" và 4 "Không". Tính Entropy(S).

### Lời giải chi tiết

**Bước 1: Xác định tỷ lệ**
- p(Có) = 4/8 = 0.5
- p(Không) = 4/8 = 0.5

**Bước 2: Tra bảng hoặc tính**
- log₂(0.5) = -1

**Bước 3: Áp dụng công thức**
```
Entropy(S) = -0.5 × log₂(0.5) - 0.5 × log₂(0.5)
           = -0.5 × (-1) - 0.5 × (-1)
           = 0.5 + 0.5
           = 1
```

**✅ Đáp án:** Entropy(S) = **1**

**💡 Giải thích:** Entropy = 1 (max) vì dữ liệu hoàn toàn hỗn loạn (50-50).

---

## Bài tập 1.3 (Đề thi thực tế)

**Đề bài:** Tập S có 14 mẫu: 9 "Yes" và 5 "No". Tính Entropy(S).

### Lời giải chi tiết

**Bước 1: Tính tỷ lệ**
- p(Yes) = 9/14 ≈ 0.643
- p(No) = 5/14 ≈ 0.357

**Bước 2: Tính các thành phần**

Sử dụng bảng tra (hoặc máy tính):
- 9/14 × log₂(9/14) = 0.643 × (-0.637) = -0.410
- 5/14 × log₂(5/14) = 0.357 × (-1.486) = -0.531

**Bước 3: Tính Entropy**
```
Entropy(S) = -(-0.410) - (-0.531)
           = 0.410 + 0.531
           = 0.941
```

**✅ Đáp án:** Entropy(S) ≈ **0.94**

---

# 🔷 DẠNG 2: TÍNH INFORMATION GAIN

## Bài tập 2.1 (Cơ bản)

**Đề bài:** Cho tập S có 14 mẫu (9 Yes, 5 No). Thuộc tính "Gió" chia S thành:
- **Yếu (8 mẫu):** 6 Yes, 2 No
- **Mạnh (6 mẫu):** 3 Yes, 3 No

Tính Gain(S, Gió).

### Lời giải chi tiết

**📍 Bước 1: Tính Entropy(S) gốc**

(Đã tính ở bài 1.3)
```
Entropy(S) = 0.94
```

**📍 Bước 2: Tính Entropy từng nhánh con**

**Nhánh Yếu (6 Yes, 2 No trong 8):**
- p(Yes) = 6/8 = 0.75
- p(No) = 2/8 = 0.25
```
Entropy(Yếu) = -0.75×log₂(0.75) - 0.25×log₂(0.25)
             = -0.75×(-0.415) - 0.25×(-2)
             = 0.311 + 0.5
             = 0.811
```

**Nhánh Mạnh (3 Yes, 3 No trong 6):**
- p(Yes) = 3/6 = 0.5
- p(No) = 3/6 = 0.5
```
Entropy(Mạnh) = -0.5×log₂(0.5) - 0.5×log₂(0.5)
              = 0.5 + 0.5
              = 1
```

**📍 Bước 3: Tính Entropy trung bình có trọng số**

```
Entropy_tb = (|S_Yếu|/|S|) × E(Yếu) + (|S_Mạnh|/|S|) × E(Mạnh)
           = (8/14) × 0.811 + (6/14) × 1
           = 0.571 × 0.811 + 0.429 × 1
           = 0.463 + 0.429
           = 0.892
```

**📍 Bước 4: Tính Gain**

```
Gain(S, Gió) = Entropy(S) - Entropy_tb
             = 0.94 - 0.892
             = 0.048
```

**✅ Đáp án:** Gain(S, Gió) = **0.048**

---

## Bài tập 2.2 (So sánh nhiều thuộc tính)

**Đề bài:** Với cùng tập S (14 mẫu: 9 Yes, 5 No), thuộc tính "Trời" chia thành:
- **Nắng (5 mẫu):** 2 Yes, 3 No
- **Mây (4 mẫu):** 4 Yes, 0 No
- **Mưa (5 mẫu):** 3 Yes, 2 No

Tính Gain(S, Trời) và so sánh với Gain(S, Gió).

### Lời giải chi tiết

**📍 Bước 1: Entropy(S) = 0.94** (đã biết)

**📍 Bước 2: Tính Entropy từng nhánh**

**Nắng (2 Yes, 3 No):**
```
E(Nắng) = -(2/5)log₂(2/5) - (3/5)log₂(3/5)
        = -0.4×(-1.322) - 0.6×(-0.737)
        = 0.529 + 0.442
        = 0.971
```

**Mây (4 Yes, 0 No):**
```
E(Mây) = 0  (tất cả đều Yes → thuần nhất)
```

**Mưa (3 Yes, 2 No):**
```
E(Mưa) = -(3/5)log₂(3/5) - (2/5)log₂(2/5)
       = 0.971
```

**📍 Bước 3: Entropy trung bình**

```
Entropy_tb = (5/14)×0.971 + (4/14)×0 + (5/14)×0.971
           = 0.347 + 0 + 0.347
           = 0.694
```

**📍 Bước 4: Tính Gain**

```
Gain(S, Trời) = 0.94 - 0.694 = 0.246
```

**📍 Bước 5: So sánh**

| Thuộc tính | Gain |
|:----------:|:----:|
| Trời | **0.246** ✅ |
| Gió | 0.048 |

**✅ Kết luận:** Chọn **"Trời"** làm nút gốc vì Gain cao hơn!

---

# 🔷 DẠNG 3: XÂY DỰNG CÂY HOÀN CHỈNH

## Bài tập 3.1

**Đề bài:** Cho bảng dữ liệu đơn giản:

| ID | Màu | Kích thước | Mua? |
|:--:|:---:|:----------:|:----:|
| 1 | Đỏ | Nhỏ | Có |
| 2 | Đỏ | Lớn | Có |
| 3 | Xanh | Nhỏ | Không |
| 4 | Xanh | Lớn | Không |

Xây dựng cây quyết định.

### Lời giải chi tiết

**📍 Bước 1: Tính Entropy(S)**
- 2 Có, 2 Không → p = 0.5
- Entropy(S) = 1

**📍 Bước 2: Tính Gain cho "Màu"**

| Màu | Có | Không | Entropy |
|:---:|:--:|:-----:|:-------:|
| Đỏ | 2 | 0 | 0 |
| Xanh | 0 | 2 | 0 |

```
Entropy_tb = (2/4)×0 + (2/4)×0 = 0
Gain(Màu) = 1 - 0 = 1  ← PERFECT!
```

**📍 Bước 3: Tính Gain cho "Kích thước"**

| Kích thước | Có | Không | Entropy |
|:----------:|:--:|:-----:|:-------:|
| Nhỏ | 1 | 1 | 1 |
| Lớn | 1 | 1 | 1 |

```
Entropy_tb = (2/4)×1 + (2/4)×1 = 1
Gain(Kích thước) = 1 - 1 = 0  ← USELESS!
```

**📍 Bước 4: Chọn và vẽ cây**

Chọn "Màu" vì Gain = 1 (hoàn hảo).

```
        [MÀU?]
       /      \
    (Đỏ)    (Xanh)
     |         |
   [CÓ]    [KHÔNG]
```

**✅ Đáp án:** Cây chỉ cần 1 nút "Màu" là đủ phân loại!

---

# 📝 BẢNG TRA CỨU LOG₂ VÀ ENTROPY

## Bảng 1: Giá trị log₂ thường gặp

| Phân số | Thập phân | log₂ |
|:-------:|:---------:|:----:|
| 1/8 | 0.125 | -3.00 |
| 1/4 | 0.25 | -2.00 |
| 1/3 | 0.333 | -1.58 |
| 2/5 | 0.4 | -1.32 |
| 1/2 | 0.5 | -1.00 |
| 3/5 | 0.6 | -0.74 |
| 2/3 | 0.667 | -0.58 |
| 3/4 | 0.75 | -0.42 |
| 4/5 | 0.8 | -0.32 |
| 1/1 | 1.0 | 0.00 |

## Bảng 2: Giá trị Entropy thường gặp

| Tỷ lệ (p+/p-) | Entropy |
|:-------------:|:-------:|
| 10/0 hoặc 0/10 | 0.00 |
| 9/1 | 0.47 |
| 8/2 | 0.72 |
| 7/3 | 0.88 |
| 6/4 | 0.97 |
| 5/5 | 1.00 |

---

# 📌 BÀI TẬP TỰ LUYỆN

**Bài 1:** Tính Entropy của tập có 7 Yes, 3 No.

**Bài 2:** Cho S=[10+, 10-]. Thuộc tính A chia thành:
- A=1: [8+, 2-]
- A=0: [2+, 8-]

Tính Gain(S, A).

**Bài 3:** Thuộc tính B chia S thành:
- B=1: [5+, 5-]
- B=0: [5+, 5-]

Tính Gain(S, B). So sánh với Gain(S, A).

---

*Hết tài liệu bài tập Decision Tree - Phương án 2*
