# PHƯƠNG ÁN 1: GIẢI THÍCH ĐƠN GIẢN
# THUẬT TOÁN K-MEANS CLUSTERING

---

## 📚 MỤC LỤC

1. [Giới thiệu tổng quan](#1-giới-thiệu-tổng-quan)
2. [Tại sao cần phân cụm?](#2-tại-sao-cần-phân-cụm)
3. [K-means là gì?](#3-k-means-là-gì)
4. [Các bước thuật toán chi tiết](#4-các-bước-thuật-toán-chi-tiết)
5. [Công thức toán học](#5-công-thức-toán-học)
6. [Ví dụ minh họa từng bước](#6-ví-dụ-minh-họa-từng-bước)
7. [Các trường hợp đặc biệt](#7-các-trường-hợp-đặc-biệt)
8. [Ưu và nhược điểm](#8-ưu-và-nhược-điểm)
9. [Câu hỏi thường gặp](#9-câu-hỏi-thường-gặp)
10. [Tổng kết](#10-tổng-kết)

---

# 1. GIỚI THIỆU TỔNG QUAN

## 1.1. Học máy là gì?

Trước khi đi vào K-means, chúng ta cần hiểu K-means thuộc lĩnh vực nào.

**Học máy (Machine Learning)** là một nhánh của trí tuệ nhân tạo, cho phép máy tính "học" từ dữ liệu mà không cần lập trình cụ thể cho từng trường hợp.

Học máy được chia thành 3 loại chính:

### 1.1.1. Học có giám sát (Supervised Learning)
- **Đặc điểm:** Dữ liệu huấn luyện có nhãn (label)
- **Ví dụ:** Phân loại email spam/không spam
  - Dữ liệu: 1000 email đã được gán nhãn "spam" hoặc "không spam"
  - Mục tiêu: Học cách phân loại email mới

### 1.1.2. Học không giám sát (Unsupervised Learning)
- **Đặc điểm:** Dữ liệu KHÔNG có nhãn
- **Ví dụ:** Phân nhóm khách hàng theo hành vi mua sắm
  - Dữ liệu: Lịch sử mua hàng của 10.000 khách
  - Mục tiêu: Tự động tìm ra các nhóm khách hàng tương tự nhau

### 1.1.3. Học tăng cường (Reinforcement Learning)
- **Đặc điểm:** Học thông qua thử và sai
- **Ví dụ:** Robot học cách đi bộ

**K-means thuộc loại HỌC KHÔNG GIÁM SÁT** - nghĩa là dữ liệu của chúng ta không có nhãn sẵn, và thuật toán sẽ tự tìm ra cấu trúc ẩn trong dữ liệu.

---

## 1.2. Phân cụm (Clustering) là gì?

**Phân cụm** là quá trình chia một tập dữ liệu thành các nhóm (cụm) sao cho:
- Các điểm trong **cùng một cụm** có đặc điểm **tương tự nhau**
- Các điểm trong **khác cụm** có đặc điểm **khác nhau**

### Ví dụ đời thường về phân cụm:

**Ví dụ 1: Thư viện sách**
- Bạn có 1000 cuốn sách
- Bạn muốn xếp chúng lên giá sao cho dễ tìm
- Cách phân: Theo thể loại (Văn học, Khoa học, Lịch sử...)
- Kết quả: Sách cùng thể loại ở gần nhau trên giá

**Ví dụ 2: Phân loại học sinh**
- Trường có 500 học sinh
- Giáo viên muốn chia thành các nhóm để dạy phù hợp
- Cách phân: Theo năng lực (Giỏi, Khá, Trung bình)
- Kết quả: Học sinh cùng trình độ học cùng lớp

**Ví dụ 3: Phân loại khách hàng**
- Siêu thị có 10.000 khách hàng
- Marketing muốn gửi khuyến mãi phù hợp
- Cách phân: Theo hành vi mua sắm
- Kết quả: 
  - Nhóm 1: Khách mua nhiều đồ ăn vặt → khuyến mãi snack
  - Nhóm 2: Khách mua nhiều rau củ → khuyến mãi thực phẩm sạch
  - Nhóm 3: Khách mua nhiều đồ gia dụng → khuyến mãi thiết bị

---

# 2. TẠI SAO CẦN PHÂN CỤM?

## 2.1. Các ứng dụng thực tế

### 2.1.1. Trong kinh doanh

**Phân khúc thị trường (Market Segmentation)**
- **Bài toán:** Công ty có hàng triệu khách hàng, làm sao tiếp cận hiệu quả?
- **Giải pháp:** Phân cụm khách hàng theo:
  - Độ tuổi
  - Thu nhập
  - Sở thích mua sắm
  - Tần suất mua hàng
- **Kết quả:** 
  - Cụm "Sinh viên": Giá rẻ, khuyến mãi lớn
  - Cụm "Gia đình": Combo tiết kiệm, đồ số lượng lớn
  - Cụm "Doanh nhân": Sản phẩm cao cấp, dịch vụ VIP

**Phát hiện gian lận (Fraud Detection)**
- **Bài toán:** Ngân hàng có hàng triệu giao dịch, làm sao phát hiện gian lận?
- **Giải pháp:** Phân cụm các giao dịch theo:
  - Số tiền
  - Thời gian
  - Địa điểm
  - Tần suất
- **Kết quả:** Giao dịch bất thường sẽ nằm trong cụm riêng → cần kiểm tra

### 2.1.2. Trong y tế

**Phân loại bệnh nhân**
- **Bài toán:** Bệnh viện có 1000 bệnh nhân, cần chia phòng hợp lý
- **Giải pháp:** Phân cụm theo:
  - Mức độ nghiêm trọng
  - Loại bệnh
  - Độ tuổi
- **Kết quả:** 
  - Cụm "Cấp cứu": Cần theo dõi 24/7
  - Cụm "Ngoại trú": Khám định kỳ
  - Cụm "Phục hồi": Chế độ nghỉ ngơi

**Phân tích gen**
- **Bài toán:** Nghiên cứu hàng nghìn mẫu gen
- **Giải pháp:** Phân cụm các gen có biểu hiện tương tự
- **Kết quả:** Phát hiện nhóm gen liên quan đến bệnh cụ thể

### 2.1.3. Trong công nghệ

**Nén ảnh (Image Compression)**
- **Bài toán:** Ảnh có hàng triệu pixel, mỗi pixel 16 triệu màu
- **Giải pháp:** Phân cụm màu sắc thành K nhóm (ví dụ K=16)
- **Kết quả:** Ảnh chỉ còn 16 màu nhưng vẫn đẹp, dung lượng giảm đáng kể

**Gom nhóm tin tức (News Clustering)**
- **Bài toán:** Hàng nghìn bài báo mỗi ngày
- **Giải pháp:** Phân cụm theo nội dung
- **Kết quả:** 
  - Cụm "Thể thao"
  - Cụm "Chính trị"
  - Cụm "Giải trí"
  - Cụm "Công nghệ"

---

## 2.2. Tại sao chọn K-means?

Có nhiều thuật toán phân cụm khác nhau:
- K-means
- Hierarchical Clustering
- DBSCAN
- Gaussian Mixture Models

**K-means được chọn vì:**

| Tiêu chí | K-means | Các thuật toán khác |
|----------|---------|---------------------|
| Đơn giản | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ |
| Tốc độ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ |
| Dễ hiểu | ⭐⭐⭐⭐⭐ | ⭐⭐ |
| Hiệu quả với dữ liệu lớn | ⭐⭐⭐⭐ | ⭐⭐⭐ |

---

# 3. K-MEANS LÀ GÌ?

## 3.1. Định nghĩa đơn giản

**K-means** là thuật toán phân cụm chia dữ liệu thành **K nhóm** dựa trên **khoảng cách** đến tâm của mỗi nhóm.

Trong đó:
- **K**: Số cụm (do người dùng chọn trước)
- **means**: Giá trị trung bình (tâm cụm được tính bằng trung bình các điểm)

## 3.2. Ý tưởng cốt lõi

Hãy tưởng tượng bạn là **chủ cửa hàng pizza** và muốn mở **3 điểm giao hàng** để phục vụ 100 khách hàng ở các vị trí khác nhau trên bản đồ.

**Câu hỏi:** Đặt 3 điểm giao hàng ở đâu để khoảng cách đến khách hàng là ngắn nhất?

**Cách giải quyết:**
1. **Chia 100 khách thành 3 nhóm** theo vị trí địa lý
2. **Đặt điểm giao hàng ở trung tâm** của mỗi nhóm

Đây chính là ý tưởng của K-means!

## 3.3. Minh họa trực quan

```
Trước khi phân cụm:               Sau khi phân cụm (K=3):

    •  •                              ○  ○      (Cụm 1)
  •  •  •                           ○  ○  ○
      •                                ○
                                    
    •    •                            △    △    (Cụm 2)
      • •                               △ △
    •                                 △
                                    
        •  •                              □  □  (Cụm 3)
      •  •  •                           □  □  □
        •                                 □

Chú thích:
• = Điểm dữ liệu chưa phân cụm
○ △ □ = Các điểm đã được gán vào cụm khác nhau
```

---

## 3.4. Các khái niệm quan trọng

### 3.4.1. Centroid (Tâm cụm)

**Centroid** là điểm đại diện cho một cụm, được tính bằng **trung bình tọa độ** của tất cả các điểm trong cụm đó.

**Ví dụ:**
- Cụm có 3 điểm: A(2, 4), B(4, 6), C(6, 8)
- Centroid = ((2+4+6)/3, (4+6+8)/3) = (4, 6)

```
      8 |         C(6,8)
      7 |       
      6 |     B(4,6) ★ ← Centroid(4,6)
      5 |       
      4 | A(2,4)
      3 |
      2 |
      1 |
        +--------------------
          1  2  3  4  5  6  7
```

### 3.4.2. Khoảng cách Euclidean

**Khoảng cách Euclidean** là khoảng cách "đường chim bay" giữa 2 điểm trong không gian.

**Công thức 2 chiều:**
```
d(A, B) = √[(x₂ - x₁)² + (y₂ - y₁)²]
```

**Ví dụ:**
- Điểm A(1, 1) và điểm B(4, 5)
- d(A, B) = √[(4-1)² + (5-1)²]
- d(A, B) = √[3² + 4²]
- d(A, B) = √[9 + 16]
- d(A, B) = √25
- d(A, B) = **5**

**Mẹo nhớ:** Đây chính là định lý Pytago mà bạn đã học!

```
    5 |       B(4,5)
    4 |       /|
    3 |      / | 4
    2 |     /  |
    1 | A(1,1)--+
      +------------
        1  2  3  4
        
    AB² = 3² + 4² = 9 + 16 = 25
    AB = 5
```

### 3.4.3. Cluster (Cụm)

**Cluster** là một nhóm các điểm dữ liệu có đặc điểm tương tự nhau.

**Đặc điểm của một cụm tốt:**
- Các điểm trong cùng cụm: **gần nhau** (intra-cluster distance nhỏ)
- Các điểm khác cụm: **xa nhau** (inter-cluster distance lớn)

---

# 4. CÁC BƯỚC THUẬT TOÁN CHI TIẾT

## 4.1. Tổng quan 4 bước

```
┌─────────────────────────────────────────────────────────┐
│                    THUẬT TOÁN K-MEANS                   │
├─────────────────────────────────────────────────────────┤
│                                                         │
│   Bước 1: Chọn K tâm cụm ban đầu (ngẫu nhiên)          │
│                       ↓                                 │
│   Bước 2: Gán mỗi điểm vào cụm có tâm gần nhất         │
│                       ↓                                 │
│   Bước 3: Tính lại tâm cụm mới                         │
│                       ↓                                 │
│   Bước 4: Nếu tâm cụm thay đổi → Quay lại Bước 2       │
│           Nếu không đổi → DỪNG                         │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

## 4.2. Bước 1: Khởi tạo tâm cụm

### Mục tiêu
Chọn K điểm làm tâm cụm ban đầu.

### Các cách khởi tạo

**Cách 1: Chọn ngẫu nhiên K điểm từ dữ liệu**
- Đơn giản nhất
- Có thể dẫn đến kết quả không tối ưu

**Cách 2: Chọn K điểm xa nhau nhất**
- Tốt hơn cách 1
- Cần tính khoảng cách ban đầu

**Cách 3: K-means++ (Nâng cao)**
- Chọn điểm đầu tiên ngẫu nhiên
- Các điểm tiếp theo được chọn sao cho xa các điểm đã chọn
- Cho kết quả tốt hơn

### Ví dụ minh họa

Cho tập dữ liệu: A(1,1), B(2,1), C(4,3), D(5,4), E(6,3)

Nếu K = 2 và chọn ngẫu nhiên:
- **Có thể chọn:** C₁ = A(1,1), C₂ = C(4,3)
- **Hoặc chọn:** C₁ = B(2,1), C₂ = E(6,3)

Tâm ban đầu khác nhau có thể dẫn đến kết quả phân cụm khác nhau!

---

## 4.3. Bước 2: Gán điểm vào cụm

### Mục tiêu
Với mỗi điểm dữ liệu, tìm tâm cụm gần nhất và gán điểm đó vào cụm tương ứng.

### Thuật toán chi tiết

```
Với mỗi điểm P trong tập dữ liệu:
    1. Tính khoảng cách từ P đến tất cả K tâm cụm
    2. Tìm tâm cụm có khoảng cách nhỏ nhất
    3. Gán P vào cụm đó
```

### Ví dụ minh họa

**Dữ liệu:** A(1,1), B(2,1), C(4,3), D(5,4)
**Tâm ban đầu:** C₁ = (1,1), C₂ = (4,3)

**Tính khoảng cách cho điểm A(1,1):**
- d(A, C₁) = √[(1-1)² + (1-1)²] = √0 = 0
- d(A, C₂) = √[(4-1)² + (3-1)²] = √[9+4] = √13 ≈ 3.61

**Kết luận:** A gần C₁ hơn → **Gán A vào Cụm 1**

**Tương tự cho các điểm khác:**

| Điểm | d(điểm, C₁) | d(điểm, C₂) | Gán vào |
|------|-------------|-------------|---------|
| A(1,1) | 0 | 3.61 | **Cụm 1** |
| B(2,1) | 1 | 2.83 | **Cụm 1** |
| C(4,3) | 3.61 | 0 | **Cụm 2** |
| D(5,4) | 5 | 1.41 | **Cụm 2** |

**Kết quả:**
- Cụm 1: {A, B}
- Cụm 2: {C, D}

---

## 4.4. Bước 3: Tính lại tâm cụm

### Mục tiêu
Sau khi các điểm đã được gán vào cụm, tính lại tâm cụm mới bằng cách lấy **trung bình tọa độ** của tất cả các điểm trong cụm.

### Công thức

```
Tâm cụm mới = (x̄, ȳ) = (Σxᵢ/n, Σyᵢ/n)
```

Với n là số điểm trong cụm.

### Ví dụ minh họa

**Cụm 1:** {A(1,1), B(2,1)}
```
C₁_mới = ((1+2)/2, (1+1)/2) = (1.5, 1)
```

**Cụm 2:** {C(4,3), D(5,4)}
```
C₂_mới = ((4+5)/2, (3+4)/2) = (4.5, 3.5)
```

---

## 4.5. Bước 4: Kiểm tra hội tụ

### Định nghĩa hội tụ
Thuật toán **hội tụ** khi tâm cụm không thay đổi (hoặc thay đổi rất nhỏ) sau khi tính lại.

### Điều kiện dừng

**Điều kiện 1: Tâm cụm không đổi**
```
Nếu C₁_mới = C₁_cũ VÀ C₂_mới = C₂_cũ VÀ ... → DỪNG
```

**Điều kiện 2: Phân cụm không đổi**
```
Nếu không có điểm nào đổi cụm → DỪNG
```

**Điều kiện 3: Đạt số vòng lặp tối đa**
```
Nếu đã lặp quá nhiều lần (ví dụ: 100 lần) → DỪNG
```

### Nếu chưa hội tụ?
Quay lại **Bước 2** với tâm cụm mới.

---

# 5. CÔNG THỨC TOÁN HỌC

## 5.1. Bảng tổng hợp công thức

| STT | Công thức | Tên | Ý nghĩa |
|-----|-----------|-----|---------|
| 1 | d = √[(x₂-x₁)² + (y₂-y₁)²] | Khoảng cách Euclidean 2D | Đo khoảng cách giữa 2 điểm |
| 2 | d = √[Σᵢ(aᵢ-bᵢ)²] | Khoảng cách Euclidean nD | Đo khoảng cách trong không gian n chiều |
| 3 | C = (Σxᵢ/n, Σyᵢ/n) | Tâm cụm (Centroid) | Điểm trung tâm của cụm |
| 4 | J = Σₖ Σᵢ∈Cₖ ‖xᵢ - μₖ‖² | Hàm mục tiêu | Tổng bình phương khoảng cách trong cụm |

## 5.2. Giải thích chi tiết từng công thức

### 5.2.1. Khoảng cách Euclidean 2D

**Công thức:**
```
d(A, B) = √[(x₂ - x₁)² + (y₂ - y₁)²]
```

**Các bước tính:**
1. Tính hiệu tọa độ x: (x₂ - x₁)
2. Tính hiệu tọa độ y: (y₂ - y₁)
3. Bình phương cả hai
4. Cộng lại
5. Lấy căn bậc 2

**Ví dụ chi tiết:**
```
A = (2, 3), B = (5, 7)

Bước 1: x₂ - x₁ = 5 - 2 = 3
Bước 2: y₂ - y₁ = 7 - 3 = 4
Bước 3: 3² = 9, 4² = 16
Bước 4: 9 + 16 = 25
Bước 5: √25 = 5

Kết quả: d(A, B) = 5
```

### 5.2.2. Khoảng cách Euclidean nD

**Công thức:**
```
d(A, B) = √[Σᵢ₌₁ⁿ (aᵢ - bᵢ)²]
```

**Ví dụ với 3 chiều:**
```
A = (1, 2, 3), B = (4, 6, 3)

d(A, B) = √[(4-1)² + (6-2)² + (3-3)²]
        = √[9 + 16 + 0]
        = √25
        = 5
```

### 5.2.3. Tâm cụm (Centroid)

**Công thức:**
```
C = (x̄, ȳ) = (Σxᵢ/n, Σyᵢ/n)
```

**Ví dụ:**
```
Cụm có 4 điểm: (1,2), (3,4), (5,6), (7,8)

x̄ = (1 + 3 + 5 + 7) / 4 = 16/4 = 4
ȳ = (2 + 4 + 6 + 8) / 4 = 20/4 = 5

Centroid = (4, 5)
```

---

# 6. VÍ DỤ MINH HỌA TỪNG BƯỚC

## 6.1. Ví dụ 1: Phân cụm đơn giản (K=2)

### Đề bài
Cho tập dữ liệu gồm 6 điểm trong không gian 2D:

| Điểm | x | y |
|------|---|---|
| P₁ | 1 | 1 |
| P₂ | 1 | 2 |
| P₃ | 2 | 1 |
| P₄ | 5 | 4 |
| P₅ | 6 | 5 |
| P₆ | 5 | 5 |

Sử dụng K-means với K=2. Tâm ban đầu: C₁ = P₁(1,1), C₂ = P₄(5,4).

---

### VÒNG LẶP 1

**Bước 1: Tính khoảng cách từ mỗi điểm đến các tâm**

**Điểm P₁(1,1):**
- d(P₁, C₁) = √[(1-1)² + (1-1)²] = √0 = 0
- d(P₁, C₂) = √[(5-1)² + (4-1)²] = √[16+9] = √25 = 5
- **Gán P₁ → Cụm 1** (vì 0 < 5)

**Điểm P₂(1,2):**
- d(P₂, C₁) = √[(1-1)² + (2-1)²] = √1 = 1
- d(P₂, C₂) = √[(5-1)² + (4-2)²] = √[16+4] = √20 ≈ 4.47
- **Gán P₂ → Cụm 1** (vì 1 < 4.47)

**Điểm P₃(2,1):**
- d(P₃, C₁) = √[(2-1)² + (1-1)²] = √1 = 1
- d(P₃, C₂) = √[(5-2)² + (4-1)²] = √[9+9] = √18 ≈ 4.24
- **Gán P₃ → Cụm 1** (vì 1 < 4.24)

**Điểm P₄(5,4):**
- d(P₄, C₁) = √[(5-1)² + (4-1)²] = √25 = 5
- d(P₄, C₂) = √[(5-5)² + (4-4)²] = √0 = 0
- **Gán P₄ → Cụm 2** (vì 0 < 5)

**Điểm P₅(6,5):**
- d(P₅, C₁) = √[(6-1)² + (5-1)²] = √[25+16] = √41 ≈ 6.40
- d(P₅, C₂) = √[(6-5)² + (5-4)²] = √[1+1] = √2 ≈ 1.41
- **Gán P₅ → Cụm 2** (vì 1.41 < 6.40)

**Điểm P₆(5,5):**
- d(P₆, C₁) = √[(5-1)² + (5-1)²] = √[16+16] = √32 ≈ 5.66
- d(P₆, C₂) = √[(5-5)² + (5-4)²] = √1 = 1
- **Gán P₆ → Cụm 2** (vì 1 < 5.66)

**Bảng tổng hợp Vòng 1:**

| Điểm | d(điểm, C₁) | d(điểm, C₂) | Gán vào |
|------|-------------|-------------|---------|
| P₁(1,1) | 0 | 5 | Cụm 1 |
| P₂(1,2) | 1 | 4.47 | Cụm 1 |
| P₃(2,1) | 1 | 4.24 | Cụm 1 |
| P₄(5,4) | 5 | 0 | Cụm 2 |
| P₅(6,5) | 6.40 | 1.41 | Cụm 2 |
| P₆(5,5) | 5.66 | 1 | Cụm 2 |

**Kết quả phân cụm Vòng 1:**
- **Cụm 1:** {P₁(1,1), P₂(1,2), P₃(2,1)}
- **Cụm 2:** {P₄(5,4), P₅(6,5), P₆(5,5)}

---

**Bước 2: Tính tâm cụm mới**

**Cụm 1:** {P₁(1,1), P₂(1,2), P₃(2,1)}
```
C₁_mới = ((1+1+2)/3, (1+2+1)/3)
       = (4/3, 4/3)
       = (1.33, 1.33)
```

**Cụm 2:** {P₄(5,4), P₅(6,5), P₆(5,5)}
```
C₂_mới = ((5+6+5)/3, (4+5+5)/3)
       = (16/3, 14/3)
       = (5.33, 4.67)
```

---

### VÒNG LẶP 2

**Tâm cụm mới:** C₁ = (1.33, 1.33), C₂ = (5.33, 4.67)

**Bước 1: Tính lại khoảng cách**

**Điểm P₁(1,1):**
- d(P₁, C₁) = √[(1-1.33)² + (1-1.33)²] = √[0.11+0.11] = √0.22 ≈ 0.47
- d(P₁, C₂) = √[(1-5.33)² + (1-4.67)²] = √[18.75+13.47] = √32.22 ≈ 5.68
- **Gán P₁ → Cụm 1**

**Điểm P₂(1,2):**
- d(P₂, C₁) = √[(1-1.33)² + (2-1.33)²] = √[0.11+0.45] = √0.56 ≈ 0.75
- d(P₂, C₂) = √[(1-5.33)² + (2-4.67)²] = √[18.75+7.13] = √25.88 ≈ 5.09
- **Gán P₂ → Cụm 1**

**Tương tự cho các điểm còn lại...**

| Điểm | d(điểm, C₁) | d(điểm, C₂) | Gán vào |
|------|-------------|-------------|---------|
| P₁(1,1) | 0.47 | 5.68 | Cụm 1 |
| P₂(1,2) | 0.75 | 5.09 | Cụm 1 |
| P₃(2,1) | 0.75 | 4.72 | Cụm 1 |
| P₄(5,4) | 4.72 | 0.75 | Cụm 2 |
| P₅(6,5) | 5.88 | 0.75 | Cụm 2 |
| P₆(5,5) | 5.09 | 0.47 | Cụm 2 |

**Kết quả:** Phân cụm không thay đổi so với Vòng 1!

---

**Bước 2: Kiểm tra hội tụ**

Vì phân cụm không thay đổi → **THUẬT TOÁN HỘI TỤ**

---

### KẾT QUẢ CUỐI CÙNG

```
┌─────────────────────────────────────────────────────────┐
│                    KẾT QUẢ PHÂN CỤM                     │
├─────────────────────────────────────────────────────────┤
│                                                         │
│   CỤM 1: {P₁(1,1), P₂(1,2), P₃(2,1)}                   │
│   Tâm cụm: (1.33, 1.33)                                │
│                                                         │
│   CỤM 2: {P₄(5,4), P₅(6,5), P₆(5,5)}                   │
│   Tâm cụm: (5.33, 4.67)                                │
│                                                         │
│   Số vòng lặp: 2                                       │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

---

## 6.2. Ví dụ 2: Phân cụm với K=3

### Đề bài
Cho tập dữ liệu 9 điểm:

| Điểm | x | y |
|------|---|---|
| A | 1 | 1 |
| B | 2 | 1 |
| C | 1 | 2 |
| D | 5 | 5 |
| E | 6 | 5 |
| F | 5 | 6 |
| G | 9 | 1 |
| H | 10 | 1 |
| I | 9 | 2 |

Phân cụm với K=3. Tâm ban đầu: C₁ = A(1,1), C₂ = D(5,5), C₃ = G(9,1).

---

### VÒNG LẶP 1

**Tính khoảng cách và gán cụm:**

| Điểm | d(C₁) | d(C₂) | d(C₃) | Gán |
|------|-------|-------|-------|-----|
| A(1,1) | 0 | 5.66 | 8 | Cụm 1 |
| B(2,1) | 1 | 5 | 7 | Cụm 1 |
| C(1,2) | 1 | 5 | 8.06 | Cụm 1 |
| D(5,5) | 5.66 | 0 | 5.66 | Cụm 2 |
| E(6,5) | 6.40 | 1 | 5 | Cụm 2 |
| F(5,6) | 6.40 | 1 | 6.40 | Cụm 2 |
| G(9,1) | 8 | 5.66 | 0 | Cụm 3 |
| H(10,1) | 9 | 6.40 | 1 | Cụm 3 |
| I(9,2) | 8.06 | 5 | 1 | Cụm 3 |

**Kết quả Vòng 1:**
- **Cụm 1:** {A, B, C}
- **Cụm 2:** {D, E, F}
- **Cụm 3:** {G, H, I}

**Tính tâm mới:**
```
C₁ = ((1+2+1)/3, (1+1+2)/3) = (1.33, 1.33)
C₂ = ((5+6+5)/3, (5+5+6)/3) = (5.33, 5.33)
C₃ = ((9+10+9)/3, (1+1+2)/3) = (9.33, 1.33)
```

---

### Kiểm tra hội tụ

Sau Vòng 2, phân cụm không đổi → **HỘI TỤ**

**Kết quả cuối cùng:**
- **Cụm 1:** {A(1,1), B(2,1), C(1,2)} - Tâm: (1.33, 1.33)
- **Cụm 2:** {D(5,5), E(6,5), F(5,6)} - Tâm: (5.33, 5.33)
- **Cụm 3:** {G(9,1), H(10,1), I(9,2)} - Tâm: (9.33, 1.33)

---

# 7. CÁC TRƯỜNG HỢP ĐẶC BIỆT

## 7.1. Điểm nằm cách đều hai tâm

**Tình huống:** Một điểm có khoảng cách bằng nhau đến 2 hoặc nhiều tâm cụm.

**Ví dụ:**
- Điểm P(3, 3)
- Tâm C₁ = (1, 3), C₂ = (5, 3)
- d(P, C₁) = |3-1| = 2
- d(P, C₂) = |5-3| = 2

**Giải quyết:**
1. Chọn cụm đầu tiên tìm được
2. Hoặc chọn ngẫu nhiên
3. Kết quả cuối cùng thường không ảnh hưởng nhiều

## 7.2. Cụm rỗng

**Tình huống:** Sau khi gán, một cụm không có điểm nào.

**Nguyên nhân:** Tâm ban đầu được chọn không tốt.

**Giải quyết:**
1. Chọn lại tâm cho cụm rỗng từ điểm xa nhất với các tâm khác
2. Hoặc khởi tạo lại từ đầu với tâm khác

## 7.3. Thuật toán không hội tụ

**Tình huống:** Thuật toán chạy mãi không dừng.

**Thực tế:** K-means luôn hội tụ về mặt lý thuyết, nhưng có thể rất chậm.

**Giải quyết:** Đặt giới hạn số vòng lặp tối đa (ví dụ: 100 vòng).

---

# 8. ƯU VÀ NHƯỢC ĐIỂM

## 8.1. Ưu điểm

| STT | Ưu điểm | Giải thích |
|-----|---------|------------|
| 1 | Đơn giản | Chỉ cần 2 công thức cơ bản |
| 2 | Nhanh | Độ phức tạp O(n×K×t) với t là số vòng lặp |
| 3 | Dễ hiểu | Trực quan, dễ giải thích |
| 4 | Hiệu quả với dữ liệu lớn | Có thể xử lý hàng triệu điểm |
| 5 | Dễ cài đặt | Vài chục dòng code |

## 8.2. Nhược điểm

| STT | Nhược điểm | Giải thích |
|-----|------------|------------|
| 1 | Phải chọn K trước | Không tự động xác định số cụm |
| 2 | Nhạy với tâm ban đầu | Tâm khác → kết quả khác |
| 3 | Chỉ tìm cụm hình cầu | Không tốt với cụm hình dạng phức tạp |
| 4 | Nhạy với outlier | Điểm ngoại lệ ảnh hưởng lớn đến tâm |
| 5 | Chỉ tìm nghiệm cục bộ | Không đảm bảo tối ưu toàn cục |

## 8.3. Làm sao chọn K?

### Phương pháp Elbow (Khuỷu tay)

1. Chạy K-means với nhiều giá trị K (1, 2, 3, ..., 10)
2. Với mỗi K, tính tổng bình phương khoảng cách trong cụm (SSE)
3. Vẽ đồ thị K vs SSE
4. Chọn K tại điểm "khuỷu tay" (nơi SSE giảm chậm lại)

```
SSE
 |
 |  *
 |    *
 |      *
 |        *----*----*----*----*
 |
 +--------------------------------- K
     1  2  3  4  5  6  7  8  9
              ↑
         Điểm khuỷu tay
         Chọn K = 4
```

---

# 9. CÂU HỎI THƯỜNG GẶP

## Q1: K-means có luôn cho kết quả giống nhau không?
**Trả lời:** KHÔNG. Vì tâm ban đầu được chọn ngẫu nhiên, mỗi lần chạy có thể cho kết quả khác nhau. Để có kết quả ổn định, nên:
- Chạy nhiều lần và chọn kết quả tốt nhất
- Sử dụng K-means++ để khởi tạo tốt hơn

## Q2: Làm sao biết K-means đã hội tụ?
**Trả lời:** Khi một trong các điều kiện sau thỏa mãn:
- Tâm cụm không thay đổi
- Không có điểm nào đổi cụm
- Đạt số vòng lặp tối đa

## Q3: K-means có thể phân cụm với dữ liệu có chiều cao không?
**Trả lời:** CÓ. K-means hoạt động với dữ liệu bất kỳ chiều nào. Chỉ cần sử dụng công thức khoảng cách Euclidean n chiều.

## Q4: Tại sao gọi là "means"?
**Trả lời:** Vì tâm cụm được tính bằng **giá trị trung bình (mean)** của các điểm trong cụm.

## Q5: K-means khác gì với K-medoids?
**Trả lời:**
- **K-means:** Tâm là điểm trung bình (có thể không phải điểm trong dữ liệu)
- **K-medoids:** Tâm phải là một điểm trong dữ liệu

---

# 10. TỔNG KẾT

## 10.1. Những điều cần nhớ

1. **K-means là thuật toán phân cụm** thuộc học không giám sát

2. **4 bước cơ bản:**
   - Chọn K tâm ban đầu
   - Gán điểm vào cụm gần nhất
   - Tính lại tâm cụm
   - Lặp lại đến khi hội tụ

3. **2 công thức quan trọng:**
   - Khoảng cách: d = √[(x₂-x₁)² + (y₂-y₁)²]
   - Tâm cụm: C = (Σxᵢ/n, Σyᵢ/n)

4. **Ưu điểm:** Đơn giản, nhanh, hiệu quả

5. **Nhược điểm:** Phải chọn K, nhạy với tâm ban đầu

## 10.2. Mẹo làm bài thi

1. **Vẽ hình** trước khi tính toán để có cái nhìn trực quan

2. **Lập bảng** khoảng cách để tránh nhầm lẫn

3. **Kiểm tra lại** phép tính căn bậc 2

4. **Nhớ công thức** tâm cụm là TRUNG BÌNH, không phải tổng

5. **Ghi rõ** kết quả phân cụm sau mỗi vòng lặp

---

## 10.3. Bài tập tự luyện

**Bài 1:** Cho 5 điểm: A(1,1), B(2,2), C(8,8), D(9,9), E(10,10). Phân cụm với K=2, tâm ban đầu C₁=A, C₂=C.

**Bài 2:** Cho 4 điểm: (0,0), (1,0), (0,1), (10,10). K=2. Xác định kết quả phân cụm cuối cùng.

**Bài 3:** Giải thích tại sao K-means nhạy với điểm ngoại lệ (outlier)?

---

*Hết phần K-means - Phương án 1: Giải thích đơn giản*
