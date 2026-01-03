# PHẦN 2: DỮ LIỆU THỰC NGHIỆM
# (Mô tả, Phân tích, Tiền xử lý và Biểu diễn dữ liệu)

---

## 📚 MỤC LỤC

1. [Nguồn dữ liệu](#1-nguồn-dữ-liệu)
2. [Mô tả bộ dữ liệu](#2-mô-tả-bộ-dữ-liệu)
3. [Các bước phân tích và tiền xử lý dữ liệu](#3-các-bước-phân-tích-và-tiền-xử-lý-dữ-liệu)
4. [Biểu diễn dữ liệu cho bài toán](#4-biểu-diễn-dữ-liệu-cho-bài-toán)

---

# 1. NGUỒN DỮ LIỆU

## 1.1. TSPLIB - Thư viện chuẩn quốc tế

### 📌 Giới thiệu

**TSPLIB** (Travelling Salesman Problem LIBrary) là bộ dữ liệu chuẩn được sử dụng rộng rãi trong nghiên cứu TSP.

**Website:** http://comopt.ifi.uni-heidelberg.de/software/TSPLIB95/

### 📌 Đặc điểm

| Đặc điểm | Mô tả |
|:---|:---|
| Số lượng bài toán | 100+ instances |
| Kích thước | 14 đến 85,900 thành phố |
| Định dạng | File `.tsp` chuẩn |
| Nghiệm tối ưu | Đã biết cho hầu hết bài toán |

### 📌 Các instance phổ biến

| Tên | Số thành phố | Nghiệm tối ưu | Ghi chú |
|:---|:---:|:---:|:---|
| `burma14` | 14 | 3,323 | Bản đồ Myanmar |
| `ulysses22` | 22 | 7,013 | Hải trình Odysseus |
| `berlin52` | 52 | 7,542 | Các địa điểm ở Berlin |
| `eil76` | 76 | 538 | Christofides instance |
| `kroA100` | 100 | 21,282 | Krolak instance |
| `pr1002` | 1,002 | 259,045 | Padberg/Rinaldi |

---

## 1.2. Dữ liệu tự sinh (Random Data)

### 📌 Phương pháp sinh dữ liệu

**Bước 1:** Chọn số lượng thành phố $n$

**Bước 2:** Sinh tọa độ $(x, y)$ ngẫu nhiên trong vùng $[0, 1000] \times [0, 1000]$

**Bước 3:** Tính ma trận khoảng cách Euclidean

**Ví dụ code Python:**
```python
import random
import math

def generate_random_cities(n, max_coord=1000):
    """Sinh n thành phố với tọa độ ngẫu nhiên"""
    cities = []
    for i in range(n):
        x = random.uniform(0, max_coord)
        y = random.uniform(0, max_coord)
        cities.append((x, y))
    return cities

def calculate_distance_matrix(cities):
    """Tính ma trận khoảng cách Euclidean"""
    n = len(cities)
    D = [[0] * n for _ in range(n)]
    for i in range(n):
        for j in range(n):
            if i != j:
                dx = cities[i][0] - cities[j][0]
                dy = cities[i][1] - cities[j][1]
                D[i][j] = math.sqrt(dx**2 + dy**2)
    return D
```

### 📌 Ưu nhược điểm

| Ưu điểm | Nhược điểm |
|:---|:---|
| Dễ tạo với kích thước tùy ý | Không có nghiệm tối ưu để so sánh |
| Kiểm soát được đặc điểm dữ liệu | Có thể tạo ra bài toán "dễ" hoặc "khó" bất thường |

---

# 2. MÔ TẢ BỘ DỮ LIỆU

## 2.1. Phân loại theo kích thước

| Loại | Số thành phố | Phương pháp giải phù hợp | Thời gian ước tính |
|:---|:---:|:---|:---:|
| **Nhỏ** | 5-15 | Brute Force | < 1 giây |
| **Vừa** | 16-50 | Dynamic Programming, Heuristic | 1 giây - 1 phút |
| **Lớn** | 51-500 | Metaheuristic | 1 - 30 phút |
| **Rất lớn** | 500+ | Advanced Metaheuristic | > 30 phút |

## 2.2. Bộ dữ liệu sử dụng trong báo cáo

### 📊 Bộ 1: Dữ liệu nhỏ (10 thành phố)

**Nguồn:** Tự sinh ngẫu nhiên

**Mục đích:** Kiểm chứng thuật toán, so sánh với Brute Force

| ID | Tên thành phố | X | Y |
|:---:|:---|:---:|:---:|
| 0 | Thành phố A | 60 | 200 |
| 1 | Thành phố B | 180 | 200 |
| 2 | Thành phố C | 80 | 180 |
| 3 | Thành phố D | 140 | 180 |
| 4 | Thành phố E | 20 | 160 |
| 5 | Thành phố F | 100 | 160 |
| 6 | Thành phố G | 200 | 160 |
| 7 | Thành phố H | 140 | 140 |
| 8 | Thành phố I | 40 | 120 |
| 9 | Thành phố J | 100 | 120 |

---

### 📊 Bộ 2: TSPLIB - berlin52

**Nguồn:** TSPLIB

**Mô tả:** 52 địa điểm tại thành phố Berlin, Đức

**Nghiệm tối ưu đã biết:** 7,542

---

### 📊 Bộ 3: TSPLIB - kroA100

**Nguồn:** TSPLIB

**Mô tả:** 100 thành phố (Krolak instance)

**Nghiệm tối ưu đã biết:** 21,282

---

# 3. CÁC BƯỚC PHÂN TÍCH VÀ TIỀN XỬ LÝ DỮ LIỆU

## 3.1. Quy trình tổng quan

```
┌───────────────────────────────────────────────────────────────┐
│              QUY TRÌNH TIỀN XỬ LÝ DỮ LIỆU TSP                │
├───────────────────────────────────────────────────────────────┤
│                                                               │
│   BƯỚC 1: Đọc dữ liệu đầu vào                                │
│                       ↓                                       │
│   BƯỚC 2: Kiểm tra và làm sạch dữ liệu                       │
│                       ↓                                       │
│   BƯỚC 3: Tính ma trận khoảng cách                           │
│                       ↓                                       │
│   BƯỚC 4: Chuẩn hóa dữ liệu (nếu cần)                        │
│                       ↓                                       │
│   BƯỚC 5: Xác nhận và lưu trữ                                │
│                                                               │
└───────────────────────────────────────────────────────────────┘
```

---

## 3.2. Chi tiết từng bước

### 📌 Bước 1: Đọc dữ liệu đầu vào

**Input có thể là:**
- File `.tsp` từ TSPLIB
- File `.csv` với các cột (ID, X, Y)
- File `.txt` với ma trận khoảng cách

**Ví dụ định dạng file TSPLIB (.tsp):**
```
NAME: example10
TYPE: TSP
COMMENT: 10 cities example
DIMENSION: 10
EDGE_WEIGHT_TYPE: EUC_2D
NODE_COORD_SECTION
1 60 200
2 180 200
3 80 180
4 140 180
5 20 160
6 100 160
7 200 160
8 140 140
9 40 120
10 100 120
EOF
```

**Code đọc file TSPLIB:**
```python
def read_tsplib(filename):
    """Đọc file TSPLIB và trả về danh sách tọa độ"""
    cities = []
    reading_coords = False
    
    with open(filename, 'r') as f:
        for line in f:
            line = line.strip()
            if line == 'NODE_COORD_SECTION':
                reading_coords = True
                continue
            if line == 'EOF':
                break
            if reading_coords:
                parts = line.split()
                x = float(parts[1])
                y = float(parts[2])
                cities.append((x, y))
    
    return cities
```

---

### 📌 Bước 2: Kiểm tra và làm sạch dữ liệu

**Các kiểm tra cần thực hiện:**

| STT | Kiểm tra | Xử lý nếu vi phạm |
|:---:|:---|:---|
| 1 | Số thành phố $\geq 2$ | Báo lỗi |
| 2 | Tọa độ là số hợp lệ | Loại bỏ dòng lỗi |
| 3 | Không có thành phố trùng lặp | Gộp các thành phố trùng |
| 4 | Tọa độ không âm (nếu cần) | Dịch chuyển về gốc tọa độ |

**Code kiểm tra:**
```python
def validate_cities(cities):
    """Kiểm tra tính hợp lệ của dữ liệu"""
    if len(cities) < 2:
        raise ValueError("Cần ít nhất 2 thành phố")
    
    # Kiểm tra trùng lặp
    unique_cities = list(set(cities))
    if len(unique_cities) < len(cities):
        print(f"Warning: Loại bỏ {len(cities) - len(unique_cities)} thành phố trùng")
        cities = unique_cities
    
    return cities
```

---

### 📌 Bước 3: Tính ma trận khoảng cách

**Công thức khoảng cách Euclidean:**
$$d_{ij} = \sqrt{(x_i - x_j)^2 + (y_i - y_j)^2}$$

**Tính chất ma trận:**
- **Đối xứng:** $D[i][j] = D[j][i]$
- **Đường chéo = 0:** $D[i][i] = 0$
- **Không âm:** $D[i][j] \geq 0$

**Code tính ma trận:**
```python
import math

def compute_distance_matrix(cities):
    """Tính ma trận khoảng cách Euclidean"""
    n = len(cities)
    D = [[0.0] * n for _ in range(n)]
    
    for i in range(n):
        for j in range(i + 1, n):
            dx = cities[i][0] - cities[j][0]
            dy = cities[i][1] - cities[j][1]
            dist = math.sqrt(dx * dx + dy * dy)
            D[i][j] = dist
            D[j][i] = dist  # Đối xứng
    
    return D
```

---

### 📌 Bước 4: Chuẩn hóa dữ liệu (nếu cần)

**Các phương pháp chuẩn hóa:**

| Phương pháp | Mô tả | Khi nào dùng |
|:---|:---|:---|
| **Làm tròn** | Chuyển khoảng cách về số nguyên | Tăng tốc tính toán |
| **Scale** | Chia tọa độ cho max | Đồng nhất đơn vị |
| **Normalize** | Đưa về [0, 1] | So sánh các bộ dữ liệu |

**Code làm tròn khoảng cách:**
```python
def round_distances(D):
    """Làm tròn ma trận khoảng cách về số nguyên"""
    n = len(D)
    for i in range(n):
        for j in range(n):
            D[i][j] = round(D[i][j])
    return D
```

---

### 📌 Bước 5: Xác nhận và lưu trữ

**Kiểm tra cuối cùng:**
- Ma trận đối xứng
- Đường chéo = 0
- Không có giá trị âm

**Lưu trữ kết quả:**
- Lưu ma trận vào file `.csv` hoặc `.npy`
- Lưu metadata (số thành phố, nguồn dữ liệu, ngày xử lý)

---

# 4. BIỂU DIỄN DỮ LIỆU CHO BÀI TOÁN

## 4.1. Các cách biểu diễn

### 📊 Biểu diễn 1: Danh sách tọa độ

**Cấu trúc:** Mảng các tuple $(x, y)$

**Ví dụ:**
```python
cities = [
    (60, 200),   # Thành phố 0
    (180, 200),  # Thành phố 1
    (80, 180),   # Thành phố 2
    ...
]
```

**Ưu điểm:** Gọn nhẹ, dễ visualize

**Nhược điểm:** Cần tính khoảng cách mỗi lần dùng

---

### 📊 Biểu diễn 2: Ma trận khoảng cách

**Cấu trúc:** Ma trận 2D $n \times n$

**Ví dụ (5 thành phố):**
```
        0       1       2       3       4
    ┌───────────────────────────────────────┐
  0 │   0      10      15      20      25   │
  1 │  10       0      35      25      30   │
  2 │  15      35       0      30      20   │
  3 │  20      25      30       0      15   │
  4 │  25      30      20      15       0   │
    └───────────────────────────────────────┘
```

**Ưu điểm:** Truy xuất O(1), phù hợp tính tổng tour

**Nhược điểm:** Tốn bộ nhớ O(n²)

---

### 📊 Biểu diễn 3: Đồ thị có trọng số

**Cấu trúc:** $G = (V, E, W)$
- $V$: Tập đỉnh (các thành phố)
- $E$: Tập cạnh (đường nối)
- $W$: Trọng số cạnh (khoảng cách)

**Ưu điểm:** Linh hoạt, dễ áp dụng thuật toán đồ thị

**Nhược điểm:** Cài đặt phức tạp hơn

---

### 📊 Biểu diễn 4: Tour (Lời giải)

**Cấu trúc:** Mảng hoán vị các thành phố

**Ví dụ:**
```python
tour = [0, 2, 4, 1, 3, 0]  # Xuất phát từ 0, về lại 0
```

**Tính tổng chi phí:**
```python
def calculate_tour_cost(tour, D):
    """Tính tổng chi phí của một tour"""
    cost = 0
    for i in range(len(tour) - 1):
        cost += D[tour[i]][tour[i + 1]]
    return cost
```

---

## 4.2. Bảng so sánh các biểu diễn

| Biểu diễn | Bộ nhớ | Truy xuất khoảng cách | Phù hợp cho |
|:---|:---:|:---:|:---|
| Tọa độ | O(n) | O(1) tính | Visualize, sinh dữ liệu |
| Ma trận | O(n²) | O(1) | Tính tour, thuật toán |
| Đồ thị | O(n²) | O(1) | TSP biến thể |
| Tour | O(n) | - | Lưu lời giải |

---

## 4.3. Ví dụ minh họa hoàn chỉnh

**Input:** 5 thành phố với tọa độ

| ID | X | Y |
|:---:|:---:|:---:|
| 0 | 0 | 0 |
| 1 | 3 | 4 |
| 2 | 6 | 0 |
| 3 | 3 | 0 |
| 4 | 0 | 4 |

**Ma trận khoảng cách (làm tròn):**
```
        0     1     2     3     4
    ┌─────────────────────────────┐
  0 │   0     5     6     3     4 │
  1 │   5     0     5     4     3 │
  2 │   6     5     0     3     7 │
  3 │   3     4     3     0     5 │
  4 │   4     3     7     5     0 │
    └─────────────────────────────┘
```

**Tour tối ưu:** [0, 3, 2, 1, 4, 0]

**Chi phí:** 3 + 3 + 5 + 3 + 4 = **18**

---

*Hết Phần 2 - Dữ liệu thực nghiệm*
