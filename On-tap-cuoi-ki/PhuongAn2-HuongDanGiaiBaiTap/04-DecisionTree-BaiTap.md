# 📚 HƯỚNG DẪN GIẢI BÀI TẬP: CÂY QUYẾT ĐỊNH (ID3)

## Phương án 2: Bài tập từng bước chi tiết - GIỐNG ĐỀ THI

---

> **⚠️ LƯU Ý QUAN TRỌNG:**
>
> Tài liệu này chứa **bài giải mẫu giống đề thi thực tế** với thuộc tính categorical (Engine, Type, Color...).
> Học theo cách giải này để đạt điểm cao!

---

# 📑 MỤC LỤC

1. [Tóm tắt công thức](#1-tóm-tắt-công-thức)
2. [Bảng tra log₂ (QUAN TRỌNG)](#2-bảng-tra-log)
3. [BÀI MẪU 1: Đề thi xe hơi (8 mẫu)](#3-bài-mẫu-1-đề-thi-xe-hơi)
4. [BÀI MẪU 2: Đề thi game (8 mẫu)](#4-bài-mẫu-2-đề-thi-game)
5. [Bài tập tự luyện](#5-bài-tập-tự-luyện)

---

# 1️⃣ TÓM TẮT CÔNG THỨC

## Entropy (Độ hỗn loạn)

$$Entropy(S) = -\sum_{i} p_i \times \log_2(p_i)$$

**Với 2 lớp (Yes/No):**
$$E(S) = -p_{Yes} \log_2(p_{Yes}) - p_{No} \log_2(p_{No})$$

## Information Gain

$$Gain(S, A) = E(S) - \sum_{v \in Values(A)} \frac{|S_v|}{|S|} \times E(S_v)$$

**Ý nghĩa:** Gain = Entropy trước - Entropy sau khi chia

---

# 2️⃣ BẢNG TRA LOG₂ (PHẢI THUỘC!)

## Bảng giá trị -p×log₂(p)

| Tỷ lệ |   p   | -p×log₂(p) |
| :---: | :---: | :--------: |
|  0/n  |   0   |   0.000    |
|  1/8  | 0.125 |   0.375    |
|  1/6  | 0.167 |   0.431    |
|  1/5  | 0.200 |   0.464    |
|  1/4  | 0.250 |   0.500    |
|  1/3  | 0.333 |   0.528    |
|  2/5  | 0.400 |   0.529    |
|  3/8  | 0.375 |   0.531    |
|  1/2  | 0.500 | **0.500**  |
|  5/8  | 0.625 |   0.424    |
|  3/5  | 0.600 |   0.442    |
|  2/3  | 0.667 |   0.390    |
|  3/4  | 0.750 |   0.311    |
|  4/5  | 0.800 |   0.258    |
|  5/6  | 0.833 |   0.222    |
|  7/8  | 0.875 |   0.169    |
|  n/n  | 1.000 |   0.000    |

## Bảng Entropy thường gặp

| Tỷ lệ Yes/No |  Entropy  |
| :----------: | :-------: |
| 8/0 hoặc 0/8 | **0.000** |
| 7/1 hoặc 1/7 |   0.544   |
| 6/2 hoặc 2/6 |   0.811   |
| 5/3 hoặc 3/5 |   0.971   |
|     4/4      | **1.000** |

---

# 3️⃣ BÀI MẪU 1: ĐỀ THI XE HƠI (Bài tập 1)

## 📝 ĐỀ BÀI

Xây dựng cây quyết định (ID3) cho bảng dữ liệu sau:

| ID  | Engine | Type  | Color  | 4WD |  Want?  |
| :-: | :----: | :---: | :----: | :-: | :-----: |
|  1  | 2000cc |  SUV  | Silver | Yes | **Yes** |
|  2  | 1000cc | Sedan | Silver | Yes | **Yes** |
|  3  | 2000cc | Sport |  Blue  | No  | **No**  |
|  4  | 1000cc |  SUV  |  Blue  | No  | **Yes** |
|  5  | 2000cc | Sedan | Silver | Yes | **No**  |
|  6  | 2000cc | Sport |  Blue  | Yes | **Yes** |
|  7  | 1000cc | Sedan |  Blue  | No  | **Yes** |
|  8  | 1000cc |  SUV  | Silver | No  | **Yes** |

---

## 🔷 GIẢI CHI TIẾT

### BƯỚC 1: Tính Entropy tập gốc S

**Đếm nhãn:**

- Yes: 6 mẫu (ID: 1, 2, 4, 6, 7, 8)
- No: 2 mẫu (ID: 3, 5)
- Tổng: 8 mẫu

**Tính Entropy:**

```
p(Yes) = 6/8 = 3/4 = 0.75
p(No) = 2/8 = 1/4 = 0.25

E(S) = -0.75×log₂(0.75) - 0.25×log₂(0.25)
     = 0.311 + 0.500     (tra bảng)
     = 0.811
```

✅ **Entropy(S) = 0.811**

---

### BƯỚC 2: Tính Gain cho thuộc tính "Engine"

**Chia theo Engine:**

| Engine | Yes | No  | Tổng |
| :----: | :-: | :-: | :--: |
| 2000cc |  2  |  2  |  4   |
| 1000cc |  4  |  0  |  4   |

**Tính Entropy từng nhánh:**

**Engine = 2000cc (2 Yes, 2 No):**

```
E(2000cc) = -0.5×log₂(0.5) - 0.5×log₂(0.5)
          = 0.5 + 0.5
          = 1.0
```

**Engine = 1000cc (4 Yes, 0 No):**

```
E(1000cc) = -1×log₂(1) - 0×log₂(0)
          = 0 + 0
          = 0  ← Thuần nhất!
```

**Tính Gain:**

```
Gain(S, Engine) = E(S) - [(4/8)×E(2000cc) + (4/8)×E(1000cc)]
                = 0.811 - [0.5×1.0 + 0.5×0]
                = 0.811 - 0.5
                = 0.311
```

✅ **Gain(Engine) = 0.311**

---

### BƯỚC 3: Tính Gain cho thuộc tính "Type"

**Chia theo Type:**

| Type  | Yes | No  | Tổng |
| :---: | :-: | :-: | :--: |
|  SUV  |  3  |  0  |  3   |
| Sedan |  2  |  1  |  3   |
| Sport |  1  |  1  |  2   |

**Tính Entropy từng nhánh:**

**Type = SUV (3 Yes, 0 No):**

```
E(SUV) = 0  ← Thuần nhất!
```

**Type = Sedan (2 Yes, 1 No):**

```
p(Yes) = 2/3, p(No) = 1/3
E(Sedan) = -0.667×log₂(0.667) - 0.333×log₂(0.333)
         = 0.390 + 0.528
         = 0.918
```

**Type = Sport (1 Yes, 1 No):**

```
E(Sport) = 1.0
```

**Tính Gain:**

```
Gain(S, Type) = 0.811 - [(3/8)×0 + (3/8)×0.918 + (2/8)×1.0]
              = 0.811 - [0 + 0.344 + 0.25]
              = 0.811 - 0.594
              = 0.217
```

✅ **Gain(Type) = 0.217**

---

### BƯỚC 4: Tính Gain cho thuộc tính "Color"

**Chia theo Color:**

| Color  | Yes | No  | Tổng |
| :----: | :-: | :-: | :--: |
| Silver |  3  |  1  |  4   |
|  Blue  |  3  |  1  |  4   |

**Tính Entropy từng nhánh:**

**Color = Silver (3 Yes, 1 No):**

```
p(Yes) = 3/4 = 0.75, p(No) = 1/4 = 0.25
E(Silver) = 0.311 + 0.500 = 0.811
```

**Color = Blue (3 Yes, 1 No):**

```
E(Blue) = 0.811  (giống Silver)
```

**Tính Gain:**

```
Gain(S, Color) = 0.811 - [(4/8)×0.811 + (4/8)×0.811]
               = 0.811 - 0.811
               = 0
```

✅ **Gain(Color) = 0** ← Thuộc tính vô dụng!

---

### BƯỚC 5: Tính Gain cho thuộc tính "4WD"

**Chia theo 4WD:**

| 4WD | Yes | No  | Tổng |
| :-: | :-: | :-: | :--: |
| Yes |  3  |  1  |  4   |
| No  |  3  |  1  |  4   |

**Tính Gain:**

```
Gain(S, 4WD) = 0.811 - [(4/8)×0.811 + (4/8)×0.811]
             = 0.811 - 0.811
             = 0
```

✅ **Gain(4WD) = 0** ← Thuộc tính vô dụng!

---

### BƯỚC 6: So sánh và chọn nút gốc

| Thuộc tính |       Gain       |
| :--------: | :--------------: |
| **Engine** | **0.311** ⭐ MAX |
|    Type    |      0.217       |
|   Color    |      0.000       |
|    4WD     |      0.000       |

✅ **Chọn "Engine" làm nút gốc!**

---

### BƯỚC 7: Xây dựng cây

```
                    ┌───────────────┐
                    │    ENGINE?    │
                    └───────┬───────┘
                            │
              ┌─────────────┴─────────────┐
              │                           │
          (2000cc)                    (1000cc)
          4 mẫu                       4 mẫu
          2Y/2N                       4Y/0N
              │                           │
              ▼                           ▼
        Tiếp tục chia              ┌─────────────┐
        (E = 1.0)                  │    YES      │
                                   │   (Leaf)    │
                                   └─────────────┘
```

**Với nhánh Engine = 2000cc (cần chia tiếp):**

Dữ liệu con: ID 1, 3, 5, 6 (2 Yes, 2 No)

| ID  | Type  | Color  | 4WD | Want? |
| :-: | :---: | :----: | :-: | :---: |
|  1  |  SUV  | Silver | Yes |  Yes  |
|  3  | Sport |  Blue  | No  |  No   |
|  5  | Sedan | Silver | Yes |  No   |
|  6  | Sport |  Blue  | Yes |  Yes  |

**Entropy tập con S' (2 Yes, 2 No):**
```
E(S') = 1.0  (vì 50-50)
```

---

#### Tính Gain(Type) cho nhánh 2000cc:

**Chia theo Type:**

| Type  | Yes | No  | Tổng |
| :---: | :-: | :-: | :--: |
|  SUV  |  1  |  0  |  1   |
| Sedan |  0  |  1  |  1   |
| Sport |  1  |  1  |  2   |

**Tính Entropy từng nhánh:**
```
E(SUV) = 0       ← Thuần nhất (1Y/0N)
E(Sedan) = 0     ← Thuần nhất (0Y/1N)
E(Sport) = 1.0   ← 50-50 (1Y/1N)
```

**Tính Gain:**
```
Gain(S', Type) = E(S') - [(1/4)×E(SUV) + (1/4)×E(Sedan) + (2/4)×E(Sport)]
               = 1.0 - [0.25×0 + 0.25×0 + 0.5×1.0]
               = 1.0 - 0.5
               = 0.5
```

✅ **Gain(Type) = 0.5**

---

#### Tính Gain(Color) cho nhánh 2000cc:

**Chia theo Color:**

| Color  | Yes | No  | Tổng |
| :----: | :-: | :-: | :--: |
| Silver |  1  |  1  |  2   |
|  Blue  |  1  |  1  |  2   |

**Tính Entropy:**
```
E(Silver) = 1.0 (50-50)
E(Blue) = 1.0 (50-50)
```

**Tính Gain:**
```
Gain(S', Color) = 1.0 - [(2/4)×1.0 + (2/4)×1.0]
                = 1.0 - 1.0
                = 0
```

✅ **Gain(Color) = 0** ← Vô dụng!

---

#### Tính Gain(4WD) cho nhánh 2000cc:

**Chia theo 4WD:**

| 4WD | Yes | No  | Tổng |
| :-: | :-: | :-: | :--: |
| Yes |  2  |  1  |  3   |
| No  |  0  |  1  |  1   |

**Tính Entropy:**
```
E(4WD=Yes) = -2/3×log₂(2/3) - 1/3×log₂(1/3) = 0.390 + 0.528 = 0.918
E(4WD=No) = 0  ← Thuần nhất (0Y/1N)
```

**Tính Gain:**
```
Gain(S', 4WD) = 1.0 - [(3/4)×0.918 + (1/4)×0]
              = 1.0 - 0.689
              = 0.311
```

✅ **Gain(4WD) = 0.311**

---

#### So sánh và chọn thuộc tính cho nhánh 2000cc:

| Thuộc tính |     Gain     |
| :--------: | :----------: |
|  **Type**  | **0.5** ⭐ MAX |
|   Color    |     0.0      |
|    4WD     |    0.311     |

✅ **Chọn "Type" làm nút tiếp theo cho nhánh 2000cc!**

---

#### Phân tích các nhánh của Type:

**Type = SUV (ID 1):** 1 Yes, 0 No → **Lá: YES**

**Type = Sedan (ID 5):** 0 Yes, 1 No → **Lá: NO**

**Type = Sport (ID 3, 6):** 1 Yes, 1 No → Cần chia tiếp!

---

#### Với nhánh Type = Sport (cần chia tiếp):

Dữ liệu con: ID 3, 6

| ID  | Color | 4WD | Want? |
| :-: | :---: | :-: | :---: |
|  3  | Blue  | No  |  No   |
|  6  | Blue  | Yes |  Yes  |

**Entropy:** E = 1.0 (50-50)

**Xét thuộc tính Color:** Cả 2 đều Blue → Không chia được

**Xét thuộc tính 4WD:**

| 4WD | Yes | No  | Tổng |
| :-: | :-: | :-: | :--: |
| Yes |  1  |  0  |  1   |
| No  |  0  |  1  |  1   |

```
E(4WD=Yes) = 0  ← Thuần nhất
E(4WD=No) = 0   ← Thuần nhất
Gain(4WD) = 1.0 - 0 = 1.0  ← Hoàn hảo!
```

✅ **Chọn 4WD:** 
- 4WD = Yes → **YES**
- 4WD = No → **NO**

**CÂY HOÀN CHỈNH:**

```
                         ┌───────────────┐
                         │    ENGINE?    │
                         └───────┬───────┘
                                 │
               ┌─────────────────┴─────────────────┐
               │                                   │
           (2000cc)                            (1000cc)
               │                                   │
               ▼                                   ▼
        ┌─────────────┐                     ┌─────────────┐
        │    TYPE?    │                     │    YES      │
        └──────┬──────┘                     └─────────────┘
               │
     ┌─────────┼─────────┐
     │         │         │
  (SUV)    (Sedan)   (Sport)
     │         │         │
     ▼         ▼         ▼
  ┌─────┐  ┌─────┐  ┌─────────┐
  │ YES │  │ NO  │  │  4WD?   │
  └─────┘  └─────┘  └────┬────┘
                         │
                    ┌────┴────┐
                    │         │
                  (Yes)     (No)
                    │         │
                    ▼         ▼
                 ┌─────┐  ┌─────┐
                 │ YES │  │ NO  │
                 └─────┘  └─────┘
```

---

# 4️⃣ BÀI MẪU 2: ĐỀ THI GAME (Đề 2)

## 📝 ĐỀ BÀI

Xây dựng cây quyết định cho bảng dữ liệu:

| ID  |  Xuất xứ   | Thể loại |  Đồ họa   | Hình thức trả phí | Chơi? |
| :-: | :--------: | :------: | :-------: | :---------------: | :---: |
|  1  | Trung Quốc |  MMORPG  |    Đẹp    |   Free to play    |  Yes  |
|  2  |   Âu/Mỹ    |   MOBA   |    Đẹp    |   Free to play    |  Yes  |
|  3  | Trung Quốc |  Sport   | Tương đối |    Pay to play    |  No   |
|  4  |   Âu/Mỹ    |  MMORPG  | Tương đối |    Pay to play    |  Yes  |
|  5  | Trung Quốc |   MOBA   |    Đẹp    |   Free to play    |  No   |
|  6  | Trung Quốc |  Sport   | Tương đối |   Free to play    |  Yes  |
|  7  |   Âu/Mỹ    |   MOBA   | Tương đối |    Pay to play    |  Yes  |
|  8  |   Âu/Mỹ    |  MMORPG  |    Đẹp    |    Pay to play    |  Yes  |

---

## 🔷 GIẢI CHI TIẾT

### BƯỚC 1: Tính Entropy tập gốc S

**Đếm nhãn:**

- Yes: 6 mẫu (ID: 1, 2, 4, 6, 7, 8)
- No: 2 mẫu (ID: 3, 5)
- Tổng: 8 mẫu

**Tính Entropy:**

```
p(Yes) = 6/8 = 3/4 = 0.75
p(No) = 2/8 = 1/4 = 0.25

E(S) = -0.75×log₂(0.75) - 0.25×log₂(0.25)
     = 0.311 + 0.500     (tra bảng)
     = 0.811
```

✅ **Entropy(S) = 0.811**

---

### BƯỚC 2: Tính Gain cho thuộc tính "Xuất xứ"

**Chia theo Xuất xứ:**

| Xuất xứ    | Yes | No  | Tổng |
| :--------: | :-: | :-: | :--: |
| Trung Quốc |  2  |  2  |  4   |
| Âu/Mỹ      |  4  |  0  |  4   |

**Tính Entropy từng nhánh:**

**Xuất xứ = Trung Quốc (2 Yes, 2 No):**

```
E(Trung Quốc) = -0.5×log₂(0.5) - 0.5×log₂(0.5)
              = 0.5 + 0.5
              = 1.0
```

**Xuất xứ = Âu/Mỹ (4 Yes, 0 No):**

```
E(Âu/Mỹ) = -1×log₂(1) - 0×log₂(0)
         = 0 + 0
         = 0  ← Thuần nhất!
```

**Tính Gain:**

```
Gain(S, Xuất xứ) = E(S) - [(4/8)×E(TQ) + (4/8)×E(ÂM)]
                 = 0.811 - [0.5×1.0 + 0.5×0]
                 = 0.811 - 0.5
                 = 0.311
```

✅ **Gain(Xuất xứ) = 0.311**

---

### BƯỚC 3: Tính Gain cho thuộc tính "Thể loại"

**Chia theo Thể loại:**

| Thể loại | Yes | No  | Tổng |
| :------: | :-: | :-: | :--: |
|  MMORPG  |  3  |  0  |  3   |
|   MOBA   |  2  |  1  |  3   |
|  Sport   |  1  |  1  |  2   |

**Tính Entropy từng nhánh:**

**Thể loại = MMORPG (3 Yes, 0 No):**

```
E(MMORPG) = 0  ← Thuần nhất!
```

**Thể loại = MOBA (2 Yes, 1 No):**

```
p(Yes) = 2/3, p(No) = 1/3
E(MOBA) = -0.667×log₂(0.667) - 0.333×log₂(0.333)
        = 0.390 + 0.528
        = 0.918
```

**Thể loại = Sport (1 Yes, 1 No):**

```
E(Sport) = 1.0
```

**Tính Gain:**

```
Gain(S, Thể loại) = 0.811 - [(3/8)×0 + (3/8)×0.918 + (2/8)×1.0]
                  = 0.811 - [0 + 0.344 + 0.25]
                  = 0.811 - 0.594
                  = 0.217
```

✅ **Gain(Thể loại) = 0.217**

---

### BƯỚC 4: Tính Gain cho thuộc tính "Đồ họa"

**Chia theo Đồ họa:**

| Đồ họa    | Yes | No  | Tổng |
| :-------: | :-: | :-: | :--: |
| Đẹp       |  3  |  1  |  4   |
| Tương đối |  3  |  1  |  4   |

**Tính Entropy từng nhánh:**

**Đồ họa = Đẹp (3 Yes, 1 No):**

```
p(Yes) = 3/4 = 0.75, p(No) = 1/4 = 0.25
E(Đẹp) = 0.311 + 0.500 = 0.811
```

**Đồ họa = Tương đối (3 Yes, 1 No):**

```
E(Tương đối) = 0.811  (giống Đẹp)
```

**Tính Gain:**

```
Gain(S, Đồ họa) = 0.811 - [(4/8)×0.811 + (4/8)×0.811]
                = 0.811 - 0.811
                = 0
```

✅ **Gain(Đồ họa) = 0** ← Thuộc tính vô dụng!

---

### BƯỚC 5: Tính Gain cho thuộc tính "Hình thức trả phí"

**Chia theo Trả phí:**

| Trả phí      | Yes | No  | Tổng |
| :----------: | :-: | :-: | :--: |
| Free to play |  3  |  1  |  4   |
| Pay to play  |  3  |  1  |  4   |

**Tính Entropy từng nhánh:**

```
E(Free to play) = 0.811 (3Y/1N)
E(Pay to play) = 0.811 (3Y/1N)
```

**Tính Gain:**

```
Gain(S, Trả phí) = 0.811 - [(4/8)×0.811 + (4/8)×0.811]
                 = 0.811 - 0.811
                 = 0
```

✅ **Gain(Trả phí) = 0** ← Thuộc tính vô dụng!

---

### BƯỚC 6: So sánh và chọn nút gốc

| Thuộc tính     |       Gain       |
| :------------: | :--------------: |
| **Xuất xứ**    | **0.311** ⭐ MAX |
| Thể loại       |      0.217       |
| Đồ họa         |      0.000       |
| Trả phí        |      0.000       |

✅ **Chọn "Xuất xứ" làm nút gốc!**

---

### BƯỚC 7: Xây dựng cây

```
                    ┌───────────────┐
                    │   XUẤT XỨ?    │
                    └───────┬───────┘
                            │
              ┌─────────────┴─────────────┐
              │                           │
        (Trung Quốc)                   (Âu/Mỹ)
          4 mẫu                         4 mẫu
          2Y/2N                         4Y/0N
              │                           │
              ▼                           ▼
        Tiếp tục chia              ┌─────────────┐
        (E = 1.0)                  │    YES      │
                                   │   (Leaf)    │
                                   └─────────────┘
```

---

### BƯỚC 8: Xử lý nhánh Xuất xứ = Trung Quốc

**Dữ liệu con:** ID 1, 3, 5, 6 (2 Yes, 2 No)

| ID  | Thể loại | Đồ họa    | Trả phí       | Chơi? |
| :-: | :------: | :-------: | :-----------: | :---: |
|  1  |  MMORPG  | Đẹp       | Free to play  |  Yes  |
|  3  |  Sport   | Tương đối | Pay to play   |  No   |
|  5  |   MOBA   | Đẹp       | Free to play  |  No   |
|  6  |  Sport   | Tương đối | Free to play  |  Yes  |

**Entropy tập con S' (2 Yes, 2 No):**
```
E(S') = 1.0  (vì 50-50)
```

---

#### Tính Gain(Thể loại) cho nhánh Trung Quốc:

**Chia theo Thể loại:**

| Thể loại | Yes | No  | Tổng |
| :------: | :-: | :-: | :--: |
|  MMORPG  |  1  |  0  |  1   |
|   MOBA   |  0  |  1  |  1   |
|  Sport   |  1  |  1  |  2   |

**Tính Entropy từng nhánh:**
```
E(MMORPG) = 0     ← Thuần nhất (1Y/0N)
E(MOBA) = 0       ← Thuần nhất (0Y/1N)
E(Sport) = 1.0    ← 50-50 (1Y/1N)
```

**Tính Gain:**
```
Gain(S', Thể loại) = E(S') - [(1/4)×E(MMORPG) + (1/4)×E(MOBA) + (2/4)×E(Sport)]
                   = 1.0 - [0.25×0 + 0.25×0 + 0.5×1.0]
                   = 1.0 - 0.5
                   = 0.5
```

✅ **Gain(Thể loại) = 0.5**

---

#### Tính Gain(Đồ họa) cho nhánh Trung Quốc:

**Chia theo Đồ họa:**

| Đồ họa    | Yes | No  | Tổng |
| :-------: | :-: | :-: | :--: |
| Đẹp       |  1  |  1  |  2   |
| Tương đối |  1  |  1  |  2   |

**Tính Entropy:**
```
E(Đẹp) = 1.0 (50-50)
E(Tương đối) = 1.0 (50-50)
```

**Tính Gain:**
```
Gain(S', Đồ họa) = 1.0 - [(2/4)×1.0 + (2/4)×1.0]
                 = 1.0 - 1.0
                 = 0
```

✅ **Gain(Đồ họa) = 0** ← Vô dụng!

---

#### Tính Gain(Trả phí) cho nhánh Trung Quốc:

**Chia theo Trả phí:**

| Trả phí      | Yes | No  | Tổng |
| :----------: | :-: | :-: | :--: |
| Free to play |  2  |  1  |  3   |
| Pay to play  |  0  |  1  |  1   |

**Tính Entropy:**
```
E(Free to play) = -2/3×log₂(2/3) - 1/3×log₂(1/3) = 0.390 + 0.528 = 0.918
E(Pay to play) = 0  ← Thuần nhất (0Y/1N)
```

**Tính Gain:**
```
Gain(S', Trả phí) = 1.0 - [(3/4)×0.918 + (1/4)×0]
                  = 1.0 - 0.689
                  = 0.311
```

✅ **Gain(Trả phí) = 0.311**

---

#### So sánh và chọn thuộc tính cho nhánh Trung Quốc:

| Thuộc tính     |     Gain        |
| :------------: | :-------------: |
| **Thể loại**   | **0.5** ⭐ MAX  |
| Đồ họa         |     0.0         |
| Trả phí        |    0.311        |

✅ **Chọn "Thể loại" làm nút tiếp theo!**

---

#### Phân tích các nhánh của Thể loại:

**Thể loại = MMORPG (ID 1):** 1 Yes, 0 No → **Lá: YES**

**Thể loại = MOBA (ID 5):** 0 Yes, 1 No → **Lá: NO**

**Thể loại = Sport (ID 3, 6):** 1 Yes, 1 No → Cần chia tiếp!

---

#### Với nhánh Thể loại = Sport (cần chia tiếp):

Dữ liệu con: ID 3, 6

| ID  | Đồ họa    | Trả phí      | Chơi? |
| :-: | :-------: | :----------: | :---: |
|  3  | Tương đối | Pay to play  |  No   |
|  6  | Tương đối | Free to play |  Yes  |

**Entropy:** E = 1.0 (50-50)

**Xét thuộc tính Đồ họa:** Cả 2 đều "Tương đối" → Không chia được

**Xét thuộc tính Trả phí:**

| Trả phí      | Yes | No  | Tổng |
| :----------: | :-: | :-: | :--: |
| Free to play |  1  |  0  |  1   |
| Pay to play  |  0  |  1  |  1   |

```
E(Free to play) = 0  ← Thuần nhất
E(Pay to play) = 0   ← Thuần nhất
Gain(Trả phí) = 1.0 - 0 = 1.0  ← Hoàn hảo!
```

✅ **Chọn Trả phí:** 
- Free to play → **YES**
- Pay to play → **NO**

---

### CÂY HOÀN CHỈNH - BÀI MẪU 2

```
                              ┌───────────────┐
                              │   XUẤT XỨ?    │
                              └───────┬───────┘
                                      │
                    ┌─────────────────┴─────────────────┐
                    │                                   │
              (Trung Quốc)                           (Âu/Mỹ)
                    │                                   │
                    ▼                                   ▼
             ┌─────────────┐                     ┌─────────────┐
             │  THỂ LOẠI?  │                     │    YES      │
             └──────┬──────┘                     └─────────────┘
                    │
          ┌─────────┼─────────┐
          │         │         │
      (MMORPG)   (MOBA)    (Sport)
          │         │         │
          ▼         ▼         ▼
       ┌─────┐  ┌─────┐  ┌───────────┐
       │ YES │  │ NO  │  │  TRẢ PHÍ? │
       └─────┘  └─────┘  └─────┬─────┘
                               │
                         ┌─────┴─────┐
                         │           │
                    (Free)      (Pay)
                         │           │
                         ▼           ▼
                      ┌─────┐   ┌─────┐
                      │ YES │   │ NO  │
                      └─────┘   └─────┘
```

---

### KIỂM TRA CÂY VỚI DỮ LIỆU BAN ĐẦU

| ID  | Xuất xứ    | Thể loại | Dự đoán theo cây | Thực tế | Đúng? |
| :-: | :--------: | :------: | :--------------: | :-----: | :---: |
|  1  | Trung Quốc |  MMORPG  |       YES        |   Yes   |  ✅   |
|  2  | Âu/Mỹ      |   -      |       YES        |   Yes   |  ✅   |
|  3  | Trung Quốc |  Sport   |  Pay → NO        |   No    |  ✅   |
|  4  | Âu/Mỹ      |   -      |       YES        |   Yes   |  ✅   |
|  5  | Trung Quốc |   MOBA   |        NO        |   No    |  ✅   |
|  6  | Trung Quốc |  Sport   |  Free → YES      |   Yes   |  ✅   |
|  7  | Âu/Mỹ      |   -      |       YES        |   Yes   |  ✅   |
|  8  | Âu/Mỹ      |   -      |       YES        |   Yes   |  ✅   |

✅ **Độ chính xác: 8/8 = 100%**

---

# 5️⃣ BÀI TẬP TỰ LUYỆN

## Bài 1: Tính Entropy

Tính Entropy cho các tập sau:

- a) S₁ = [5 Yes, 3 No]
- b) S₂ = [6 Yes, 2 No]
- c) S₃ = [4 Yes, 4 No]

<details>
<summary>📝 Đáp án</summary>

a) E(S₁) = -5/8×log₂(5/8) - 3/8×log₂(3/8) = 0.424 + 0.531 = **0.954**

b) E(S₂) = -6/8×log₂(6/8) - 2/8×log₂(2/8) = 0.311 + 0.500 = **0.811**

