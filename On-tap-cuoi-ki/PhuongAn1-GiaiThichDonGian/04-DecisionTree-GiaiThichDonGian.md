# 📚 TÀI LIỆU ÔN TẬP: CÂY QUYẾT ĐỊNH (DECISION TREE)
## Thuật toán ID3 - Phương án 1: Giải thích đơn giản, dễ hiểu

---

> **Lời mở đầu của Giảng viên:**
> 
> Chào các bạn! Hôm nay chúng ta học về **Cây quyết định (Decision Tree)** - một trong những thuật toán **trực quan nhất** trong Machine Learning.
> 
> Tại sao gọi là "trực quan"? Vì sau khi xây dựng xong, bạn có thể **nhìn vào cây** và hiểu ngay **TẠI SAO** máy tính đưa ra quyết định đó. Điều này rất quý giá trong nhiều lĩnh vực như y tế, tài chính...

---

## 1️⃣ CÂY QUYẾT ĐỊNH LÀ GÌ?

### 1.1. Ý tưởng cốt lõi

Hãy tưởng tượng cách bạn quyết định **có đi chơi tennis hôm nay không**:

```
Hỏi: Trời có mưa không?
├── CÓ mưa → KHÔNG đi (ở nhà)
└── KHÔNG mưa → Hỏi tiếp: Độ ẩm thế nào?
    ├── CAO → KHÔNG đi (nóng quá)
    └── BÌNH THƯỜNG → ĐI chơi!
```

Đây chính là một **Cây quyết định**!

### 1.2. Các thành phần của cây

| Thuật ngữ | Ý nghĩa | Ví dụ |
|-----------|---------|-------|
| **Root Node (Nút gốc)** | Câu hỏi đầu tiên, quan trọng nhất | "Trời có mưa không?" |
| **Internal Node (Nút trong)** | Các câu hỏi tiếp theo | "Độ ẩm thế nào?" |
| **Branch (Nhánh)** | Câu trả lời/điều kiện | "Có", "Không", "Cao", "Thấp" |
| **Leaf Node (Nút lá)** | Kết luận cuối cùng | "Đi chơi", "Ở nhà" |

### 1.3. Định nghĩa chính thức

> **Cây quyết định** là một cấu trúc cây dùng để phân loại dữ liệu bằng cách đặt các câu hỏi liên tiếp. Mỗi câu hỏi chia dữ liệu thành các nhóm nhỏ hơn, cho đến khi đạt được kết luận cuối cùng.

---

## 2️⃣ THUẬT TOÁN ID3

### 2.1. ID3 là gì?

**ID3 (Iterative Dichotomiser 3)** là thuật toán xây dựng cây quyết định được phát triển bởi Ross Quinlan (1986).

**Câu hỏi cốt lõi:** Làm sao biết câu hỏi nào nên hỏi **TRƯỚC**?

**Trả lời:** Hỏi câu nào giúp phân loại dữ liệu **TỐT NHẤT** trước!

### 2.2. Hai khái niệm quan trọng

#### 📊 ENTROPY (Độ hỗn loạn)

**Entropy** đo lường mức độ **"hỗn loạn"** hay **"không chắc chắn"** của dữ liệu.

**Công thức:**
$$Entropy(S) = -\sum_{i=1}^{c} p_i \times \log_2(p_i)$$

Trong đó:
- **S**: Tập dữ liệu
- **c**: Số lớp (ví dụ: 2 lớp "Có" và "Không")
- **p_i**: Tỷ lệ của lớp thứ i trong tập S

**Ý nghĩa:**
| Entropy | Ý nghĩa | Trạng thái |
|:-------:|---------|------------|
| **0** | Hoàn toàn đồng nhất | Tất cả đều "Có" hoặc "Không" → **RẤT TỐT** |
| **1** | Hoàn toàn hỗn loạn | 50% "Có", 50% "Không" → **RẤT TỆ** |

#### 📈 INFORMATION GAIN (Độ lợi thông tin)

**Gain** đo lường **mức độ giảm Entropy** khi chia dữ liệu theo một thuộc tính.

**Công thức:**
$$Gain(S, A) = Entropy(S) - \sum_{v \in Values(A)} \frac{|S_v|}{|S|} \times Entropy(S_v)$$

