# PHẦN 3: THUẬT TOÁN GIẢI BÀI TOÁN TSP
# (Brute Force, Nearest Neighbor, Genetic Algorithm)

---

## 📚 MỤC LỤC

1. [Tổng quan các phương pháp](#1-tổng-quan-các-phương-pháp)
2. [Thuật toán 1: Brute Force (Vét cạn)](#2-thuật-toán-1-brute-force-vét-cạn)
3. [Thuật toán 2: Nearest Neighbor (Hàng xóm gần nhất)](#3-thuật-toán-2-nearest-neighbor-hàng-xóm-gần-nhất)
4. [Thuật toán 3: Genetic Algorithm (Giải thuật di truyền)](#4-thuật-toán-3-genetic-algorithm-giải-thuật-di-truyền)
5. [So sánh các thuật toán](#5-so-sánh-các-thuật-toán)

---

# 1. TỔNG QUAN CÁC PHƯƠNG PHÁP

## 1.1. Phân loại thuật toán giải TSP

| Loại | Đặc điểm | Ưu điểm | Nhược điểm |
|:---|:---|:---|:---|
| **Exact (Chính xác)** | Tìm nghiệm tối ưu toàn cục | Đảm bảo kết quả tốt nhất | Chỉ dùng được với n nhỏ |
| **Heuristic** | Sử dụng chiến lược tham lam | Nhanh, đơn giản | Không đảm bảo tối ưu |
| **Metaheuristic** | Kết hợp tìm kiếm địa phương + ngẫu nhiên | Cân bằng chất lượng/thời gian | Cần tinh chỉnh tham số |

## 1.2. Ba thuật toán được triển khai

| STT | Thuật toán | Loại | Độ phức tạp | Kích thước phù hợp |
|:---:|:---|:---:|:---:|:---:|
| 1 | **Brute Force** | Exact | O(n!) | n ≤ 12 |
| 2 | **Nearest Neighbor** | Heuristic | O(n²) | n ≤ 10,000 |
| 3 | **Genetic Algorithm** | Metaheuristic | O(g × p × n) | n ≤ 1,000 |

---

# 2. THUẬT TOÁN 1: BRUTE FORCE (VÉT CẠN)

## 2.1. Ý tưởng thuật toán

### 📌 Dễ hiểu (Ẩn dụ)

Bạn có 5 ngôi nhà cần ghé thăm. Thay vì đoán xem nên đi theo thứ tự nào, bạn **liệt kê TẤT CẢ** các cách đi có thể, tính quãng đường cho từng cách, rồi chọn cách **ngắn nhất**.

### 📌 Học thuật

> **Brute Force** duyệt qua **tất cả hoán vị** có thể của các thành phố, tính tổng chi phí cho mỗi hoán vị, và chọn hoán vị có chi phí nhỏ nhất.

**Số hoán vị cần xét:**
- TSP đối xứng: $(n-1)! / 2$
- TSP bất đối xứng: $(n-1)!$

---

## 2.2. Pseudocode

```
ALGORITHM Brute_Force_TSP:

INPUT:
    - n: số thành phố
    - D[n][n]: ma trận khoảng cách

OUTPUT:
    - best_tour: hành trình tối ưu
    - best_cost: chi phí tối thiểu

STEPS:
    1. best_cost = ∞
    2. best_tour = null
    
    3. FOR each permutation P of (1, 2, ..., n-1):
        a. tour = [0] + P + [0]  // Thêm điểm xuất phát
        b. cost = calculate_tour_cost(tour, D)
        c. IF cost < best_cost:
            best_cost = cost
            best_tour = tour
    
    4. RETURN best_tour, best_cost
```

---

## 2.3. Code Python

```python
from itertools import permutations

def brute_force_tsp(D):
    """
    Giải TSP bằng phương pháp vét cạn
    
    Args:
        D: Ma trận khoảng cách n x n
    
    Returns:
        best_tour: Hành trình tối ưu
        best_cost: Chi phí tối thiểu
    """
    n = len(D)
    cities = list(range(1, n))  # Không xét thành phố 0 (điểm xuất phát)
    
    best_tour = None
    best_cost = float('inf')
    
    # Duyệt tất cả hoán vị
    for perm in permutations(cities):
        # Tạo tour: 0 -> ... -> 0
        tour = [0] + list(perm) + [0]
        
        # Tính chi phí
        cost = 0
        for i in range(len(tour) - 1):
            cost += D[tour[i]][tour[i + 1]]
        
        # Cập nhật best
        if cost < best_cost:
            best_cost = cost
            best_tour = tour
    
    return best_tour, best_cost
```

---

## 2.4. Ví dụ minh họa

**Input:** 4 thành phố (0, 1, 2, 3)

**Ma trận khoảng cách:**
```
     0    1    2    3
 0   0   10   15   20
 1  10    0   35   25
 2  15   35    0   30
 3  20   25   30    0
```

**Quá trình duyệt:**

| STT | Hoán vị | Tour đầy đủ | Chi phí |
|:---:|:---|:---|:---:|
| 1 | (1, 2, 3) | 0→1→2→3→0 | 10+35+30+20 = 95 |
| 2 | (1, 3, 2) | 0→1→3→2→0 | 10+25+30+15 = **80** ✓ |
| 3 | (2, 1, 3) | 0→2→1→3→0 | 15+35+25+20 = 95 |
| 4 | (2, 3, 1) | 0→2→3→1→0 | 15+30+25+10 = **80** ✓ |
| 5 | (3, 1, 2) | 0→3→1→2→0 | 20+25+35+15 = 95 |
| 6 | (3, 2, 1) | 0→3→2→1→0 | 20+30+35+10 = 95 |

**Kết quả:** Tour tối ưu = 0→1→3→2→0, Chi phí = **80**

---

## 2.5. Phân tích độ phức tạp

| Yếu tố | Phân tích |
|:---|:---|
| **Thời gian** | O(n!) - Duyệt tất cả hoán vị |
| **Bộ nhớ** | O(n) - Lưu 1 tour tại mỗi thời điểm |
| **Đảm bảo tối ưu** | 100% |

**Giới hạn thực tế:**
| n | Số hoán vị | Thời gian (1M/s) |
|:---:|:---:|:---|
| 10 | 181,440 | 0.18 giây |
| 12 | 19,958,400 | 20 giây |
| 15 | 43 tỷ | **12 giờ** |

> [!WARNING]
> **Kết luận:** Brute Force chỉ dùng được với **n ≤ 12 thành phố**!

---

# 3. THUẬT TOÁN 2: NEAREST NEIGHBOR (HÀNG XÓM GẦN NHẤT)

## 3.1. Ý tưởng thuật toán

### 📌 Dễ hiểu (Ẩn dụ)

Bạn đang ở một thành phố và cần ghé thăm nhiều nơi. Chiến lược đơn giản: **Luôn đi đến nơi GẦN NHẤT mà chưa đến!**

### 📌 Học thuật

> **Nearest Neighbor** là thuật toán **tham lam (greedy)**, tại mỗi bước chọn thành phố chưa thăm có khoảng cách ngắn nhất đến vị trí hiện tại.

---

## 3.2. Pseudocode

```
ALGORITHM Nearest_Neighbor_TSP:

INPUT:
    - n: số thành phố
    - D[n][n]: ma trận khoảng cách
    - start: thành phố xuất phát (mặc định = 0)

OUTPUT:
    - tour: hành trình tìm được
    - cost: tổng chi phí

STEPS:
    1. tour = [start]
    2. visited = {start}
    3. current = start
    4. cost = 0
    
    5. WHILE len(visited) < n:
        a. Find nearest unvisited city:
           next_city = argmin{D[current][j] : j not in visited}
        b. tour.append(next_city)
        c. cost += D[current][next_city]
        d. visited.add(next_city)
        e. current = next_city
    
    6. // Quay về điểm xuất phát
       tour.append(start)
       cost += D[current][start]
    
    7. RETURN tour, cost
```

---

## 3.3. Code Python

```python
def nearest_neighbor_tsp(D, start=0):
    """
    Giải TSP bằng thuật toán Nearest Neighbor
    
    Args:
        D: Ma trận khoảng cách n x n
        start: Thành phố xuất phát (mặc định = 0)
    
    Returns:
        tour: Hành trình tìm được
        cost: Tổng chi phí
    """
    n = len(D)
    visited = set([start])
    tour = [start]
    cost = 0
    current = start
    
    while len(visited) < n:
        # Tìm thành phố gần nhất chưa thăm
        nearest = None
        min_dist = float('inf')
        
        for j in range(n):
            if j not in visited and D[current][j] < min_dist:
                min_dist = D[current][j]
                nearest = j
        
        # Di chuyển đến thành phố gần nhất
        tour.append(nearest)
        cost += min_dist
        visited.add(nearest)
        current = nearest
    
    # Quay về điểm xuất phát
    tour.append(start)
    cost += D[current][start]
    
    return tour, cost
```

---

## 3.4. Ví dụ minh họa

**Input:** 5 thành phố với ma trận khoảng cách:
```
     0    1    2    3    4
 0   0    5    6    3    4
 1   5    0    5    4    3
 2   6    5    0    3    7
 3   3    4    3    0    5
 4   4    3    7    5    0
```

**Quá trình thực hiện (xuất phát từ 0):**

| Bước | Vị trí | Chưa thăm | Khoảng cách | Chọn | Chi phí tích lũy |
|:---:|:---:|:---|:---|:---:|:---:|
| 1 | 0 | {1,2,3,4} | 5,6,**3**,4 | 3 | 3 |
| 2 | 3 | {1,2,4} | 4,**3**,5 | 2 | 3+3=6 |
| 3 | 2 | {1,4} | **5**,7 | 1 | 6+5=11 |
| 4 | 1 | {4} | **3** | 4 | 11+3=14 |
| 5 | 4 | {} | Về 0: 4 | 0 | 14+4=**18** |

**Kết quả:** Tour = 0→3→2→1→4→0, Chi phí = **18**

---

## 3.5. Cải tiến: Chạy từ nhiều điểm xuất phát

```python
def nearest_neighbor_best(D):
    """Chạy NN từ tất cả các điểm xuất phát, chọn kết quả tốt nhất"""
    n = len(D)
    best_tour = None
    best_cost = float('inf')
    
    for start in range(n):
        tour, cost = nearest_neighbor_tsp(D, start)
        if cost < best_cost:
            best_cost = cost
            best_tour = tour
    
    return best_tour, best_cost
```

---

## 3.6. Phân tích độ phức tạp

| Yếu tố | Phân tích |
|:---|:---|
| **Thời gian** | O(n²) - Mỗi bước tìm min trong n phần tử, lặp n bước |
| **Bộ nhớ** | O(n) - Lưu visited set và tour |
| **Đảm bảo tối ưu** | **KHÔNG** - Có thể sai 20-25% so với nghiệm tối ưu |

> [!TIP]
> **Kết luận:** Nearest Neighbor **rất nhanh** và cho kết quả **chấp nhận được** cho bài toán lớn.

---

# 4. THUẬT TOÁN 3: GENETIC ALGORITHM (GIẢI THUẬT DI TRUYỀN)

## 4.1. Ý tưởng thuật toán

### 📌 Dễ hiểu (Ẩn dụ)

Hãy tưởng tượng bạn đang **lai tạo giống** để tìm ra con vật tốt nhất:
1. **Quần thể ban đầu:** Có nhiều con vật khác nhau (nhiều tour khác nhau)
2. **Chọn lọc:** Giữ lại những con khỏe mạnh nhất (tour ngắn nhất)
3. **Lai ghép:** Cho 2 con phối giống để tạo con mới (kết hợp 2 tour)
4. **Đột biến:** Đôi khi có con bị đột biến (thay đổi ngẫu nhiên trong tour)
5. **Lặp lại:** Qua nhiều thế hệ, dần dần được con vật tốt nhất!

### 📌 Học thuật

> **Genetic Algorithm (GA)** là thuật toán tối ưu hóa dựa trên nguyên lý **tiến hóa tự nhiên**, bao gồm: Selection, Crossover, và Mutation.

---

## 4.2. Các thành phần của GA

### 🧬 Biểu diễn cá thể (Chromosome)

Mỗi cá thể là một **hoán vị** các thành phố (không bao gồm điểm xuất phát).

**Ví dụ:** Với 5 thành phố (0-4), cá thể có thể là `[1, 3, 2, 4]`

Tour đầy đủ: 0 → 1 → 3 → 2 → 4 → 0

---

### 🎯 Hàm fitness

**Fitness = Nghịch đảo của chi phí tour**

$$fitness = \frac{1}{cost + 1}$$

Fitness cao hơn = Tour tốt hơn

---

### 🏆 Selection (Chọn lọc)

**Phương pháp Tournament Selection:**
1. Chọn ngẫu nhiên k cá thể từ quần thể
2. Chọn cá thể có fitness cao nhất

```python
def tournament_selection(population, fitnesses, k=3):
    """Chọn lọc bằng tournament"""
    selected = random.sample(range(len(population)), k)
    best = max(selected, key=lambda i: fitnesses[i])
    return population[best]
```

---

### ✂️ Crossover (Lai ghép)

**Phương pháp Order Crossover (OX):**
1. Chọn một đoạn từ parent 1
2. Điền các phần tử còn lại theo thứ tự từ parent 2

**Ví dụ:**
```
Parent 1: [1, 2, 3, 4, 5]
Parent 2: [3, 5, 4, 2, 1]
Đoạn chọn: vị trí 1-3 từ P1 → [2, 3, 4]
Child:    [5, 2, 3, 4, 1]  (điền 5, 1 từ P2)
```

```python
def order_crossover(p1, p2):
    """Order Crossover (OX)"""
    size = len(p1)
    start, end = sorted(random.sample(range(size), 2))
    
    # Lấy đoạn từ p1
    child = [None] * size
    child[start:end+1] = p1[start:end+1]
    
    # Điền từ p2
    p2_filtered = [x for x in p2 if x not in child]
    j = 0
    for i in range(size):
        if child[i] is None:
            child[i] = p2_filtered[j]
            j += 1
    
    return child
```

---

### 🔀 Mutation (Đột biến)

**Phương pháp Swap Mutation:**
Hoán đổi vị trí của 2 thành phố ngẫu nhiên.

```python
def swap_mutation(individual, mutation_rate=0.1):
    """Đột biến bằng hoán đổi"""
    if random.random() < mutation_rate:
        i, j = random.sample(range(len(individual)), 2)
        individual[i], individual[j] = individual[j], individual[i]
    return individual
```

---

## 4.3. Pseudocode

```
ALGORITHM Genetic_Algorithm_TSP:

INPUT:
    - n: số thành phố
    - D[n][n]: ma trận khoảng cách
    - pop_size: kích thước quần thể
    - generations: số thế hệ
    - mutation_rate: tỷ lệ đột biến

OUTPUT:
    - best_tour: hành trình tốt nhất
    - best_cost: chi phí tốt nhất

STEPS:
    1. // Khởi tạo quần thể ban đầu
       population = [random_permutation(1..n-1) for _ in range(pop_size)]
    
    2. FOR generation = 1 to generations:
        a. // Tính fitness
           fitnesses = [1 / (tour_cost(ind) + 1) for ind in population]
        
        b. // Tạo thế hệ mới
           new_population = []
           WHILE len(new_population) < pop_size:
               - parent1 = tournament_selection(population, fitnesses)
               - parent2 = tournament_selection(population, fitnesses)
               - child = order_crossover(parent1, parent2)
               - child = swap_mutation(child, mutation_rate)
               - new_population.append(child)
        
        c. population = new_population
    
    3. // Tìm cá thể tốt nhất
       best = min(population, key=tour_cost)
       best_tour = [0] + best + [0]
       best_cost = tour_cost(best)
    
    4. RETURN best_tour, best_cost
```

---

## 4.4. Code Python đầy đủ

```python
import random

def genetic_algorithm_tsp(D, pop_size=100, generations=500, mutation_rate=0.1):
    """
    Giải TSP bằng Genetic Algorithm
    
    Args:
        D: Ma trận khoảng cách n x n
        pop_size: Kích thước quần thể
        generations: Số thế hệ
        mutation_rate: Tỷ lệ đột biến
    
    Returns:
        best_tour: Hành trình tốt nhất
        best_cost: Chi phí tốt nhất
    """
    n = len(D)
    cities = list(range(1, n))  # Không bao gồm thành phố 0
    
    def tour_cost(individual):
        """Tính chi phí của một cá thể"""
        full_tour = [0] + individual + [0]
        cost = sum(D[full_tour[i]][full_tour[i+1]] for i in range(len(full_tour)-1))
        return cost
    
    def create_individual():
        """Tạo cá thể ngẫu nhiên"""
        ind = cities.copy()
        random.shuffle(ind)
        return ind
    
    def tournament_selection(pop, fitnesses, k=3):
        """Chọn lọc tournament"""
        selected = random.sample(range(len(pop)), k)
        best = max(selected, key=lambda i: fitnesses[i])
        return pop[best].copy()
    
    def order_crossover(p1, p2):
        """Order Crossover"""
        size = len(p1)
        start, end = sorted(random.sample(range(size), 2))
        child = [None] * size
        child[start:end+1] = p1[start:end+1]
        p2_filtered = [x for x in p2 if x not in child]
        j = 0
        for i in range(size):
            if child[i] is None:
                child[i] = p2_filtered[j]
                j += 1
        return child
    
    def mutate(individual):
        """Swap mutation"""
        if random.random() < mutation_rate:
            i, j = random.sample(range(len(individual)), 2)
            individual[i], individual[j] = individual[j], individual[i]
        return individual
    
    # Khởi tạo quần thể
    population = [create_individual() for _ in range(pop_size)]
    
    # Tiến hóa qua các thế hệ
    for gen in range(generations):
        # Tính fitness
        fitnesses = [1 / (tour_cost(ind) + 1) for ind in population]
        
        # Tạo thế hệ mới
        new_population = []
        while len(new_population) < pop_size:
            p1 = tournament_selection(population, fitnesses)
            p2 = tournament_selection(population, fitnesses)
            child = order_crossover(p1, p2)
            child = mutate(child)
            new_population.append(child)
        
        population = new_population
    
    # Tìm cá thể tốt nhất
    best_individual = min(population, key=tour_cost)
    best_tour = [0] + best_individual + [0]
    best_cost = tour_cost(best_individual)
    
    return best_tour, best_cost
```

---

## 4.5. Phân tích độ phức tạp

| Yếu tố | Phân tích |
|:---|:---|
| **Thời gian** | O(g × p × n) với g = generations, p = pop_size |
| **Bộ nhớ** | O(p × n) - Lưu các quần thể |
| **Đảm bảo tối ưu** | **KHÔNG** - Nhưng thường tìm được nghiệm gần tối ưu |

**Tham số quan trọng:**
| Tham số | Giá trị khuyến nghị | Ảnh hưởng |
|:---|:---:|:---|
| pop_size | 50-200 | Lớn → Đa dạng hơn, chậm hơn |
| generations | 100-1000 | Lớn → Kết quả tốt hơn, lâu hơn |
| mutation_rate | 0.01-0.1 | Lớn → Khám phá nhiều, có thể mất elite |

---

# 5. SO SÁNH CÁC THUẬT TOÁN

## 5.1. Bảng so sánh tổng hợp

| Tiêu chí | Brute Force | Nearest Neighbor | Genetic Algorithm |
|:---|:---:|:---:|:---:|
| **Loại** | Exact | Heuristic | Metaheuristic |
| **Độ phức tạp thời gian** | O(n!) | O(n²) | O(g×p×n) |
| **Đảm bảo tối ưu** | ✅ 100% | ❌ | ❌ |
| **Chất lượng nghiệm** | Tốt nhất | ~75-80% tối ưu | ~95-99% tối ưu |
| **Kích thước phù hợp** | n ≤ 12 | n ≤ 10,000 | n ≤ 1,000 |
| **Độ khó cài đặt** | Dễ | Dễ | Trung bình |

## 5.2. Khi nào dùng thuật toán nào?

| Trường hợp | Thuật toán phù hợp |
|:---|:---|
| n ≤ 12 và cần nghiệm chính xác | **Brute Force** |
| n lớn, cần kết quả nhanh, chấp nhận sai số | **Nearest Neighbor** |
| n vừa, cần cân bằng chất lượng và thời gian | **Genetic Algorithm** |
| Cần benchmark cho thuật toán mới | **Brute Force** (làm baseline) |

---

*Hết Phần 3 - Thuật toán giải bài toán TSP*