c) E(S₃) = -0.5×log₂(0.5) - 0.5×log₂(0.5) = 0.5 + 0.5 = **1.0**

</details>

---

## Bài 2: Tính Gain

Cho S = [6 Yes, 2 No], E(S) = 0.811

Thuộc tính A chia S thành:

- A = 1: [4 Yes, 0 No]
- A = 0: [2 Yes, 2 No]

Tính Gain(S, A).

<details>
<summary>📝 Đáp án</summary>

E(A=1) = 0 (thuần nhất)
E(A=0) = 1.0 (50-50)

Gain = 0.811 - [(4/8)×0 + (4/8)×1.0]
= 0.811 - 0.5
= **0.311**

</details>

---

## Bài 3: So sánh thuộc tính

Cho S = [4 Yes, 4 No], E(S) = 1.0

Thuộc tính B chia S thành:

- B = 1: [3 Yes, 1 No]
- B = 0: [1 Yes, 3 No]

Thuộc tính C chia S thành:

- C = 1: [2 Yes, 2 No]
- C = 0: [2 Yes, 2 No]

Thuộc tính nào tốt hơn?

<details>
<summary>📝 Đáp án</summary>

**Thuộc tính B:**

- E(B=1) = E(B=0) = 0.811 (tra bảng 3/4, 1/4)
- Gain(B) = 1.0 - [(4/8)×0.811 + (4/8)×0.811] = 1.0 - 0.811 = **0.189**

