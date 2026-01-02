# 📚 TÀI LIỆU ÔN TẬP: K-NEAREST NEIGHBOR (KNN)
## Phương án 1: Giải thích đơn giản, dễ hiểu

---

> **Lời mở đầu của Giảng viên:**
> 
> Xin chào các bạn sinh viên! Hôm nay chúng ta sẽ học về một thuật toán rất đơn giản nhưng cực kỳ hiệu quả trong Machine Learning - đó là **K-Nearest Neighbor (KNN)**.
> 
> Thuật toán này dựa trên một nguyên lý rất gần gũi trong cuộc sống: **"Ngưu tầm ngưu, mã tầm mã"** - tức là những thứ giống nhau thường ở gần nhau.

---

## 1️⃣ KNN LÀ GÌ?

### 1.1. Ý tưởng cốt lõi

Hãy tưởng tượng bạn đang ở một khu phố mới và muốn biết **nhà hàng này có ngon không**?

Cách đơn giản nhất là: **Hỏi những người đang ăn ở đó!**
- Nếu 3 người nói **"ngon"** và 1 người nói **"dở"** → Bạn kết luận: **Có lẽ ngon!**

Đây chính là cách KNN hoạt động:
- **K** = Số người bạn hỏi (số láng giềng gần nhất)
- **Nearest** = Những người ở gần nhất
- **Neighbor** = Láng giềng

### 1.2. Định nghĩa chính thức

> **KNN (K-Nearest Neighbor)** là thuật toán phân loại dựa trên việc tìm K điểm dữ liệu gần nhất với điểm cần phân loại, sau đó gán nhãn theo **đa số phiếu bầu**.

---

## 2️⃣ THUẬT TOÁN KNN TỪNG BƯỚC

### Bước 1: Chuẩn bị dữ liệu huấn luyện
Chúng ta có sẵn một tập dữ liệu đã được gán nhãn (ví dụ: các điểm đã biết là "Xanh" hoặc "Đỏ").

### Bước 2: Chọn giá trị K
K là số láng giềng mà ta sẽ tham khảo ý kiến.

**📌 Lưu ý quan trọng:**
- **K nên là số LẺ** (1, 3, 5, 7...) để tránh tình trạng hòa phiếu
- **K quá nhỏ** (K=1): Dễ bị nhiễu ảnh hưởng
- **K quá lớn**: Ranh giới phân loại bị mờ

### Bước 3: Tính khoảng cách
Với mỗi điểm mới cần phân loại, tính khoảng cách từ nó đến **TẤT CẢ** các điểm trong tập huấn luyện.

### Bước 4: Chọn K điểm gần nhất
Sắp xếp các khoảng cách theo thứ tự tăng dần, chọn K điểm có khoảng cách nhỏ nhất.

### Bước 5: Bỏ phiếu và quyết định
Trong K điểm đó, nhãn nào xuất hiện **nhiều nhất** sẽ được gán cho điểm mới.

---

## 3️⃣ CÔNG THỨC TÍNH KHOẢNG CÁCH

### 3.1. Khoảng cách Euclidean (Quan trọng nhất!)

Đây là công thức thầy **CHẮC CHẮN hỏi trong đề thi**:

#### Trường hợp 2 chiều (2D):
Cho 2 điểm: **A(x₁, y₁)** và **B(x₂, y₂)**

$$d(A, B) = \sqrt{(x_2 - x_1)^2 + (y_2 - y_1)^2}$$

#### Trường hợp n chiều (nD):
Cho 2 điểm: **A(a₁, a₂, ..., aₙ)** và **B(b₁, b₂, ..., bₙ)**

$$d(A, B) = \sqrt{\sum_{i=1}^{n}(b_i - a_i)^2}$$

### 3.2. Ví dụ tính tay

**Bài toán:** Tính khoảng cách giữa A(1, 2) và B(4, 6)

**Lời giải:**
```
d(A, B) = √[(4-1)² + (6-2)²]
        = √[3² + 4²]
        = √[9 + 16]
        = √25
        = 5
```

**💡 Mẹo nhớ:** Đây chính là tam giác vuông 3-4-5 quen thuộc!

---

## 4️⃣ VÍ DỤ MINH HỌA CHI TIẾT

### 4.1. Bài toán
Cho tập dữ liệu huấn luyện:

| Điểm | Tọa độ (x, y) | Nhãn |
|:----:|:-------------:|:----:|
| P₁ | (1, 1) | 🔵 Xanh |
| P₂ | (2, 1) | 🔵 Xanh |
| P₃ | (4, 3) | 🔴 Đỏ |
| P₄ | (5, 4) | 🔴 Đỏ |

**Hỏi:** Điểm mới **Q(3, 2)** thuộc lớp nào với **K = 3**?