Trong đó:
- **S**: Tập dữ liệu ban đầu
- **A**: Thuộc tính đang xét
- **Values(A)**: Các giá trị có thể của A
- **S_v**: Tập con của S khi A = v

**Ý nghĩa:**
- **Gain CAO** → Thuộc tính A giúp phân loại TỐT → **CHỌN LÀM NÚT GỐC**
- **Gain THẤP** → Thuộc tính A không tốt → Bỏ qua

---

## 3️⃣ VÍ DỤ TÍNH TOÁN CHI TIẾT

### 3.1. Bài toán

Cho bảng dữ liệu về việc **chơi tennis**:

| Ngày | Thời tiết | Độ ẩm | Gió | Chơi? |
|:----:|:---------:|:-----:|:---:|:-----:|
| 1 | Nắng | Cao | Yếu | Không |
| 2 | Nắng | Cao | Mạnh | Không |
| 3 | Mây | Cao | Yếu | Có |
| 4 | Mưa | Cao | Yếu | Có |
| 5 | Mưa | Bình thường | Yếu | Có |
| 6 | Mưa | Bình thường | Mạnh | Không |
| 7 | Mây | Bình thường | Mạnh | Có |
| 8 | Nắng | Cao | Yếu | Không |
| 9 | Nắng | Bình thường | Yếu | Có |
| 10 | Mưa | Bình thường | Yếu | Có |
| 11 | Nắng | Bình thường | Mạnh | Có |
| 12 | Mây | Cao | Mạnh | Có |
| 13 | Mây | Bình thường | Yếu | Có |
| 14 | Mưa | Cao | Mạnh | Không |

**Yêu cầu:** Xây dựng cây quyết định sử dụng ID3.

### 3.2. Bước 1: Tính Entropy của tập gốc

**Đếm nhãn:**
- **Có (Yes):** 9 mẫu
- **Không (No):** 5 mẫu
- **Tổng:** 14 mẫu

**Tính tỷ lệ:**
- p(Có) = 9/14 ≈ 0.643
- p(Không) = 5/14 ≈ 0.357

**Áp dụng công thức:**
```
Entropy(S) = - p(Có) × log₂(p(Có)) - p(Không) × log₂(p(Không))
           = - (9/14) × log₂(9/14) - (5/14) × log₂(5/14)
           = - 0.643 × (-0.637) - 0.357 × (-1.486)
           = 0.410 + 0.531
           = 0.940
```

**Kết quả:** Entropy(S) = **0.940** (khá hỗn loạn)

### 3.3. Bước 2: Tính Gain cho thuộc tính "Thời tiết"

**Chia theo giá trị của "Thời tiết":**

| Thời tiết | Có | Không | Tổng |
|:---------:|:--:|:-----:|:----:|
| Nắng | 2 | 3 | 5 |
| Mây | 4 | 0 | 4 |
| Mưa | 3 | 2 | 5 |

**Tính Entropy từng nhánh:**

**Nắng:**
```
Entropy(Nắng) = -(2/5)log₂(2/5) - (3/5)log₂(3/5)
              = -0.4 × (-1.322) - 0.6 × (-0.737)
              = 0.529 + 0.442
              = 0.971
```

**Mây:**
```
Entropy(Mây) = -(4/4)log₂(4/4) - (0/4)log₂(0/4)
             = -1 × 0 - 0
             = 0  ← Hoàn toàn đồng nhất (tất cả đều "Có")!
```

**Mưa:**
```
Entropy(Mưa) = -(3/5)log₂(3/5) - (2/5)log₂(2/5)
             = 0.971
```

**Tính Gain:**
```
Gain(S, Thời tiết) = Entropy(S) - [(5/14)×E(Nắng) + (4/14)×E(Mây) + (5/14)×E(Mưa)]
                   = 0.940 - [0.357×0.971 + 0.286×0 + 0.357×0.971]
                   = 0.940 - [0.347 + 0 + 0.347]
                   = 0.940 - 0.694
                   = 0.246
```

### 3.4. Bước 3: So sánh và chọn