**Thuộc tính C:**

- E(C=1) = E(C=0) = 1.0
- Gain(C) = 1.0 - [(4/8)×1.0 + (4/8)×1.0] = 1.0 - 1.0 = **0**

→ **B tốt hơn** vì Gain(B) > Gain(C)

</details>

---

# 📋 CHECKLIST LÀM BÀI THI DECISION TREE

- [ ] **Bước 0:** Đếm Yes/No của tập gốc
- [ ] **Bước 1:** Tính E(S) gốc
- [ ] **Bước 2:** Với MỖI thuộc tính:
  - [ ] Lập bảng chia theo từng giá trị
  - [ ] Đếm Yes/No mỗi nhánh
  - [ ] Tính E() mỗi nhánh (tra bảng!)
  - [ ] Tính Gain = E(S) - Σ(weight × E_nhánh)
- [ ] **Bước 3:** Chọn thuộc tính có Gain MAX → Nút gốc
- [ ] **Bước 4:** Nhánh nào E=0 → Tạo lá
- [ ] **Bước 5:** Nhánh nào E>0 → Lặp lại từ bước 1

---

> **💡 MẸO LÀM NHANH:**
>
> 1. **Thuộc lòng bảng tra** để không cần tính log₂
> 2. **E = 0** khi tất cả cùng lớp → DỪNG
> 3. **E = 1** khi 50-50
> 4. **Gain = 0** nghĩa là thuộc tính vô dụng

---

_Hết tài liệu Decision Tree Bài tập - Phương án 2_
