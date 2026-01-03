# PHẦN 1: GIỚI THIỆU BÀI TOÁN TSP
# (Travelling Salesman Problem - Bài toán Người bán hàng)

---

## 📚 MỤC LỤC

1. [Định nghĩa bài toán](#1-định-nghĩa-bài-toán)
2. [Lịch sử hình thành](#2-lịch-sử-hình-thành)
3. [Ý nghĩa thực tế của bài toán](#3-ý-nghĩa-thực-tế-của-bài-toán)
4. [Lý do lựa chọn bài toán](#4-lý-do-lựa-chọn-bài-toán)

---

# 1. ĐỊNH NGHĨA BÀI TOÁN

## 1.1. Phát biểu bài toán

### 📌 Dễ hiểu (Ẩn dụ đời thường)

Hãy tưởng tượng bạn là một **người giao hàng**. Sáng nay bạn có 10 đơn hàng cần giao đến 10 địa chỉ khác nhau trong thành phố. Bạn xuất phát từ kho, giao đến tất cả 10 địa chỉ, rồi quay về kho.

**Câu hỏi:** Bạn nên đi theo thứ tự nào để **tổng quãng đường ngắn nhất**?

---

### 📌 Học thuật (Định nghĩa chính thức)

> **Bài toán Người bán hàng (TSP):** Cho một tập hợp $n$ thành phố và khoảng cách giữa từng cặp thành phố, tìm **hành trình ngắn nhất** đi qua tất cả các thành phố đúng một lần và quay về điểm xuất phát.

**Đầu vào:**
- Số lượng thành phố: $n$
- Ma trận khoảng cách: $D[i][j]$ = khoảng cách từ thành phố $i$ đến thành phố $j$

**Đầu ra:**
- Một **hoán vị** $(p_1, p_2, ..., p_n)$ sao cho tổng chi phí tối thiểu:
$$\text{minimize } \sum_{i=1}^{n-1} D[p_i][p_{i+1}] + D[p_n][p_1]$$

**Ràng buộc:**
- Mỗi thành phố được thăm **đúng một lần** (trừ điểm xuất phát)
- Phải **quay về** điểm xuất phát

---

## 1.2. Phân loại bài toán TSP

| Loại | Đặc điểm | Ví dụ |
|:---|:---|:---|
| **Symmetric TSP** | $D[i][j] = D[j][i]$ | Đường hai chiều |
| **Asymmetric TSP** | $D[i][j] \neq D[j][i]$ | Đường một chiều |
| **Metric TSP** | Thỏa mãn bất đẳng thức tam giác | Khoảng cách Euclidean |
| **Euclidean TSP** | Tọa độ trên mặt phẳng 2D | Bản đồ thực tế |

---

## 1.3. Ví dụ minh họa

**Bài toán:** 4 thành phố A, B, C, D với ma trận khoảng cách:

```
       A    B    C    D
   A   0   10   15   20
   B  10    0   35   25
   C  15   35    0   30
   D  20   25   30    0
```

**Các hành trình có thể:**
| STT | Hành trình | Tổng khoảng cách |
|:---:|:---|:---:|
| 1 | A → B → C → D → A | 10 + 35 + 30 + 20 = **95** |
| 2 | A → B → D → C → A | 10 + 25 + 30 + 15 = **80** |
| 3 | A → C → B → D → A | 15 + 35 + 25 + 20 = **95** |
| 4 | A → C → D → B → A | 15 + 30 + 25 + 10 = **80** |
| 5 | A → D → B → C → A | 20 + 25 + 35 + 15 = **95** |
| 6 | A → D → C → B → A | 20 + 30 + 35 + 10 = **95** |

**Kết quả tối ưu:** A → B → D → C → A hoặc A → C → D → B → A với **chi phí = 80**

---

# 2. LỊCH SỬ HÌNH THÀNH

## 2.1. Nguồn gốc bài toán

| Năm | Sự kiện |
|:---:|:---|
| **1930s** | Bài toán được nghiên cứu đầu tiên bởi nhà toán học Karl Menger tại Vienna |
| **1954** | Dantzig, Fulkerson và Johnson giải được TSP với 49 thành phố |
| **1972** | Richard Karp chứng minh TSP thuộc lớp **NP-hard** |
| **1988** | Giải được TSP với 2,392 thành phố (TSPLIB) |
| **2004** | Giải được TSP với 24,978 thành phố (Sweden tour) |
| **Hiện tại** | Nghiên cứu các thuật toán xấp xỉ và metaheuristic |

## 2.2. Độ phức tạp tính toán

> **TSP là bài toán NP-hard**

**Điều này có nghĩa gì?**
- Không tồn tại thuật toán **đa thức** để giải chính xác (chưa ai chứng minh được)
- Số lượng hoán vị có thể: $(n-1)!/2$ (với TSP đối xứng)

**Ví dụ về sự bùng nổ tổ hợp:**
| n (số thành phố) | Số hoán vị | Thời gian (1 triệu/giây) |
|:---:|:---:|:---|
| 5 | 12 | 0.000012 giây |
| 10 | 181,440 | 0.18 giây |
| 15 | 43 tỷ | 12 giờ |
| 20 | $6 \times 10^{16}$ | **1.9 triệu năm** |
| 25 | $3 \times 10^{23}$ | Tuổi vũ trụ! |

> [!WARNING]
> **Với n = 20 thành phố**, brute-force cần **1.9 triệu năm** để kiểm tra hết!

---

# 3. Ý NGHĨA THỰC TẾ CỦA BÀI TOÁN

## 3.1. Ứng dụng trong Logistics & Vận tải

### 🚚 Tối ưu hóa giao hàng

**Ví dụ:** Công ty Shopee với 50 đơn hàng/ngày tại TP.HCM.

**Bài toán:** Tìm lộ trình tối ưu cho shipper đi qua 50 điểm giao hàng.

**Lợi ích khi giải TSP:**
- ⬇️ Giảm 20-30% quãng đường
- ⬇️ Giảm chi phí xăng dầu
- ⬆️ Tăng số đơn xử lý/ngày

### 🚌 Lộ trình xe buýt trường học

**Ví dụ:** Xe buýt đón 30 học sinh từ 30 địa chỉ khác nhau.

**Mục tiêu:** Đón đủ học sinh với thời gian ngắn nhất.

---

## 3.2. Ứng dụng trong Sản xuất

### 🤖 Lập lịch Robot công nghiệp

**Ví dụ:** Robot hàn trong nhà máy ô tô cần hàn 100 điểm trên khung xe.

**Bài toán TSP:** Tìm thứ tự hàn để tổng quãng đường di chuyển của cánh tay robot là ngắn nhất.

### 🔩 Khoan lỗ trên bo mạch (PCB)

**Ví dụ:** Máy CNC khoan 500 lỗ trên bo mạch in.

**Lợi ích:** Giảm thời gian sản xuất, tăng năng suất.

---

## 3.3. Ứng dụng trong Công nghệ

### 🧬 Giải mã trình tự DNA

**Ví dụ:** Sắp xếp các đoạn DNA ngắn thành chuỗi hoàn chỉnh.

**Cách áp dụng:** Mỗi đoạn DNA là 1 "thành phố", khoảng cách là độ tương đồng giữa các đoạn.

### 📡 Định tuyến mạng

**Ví dụ:** Gói tin cần đi qua nhiều node mạng với độ trễ tối thiểu.

---

## 3.4. Ứng dụng trong Đời sống

### 🗺️ Lập kế hoạch du lịch

**Ví dụ:** Du khách muốn thăm 10 điểm du lịch tại Đà Nẵng trong 1 ngày.

**Mục tiêu:** Đi hết các điểm với thời gian di chuyển ít nhất.

### 🏥 Lịch trình bác sĩ thăm khám

**Ví dụ:** Bác sĩ cần khám cho 20 bệnh nhân ở 20 nơi khác nhau.

---

# 4. LÝ DO LỰA CHỌN BÀI TOÁN

## 4.1. Tính kinh điển

- TSP là một trong những bài toán **nổi tiếng nhất** trong Khoa học Máy tính
- Xuất hiện trong hầu hết các giáo trình về Thuật toán và Tối ưu hóa
- Là bài toán chuẩn để **benchmark** các thuật toán mới

## 4.2. Phù hợp để demo thuật toán

TSP cho phép so sánh nhiều **loại thuật toán** khác nhau:

| Loại thuật toán | Ví dụ | Đặc điểm |
|:---|:---|:---|
| **Exact** | Brute Force, Branch & Bound | Tìm nghiệm tối ưu |
| **Greedy** | Nearest Neighbor | Nhanh, đơn giản |
| **Metaheuristic** | Genetic Algorithm, Simulated Annealing | Cân bằng chất lượng/thời gian |

## 4.3. Nhiều ứng dụng thực tế

Như đã trình bày ở mục 3, TSP có **ứng dụng rộng rãi** trong:
- Logistics
- Sản xuất
- Công nghệ sinh học
- Đời sống hàng ngày

## 4.4. Tính thách thức

- Bài toán **NP-hard** → Không có thuật toán "hoàn hảo"
- Kích thước bài toán tăng → Độ khó tăng **theo cấp số mũ**
- Buộc phải sử dụng **thuật toán xấp xỉ** cho bài toán lớn

> [!IMPORTANT]
> **Kết luận:** TSP là bài toán lý tưởng để nghiên cứu vì nó vừa có **giá trị thực tiễn** cao, vừa có **độ khó phù hợp** để demo các chiến lược thuật toán khác nhau.

---

*Hết Phần 1 - Giới thiệu bài toán TSP*