Tính tương tự với các thuộc tính khác:
- **Gain(Độ ẩm)** = 0.151
- **Gain(Gió)** = 0.048

**So sánh:**
| Thuộc tính | Gain |
|:----------:|:----:|
| **Thời tiết** | **0.246** ← MAX |
| Độ ẩm | 0.151 |
| Gió | 0.048 |

**Kết luận:** Chọn **"Thời tiết"** làm nút gốc!

### 3.5. Bước 4: Vẽ cây

```
                    [THỜI TIẾT?]
                   /      |      \
              (Nắng)    (Mây)    (Mưa)
               /          |         \
          [ĐỘ ẨM?]      [CÓ]     [GIÓ?]
          /      \                /    \
       (Cao)  (BT)            (Yếu) (Mạnh)
         |       |               |      |
      [KHÔNG]  [CÓ]            [CÓ] [KHÔNG]
```

---

## 4️⃣ BẢNG TRA CỨU LOG₂ (RẤT QUAN TRỌNG!)

Vì đề thi thường **không cho phép dùng máy tính**, hãy thuộc bảng này:

| p | p × log₂(p) | Ghi chú |
|:-:|:-----------:|---------|
| 1/2 = 0.5 | -0.500 | Nhớ: log₂(0.5) = -1 |
| 1/3 ≈ 0.33 | -0.528 | |
| 2/3 ≈ 0.67 | -0.389 | |
| 1/4 = 0.25 | -0.500 | Nhớ: log₂(0.25) = -2 |
| 3/4 = 0.75 | -0.311 | |
| 1/5 = 0.2 | -0.464 | |
| 2/5 = 0.4 | -0.529 | |
| 3/5 = 0.6 | -0.442 | |
| 4/5 = 0.8 | -0.258 | |

**Mẹo nhớ nhanh:**
- log₂(1) = 0
- log₂(0.5) = -1
- log₂(0.25) = -2
- log₂(0.125) = -3

---

## 5️⃣ QUY TRÌNH LÀM BÀI THI

### 📝 Checklist từng bước

- [ ] **Bước 1:** Đếm số lượng Có/Không của tập gốc
- [ ] **Bước 2:** Tính Entropy(S) gốc
- [ ] **Bước 3:** Với MỖI thuộc tính:
  - [ ] Chia dữ liệu theo từng giá trị
  - [ ] Tính Entropy của từng nhánh con
  - [ ] Tính Gain
- [ ] **Bước 4:** Chọn thuộc tính có **Gain MAX** làm nút
- [ ] **Bước 5:** Vẽ cây và lặp lại với các nhánh chưa thuần nhất

### ⚠️ Những lỗi thường gặp

1. **Quên dấu âm** trong công thức Entropy
2. **Nhầm log₂ với ln** (log tự nhiên)
3. **Quên chia trọng số** |Sv|/|S| khi tính Gain
4. **Tiếp tục chia** khi Entropy đã = 0 (nhánh đã thuần nhất)

---

## 6️⃣ CÂU HỎI TỰ KIỂM TRA

1. **Entropy = 0 có nghĩa là gì?**
   <details>
   <summary>Xem đáp án</summary>
   Dữ liệu hoàn toàn đồng nhất, tất cả thuộc cùng một lớp.
   </details>

2. **Tại sao chọn thuộc tính có Gain cao nhất?**
   <details>
   <summary>Xem đáp án</summary>
   Vì Gain cao = giảm Entropy nhiều = phân loại tốt hơn.
   </details>

3. **Khi nào dừng chia cây?**
   <details>
   <summary>Xem đáp án</summary>
   Khi Entropy của nhánh = 0, hoặc hết thuộc tính để chia.
   </details>

---

> **Lời kết của Giảng viên:**
> 
> Cây quyết định là thuật toán **"đẹp"** nhất trong ML vì tính minh bạch của nó. Sau khi xây xong cây, bạn có thể giải thích cho bất kỳ ai tại sao máy tính quyết định như vậy.
> 
> Trong đề thi, phần khó nhất là **tính toán thủ công** các giá trị log₂. Hãy học thuộc bảng tra cứu và luyện tập nhiều nhé!

---

*Hết tài liệu Decision Tree - Phương án 1*
