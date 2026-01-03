# 📚 TÀI LIỆU ÔN TẬP: CÂY QUYẾT ĐỊNH (DECISION TREE)

## Thuật toán ID3 - Giải thích đơn giản, dễ hiểu, dễ thực hành

---

> **Mục tiêu tài liệu:**
> - ✅ Đơn giản, dễ hiểu
> - ✅ Dễ thực hành, làm bài được ngay
> - ✅ Chi tiết từng bước
> - ✅ Đúng đắn theo slide bài giảng

---

# 📑 MỤC LỤC

1. [Cây Quyết Định là gì?](#1-cây-quyết-định-là-gì)
2. [Thuật toán ID3](#2-thuật-toán-id3)
3. [Entropy - Độ hỗn loạn](#3-entropy-độ-hỗn-loạn)
4. [Information Gain](#4-information-gain)
5. [Ví dụ tính toán chi tiết](#5-ví-dụ-tính-toán-chi-tiết)
6. [Bảng tra cứu LOG₂](#6-bảng-tra-cứu-log₂)
7. [Quy trình làm bài thi](#7-quy-trình-làm-bài-thi)
8. [Các trường hợp đặc biệt](#8-các-trường-hợp-đặc-biệt)
9. [Bài tập tự luyện](#9-bài-tập-tự-luyện)

---

# 1️⃣ CÂY QUYẾT ĐỊNH LÀ GÌ?

## 1.1. Ý tưởng đơn giản nhất

**Cây quyết định = Một loạt câu hỏi Yes/No để đưa ra kết luận**

Ví dụ hàng ngày: Bạn quyết định có đi chơi tennis không?

```
❓ Trời có mưa không?
    │
    ├── CÓ ─────→ ❌ KHÔNG ĐI
    │
    └── KHÔNG ──→ ❓ Độ ẩm cao không?
                       │
                       ├── CÓ ────→ ❌ KHÔNG ĐI
                       │
                       └── KHÔNG ─→ ✅ ĐI CHƠI!
```

## 1.2. Các thành phần của cây

| Thành phần | Tiếng Anh | Ý nghĩa | Ví dụ |
|------------|-----------|---------|-------|
| **Nút gốc** | Root Node | Câu hỏi đầu tiên | "Trời có mưa?" |
| **Nút trong** | Internal Node | Các câu hỏi tiếp theo | "Độ ẩm cao?" |
| **Nút lá** | Leaf Node | Kết luận cuối cùng | "Đi chơi" / "Ở nhà" |
| **Nhánh** | Branch | Câu trả lời | "Có", "Không" |

## 1.3. Tại sao Decision Tree quan trọng?

**Ưu điểm:**
- ✅ Dễ hiểu, dễ giải thích (nhìn cây là hiểu ngay)
- ✅ Không cần chuẩn hóa dữ liệu
- ✅ Xử lý được cả dữ liệu số và phân loại

**Nhược điểm:**
- ❌ Dễ overfitting nếu cây quá sâu
- ❌ Nhạy cảm với dữ liệu thay đổi

---

# 2️⃣ THUẬT TOÁN ID3

## 2.1. ID3 là gì?

**ID3 (Iterative Dichotomiser 3)** là thuật toán xây dựng cây quyết định do Ross Quinlan phát triển năm 1986.

### 🤔 Câu hỏi then chốt:

> Khi có nhiều thuộc tính (ví dụ: Thời tiết, Độ ẩm, Gió...), nên hỏi câu nào **TRƯỚC**?

### 💡 Trả lời:

> Hỏi câu nào giúp **phân loại TỐT NHẤT** → Chọn thuộc tính có **Information Gain CAO NHẤT**!

### Ví dụ trực quan:

```
Giả sử bạn muốn phân loại 14 ngày: "Có nên chơi tennis?"

Nếu hỏi "Thời tiết thế nào?":
- Nắng: 5 ngày (2 Có, 3 Không) → Chưa rõ ràng
- Mây:  4 ngày (4 Có, 0 Không) → Rõ ràng! Luôn chơi!
- Mưa:  5 ngày (3 Có, 2 Không) → Chưa rõ ràng

→ Câu hỏi này giúp phân loại khá tốt (Gain = 0.247)

Nếu hỏi "Gió thế nào?":
- Yếu:  8 ngày (6 Có, 2 Không) → Vẫn lộn xộn
- Mạnh: 6 ngày (3 Có, 3 Không) → 50-50, rất lộn xộn!

→ Câu hỏi này không giúp nhiều (Gain = 0.048)

⭐ KẾT LUẬN: Hỏi "Thời tiết" trước vì Gain cao hơn!
```

## 2.2. Các bước thuật toán ID3

```
┌─────────────────────────────────────────────────────────┐
│              THUẬT TOÁN ID3 - 4 BƯỚC                    │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  Bước 1: Tính Entropy của tập dữ liệu gốc              │
│          → Đo độ "lộn xộn" ban đầu                     │
│                      ↓                                  │
│  Bước 2: Tính Information Gain cho MỖI thuộc tính      │
│          → Xem thuộc tính nào giảm lộn xộn nhiều nhất  │
│                      ↓                                  │
│  Bước 3: Chọn thuộc tính có Gain CAO NHẤT              │
│          → Đây là thuộc tính phân loại tốt nhất        │
│                      ↓                                  │
│  Bước 4: Chia dữ liệu, lặp lại với các nhánh con       │
│          → Đệ quy cho đến khi tất cả nhánh thuần nhất  │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

## 2.3. Điều kiện DỪNG

Thuật toán **DỪNG** khi gặp một trong các trường hợp sau:

| Điều kiện | Giải thích | Hành động |
|-----------|------------|-----------|
| **Entropy = 0** | Tất cả mẫu cùng lớp | Tạo nút lá với nhãn đó |
| **Hết thuộc tính** | Không còn gì để chia | Tạo lá với nhãn đa số |
| **Tập con rỗng** | Không có mẫu nào | Tạo lá với nhãn đa số của cha |

---

# 3️⃣ ENTROPY (Độ hỗn loạn)

## 3.1. Khái niệm đơn giản

**Entropy đo mức độ "lộn xộn" của dữ liệu.**

### 🤔 Hiểu Entropy qua ví dụ đời thường:

Tưởng tượng bạn có một hộp bi:

**Trường hợp 1: Hộp chỉ có bi XANH**
```
Hộp: 🔵🔵🔵🔵🔵 (5 bi xanh, 0 bi đỏ)

Hỏi: "Lấy ngẫu nhiên 1 bi, nó màu gì?"
Trả lời: "XANH!" - Chắc chắn 100%!

→ Entropy = 0 (Không có gì bất định)
```

**Trường hợp 2: Hộp có 50% xanh, 50% đỏ**
```
Hộp: 🔵🔵🔴🔴 (2 xanh, 2 đỏ)

Hỏi: "Lấy ngẫu nhiên 1 bi, nó màu gì?"
Trả lời: "Không biết!" - Khó đoán nhất!

→ Entropy = 1.0 (Bất định tối đa)
```

### 📊 Bảng tổng hợp:

| Tình huống | Entropy | Ý nghĩa |
|------------|---------|---------|
| 🔵🔵🔵🔵🔵 (100% xanh) | **0** | Hoàn toàn thuần nhất ✅ |
| 🔵🔵🔵🔵🔴 (80%-20%) | **0.72** | Khá thuần |
| 🔵🔵🔵🔴🔴 (60%-40%) | **0.97** | Khá lộn xộn |
| 🔵🔵🔴🔴 (50%-50%) | **1.0** | Lộn xộn nhất ❌ |

### 💡 Nguyên tắc quan trọng:

> **Entropy càng THẤP → Dữ liệu càng THUẦN NHẤT → Càng TỐT!**

## 3.2. Công thức Entropy

### Công thức cho 2 lớp (Yes/No):

$$Entropy(S) = -p_{yes} \times \log_2(p_{yes}) - p_{no} \times \log_2(p_{no})$$

Trong đó:
- **p_yes** = Số mẫu Yes / Tổng số mẫu
- **p_no** = Số mẫu No / Tổng số mẫu

### ⚠️ Quy ước quan trọng:
$$0 \times \log_2(0) = 0$$

## 3.3. Ví dụ tính Entropy

### Ví dụ 1: Tập thuần nhất
```
Tập S: 10 Yes, 0 No

p(Yes) = 10/10 = 1.0
p(No) = 0/10 = 0

Entropy(S) = -1.0 × log₂(1.0) - 0 × log₂(0)
           = -1.0 × 0 - 0
           = 0 ✅
```

### Ví dụ 2: Tập 50-50 (lộn xộn nhất)
```
Tập S: 5 Yes, 5 No

p(Yes) = 5/10 = 0.5
p(No) = 5/10 = 0.5

log₂(0.5) = -1  ← CẦN NHỚ!

Entropy(S) = -0.5 × (-1) - 0.5 × (-1)
           = 0.5 + 0.5
           = 1.0 ❌ (Lộn xộn nhất)
```

### Ví dụ 3: Tập thực tế (9 Yes, 5 No)
```
Tập S: 9 Yes, 5 No (Tổng 14 mẫu)

p(Yes) = 9/14 ≈ 0.643
p(No) = 5/14 ≈ 0.357

Entropy(S) = -(9/14) × log₂(9/14) - (5/14) × log₂(5/14)
           ≈ 0.410 + 0.531
           = 0.941
```

---

# 4️⃣ INFORMATION GAIN

## 4.1. Khái niệm đơn giản

**Information Gain = Entropy GIẢM được bao nhiêu sau khi chia**

### 🤔 Hiểu Gain qua ví dụ:

Tưởng tượng bạn có đống bài lộn xộn (Entropy cao):

```
TRƯỚC KHI CHIA:              SAU KHI CHIA THEO MÀU:
┌─────────────────┐          ┌────────┐  ┌────────┐
│ ♥ ♠ ♦ ♣ ♥ ♠ ♦ ♣ │          │ ♥ ♥ ♦ ♦ │  │ ♠ ♠ ♣ ♣ │
│   Lộn xộn!      │    →     │  Đỏ    │  │  Đen   │
│ Entropy = 1.0   │          │ E ≈ 0  │  │ E ≈ 0  │
└─────────────────┘          └────────┘  └────────┘

Gain = 1.0 - 0 = 1.0 → Rất tốt!
```

**Giải thích:** Chia theo màu giúp giảm Entropy từ 1.0 xuống gần 0 → Gain cao!

### 💡 Công thức nhớ nhanh:

```
Gain = [Lộn xộn BAN ĐẦU] - [Lộn xộn SAU KHI CHIA]
     = Entropy(S) - Entropy_trung_bình(các nhánh con)
```

### ⚠️ Nguyên tắc quan trọng:

> **Gain càng CAO → Chia càng TỐT → Nên chọn thuộc tính đó!**
>
> **Gain = 0 → Thuộc tính VÔ DỤNG (không giúp phân loại)**

## 4.2. Công thức Information Gain

$$Gain(S, A) = Entropy(S) - \sum_{v \in Values(A)} \frac{|S_v|}{|S|} \times Entropy(S_v)$$

### 📖 Giải thích từng phần của công thức:

```
Gain(S, A) = Entropy(S)  -  Σ [ (|Sv|/|S|) × Entropy(Sv) ]
             ────┬────      ────────────┬────────────────
                 │                      │
         Entropy BAN ĐẦU      Entropy TRUNG BÌNH sau chia
        (độ lộn xộn gốc)      (có tính trọng số!)
```

**Chi tiết từng thành phần:**

| Ký hiệu | Ý nghĩa | Ví dụ |
|---------|---------|-------|
| **S** | Tập dữ liệu gốc | 14 mẫu |
| **A** | Thuộc tính đang xét | "Gió" |
| **Values(A)** | Các giá trị có thể của A | {Yếu, Mạnh} |
| **Sv** | Tập con khi A = v | Gió=Yếu: 8 mẫu |
| **\|Sv\|/\|S\|** | Tỷ trọng của nhánh con | 8/14 ≈ 0.57 |

### 🔑 Tại sao phải nhân với tỷ trọng?

Vì các nhánh con có kích thước khác nhau!

```
Ví dụ: Chia theo thuộc tính "Gió"

Tập gốc S (14 mẫu)
        │
    ┌───┴───┐
    │       │
 Yếu (8)  Mạnh (6)    ← Số mẫu khác nhau!
    │       │
    ↓       ↓
Weight = 8/14   Weight = 6/14

Entropy_tb = (8/14) × E(Yếu) + (6/14) × E(Mạnh)
           = trọng số × entropy + trọng số × entropy
```

**Nhánh lớn hơn (8 mẫu) ảnh hưởng NHIỀU hơn nhánh nhỏ (6 mẫu)!**

## 4.3. Ví dụ tính Gain

### Bài toán:
```
Tập S: 14 mẫu (9 Yes, 5 No) → Entropy(S) = 0.94

Thuộc tính "Gió" chia thành:
• Yếu: 8 mẫu (6 Yes, 2 No)
• Mạnh: 6 mẫu (3 Yes, 3 No)

Tính Gain(S, Gió)?
```

### Giải:

**Bước 1: Entropy ban đầu**
```
Entropy(S) = 0.94 (đã cho)
```

**Bước 2: Entropy từng nhánh**
```
Nhánh "Yếu" (6Y, 2N):
E(Yếu) = -(6/8)×log₂(6/8) - (2/8)×log₂(2/8)
       = -(0.75)×(-0.415) - (0.25)×(-2)
       = 0.311 + 0.500
       = 0.811

Nhánh "Mạnh" (3Y, 3N):
E(Mạnh) = -(3/6)×log₂(3/6) - (3/6)×log₂(3/6)
        = -(0.5)×(-1) - (0.5)×(-1)
        = 0.5 + 0.5
        = 1.0
```

**Bước 3: Entropy trung bình**
```
E_tb = (8/14) × 0.811 + (6/14) × 1.0
     = 0.463 + 0.429
     = 0.892
```

**Bước 4: Tính Gain**
```
Gain(S, Gió) = 0.94 - 0.892 = 0.048
```

---

# 5️⃣ VÍ DỤ TÍNH TOÁN CHI TIẾT

## 5.1. Bài toán Tennis

### Dữ liệu:

| Ngày | Thời tiết | Nhiệt độ | Độ ẩm | Gió | Chơi? |
|:----:|:---------:|:--------:|:-----:|:---:|:-----:|
| 1 | Nắng | Nóng | Cao | Yếu | ❌ |
| 2 | Nắng | Nóng | Cao | Mạnh | ❌ |
| 3 | Mây | Nóng | Cao | Yếu | ✅ |
| 4 | Mưa | Ấm | Cao | Yếu | ✅ |
| 5 | Mưa | Mát | BT | Yếu | ✅ |
| 6 | Mưa | Mát | BT | Mạnh | ❌ |
| 7 | Mây | Mát | BT | Mạnh | ✅ |
| 8 | Nắng | Ấm | Cao | Yếu | ❌ |
| 9 | Nắng | Mát | BT | Yếu | ✅ |
| 10 | Mưa | Ấm | BT | Yếu | ✅ |
| 11 | Nắng | Ấm | BT | Mạnh | ✅ |
| 12 | Mây | Ấm | Cao | Mạnh | ✅ |
| 13 | Mây | Nóng | BT | Yếu | ✅ |
| 14 | Mưa | Ấm | Cao | Mạnh | ❌ |

**Tổng: 9 Có (✅), 5 Không (❌)**

---

### BƯỚC 1: Tính Entropy(S) gốc

```
p(Yes) = 9/14 ≈ 0.643
p(No) = 5/14 ≈ 0.357

Entropy(S) = -(9/14)×log₂(9/14) - (5/14)×log₂(5/14)
           ≈ 0.410 + 0.531
           = 0.941 ✓
```

---

### BƯỚC 2: Tính Gain cho "Thời tiết"

**Chia theo Thời tiết:**

| Thời tiết | Yes | No | Tổng |
|:---------:|:---:|:--:|:----:|
| Nắng | 2 | 3 | 5 |
| Mây | 4 | 0 | 4 |
| Mưa | 3 | 2 | 5 |

**Entropy từng nhánh:**

```
E(Nắng) = -(2/5)×log₂(2/5) - (3/5)×log₂(3/5)
        = 0.529 + 0.442 = 0.971

E(Mây) = -(4/4)×log₂(4/4) - (0/4)×log₂(0/4)
       = 0 + 0 = 0  ← Thuần nhất!

E(Mưa) = -(3/5)×log₂(3/5) - (2/5)×log₂(2/5)
       = 0.442 + 0.529 = 0.971
```

**Entropy trung bình:**
```
E_tb = (5/14)×0.971 + (4/14)×0 + (5/14)×0.971
     = 0.347 + 0 + 0.347
     = 0.694
```

**Gain:**
```
Gain(S, Thời tiết) = 0.941 - 0.694 = 0.247 ✓
```

---

### BƯỚC 3: Tính Gain cho các thuộc tính khác

**(Tương tự, kết quả:)**

| Thuộc tính | Gain |
|:----------:|:----:|
| **Thời tiết** | **0.247** ⭐ MAX |
| Độ ẩm | 0.151 |
| Gió | 0.048 |
| Nhiệt độ | 0.029 |

**→ Chọn "Thời tiết" làm nút gốc!**

---

### BƯỚC 4: Xây dựng cây

```
                    ┌───────────────┐
                    │  THỜI TIẾT?   │ ← Root
                    └───────┬───────┘
                            │
          ┌─────────────────┼─────────────────┐
          │                 │                 │
       (Nắng)             (Mây)            (Mưa)
          │                 │                 │
          ▼                 ▼                 ▼
    ┌─────────┐      ┌─────────┐      ┌─────────┐
    │ ĐỘ ẨM?  │      │   CÓ    │      │  GIÓ?   │
    └────┬────┘      └─────────┘      └────┬────┘
         │                                  │
    ┌────┴────┐                       ┌────┴────┐
  (Cao)    (BT)                    (Yếu)   (Mạnh)
    │        │                        │        │
    ▼        ▼                        ▼        ▼
┌───────┐ ┌───────┐              ┌───────┐ ┌───────┐
│ KHÔNG │ │  CÓ   │              │  CÓ   │ │ KHÔNG │
└───────┘ └───────┘              └───────┘ └───────┘
```

---

# 6️⃣ BẢNG TRA CỨU LOG₂

## 6.1. Giá trị cần nhớ

| p | Phân số | log₂(p) | -p×log₂(p) |
|:-:|:-------:|:-------:|:----------:|
| 1.0 | 1/1 | 0 | 0 |
| 0.875 | 7/8 | -0.193 | 0.169 |
| 0.8 | 4/5 | -0.322 | 0.258 |
| 0.75 | 3/4 | -0.415 | 0.311 |
| 0.667 | 2/3 | -0.585 | 0.390 |
| 0.6 | 3/5 | -0.737 | 0.442 |
| **0.5** | **1/2** | **-1.0** | **0.5** |
| 0.4 | 2/5 | -1.322 | 0.529 |
| 0.333 | 1/3 | -1.585 | 0.528 |
| 0.25 | 1/4 | -2.0 | 0.500 |
| 0.2 | 1/5 | -2.322 | 0.464 |
| 0.0 | 0/n | undefined | **0** |

## 6.2. Bảng Entropy nhanh (2 lớp)

| Tỷ lệ (+/-) | Entropy |
|:-----------:|:-------:|
| 10/0 hoặc 0/10 | 0.00 |
| 9/1 hoặc 1/9 | 0.47 |
| 8/2 hoặc 2/8 | 0.72 |
| 7/3 hoặc 3/7 | 0.88 |
| 6/4 hoặc 4/6 | 0.97 |
| **5/5** | **1.00** |

## 6.3. Mẹo nhớ nhanh

```
log₂(1) = 0
log₂(1/2) = -1
log₂(1/4) = -2
log₂(1/8) = -3
```

---

# 7️⃣ QUY TRÌNH LÀM BÀI THI

## 7.1. Checklist 5 bước

```
□ Bước 0: Đọc đề, đếm số mẫu mỗi lớp
    → Ví dụ: 9 Yes, 5 No

□ Bước 1: Tính Entropy(S) gốc
    → Công thức: E = -p₊×log₂(p₊) - p₋×log₂(p₋)

□ Bước 2: VỚI MỖI thuộc tính:
    a. Lập bảng chia theo từng giá trị
    b. Tính Entropy từng nhánh
    c. Tính Entropy trung bình có trọng số
    d. Tính Gain = E(S) - E_tb

□ Bước 3: Chọn thuộc tính có Gain MAX
    → Tạo nút với thuộc tính đó

□ Bước 4: Lặp lại với các nhánh con
    → Dừng khi E=0 hoặc hết thuộc tính
```

## 7.2. Template tính Gain

```
════════════════════════════════════
TÍNH GAIN CHO THUỘC TÍNH [TÊN]
════════════════════════════════════

Bảng phân chia:
┌─────────────┬─────┬─────┬──────┐
│ Giá trị     │ Yes │ No  │ Tổng │
├─────────────┼─────┼─────┼──────┤
│ Giá trị 1   │ ___ │ ___ │ ___  │
│ Giá trị 2   │ ___ │ ___ │ ___  │
└─────────────┴─────┴─────┴──────┘

Entropy từng nhánh:
E(Giá trị 1) = ___
E(Giá trị 2) = ___

Entropy trung bình:
E_tb = (___/___) × ___ + (___/___) × ___
     = ___

GAIN = ___ - ___ = ___
```

---

# 8️⃣ CÁC TRƯỜNG HỢP ĐẶC BIỆT

## 8.1. Entropy = 0 (Tất cả cùng lớp)
→ **Tạo lá ngay**, không cần chia tiếp

## 8.2. Hết thuộc tính nhưng chưa thuần nhất
→ **Tạo lá với nhãn đa số**
```
Ví dụ: 7 Yes, 3 No → Tạo lá "Yes"
```

## 8.3. Nhiều thuộc tính có cùng Gain MAX
→ **Chọn bất kỳ** (hoặc theo alphabet)

## 8.4. Tập con rỗng
→ **Tạo lá với nhãn đa số của tập cha**

---

# 🔟 CÂU HỎI THƯỜNG GẶP (FAQ)

## Q1: Tại sao log cơ số 2, không phải 10?

**Trả lời:** Vì Entropy đo lường **lượng thông tin** tính bằng **bit**:
- 1 bit = thông tin cần để phân biệt 2 khả năng (Yes/No)
- log₂ phù hợp với hệ nhị phân (binary)

## Q2: 0 × log₂(0) = 0 có đúng không?

**Trả lời:** Về toán học, log₂(0) không xác định. Nhưng:
```
lim(x→0⁺) x × log₂(x) = 0
```
→ Theo **quy ước**, ta lấy 0 × log₂(0) = 0 ✓

## Q3: Tại sao chọn thuộc tính có Gain CAO nhất?

**Trả lời:**
- Gain cao = Giảm Entropy nhiều = Phân loại tốt hơn
- Cây sẽ ngắn hơn (ít tầng)
- Quyết định nhanh hơn
- Tổng quát hóa tốt hơn (ít overfitting)

## Q4: Entropy có thể âm không?

**Trả lời:** **KHÔNG!** Entropy luôn trong khoảng [0, 1] với 2 lớp:
- Entropy = 0 → Thuần nhất hoàn toàn
- Entropy = 1 → Lộn xộn nhất (50-50)

## Q5: Gain có thể âm không?

**Trả lời:** **KHÔNG!** Gain luôn ≥ 0:
- Gain = 0 → Thuộc tính không giúp ích gì
- Gain > 0 → Thuộc tính giúp phân loại

## Q6: ID3 khác gì C4.5 và CART?

| Thuật toán | Điểm khác biệt |
|------------|----------------|
| **ID3** | Chỉ thuộc tính rời rạc, dùng Gain |
| **C4.5** | Xử lý được liên tục, dùng Gain Ratio |
| **CART** | Cây nhị phân, dùng Gini Index |

---

# 1️⃣1️⃣ BÀI TẬP TỰ LUYỆN

## Bài 1: Tính Entropy

Cho các tập sau, tính Entropy:
- a) S₁ = [10 Yes, 0 No]
- b) S₂ = [6 Yes, 6 No]
- c) S₃ = [8 Yes, 4 No]

<details>
<summary>✅ Đáp án</summary>

a) E(S₁) = 0 (thuần nhất)
b) E(S₂) = 1.0 (lộn xộn nhất)
c) E(S₃) = 0.918

</details>

---

## Bài 2: So sánh Gain

Cho S = [8+, 8-], E(S) = 1.0

- Thuộc tính A: A=1 → [6+, 2-], A=0 → [2+, 6-]
- Thuộc tính B: B=1 → [4+, 4-], B=0 → [4+, 4-]

Thuộc tính nào tốt hơn?

<details>
<summary>✅ Đáp án</summary>

Gain(A) = 1.0 - 0.811 = 0.189
Gain(B) = 1.0 - 1.0 = 0

→ **A tốt hơn!**

</details>

---

## Bài 3: Xây dựng cây

| Màu | Hình | Mua? |
|:---:|:----:|:----:|
| Đỏ | Tròn | Có |
| Đỏ | Vuông | Có |
| Xanh | Tròn | Không |
| Xanh | Vuông | Không |

<details>
<summary>✅ Đáp án</summary>

```
      [MÀU?]
      /    \
   (Đỏ)  (Xanh)
     |       |
   [CÓ]  [KHÔNG]
```

Gain(Màu) = 1.0, Gain(Hình) = 0

</details>

---

> **💡 Lời khuyên cho kỳ thi:**
> 1. Học thuộc bảng log₂ thông dụng
> 2. Ghi rõ từng bước tính
> 3. Kiểm tra: Entropy luôn từ 0 đến 1
> 4. Gain = Entropy giảm được → luôn ≥ 0

---

**📚 Tài liệu tham khảo:**
- Slide Chương 6: Học máy (Slide 56-73)
- Quinlan, J.R. (1986). "Induction of Decision Trees"

---

_Hết tài liệu Decision Tree - Phương án 1: Giải thích đơn giản_
