# PHƯƠNG ÁN 1: GIẢI THÍCH ĐƠN GIẢN
# MẠNG NƠ-RON NHÂN TẠO (ARTIFICIAL NEURAL NETWORK - ANN)

---

## 📚 MỤC LỤC

1. [Giới thiệu tổng quan](#1-giới-thiệu-tổng-quan)
2. [Nơ-ron sinh học vs Nơ-ron nhân tạo](#2-nơ-ron-sinh-học-vs-nơ-ron-nhân-tạo)
3. [Cấu trúc mạng nơ-ron](#3-cấu-trúc-mạng-nơ-ron)
4. [Hàm kích hoạt (Activation Functions)](#4-hàm-kích-hoạt-activation-functions)
5. [Forward Propagation](#5-forward-propagation)
6. [Backpropagation](#6-backpropagation)
7. [Ví dụ minh họa từng bước](#7-ví-dụ-minh-họa-từng-bước)
8. [Huấn luyện mạng nơ-ron](#8-huấn-luyện-mạng-nơ-ron)
9. [Các vấn đề thường gặp](#9-các-vấn-đề-thường-gặp)
10. [Tổng kết](#10-tổng-kết)

---

# 1. GIỚI THIỆU TỔNG QUAN

## 1.1. Mạng nơ-ron là gì?

**Mạng nơ-ron nhân tạo (ANN)** là một mô hình tính toán được lấy cảm hứng từ cách hoạt động của **não người**.

**Ví dụ đời thường:**

Khi bạn nhìn một bức ảnh và nhận ra đó là con mèo, não bạn đã:
1. Nhận thông tin từ mắt (pixels)
2. Xử lý qua hàng tỷ nơ-ron thần kinh
3. Đưa ra kết luận "Đây là con mèo"

Mạng nơ-ron nhân tạo mô phỏng quá trình này!

## 1.2. Tại sao cần mạng nơ-ron?

**Hạn chế của Linear Regression:**
- Chỉ học được mối quan hệ **tuyến tính** (đường thẳng)
- Không xử lý được các bài toán phức tạp

**Ví dụ:**

```
Linear Regression:           Mạng nơ-ron:
      y                            y
      |    /                       |    ___
      |   /                        |   /   \
      |  /                         |  /     \
      | /                          | /       \
      +-------→ x                  +----------→ x

Chỉ vẽ đường thẳng            Có thể vẽ đường cong phức tạp
```

## 1.3. Ứng dụng của mạng nơ-ron

| Lĩnh vực | Ứng dụng |
|----------|----------|
| Thị giác máy | Nhận diện khuôn mặt, phân loại ảnh |
| Xử lý ngôn ngữ | Dịch thuật, chatbot |
| Y tế | Chẩn đoán bệnh từ ảnh X-quang |
| Tài chính | Dự đoán giá cổ phiếu |
| Game | AI chơi cờ, game |

---

# 2. NƠ-RON SINH HỌC VS NƠ-RON NHÂN TẠO

## 2.1. Nơ-ron sinh học (trong não)

```
                    Nhân tế bào
                         ●
                        /|\
      Đuôi gai ───────→ │ │ │
      (Dendrites)       │ │ │
                        │ │ │
                         \│/
                          │
                          │ ← Sợi trục (Axon)
                          │
                          ↓
                    Đầu ra (đến nơ-ron khác)
```

**Cách hoạt động:**
1. **Đuôi gai (Dendrites):** Nhận tín hiệu từ các nơ-ron khác
2. **Nhân tế bào (Cell body):** Xử lý tín hiệu
3. **Sợi trục (Axon):** Truyền tín hiệu đi

**Đặc điểm quan trọng:**
- Nơ-ron chỉ "kích hoạt" khi tín hiệu đủ mạnh
- Kết nối giữa các nơ-ron có **độ mạnh khác nhau**

## 2.2. Nơ-ron nhân tạo (trong máy tính)

```
      x₁ ───w₁───┐
                  ↘
      x₂ ───w₂───→ [Σ + b] ──→ [f] ──→ y
                  ↗
      x₃ ───w₃───┘

Trong đó:
- x₁, x₂, x₃: Đầu vào (inputs)
- w₁, w₂, w₃: Trọng số (weights)
- b: Bias (độ lệch)
- Σ: Tổng có trọng số
- f: Hàm kích hoạt
- y: Đầu ra (output)
```

**Cách hoạt động:**
1. Nhận đầu vào x₁, x₂, x₃
2. Nhân với trọng số: w₁x₁, w₂x₂, w₃x₃
3. Cộng lại + bias: z = w₁x₁ + w₂x₂ + w₃x₃ + b
4. Đưa qua hàm kích hoạt: y = f(z)

## 2.3. So sánh

| Đặc điểm | Nơ-ron sinh học | Nơ-ron nhân tạo |
|----------|-----------------|-----------------|
| Đầu vào | Tín hiệu điện từ nơ-ron khác | Số thực x₁, x₂, ... |
| Độ mạnh kết nối | Độ mạnh synapse | Trọng số w |
| Ngưỡng kích hoạt | Điện thế ngưỡng | Hàm kích hoạt f |
| Đầu ra | Xung điện | Số thực y |

---

# 3. CẤU TRÚC MẠNG NƠ-RON

## 3.1. Các thành phần chính

### 3.1.1. Node (Nơ-ron)

**Node** là đơn vị tính toán cơ bản của mạng.

```
         ┌─────────┐
x₁ ──w₁──►│         │
         │  Node   │──► y
x₂ ──w₂──►│         │
         └─────────┘
```

### 3.1.2. Layer (Lớp)

**Layer** là một nhóm các node hoạt động song song.

```
Layer 1    Layer 2    Layer 3
  ○          ○          ○
  ○          ○          ○
  ○          ○          
```

### 3.1.3. Weight (Trọng số)

**Weight** là độ mạnh của kết nối giữa 2 node.

- w > 0: Kết nối kích thích (tăng cường tín hiệu)
- w < 0: Kết nối ức chế (giảm tín hiệu)
- w = 0: Không có kết nối

### 3.1.4. Bias (Độ lệch)

**Bias** là một giá trị cộng thêm (hoặc trừ đi) giúp mạng nơ-ron điều chỉnh "ngưỡng kích hoạt".

**Hiểu đơn giản:**
Hãy tưởng tượng $Weighted Sum$ (Tổng có trọng số) là **điểm thi** của bạn.
- Nếu không có Bias: Bạn so sánh điểm với số 0. ($Điểm > 0$ là đậu).
- Nếu **Bias = -5**: Bạn cần $Điểm + (-5) > 0 \Leftrightarrow Điểm > 5$ mới đậu. (Bias đóng vai trò là ngưỡng đậu).
- Nếu **Bias = +2**: Bạn chỉ cần $Điểm + 2 > 0 \Leftrightarrow Điểm > -2$. (Bạn được cộng điểm vùng, dễ đậu hơn).

**Ý nghĩa toán học:** Cho phép đường quyết định **tịnh tiến** (dời lên/xuống/trái/phải) để khớp với dữ liệu tốt hơn, thay vì bị "trói buộc" phải luôn đi qua gốc tọa độ (0,0).

## 3.2. Các loại layer

### 3.2.1. Input Layer (Lớp đầu vào)

- Là lớp đầu tiên của mạng
- Nhận dữ liệu thô từ bên ngoài
- **Không có trọng số**, chỉ truyền dữ liệu đi

**Ví dụ:**
- Ảnh 28×28 pixels → 784 node input
- Dữ liệu có 3 features → 3 node input

### 3.2.2. Hidden Layer (Lớp ẩn)

- Là các lớp nằm giữa input và output
- Thực hiện các phép tính toán chính
- Có thể có **nhiều hidden layer**

**Ý nghĩa:**
- Hidden layer "học" các **đặc trưng** từ dữ liệu
- Càng nhiều layer → học được đặc trưng càng phức tạp

### 3.2.3. Output Layer (Lớp đầu ra)

- Là lớp cuối cùng
- Đưa ra kết quả dự đoán

**Ví dụ:**
- Phân loại 2 lớp (chó/mèo) → 1 node output (xác suất là mèo)
- Phân loại 10 lớp (chữ số 0-9) → 10 node output

## 3.3. Kiến trúc tổng thể

```
   INPUT LAYER      HIDDEN LAYER      OUTPUT LAYER
       (3)              (4)               (2)

       ○ ─────────────→ ○ ─────────────→ ○
       │ ╲             ╱│╲             ╱ │
       │  ╲           ╱ │ ╲           ╱  │
       ○ ──╲─────────╱──○──╲─────────╱───○
       │    ╲       ╱   │   ╲       ╱    
       │     ╲     ╱    │    ╲     ╱     
       ○ ─────╲───╱─────○─────╲───╱──────
                ╲╱             ╲╱
                 ○              

   Nhận          Học đặc         Đưa ra
   dữ liệu       trưng           kết quả
```

## 3.4. Fully Connected (Dense)

Trong mạng **Fully Connected**:
- Mỗi node ở layer này kết nối với **TẤT CẢ** node ở layer trước
- Còn gọi là **Dense Layer**

```
Layer 1    Layer 2
   ○ ────────○
    ╲      ╱
     ╲    ╱
      ╲  ╱
   ○ ──╳──○
      ╱  ╲
     ╱    ╲
    ╱      ╲
   ○ ────────○
```

---

# 4. HÀM KÍCH HOẠT (ACTIVATION FUNCTIONS)

## 4.1. Tại sao cần hàm kích hoạt? (QUAN TRỌNG)

### Hiểu đơn giản: "Bộ lọc thông tin"
- Hàm kích hoạt giống như một **"người gác cổng"** tại mỗi nơ-ron.
- Nó quyết định xem thông tin này có **quan trọng** để truyền tiếp hay không.
- **Ví dụ:** Nếu điểm số < 5, hàm kích hoạt ReLU sẽ biến nó thành 0 (Rớt, không cần quan tâm nữa). Nếu > 5, nó giữ nguyên hoặc biến đổi để truyền đi.

### Hiểu theo toán học: "Uốn cong đường thẳng"
- **Không có hàm kích hoạt:** Mạng nơ-ron chỉ là các phép nhân cộng tuyến tính ($y = ax + b$). Dù có xếp 100 lớp chồng lên nhau, nó vẫn chỉ vẽ được một **đường thẳng**.

    **Chứng minh:**
    Giả sử ta có 2 lớp chồng lên nhau (không có hàm kích hoạt):
    1. Lớp 1: $y_1 = w_1 \cdot x + b_1$
    2. Lớp 2: $y_2 = w_2 \cdot y_1 + b_2$

    Thay $y_1$ vào $y_2$:
    $$ y_2 = w_2(w_1 \cdot x + b_1) + b_2 $$
    $$ y_2 = (w_2 \cdot w_1) \cdot x + (w_2 \cdot b_1 + b_2) $$

    Đặt $W_{moi} = w_2 \cdot w_1$ và $B_{moi} = w_2 \cdot b_1 + b_2$.
    Ta có: **$y_2 = W_{moi} \cdot x + B_{moi}$**
    👉 **Kết luận:** Đây vẫn chỉ là phương trình đường thẳng ($y = ax + b$). Việc thêm lớp thứ 2 không làm tăng sức mạnh của mô hình, nó chỉ tương đương với 1 lớp duy nhất!

- **Có hàm kích hoạt (Phi tuyến):** Nó giúp **"bẻ cong"** các đường thẳng này. Nhờ đó, mạng nơ-ron có thể vẽ được bất kỳ hình dạng biên giới nào để phân loại dữ liệu phức tạp (như phân loại ảnh chó mèo - dữ liệu phân bố cong queo).

👉 **Tóm lại:** Hàm kích hoạt đem lại khả năng **"tư duy phức tạp"** cho mạng nơ-ron.

## 4.2. Ví dụ trực quan: Tại sao dữ liệu ảnh lại "cong queo"?

Nhiều bạn thắc mắc: *"Tại sao phân loại chó mèo lại phức tạp đến mức không thể dùng đường thẳng?"*

### 1. Dữ liệu Tuyến Tính (Linear - Đơn giản)
- **Ví dụ:** Phân loại **người lớn** và **trẻ em** dựa trên **Chiều cao**.
- **Dữ liệu:**
    - Trẻ em: Cao < 1m4
    - Người lớn: Cao > 1m4
- **Giải quyết:** Bạn chỉ cần kẻ **một vạch thẳng** tại mốc 1m4 là xong. Đây là bài toán tuyến tính.

### 2. Dữ liệu Phi Tuyến (Non-Linear - Phức tạp)
- **Ví dụ:** Phân loại **Chó** và **Mèo** dựa trên **Hàng triệu điểm ảnh (pixels)**.
- **Vấn đề:**
    - Không có bất kỳ "vạch thẳng" đơn giản nào tách được chúng.
    - Một con mèo màu trắng có thể giống "đám mây".
    - Một con chó cuộn tròn có thể giống "cục bông".
    - Trong không gian dữ liệu, các điểm ảnh của "Chó" và "Mèo" **xoắn quyện vào nhau** (giống như âm và dương trong vòng tròn bát quái).
- **Giải quyết:** Mạng nơ-ron cần các hàm kích hoạt để **uốn cong** các đường biên giới, luồn lách qua các đám dữ liệu xoắn nùi đó để tách chúng ra.

> **Tưởng tượng:** Dữ liệu chó/mèo giống như hai sợi dây thừng xanh/đỏ xoắn vào nhau. Bạn không thể dùng một nhát dao thẳng (Linear) để cắt rời chúng mà không làm đứt dây. Bạn cần "gỡ rối" (Non-Linear) từ từ.


## 4.3. Các loại Hàm Kích Hoạt phổ biến

---

# 🟢 PHẦN 1: HIỂU NHANH BẰNG ẨN DỤ ĐỜI THƯỜNG

> *Phần này giúp bạn hiểu bản chất và ghi nhớ lâu. Đọc phần này trước khi đi vào toán học.*

### 1. Sigmoid - "Bộ lọc Xác suất" (Giống Giáo viên chấm điểm)

**Tính cách:** Nó ép mọi con số về khoảng **0 đến 1**.
- **Ví dụ:** Dù bạn làm bài siêu tốt (giá trị 1 triệu) hay siêu tệ (giá trị -1 tỷ), Sigmoid cũng chỉ cho bạn điểm từ 0 đến 1 (0% đến 100%).
    - Làm bài cực tốt → Gần 1 (gần 100%).
    - Làm bài cực tệ → Gần 0 (gần 0%).
    - Làm bình thường (Input = 0) → Đúng 0.5 (50%).

**Dùng khi nào?**
- Chỉ dùng ở **Cổng ra (Output Layer)** khi bạn cần tính xác suất (Có/Không, Đậu/Rớt).
- **Đừng dùng ở lớp ẩn** vì nó học rất chậm (bệnh "Vanishing Gradient" - sẽ giải thích ở Phần 2).

---

### 2. ReLU - "Thầy Giám Thị Khắt Khe" (Giống Cổng soát vé)

**Biệt danh:** Đây là hàm **"quốc dân"**, dùng nhiều nhất trong Deep Learning.

**Tính cách:** Cực kỳ dứt khoát!
- Nếu là số **Âm**: **"Cút!"** (Cho về 0 luôn).
- Nếu là số **Dương**: **"Mời vào!"** (Giữ nguyên giá trị).

**Hình ảnh:** Giống như cổng soát vé:
- Không có vé (Giá trị âm): Không được vào (Output = 0).
- Có vé (Giá trị dương): Mời vào y nguyên.

**Dùng khi nào?**
- **Luôn là lựa chọn số 1 cho các lớp ẩn (Hidden Layers).**
- Lý do: Tính toán siêu nhanh và giúp mạng học tốt hơn Sigmoid rất nhiều.

---

### 3. Tanh - "Sigmoid phiên bản Mạnh Mẽ"

**Tính cách:** Giống Sigmoid (cũng hình chữ S) nhưng mạnh mẽ hơn. Nó ép giá trị về khoảng **-1 đến 1** (thay vì 0 đến 1).

**Điểm khác biệt quan trọng:**
- Sigmoid: Tâm ở 0.5 (chỉ có số dương).
- Tanh: Tâm ở 0 (có cả âm và dương) → Tốt hơn cho việc học.

**Dùng khi nào?**
- Tốt hơn Sigmoid một chút ở lớp ẩn, nhưng vẫn thua ReLU về tốc độ.
- Dùng trong một số kiến trúc đặc biệt (như RNN, LSTM).

---

### Bảng Tóm Tắt Nhanh (Dễ nhớ)

| Hàm | Ẩn dụ | Khoảng giá trị | Dùng ở đâu? |
|:---:|:---:|:---:|:---:|
| **Sigmoid** | Giáo viên chấm điểm 0-100% | $(0, 1)$ | Output (Xác suất) |
| **ReLU** | Cổng soát vé (Âm thì loại) | $[0, +\infty)$ | Hidden Layers (Mặc định) |
| **Tanh** | Sigmoid mạnh hơn | $(-1, 1)$ | Hidden (Đôi khi) |

---
---

# 🔵 PHẦN 2: KIẾN THỨC HỌC THUẬT (ĐỂ ĐI THI)

> *Phần này chứa công thức toán học, đạo hàm, và các vấn đề kỹ thuật. Đây là những gì bạn cần viết vào bài thi.*

### 1. Hàm Sigmoid (Logistic Function)

#### a. Công thức Toán học
- **Công thức chính:** 
$$\sigma(z) = \frac{1}{1 + e^{-z}}$$

- **Đạo hàm:**
$$\sigma'(z) = \sigma(z) \cdot (1 - \sigma(z))$$

- **Tính chất đặc biệt:** Nếu đặt $a = \sigma(z)$, thì $\sigma'(z) = a(1-a)$. Điều này rất hữu ích trong Backpropagation vì ta chỉ cần lưu giá trị $a$ (output) mà không cần tính lại $z$ (input).

#### b. Đồ thị
```
σ(z)
  1 |           ___________
    |          /
0.5 |_________/
    |        /
  0 |_______/
    +------------------------→ z
        -5   -2   0   2   5
```

#### c. Bảng tra cứu giá trị (Dùng khi làm bài tập)

| $z$ | $e^{-z}$ | $\sigma(z)$ | Ghi nhớ |
|:---:|:---:|:---:|:---|
| -3 | 20.09 | **0.047** | ≈ 5% |
| -2 | 7.39 | **0.119** | ≈ 12% |
| -1 | 2.72 | **0.269** | ≈ 27% |
| 0 | 1.00 | **0.500** | Chính xác 50% |
| 1 | 0.37 | **0.731** | ≈ 73% |
| 2 | 0.14 | **0.881** | ≈ 88% |
| 3 | 0.05 | **0.953** | ≈ 95% |

> **Mẹo:** $\sigma(-z) = 1 - \sigma(z)$. Ví dụ: $\sigma(-2) = 1 - \sigma(2) = 1 - 0.881 = 0.119$.

#### d. Vấn đề học thuật: Vanishing Gradient
- **Đạo hàm max của Sigmoid chỉ là 0.25** (tại $z=0$).
- Khi mạng có nhiều lớp, Backpropagation phải nhân liên tiếp các đạo hàm (Chain Rule):
$$\frac{\partial L}{\partial w_1} = \frac{\partial L}{\partial a_n} \cdot \sigma'(z_n) \cdot \sigma'(z_{n-1}) \cdot ... \cdot \sigma'(z_1)$$
- Nếu có 10 lớp: $0.25^{10} \approx 0.0000009$ → Gradient gần bằng 0!
- **Kết quả:** Các lớp đầu tiên không được cập nhật trọng số → Mạng không học được → Gọi là **Vanishing Gradient Problem**.

---

### 2. Hàm Tanh (Hyperbolic Tangent)

#### a. Công thức Toán học
- **Công thức chính:**
$$\tanh(z) = \frac{e^z - e^{-z}}{e^z + e^{-z}}$$

- **Đạo hàm:**
$$\tanh'(z) = 1 - \tanh^2(z)$$

- **Tính chất:** Nếu đặt $a = \tanh(z)$, thì $\tanh'(z) = 1 - a^2$.

#### b. Đồ thị
```
tanh(z)
  1 |           ___________
    |          /
  0 |_________/____________
    |        /
 -1 |_______/
    +------------------------→ z
        -5   -2   0   2   5
```

#### c. Mối quan hệ với Sigmoid
$$\tanh(z) = 2 \cdot \sigma(2z) - 1$$

#### d. Ưu điểm so với Sigmoid
- **Zero-centered:** Tâm dữ liệu là 0 (có cả âm và dương).
- Điều này giúp việc cập nhật trọng số đi đúng hướng hơn (ít zig-zag).
- Đạo hàm max là **1.0** (lớn hơn 0.25 của Sigmoid).

#### e. Nhược điểm
- Vẫn bị **Vanishing Gradient** khi $|z|$ lớn (đạo hàm tiến về 0 ở hai cực).

---

### 3. Hàm ReLU (Rectified Linear Unit)

#### a. Công thức Toán học
- **Công thức chính:**
$$f(z) = \max(0, z) = \begin{cases} z & \text{nếu } z > 0 \\ 0 & \text{nếu } z \leq 0 \end{cases}$$

- **Đạo hàm:**
$$f'(z) = \begin{cases} 1 & \text{nếu } z > 0 \\ 0 & \text{nếu } z \leq 0 \end{cases}$$

#### b. Đồ thị
```
f(z)
  5 |              /
  4 |             /
  3 |            /
  2 |           /
  1 |          /
  0 |_________/
    +------------------------→ z
        -3   -1   0   1   3
```

#### c. Tại sao ReLU là Vua của Hidden Layers?
1. **Giải quyết Vanishing Gradient:**
   - Đạo hàm = 1 (với $z > 0$). Nhân 1 triệu lần số 1 vẫn là 1!
   - Gradient được bảo toàn xuyên suốt mạng sâu.

2. **Tính toán siêu nhanh:**
   - Chỉ cần so sánh $z$ với 0 (nhanh hơn nhiều so với tính $e^z$ của Sigmoid/Tanh).

#### d. Vấn đề học thuật: Dying ReLU
- Nếu input luôn âm ($z < 0$), đạo hàm = 0 mãi mãi.
- Nơ-ron sẽ ngừng học hoàn toàn → Gọi là **"Dying ReLU"** (Nơ-ron chết).
- **Khắc phục:** Dùng **Leaky ReLU** (cho phép đạo hàm nhỏ thay vì 0 khi $z < 0$).

---

### 4. Bảng So Sánh Tổng Hợp (QUAN TRỌNG - NHỚ ĐỂ ĐI THI)

| Tiêu chí | Sigmoid | Tanh | ReLU |
|:---|:---:|:---:|:---:|
| **Công thức** | $\frac{1}{1+e^{-z}}$ | $\frac{e^z - e^{-z}}{e^z + e^{-z}}$ | $\max(0, z)$ |
| **Khoảng giá trị** | $(0, 1)$ | $(-1, 1)$ | $[0, +\infty)$ |
| **Đạo hàm** | $\sigma(1-\sigma)$ | $1 - \tanh^2$ | $0$ hoặc $1$ |
| **Đạo hàm Max** | $0.25$ | $1.0$ | $1.0$ |
| **Tâm tại 0?** | ❌ Không | ✅ Có | ❌ Không |
| **Vấn đề lớn** | Vanishing Gradient | Vanishing Gradient | Dying ReLU |
| **Tốc độ tính** | Chậm (mũ) | Chậm (mũ) | **Rất nhanh** |
| **Dùng ở đâu?** | Output (Xác suất) | Hidden (Ít dùng) | **Hidden (Mặc định)** |

---



# 5. FORWARD PROPAGATION

## 5.1. Khái niệm

**Forward Propagation** (Lan truyền tiến) là quá trình tính output của mạng bằng cách truyền dữ liệu từ **input → hidden → output**.

```
INPUT          HIDDEN          OUTPUT
  x      →       a       →       ŷ
     (Forward)       (Forward)
```

## 5.2. Công thức

### Tại mỗi node:

**Bước 1: Tính tổng có trọng số (weighted sum)**
```
z = Σ(wᵢ × xᵢ) + b
  = w₁x₁ + w₂x₂ + ... + wₙxₙ + b
```

**Bước 2: Áp dụng hàm kích hoạt**
```
a = f(z)
```

Trong đó:
- z: Tổng có trọng số (pre-activation)
- a: Activation (post-activation)
- f: Hàm kích hoạt (sigmoid, ReLU, ...)

## 5.3. Ví dụ đơn giản

**Cho mạng 1 node:**
```
x₁ = 0.5 ─── w₁=0.4 ───┐
                        ↘
                         [Σ + b] ─→ [σ] ─→ y
                        ↗
x₂ = 0.3 ─── w₂=0.6 ───┘
                    b = 0.1
```

**Bước 1: Tính z**
```
z = w₁×x₁ + w₂×x₂ + b
  = 0.4×0.5 + 0.6×0.3 + 0.1
  = 0.2 + 0.18 + 0.1
  = 0.48
```

**Bước 2: Áp dụng sigmoid**
```
y = σ(z) = 1 / (1 + e⁻⁰·⁴⁸)
  = 1 / (1 + 0.619)
  = 1 / 1.619
  ≈ 0.618
```

**Kết quả:** Output = 0.618

## 5.4. Forward qua nhiều layer

**Ký hiệu:**
- **a⁽ˡ⁾**: Activation của layer l
- **W⁽ˡ⁾**: Ma trận trọng số từ layer (l-1) đến layer l
- **b⁽ˡ⁾**: Vector bias của layer l

**Công thức cho layer l:**
```
z⁽ˡ⁾ = W⁽ˡ⁾ × a⁽ˡ⁻¹⁾ + b⁽ˡ⁾
a⁽ˡ⁾ = f(z⁽ˡ⁾)
```

## 5.5. Ví dụ mạng 2 layer

**Cấu trúc:** 2 input → 2 hidden → 1 output

```
        Hidden          Output
x₁ ─────→ h₁ ────────→
    ╲    ╱    ╲       ╲
     ╲  ╱      ╲       → y
      ╳         ╲     ╱
     ╱  ╲        ╲   ╱
    ╱    ╲        ╲ ╱
x₂ ─────→ h₂ ────────→
```

**Cho:**
- Input: x₁ = 1, x₂ = 0
- Hidden layer weights: 
  - w₁₁ = 0.5, w₁₂ = 0.3 (đến h₁)
  - w₂₁ = 0.2, w₂₂ = 0.4 (đến h₂)
- Hidden biases: b₁ = 0.1, b₂ = 0.2
- Output layer weights: v₁ = 0.6, v₂ = 0.7
- Output bias: b₃ = 0.1
- Activation: Sigmoid

---

**BƯỚC 1: Tính hidden layer**

**Node h₁:**
```
z₁ = w₁₁×x₁ + w₁₂×x₂ + b₁
   = 0.5×1 + 0.3×0 + 0.1
   = 0.5 + 0 + 0.1 = 0.6

a₁ = σ(0.6) = 1/(1 + e⁻⁰·⁶)
   = 1/(1 + 0.549) = 1/1.549 ≈ 0.646
```

**Node h₂:**
```
z₂ = w₂₁×x₁ + w₂₂×x₂ + b₂
   = 0.2×1 + 0.4×0 + 0.2
   = 0.2 + 0 + 0.2 = 0.4

a₂ = σ(0.4) = 1/(1 + e⁻⁰·⁴)
   = 1/(1 + 0.670) = 1/1.670 ≈ 0.599
```

---

**BƯỚC 2: Tính output layer**

```
z₃ = v₁×a₁ + v₂×a₂ + b₃
   = 0.6×0.646 + 0.7×0.599 + 0.1
   = 0.388 + 0.419 + 0.1
   = 0.907

ŷ = σ(0.907) = 1/(1 + e⁻⁰·⁹⁰⁷)
  = 1/(1 + 0.404) ≈ 0.712
```

**Kết quả cuối cùng:** ŷ = 0.712

---

# 6. BACKPROPAGATION

## 6.1. Khái niệm

**Backpropagation** (Lan truyền ngược) là thuật toán tính **đạo hàm** của hàm lỗi theo từng trọng số, để cập nhật trọng số theo hướng giảm lỗi.

```
OUTPUT          HIDDEN          INPUT
  ŷ       ←       a       ←       x
     (Backward)       (Backward)
        δ              δ
```

## 6.2. Ý tưởng

1. Tính **sai số** tại output: e = ŷ - y
2. "Lan truyền" sai số **ngược về** các layer trước
3. Tính **đạo hàm** theo từng trọng số
4. **Cập nhật** trọng số để giảm sai số

## 6.3. Hàm lỗi (Loss Function)

**Mean Squared Error (MSE):**
```
L = (1/2) × (ŷ - y)²
```

**Binary Cross-Entropy:**
```
L = -[y×log(ŷ) + (1-y)×log(1-ŷ)]
```

## 6.4. Quy tắc chuỗi (Chain Rule)

Để tính đạo hàm của L theo w, ta dùng **quy tắc chuỗi**:

```
∂L/∂w = ∂L/∂ŷ × ∂ŷ/∂z × ∂z/∂w
```

Trong đó:
- ∂L/∂ŷ: Đạo hàm lỗi theo output
- ∂ŷ/∂z: Đạo hàm của hàm kích hoạt
- ∂z/∂w: Đạo hàm của tổng có trọng số theo w

## 6.5. Công thức Backpropagation

### Tại Output Layer:

**Sai số (error/delta):**
```
δ_output = (ŷ - y) × σ'(z)
         = (ŷ - y) × ŷ × (1 - ŷ)
```

**Cập nhật trọng số:**
```
w_mới = w_cũ - α × δ × a_input
```

### Tại Hidden Layer:

**Sai số:**
```
δ_hidden = (Σ wⱼ × δⱼ) × σ'(z)
         = (Σ wⱼ × δⱼ) × a × (1 - a)
```

Trong đó: wⱼ và δⱼ là trọng số và sai số của layer kế tiếp.

**Cập nhật trọng số:**
```
w_mới = w_cũ - α × δ × x_input
```

### Cập nhật bias:
```
b_mới = b_cũ - α × δ
```

---

# 7. VÍ DỤ MINH HỌA TỪNG BƯỚC

## 7.1. Đề bài

**Mạng nơ-ron đơn giản:**
- **Input:** x₁ = 0.5, x₂ = 0.3
- **Hidden layer:** 1 node (h)
  - w₁ = 0.4, w₂ = 0.6, b₁ = 0.1
- **Output layer:** 1 node (y)
  - w₃ = 0.5, b₂ = 0.2
- **Hàm kích hoạt:** Sigmoid
- **Giá trị thực:** y = 1
- **Learning rate:** α = 0.5

**Yêu cầu:** Thực hiện 1 vòng Forward + Backpropagation.

---

## 7.2. Forward Propagation

### Bước 1: Tính Hidden Layer

```
z₁ = w₁×x₁ + w₂×x₂ + b₁
   = 0.4×0.5 + 0.6×0.3 + 0.1
   = 0.2 + 0.18 + 0.1
   = 0.48

a₁ = σ(z₁) = 1/(1 + e⁻⁰·⁴⁸)
```

**Tính e⁻⁰·⁴⁸:**
```
e⁻⁰·⁴⁸ ≈ 0.619
```

```
a₁ = 1/(1 + 0.619) = 1/1.619 ≈ 0.618
```

### Bước 2: Tính Output Layer

```
z₂ = w₃×a₁ + b₂
   = 0.5×0.618 + 0.2
   = 0.309 + 0.2
   = 0.509

ŷ = σ(z₂) = 1/(1 + e⁻⁰·⁵⁰⁹)
```

**Tính e⁻⁰·⁵⁰⁹:**
```
e⁻⁰·⁵⁰⁹ ≈ 0.601
```

```
ŷ = 1/(1 + 0.601) = 1/1.601 ≈ 0.625
```

### Kết quả Forward:
```
Hidden: a₁ = 0.618
Output: ŷ = 0.625
```

---

## 7.3. Tính sai số

```
Error = ŷ - y = 0.625 - 1 = -0.375
```

Mạng dự đoán 0.625 nhưng thực tế là 1 → Sai!

---

## 7.4. Backpropagation

### Bước 1: Tính delta tại Output Layer

```
δ₂ = (ŷ - y) × σ'(z₂)
   = (ŷ - y) × ŷ × (1 - ŷ)
   = (-0.375) × 0.625 × (1 - 0.625)
   = (-0.375) × 0.625 × 0.375
   = -0.0879
```

### Bước 2: Cập nhật trọng số Output Layer

**Cập nhật w₃:**
```
w₃_mới = w₃_cũ - α × δ₂ × a₁
       = 0.5 - 0.5 × (-0.0879) × 0.618
       = 0.5 - (-0.0272)
       = 0.5 + 0.0272
       = 0.527
```

**Cập nhật b₂:**
```
b₂_mới = b₂_cũ - α × δ₂
       = 0.2 - 0.5 × (-0.0879)
       = 0.2 + 0.044
       = 0.244
```

### Bước 3: Tính delta tại Hidden Layer

```
δ₁ = (w₃ × δ₂) × σ'(z₁)
   = (w₃ × δ₂) × a₁ × (1 - a₁)
   = (0.5 × (-0.0879)) × 0.618 × (1 - 0.618)
   = (-0.044) × 0.618 × 0.382
   = -0.0104
```

### Bước 4: Cập nhật trọng số Hidden Layer

**Cập nhật w₁:**
```
w₁_mới = w₁_cũ - α × δ₁ × x₁
       = 0.4 - 0.5 × (-0.0104) × 0.5
       = 0.4 - (-0.0026)
       = 0.4 + 0.0026
       = 0.4026
```

**Cập nhật w₂:**
```
w₂_mới = w₂_cũ - α × δ₁ × x₂
       = 0.6 - 0.5 × (-0.0104) × 0.3
       = 0.6 - (-0.0016)
       = 0.6 + 0.0016
       = 0.6016
```

**Cập nhật b₁:**
```
b₁_mới = b₁_cũ - α × δ₁
       = 0.1 - 0.5 × (-0.0104)
       = 0.1 + 0.0052
       = 0.1052
```

---

## 7.5. Tổng kết kết quả

### Bảng cập nhật trọng số:

| Tham số | Giá trị cũ | Giá trị mới | Thay đổi |
|---------|------------|-------------|----------|
| w₁ | 0.400 | 0.4026 | +0.0026 |
| w₂ | 0.600 | 0.6016 | +0.0016 |
| b₁ | 0.100 | 0.1052 | +0.0052 |
| w₃ | 0.500 | 0.527 | +0.027 |
| b₂ | 0.200 | 0.244 | +0.044 |

### Kiểm tra:
- Tất cả trọng số **tăng** (vì sai số âm, cần tăng output)
- Sau nhiều vòng lặp, output sẽ tiến gần 1

---

## 7.6. Mẹo tính toán

### Tính sigmoid nhanh:
```
e⁻⁰ = 1        → σ(0) = 0.5
e⁻¹ ≈ 0.368    → σ(1) ≈ 0.73
e⁻² ≈ 0.135    → σ(2) ≈ 0.88
e⁻⁰·⁵ ≈ 0.607  → σ(0.5) ≈ 0.62
```

### Đạo hàm sigmoid:
```
Nếu biết a = σ(z), thì:
σ'(z) = a × (1 - a)
```

### Dấu của delta:
```
δ = (ŷ - y) × ...

- Nếu ŷ > y: δ > 0 → giảm w
- Nếu ŷ < y: δ < 0 → tăng w
```

---

# 8. HUẤN LUYỆN MẠNG NƠ-RON

## 8.1. Quy trình huấn luyện

```
┌─────────────────────────────────────────────────────────┐
│            QUY TRÌNH HUẤN LUYỆN MẠNG NƠ-RON            │
├─────────────────────────────────────────────────────────┤
│                                                         │
│   1. Khởi tạo trọng số ngẫu nhiên                      │
│                       ↓                                 │
│   2. Forward: Tính output                               │
│                       ↓                                 │
│   3. Tính Loss (sai số)                                 │
│                       ↓                                 │
│   4. Backward: Tính gradient                            │
│                       ↓                                 │
│   5. Cập nhật trọng số                                  │
│                       ↓                                 │
│   6. Lặp lại 2-5 cho đến khi hội tụ                    │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

## 8.2. Epochs và Batches

### Epoch:
- Một **epoch** = 1 lần duyệt qua **toàn bộ** tập dữ liệu

### Batch:
- Một **batch** = 1 nhóm nhỏ dữ liệu
- Thay vì cập nhật sau mỗi điểm, cập nhật sau mỗi batch

**Ví dụ:**
- Có 1000 điểm dữ liệu
- Batch size = 100
- → 10 batches = 1 epoch

## 8.3. Learning Rate

**α quá nhỏ:**
- Hội tụ rất chậm
- Có thể mắc kẹt ở local minimum

**α quá lớn:**
- Không hội tụ
- Nhảy qua minimum

**Giá trị thường dùng:** 0.001, 0.01, 0.1

---

# 9. CÁC VẤN ĐỀ THƯỜNG GẶP

## 9.1. Vanishing Gradient

**Vấn đề:** Gradient trở nên rất nhỏ ở các layer sâu → trọng số không được cập nhật.

**Nguyên nhân:** Đạo hàm sigmoid < 0.25 → nhân nhiều lần → gradient → 0

**Giải pháp:** Dùng ReLU thay vì Sigmoid

## 9.2. Overfitting

**Vấn đề:** Mô hình học "thuộc lòng" dữ liệu huấn luyện, dự đoán kém trên dữ liệu mới.

**Giải pháp:**
- Thêm dữ liệu
- Regularization (L1, L2)
- Dropout

## 9.3. Underfitting

**Vấn đề:** Mô hình quá đơn giản, không học được pattern.

**Giải pháp:**
- Thêm layer/node
- Huấn luyện lâu hơn
- Giảm regularization

---

# 10. TỔNG KẾT

## 10.1. Những điều cần nhớ

1. **Cấu trúc mạng:** Input → Hidden → Output

2. **Forward Propagation:**
   ```
   z = Σwᵢxᵢ + b
   a = σ(z)
   ```

3. **Sigmoid:**
   ```
   σ(z) = 1/(1 + e⁻ᶻ)
   σ'(z) = σ(z) × (1 - σ(z)) = a × (1 - a)
   ```

4. **Backpropagation:**
   ```
   δ_output = (ŷ - y) × a × (1 - a)
   δ_hidden = (Σwⱼδⱼ) × a × (1 - a)
   ```

5. **Cập nhật:**
   ```
   w := w - α × δ × input
   b := b - α × δ
   ```

## 10.2. Quy trình làm bài

1. **Vẽ sơ đồ** mạng với các trọng số
2. **Forward:** Tính z và a cho từng node, từ trái sang phải
3. **Tính Loss:** (ŷ - y)
4. **Backward:** Tính δ cho từng node, từ phải sang trái
5. **Cập nhật:** Tính w_mới và b_mới

## 10.3. Bài tập tự luyện

**Bài 1:** Tính σ(0), σ(1), σ(-1) và đạo hàm tương ứng.

**Bài 2:** Cho mạng 1 node với x=1, w=0.5, b=0.2. Tính output nếu dùng sigmoid.

**Bài 3:** Với bài 2, nếu y_thực = 1 và α = 0.5, tính w_mới và b_mới sau 1 vòng backprop.

---

*Hết phần ANN - Phương án 1: Giải thích đơn giản*