### 4.2. Lời giải từng bước

**📍 Bước 1: Tính khoảng cách từ Q đến tất cả các điểm**

| Điểm | Công thức | Kết quả |
|:----:|:----------|:-------:|
| d(Q, P₁) | √[(3-1)² + (2-1)²] = √[4+1] | √5 ≈ **2.24** |
| d(Q, P₂) | √[(3-2)² + (2-1)²] = √[1+1] | √2 ≈ **1.41** |
| d(Q, P₃) | √[(3-4)² + (2-3)²] = √[1+1] | √2 ≈ **1.41** |
| d(Q, P₄) | √[(3-5)² + (2-4)²] = √[4+4] | √8 ≈ **2.83** |

**📍 Bước 2: Sắp xếp theo khoảng cách tăng dần**

| Thứ tự | Điểm | Khoảng cách | Nhãn |
|:------:|:----:|:-----------:|:----:|
| 1 | P₂ | 1.41 | 🔵 Xanh |
| 2 | P₃ | 1.41 | 🔴 Đỏ |
| 3 | P₁ | 2.24 | 🔵 Xanh |
| 4 | P₄ | 2.83 | 🔴 Đỏ |

**📍 Bước 3: Chọn K=3 điểm gần nhất**

3 điểm gần nhất là: **P₂, P₃, P₁**

**📍 Bước 4: Bỏ phiếu**

| Nhãn | Số phiếu |
|:----:|:--------:|
| 🔵 Xanh | 2 (P₂, P₁) |
| 🔴 Đỏ | 1 (P₃) |

**📍 Kết luận:** Điểm Q(3, 2) được gán nhãn **🔵 XANH** (vì 2 > 1)

---

## 5️⃣ ƯU ĐIỂM VÀ NHƯỢC ĐIỂM

### ✅ Ưu điểm
| Ưu điểm | Giải thích |
|---------|------------|
| **Đơn giản** | Không cần xây dựng mô hình phức tạp |
| **Không giả định phân phối** | Không cần biết dữ liệu tuân theo phân phối nào |
| **Dễ hiểu** | Ai cũng có thể hiểu được nguyên lý hoạt động |

### ❌ Nhược điểm
| Nhược điểm | Giải thích |
|------------|------------|
| **Chậm với dữ liệu lớn** | Phải tính khoảng cách với TẤT CẢ các điểm |
| **Nhạy với nhiễu** | Điểm dữ liệu sai có thể ảnh hưởng kết quả |
| **Cần chọn K phù hợp** | K khác nhau cho kết quả khác nhau |

---

## 6️⃣ MẸO LÀM BÀI THI

### 📝 Checklist khi làm bài

- [ ] Đọc kỹ đề xem **K bằng bao nhiêu**
- [ ] Lập bảng tính khoảng cách (ghi rõ từng bước)
- [ ] Sắp xếp từ bé đến lớn
- [ ] Chọn đúng K điểm đầu tiên
- [ ] Đếm số phiếu mỗi nhãn
- [ ] Kết luận rõ ràng

### 🔢 Bảng căn bậc 2 thường gặp (để tính nhanh)

| √1 | √2 | √3 | √4 | √5 | √8 | √9 | √10 |
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:---:|
| 1 | 1.41 | 1.73 | 2 | 2.24 | 2.83 | 3 | 3.16 |

---

## 7️⃣ CÂU HỎI TỰ KIỂM TRA

1. **Tại sao K thường được chọn là số lẻ?**
   <details>
   <summary>Xem đáp án</summary>
   Để tránh tình trạng hòa phiếu (ví dụ: 2 Xanh vs 2 Đỏ với K=4)
   </details>

2. **Nếu K = N (toàn bộ dữ liệu), điều gì xảy ra?**
   <details>
   <summary>Xem đáp án</summary>
   Mọi điểm mới đều được gán nhãn của lớp chiếm đa số trong tập huấn luyện
   </details>

3. **KNN có cần giai đoạn "huấn luyện" không?**
   <details>
   <summary>Xem đáp án</summary>
   Không. KNN là thuật toán "lazy learning" - chỉ lưu dữ liệu, không học gì cả.
   </details>

---

> **Lời kết của Giảng viên:**
> 
> KNN là thuật toán "ai cũng có thể hiểu được" nhưng đừng coi thường nó nhé! Trong thực tế, KNN vẫn được sử dụng rộng rãi trong nhiều bài toán như nhận dạng chữ viết tay, đề xuất sản phẩm...
> 
> Quan trọng nhất là các bạn phải **làm được bài tập tính tay** - đó là phần chắc chắn có trong đề thi!

---

*Hết tài liệu KNN - Phương án 1*
