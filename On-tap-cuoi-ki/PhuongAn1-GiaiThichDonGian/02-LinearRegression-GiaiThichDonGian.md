# PHƯƠNG ÁN 1: GIẢI THÍCH ĐƠN GIẢN
# HỒI QUY TUYẾN TÍNH (LINEAR REGRESSION)

---

## 📚 MỤC LỤC

1. [Giới thiệu tổng quan](#1-giới-thiệu-tổng-quan)
2. [Phương trình đường thẳng](#2-phương-trình-đường-thẳng)
3. [Hàm lỗi (Loss Function)](#3-hàm-lỗi-loss-function)
4. [Gradient Descent (Thuật toán Xuống đồi)](#4-gradient-descent-thuật-toán-xuống-đồi)
5. [Quy trình huấn luyện (Pipeline)](#5-quy-trình-huấn-luyện-pipeline)
6. [Ví dụ tính tay chi tiết](#6-ví-dụ-tính-tay-chi-tiết)
7. [Bảng tổng hợp & Mẹo thi](#7-bảng-tổng-hợp--mẹo-thi)

---

# 1. GIỚI THIỆU TỔNG QUAN

## 1.1. Linear Regression là gì?

# 🟢 PHẦN 1: HIỂU NHANH BẰNG ẨN DỤ ĐỜI THƯỜNG

### Ẩn dụ: "Ông Cò Đất"

Hãy tưởng tượng bạn là một **"cò đất"** (môi giới bất động sản) lão luyện. Sau nhiều năm kinh nghiệm, bạn có một "linh cảm" rất hay:

> *"Cứ mỗi mét vuông đất ở khu này thì giá khoảng 40 triệu, cộng thêm 500 triệu tiền vị trí nền."*

Nếu ai đó hỏi mua mảnh 60m², bạn nhẩm ngay:
$$ 60 \times 40 + 500 = 2900 \text{ triệu} = 2.9 \text{ tỷ} $$

**Cái "linh cảm" đó chính là Linear Regression!**

Nó là một **quy tắc đơn giản** giúp bạn dự đoán một thứ (giá đất) dựa trên thông tin khác (diện tích).

---

# 🔵 PHẦN 2: KIẾN THỨC HỌC THUẬT (ĐỂ ĐI THI)

**Định nghĩa chính thức:**
> **Hồi quy tuyến tính (Linear Regression)** là một phương pháp thống kê để mô hình hóa mối quan hệ giữa **biến phụ thuộc** (Y - giá trị cần dự đoán) và một hoặc nhiều **biến độc lập** (X - thông tin đầu vào).

**Đặc điểm:**
- Biến phụ thuộc Y có **giá trị liên tục** (ví dụ: giá nhà, lương, nhiệt độ).
- Mối quan hệ giữa X và Y được biểu diễn bằng **phương trình đường thẳng**.

**Phân loại:**
| Loại | Số biến độc lập | Ví dụ |
|:---|:---:|:---|
| **Simple Linear Regression** | 1 | Dự đoán lương dựa trên số năm kinh nghiệm |
| **Multiple Linear Regression** | Nhiều | Dự đoán giá nhà dựa trên diện tích, vị trí, số phòng |

---

## 1.2. Tại sao cần Linear Regression?

# 🟢 PHẦN 1: HIỂU NHANH BẰNG ẨN DỤ ĐỜI THƯỜNG

**Bài toán thực tế:**
Bạn là quản lý nhân sự. Sếp hỏi: *"Nhân viên mới có 7 năm kinh nghiệm thì nên trả lương bao nhiêu?"*

Bạn có bảng dữ liệu cũ:
| Kinh nghiệm (năm) | Lương (triệu) |
|:---:|:---:|
| 3 | 60 |
| 4 | 55 |
| 5 | 66 |
| 6 | 93 |

**Vấn đề:** Bạn không thể tra bảng vì chưa có nhân viên nào 7 năm kinh nghiệm!

**Giải pháp:** Linear Regression giúp bạn **vẽ một đường thẳng** đi qua gần các điểm dữ liệu nhất, rồi dùng đường thẳng đó để dự đoán lương cho 7 năm kinh nghiệm.

---

# 🔵 PHẦN 2: KIẾN THỨC HỌC THUẬT (ĐỂ ĐI THI)

**Ứng dụng trong Machine Learning:**
- **Dự báo (Forecasting):** Dự đoán doanh thu, giá cổ phiếu, thời tiết.
- **Đánh giá xu hướng:** Mối quan hệ giữa quảng cáo và doanh số.
- **Nền tảng cho thuật toán phức tạp hơn:** Linear Regression là "viên gạch đầu tiên" để hiểu Neural Networks.

---

# 2. PHƯƠNG TRÌNH ĐƯỜNG THẲNG

## 2.1. Công thức cơ bản: y = wx + b

# 🟢 PHẦN 1: HIỂU NHANH BẰNG ẨN DỤ ĐỜI THƯỜNG

Quay lại ví dụ **ông cò đất**:
> *"Cứ mỗi mét vuông đất thì giá khoảng **40 triệu** (w), cộng thêm **500 triệu** tiền vị trí nền (b)."*

Công thức dự đoán giá:
$$ \text{Giá đất} = 40 \times \text{Diện tích} + 500 $$

**Ý nghĩa từng thành phần:**
| Thành phần | Ký hiệu | Ẩn dụ | Giá trị ví dụ |
|:---|:---:|:---|:---:|
| **Đầu vào** | $x$ | Diện tích mảnh đất (m²) | 60 |
| **Đầu ra (Dự đoán)** | $\hat{y}$ | Giá đất dự đoán (triệu) | 2900 |
| **Trọng số** | $w$ | Đơn giá mỗi m² | 40 |
| **Độ lệch** | $b$ | Giá nền cố định (vị trí, hạ tầng) | 500 |

---

# 🔵 PHẦN 2: KIẾN THỨC HỌC THUẬT (ĐỂ ĐI THI)

**Công thức chuẩn:**
$$ \hat{y} = f(x) = w \cdot x + b $$

**Giải thích ký hiệu:**
| Ký hiệu | Tên tiếng Anh | Ý nghĩa |
|:---:|:---|:---|
| $x$ | Input / Feature | Biến độc lập (đầu vào) |
| $\hat{y}$ | Prediction / Output | Giá trị dự đoán |
| $y$ | Target / Label | Giá trị thực tế (nhãn) |
| $w$ | Weight | Trọng số (Hệ số góc của đường thẳng) |
| $b$ | Bias | Độ lệch (Hệ số tự do) |

**Ý nghĩa hình học:**
- $w$ (Weight): Quyết định **độ dốc** của đường thẳng. $w > 0$ → đường đi lên, $w < 0$ → đường đi xuống.
- $b$ (Bias): Quyết định **vị trí** đường thẳng cắt trục tung (khi $x = 0$).

---

## 2.2. Ví dụ minh họa: Nhiều đường thẳng, nhiều dự đoán

# 🟢 PHẦN 1: HIỂU NHANH BẰNG ẨN DỤ ĐỜI THƯỜNG

**Vấn đề:** Có vô số đường thẳng có thể vẽ qua đám mây điểm dữ liệu. Mỗi đường thẳng cho một kết quả dự đoán khác nhau!

**Hình dung:**
```
   Lương (Y)
     ^
   93|                    * (6, 93)
     |                   /
   66|             * (5,66)
     |            /
   55|       * (4,55)
     |      /
   60|   * (3,60)
     |  /
     +-------------------------> Kinh nghiệm (X)
        3   4   5   6   7
```
- **Đường màu đỏ:** $y = 10x + 20$ → Dự đoán lương 7 năm = 90 triệu.
- **Đường màu xanh:** $y = 15x - 5$ → Dự đoán lương 7 năm = 100 triệu.
- **Đường màu vàng:** $y = 12x + 10$ → Dự đoán lương 7 năm = 94 triệu.

**Câu hỏi:** Đường nào là **tốt nhất**?

---

# 🔵 PHẦN 2: KIẾN THỨC HỌC THUẬT (ĐỂ ĐI THI)

**Bài toán tối ưu:**
Với mỗi bộ tham số $(w, b)$ khác nhau, ta có một đường thẳng khác nhau.

**Mục tiêu:** Tìm bộ $(w^*, b^*)$ sao cho đường thẳng đó **xấp xỉ tốt nhất** các điểm dữ liệu đã biết.

**Tiêu chí đánh giá "tốt":** Sử dụng **Hàm lỗi (Loss Function)** - sẽ giải thích ở mục 3.

---

# 3. HÀM LỖI (LOSS FUNCTION)

## 3.1. Loss là gì?

# 🟢 PHẦN 1: HIỂU NHANH BẰNG ẨN DỤ ĐỜI THƯỜNG

### Ẩn dụ: "Thầy giáo chấm điểm"

Hãy tưởng tượng bạn là **thầy giáo chấm bài**:
- **Đáp án đúng (y):** Lương thực tế của nhân viên (93 triệu).
- **Bài làm của trò ($\hat{y}$):** Lương mà mô hình dự đoán (77 triệu).
- **Lỗi (Loss):** Khoảng cách sai lệch = |93 - 77| = 16 triệu.

**Mục tiêu:** Tìm đường thẳng sao cho **tổng các lỗi** của tất cả học sinh (điểm dữ liệu) là **nhỏ nhất**.

**Hình dung:**
```
   Lương (Y)
     ^
   93|                    * (Thực tế)
     |                    |
   77|--------------------o (Dự đoán)
     |                    | <- Error = 16
     +-------------------------> Kinh nghiệm (X)
                          6
```
Các đoạn nét đứt đỏ chính là **Error** (Sai số).

---

# 🔵 PHẦN 2: KIẾN THỨC HỌC THUẬT (ĐỂ ĐI THI)

**Định nghĩa Loss:**
Loss (Lỗi) là thước đo **sự chênh lệch** giữa giá trị dự đoán ($\hat{y}$) và giá trị thực tế ($y$).

**Công thức Loss cho MỘT điểm dữ liệu (Squared Error):**
$$ L = (\hat{y}_i - y_i)^2 = ((w \cdot x_i + b) - y_i)^2 $$

**Tại sao lại bình phương?**
- Để biến mọi sai số (dương hoặc âm) thành số dương.
- Để "phạt nặng" những sai số lớn hơn.

**Công thức Loss cho TẤT CẢ điểm dữ liệu (Mean Squared Error - MSE):**
$$ L_{total} = \frac{1}{n} \sum_{i=1}^{n} (\hat{y}_i - y_i)^2 $$

---

## 3.2. Mục tiêu: Tìm đường thẳng có Loss nhỏ nhất

# 🟢 PHẦN 1: HIỂU NHANH BẰNG ẨN DỤ ĐỜI THƯỜNG

### Ẩn dụ: "Tìm đường đi ngắn nhất"

Hãy tưởng tượng bạn đang chơi trò chơi:
- Mỗi điểm dữ liệu là một **ngôi nhà**.
- Đường thẳng bạn vẽ là **một con đường**.
- Khoảng cách từ nhà đến đường là **sai số**.

**Mục tiêu:** Vẽ con đường sao cho **tổng khoảng cách từ tất cả các ngôi nhà đến đường** là ngắn nhất.

---

# 🔵 PHẦN 2: KIẾN THỨC HỌC THUẬT (ĐỂ ĐI THI)

**Bài toán tối ưu hóa:**
$$ (w^*, b^*) = \arg\min_{w, b} \sum_{i=1}^{n} (\hat{y}_i - y_i)^2 $$

Tìm bộ tham số $(w, b)$ sao cho tổng bình phương sai số là **cực tiểu**.

---

## 3.3. Đồ thị Loss theo b là Parabol

# 🟢 PHẦN 1: HIỂU NHANH BẰNG ẨN DỤ ĐỜI THƯỜNG

Nếu ta **cố định** $w$ và chỉ thay đổi $b$, thì đồ thị Loss phụ thuộc vào $b$ sẽ có hình dạng **chữ U** (Parabol).

**Hình dung:**
```
   Loss (L)
     ^
     |  \             /
     |   \           /
     |    \_________/   <- Đáy = Loss nhỏ nhất
     |         .
     |         b*     <- Giá trị b tối ưu
     +----------------------------> b
```
- **Đỉnh của chữ U (Đáy Parabol):** Là vị trí có Loss nhỏ nhất.
- **Giá trị b tại đỉnh:** Là $b^*$ (b tối ưu).

---

# 🔵 PHẦN 2: KIẾN THỨC HỌC THUẬT (ĐỂ ĐI THI)

**Giải thích toán học:**
Xét hàm Loss theo b (cố định w):
$$ L(b) = ((wx_i + b) - y_i)^2 $$

Đây là một **hàm bậc 2 theo b**, có dạng:
$$ L(b) = b^2 + (\text{hệ số b}) + (\text{hằng số}) $$

Hàm bậc 2 luôn có đồ thị là **Parabol**, với một điểm **cực tiểu** duy nhất.

---

# 4. GRADIENT DESCENT (THUẬT TOÁN XUỐNG ĐỒI)

## 4.1. Ý tưởng cốt lõi

# 🟢 PHẦN 1: HIỂU NHANH BẰNG ẨN DỤ ĐỜI THƯỜNG

### Ẩn dụ: "Viên bi lăn xuống đáy thung lũng"

Hãy tưởng tượng bạn thả một **viên bi** từ một vị trí ngẫu nhiên trên sườn núi:
1. Viên bi sẽ tự động lăn xuống theo hướng **dốc nhất**.
2. Dần dần, nó sẽ tiến về **đáy thung lũng** (nơi có độ cao thấp nhất).
3. Khi đến đáy, viên bi dừng lại.

**Áp dụng vào ML:**
- **Sườn núi:** Đồ thị hàm Loss (hình chữ U).
- **Vị trí viên bi:** Giá trị hiện tại của $b$ (hoặc $w$).
- **Đáy thung lũng:** Giá trị $b^*$ (hoặc $w^*$) tối ưu.
- **Lăn xuống:** Cập nhật $b$ theo hướng giảm Loss.

---

# 🔵 PHẦN 2: KIẾN THỨC HỌC THUẬT (ĐỂ ĐI THI)

**Gradient Descent là gì?**
Là một thuật toán **tối ưu hóa lặp** (iterative optimization) để tìm điểm cực tiểu của hàm Loss.

**Nguyên lý:**
1. **Tính đạo hàm (Gradient):** Đạo hàm cho biết **hướng tăng nhanh nhất** của hàm số.
2. **Di chuyển ngược hướng đạo hàm:** Để đi về phía **giảm nhanh nhất** (xuống đồi).
3. **Lặp lại:** Cho đến khi đạt điểm cực tiểu (đạo hàm ≈ 0).

**Ý nghĩa của đạo hàm:**
- Đạo hàm **dương** ($\frac{dL}{db} > 0$): Hàm đang **tăng** → Điểm cực tiểu nằm bên **trái** → Di chuyển $b$ sang **trái** (giảm $b$).
- Đạo hàm **âm** ($\frac{dL}{db} < 0$): Hàm đang **giảm** → Điểm cực tiểu nằm bên **phải** → Di chuyển $b$ sang **phải** (tăng $b$).

---

## 4.2. Công thức đạo hàm

# 🔵 PHẦN 2: KIẾN THỨC HỌC THUẬT (ĐỂ ĐI THI)

**Công thức đạo hàm riêng (Partial Derivatives):**

Với hàm Loss $L = (\hat{y}_i - y_i)^2 = (wx_i + b - y_i)^2$:

| Tham số | Công thức đạo hàm |
|:---:|:---|
| $\frac{\partial L}{\partial w}$ | $2 \cdot x_i \cdot (\hat{y}_i - y_i)$ |
| $\frac{\partial L}{\partial b}$ | $2 \cdot (\hat{y}_i - y_i)$ |

**Cách nhớ:**
- Đạo hàm theo $w$: Nhân thêm $x_i$ (vì $w$ đi kèm với $x$).
- Đạo hàm theo $b$: Không nhân $x_i$ (vì $b$ đứng một mình).
- Cả hai đều nhân với $2(\hat{y} - y)$ (từ đạo hàm của bình phương).

---

## 4.3. Công thức cập nhật tham số

# 🟢 PHẦN 1: HIỂU NHANH BẰNG ẨN DỤ ĐỜI THƯỜNG

### Ẩn dụ: "Learning Rate = Độ dài bước chân"

Khi viên bi lăn xuống đồi, **tốc độ lăn** rất quan trọng:
- **Lăn quá nhanh (Learning rate lớn):** Có thể **vượt qua** đáy thung lũng, dao động qua lại mãi.
- **Lăn quá chậm (Learning rate nhỏ):** Mất **quá nhiều thời gian** để đến đáy.
- **Tốc độ vừa phải:** Đến đáy nhanh và chính xác.

---

# 🔵 PHẦN 2: KIẾN THỨC HỌC THUẬT (ĐỂ ĐI THI)

**Công thức cập nhật:**
$$ w_{new} = w_{old} - \eta \cdot \frac{\partial L}{\partial w} $$
$$ b_{new} = b_{old} - \eta \cdot \frac{\partial L}{\partial b} $$

**Giải thích:**
| Ký hiệu | Tên | Ý nghĩa |
|:---:|:---|:---|
| $\eta$ | Learning Rate | Tốc độ học (thường nằm trong khoảng 0.001 - 0.1) |
| $\frac{\partial L}{\partial w}$ | Gradient of w | Hướng và độ lớn cần điều chỉnh $w$ |
| $\frac{\partial L}{\partial b}$ | Gradient of b | Hướng và độ lớn cần điều chỉnh $b$ |

**Tại sao dấu trừ (-)?**
- Vì ta đi **ngược hướng** đạo hàm để giảm Loss.

> [!TIP]
> **Mẹo nhớ:** Công thức cập nhật = "Giá trị cũ - (Tốc độ học × Đạo hàm)"

---

# 5. QUY TRÌNH HUẤN LUYỆN (PIPELINE)

## 5.1. Sơ đồ tổng quát 7 bước

# 🟢 PHẦN 1: HIỂU NHANH BẰNG ẨN DỤ ĐỜI THƯỜNG

**Quy trình huấn luyện như một vòng lặp học tập:**
1. **Bắt đầu:** Đoán bừa ($w, b$ ngẫu nhiên).
2. **Làm bài (Dự đoán):** Tính $\hat{y}$ cho một mẫu dữ liệu.
3. **Chấm điểm (Tính Loss):** So sánh $\hat{y}$ với đáp án đúng $y$.
4. **Phân tích lỗi (Tính đạo hàm):** Xem sai ở đâu, sai bao nhiêu.
5. **Sửa sai (Cập nhật $w, b$):** Điều chỉnh để lần sau làm tốt hơn.
6. **Lặp lại:** Làm bài tiếp với mẫu dữ liệu khác.
7. **Hoàn thành:** Khi đã duyệt hết tất cả mẫu dữ liệu.

---

# 🔵 PHẦN 2: KIẾN THỨC HỌC THUẬT (ĐỂ ĐI THI)

**Sơ đồ Pipeline:**
```
┌───────────────────────────────────────────────────────────────┐
│  1. KHỞI TẠO: Chọn w, b ngẫu nhiên                            │
└───────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌───────────────────────────────────────────────────────────────┐
│  2. LẤY MẪU: Lấy (x_i, y_i) từ dữ liệu huấn luyện             │
└───────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌───────────────────────────────────────────────────────────────┐
│  3. TÍNH OUTPUT: ŷ_i = w * x_i + b                            │
└───────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌───────────────────────────────────────────────────────────────┐
│  4. TÍNH LOSS: L = (ŷ_i - y_i)²                               │
└───────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌───────────────────────────────────────────────────────────────┐
│  5. TÍNH ĐẠO HÀM: dL/dw, dL/db                                │
└───────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌───────────────────────────────────────────────────────────────┐
│  6. CẬP NHẬT THAM SỐ: w = w - η*dL/dw, b = b - η*dL/db        │
└───────────────────────────────────────────────────────────────┘
                              │
                              ▼
                    ┌─────────────────┐
                    │ Còn mẫu dữ liệu?│
                    └─────────────────┘
                      │           │
                    CÓ           KHÔNG
                      │           │
                      ▼           ▼
              Quay lại bước 2   KẾT THÚC
```

---

## 5.2. Giải thuật chi tiết (Pseudocode)

```
ALGORITHM Linear_Regression_Training:

INPUT:
    - Dữ liệu huấn luyện: {(x_1, y_1), (x_2, y_2), ..., (x_n, y_n)}
    - Tốc độ học: η

OUTPUT:
    - Tham số tối ưu: w*, b*

STEPS:
    1. Khởi tạo w, b ngẫu nhiên (ví dụ: w = 10, b = 5)
    2. FOR mỗi mẫu (x_i, y_i) trong dữ liệu:
        (a) Tính output:     ŷ_i = w * x_i + b
        (b) Tính loss:       L = (ŷ_i - y_i)²
        (c) Tính đạo hàm:    dL/dw = 2 * x_i * (ŷ_i - y_i)
                             dL/db = 2 * (ŷ_i - y_i)
        (d) Cập nhật:        w = w - η * dL/dw
                             b = b - η * dL/db
    3. RETURN w, b
```

---

# 6. VÍ DỤ TÍNH TAY CHI TIẾT

## 6.1. Dữ liệu bài toán

**Bài toán:** Dự đoán lương nhân viên dựa trên số năm kinh nghiệm.

**Dữ liệu huấn luyện:**
| Index | $x$ (Kinh nghiệm) | $y$ (Lương - triệu VND) |
|:---:|:---:|:---:|
| 0 | 3 | 60 |
| 1 | 4 | 55 |
| 2 | 5 | 66 |
| 3 | 6 | 93 |

**Tham số ban đầu:**
- $w = 10$
- $b = 5$
- $\eta = 0.01$

---

## 6.2. Iteration 1: Mẫu (3, 60)

**Dữ liệu:** $x_0 = 3$, $y_0 = 60$

**Bước (a): Tính Output**
$$ \hat{y}_0 = w \cdot x_0 + b = 10 \times 3 + 5 = 35 $$

**Bước (b): Tính Loss**
$$ L = (\hat{y}_0 - y_0)^2 = (35 - 60)^2 = (-25)^2 = 625 $$

> [!WARNING]
> Loss = 625 là rất cao! Mô hình dự đoán quá thấp so với thực tế (35 triệu vs 60 triệu).

**Bước (c): Tính Đạo hàm**
$$ \frac{\partial L}{\partial w} = 2 \times x_0 \times (\hat{y}_0 - y_0) = 2 \times 3 \times (35 - 60) = 6 \times (-25) = -150 $$
$$ \frac{\partial L}{\partial b} = 2 \times (\hat{y}_0 - y_0) = 2 \times (-25) = -50 $$

**Bước (d): Cập nhật tham số**
$$ w_{new} = w - \eta \cdot \frac{\partial L}{\partial w} = 10 - 0.01 \times (-150) = 10 + 1.5 = 11.5 $$
$$ b_{new} = b - \eta \cdot \frac{\partial L}{\partial b} = 5 - 0.01 \times (-50) = 5 + 0.5 = 5.5 $$

**✅ Kết quả sau Iteration 1:** $w = 11.5$, $b = 5.5$

---

## 6.3. Iteration 2: Mẫu (4, 55)

**Dữ liệu:** $x_1 = 4$, $y_1 = 55$
**Tham số hiện tại:** $w = 11.5$, $b = 5.5$

**Bước (a): Tính Output**
$$ \hat{y}_1 = 11.5 \times 4 + 5.5 = 46 + 5.5 = 51.5 $$

**Bước (b): Tính Loss**
$$ L = (51.5 - 55)^2 = (-3.5)^2 = 12.25 $$

> [!NOTE]
> Loss giảm từ 625 xuống còn 12.25! Mô hình đang học tốt.

**Bước (c): Tính Đạo hàm**
$$ \frac{\partial L}{\partial w} = 2 \times 4 \times (51.5 - 55) = 8 \times (-3.5) = -28 $$
$$ \frac{\partial L}{\partial b} = 2 \times (-3.5) = -7 $$

**Bước (d): Cập nhật tham số**
$$ w_{new} = 11.5 - 0.01 \times (-28) = 11.5 + 0.28 = 11.78 $$
$$ b_{new} = 5.5 - 0.01 \times (-7) = 5.5 + 0.07 = 5.57 $$

**✅ Kết quả sau Iteration 2:** $w = 11.78$, $b = 5.57$

---

## 6.4. Iteration 3: Mẫu (5, 66)

**Dữ liệu:** $x_2 = 5$, $y_2 = 66$
**Tham số hiện tại:** $w = 11.78$, $b = 5.57$

**Bước (a): Tính Output**
$$ \hat{y}_2 = 11.78 \times 5 + 5.57 = 58.9 + 5.57 = 64.47 $$

**Bước (b): Tính Loss**
$$ L = (64.47 - 66)^2 = (-1.53)^2 \approx 2.34 $$

**Bước (c): Tính Đạo hàm**
$$ \frac{\partial L}{\partial w} = 2 \times 5 \times (-1.53) = -15.3 $$
$$ \frac{\partial L}{\partial b} = 2 \times (-1.53) = -3.06 $$

**Bước (d): Cập nhật tham số**
$$ w_{new} = 11.78 - 0.01 \times (-15.3) = 11.78 + 0.153 = 11.933 $$
$$ b_{new} = 5.57 - 0.01 \times (-3.06) = 5.57 + 0.0306 = 5.6006 $$

**✅ Kết quả sau Iteration 3:** $w = 11.933$, $b = 5.6006$

---

## 6.5. Iteration 4: Mẫu (6, 93)

**Dữ liệu:** $x_3 = 6$, $y_3 = 93$
**Tham số hiện tại:** $w = 11.933$, $b = 5.6006$

**Bước (a): Tính Output**
$$ \hat{y}_3 = 11.933 \times 6 + 5.6006 = 71.598 + 5.6006 = 77.1986 $$

**Bước (b): Tính Loss**
$$ L = (77.1986 - 93)^2 = (-15.8014)^2 \approx 249.68 $$

> [!WARNING]
> Loss tăng lên vì dữ liệu này có độ lệch lớn so với xu hướng chung.

**Bước (c): Tính Đạo hàm**
$$ \frac{\partial L}{\partial w} = 2 \times 6 \times (-15.8014) \approx -189.62 $$
$$ \frac{\partial L}{\partial b} = 2 \times (-15.8014) \approx -31.60 $$

**Bước (d): Cập nhật tham số**
$$ w_{new} = 11.933 - 0.01 \times (-189.62) = 11.933 + 1.8962 = 13.8292 $$
$$ b_{new} = 5.6006 - 0.01 \times (-31.60) = 5.6006 + 0.316 = 5.9166 $$

**✅ Kết quả sau Iteration 4:** $w = 13.8292$, $b = 5.9166$

---

## 6.6. Kiểm chứng kết quả

**Câu hỏi:** Dự đoán lương cho nhân viên 7 năm kinh nghiệm?

**Với tham số cuối cùng:** $w = 13.8292$, $b = 5.9166$

$$ \hat{y} = 13.8292 \times 7 + 5.9166 = 96.8044 + 5.9166 \approx 102.72 \text{ (triệu VND)} $$

**So sánh Loss trước và sau huấn luyện:**
| Thời điểm | Tham số | Dự đoán (7 năm) | Loss (giả sử thực tế = 100) |
|:---|:---:|:---:|:---:|
| **Trước huấn luyện** | $w=10, b=5$ | $10 \times 7 + 5 = 75$ | $(75-100)^2 = 625$ |
| **Sau huấn luyện** | $w=13.83, b=5.92$ | $\approx 102.72$ | $(102.72-100)^2 \approx 7.4$ |

> [!IMPORTANT]
> **Kết luận:** Loss giảm từ **625** xuống còn **7.4** (giảm ~98.8%)! Mô hình đã học được quy luật từ dữ liệu.

---

# 7. BẢNG TỔNG HỢP & MẸO THI

## 7.1. Bảng tổng hợp công thức

| Công thức | Ký hiệu | Ý nghĩa |
|:---|:---:|:---|
| **Phương trình dự đoán** | $\hat{y} = wx + b$ | Tính giá trị dự đoán |
| **Hàm Loss (Squared Error)** | $L = (\hat{y} - y)^2$ | Đo độ sai lệch |
| **Đạo hàm theo w** | $\frac{\partial L}{\partial w} = 2x(\hat{y}-y)$ | Hướng điều chỉnh w |
| **Đạo hàm theo b** | $\frac{\partial L}{\partial b} = 2(\hat{y}-y)$ | Hướng điều chỉnh b |
| **Cập nhật w** | $w = w - \eta \cdot \frac{\partial L}{\partial w}$ | Điều chỉnh trọng số |
| **Cập nhật b** | $b = b - \eta \cdot \frac{\partial L}{\partial b}$ | Điều chỉnh độ lệch |

---

## 7.2. Mẹo bấm máy tính Casio

> [!TIP]
> **Mẹo 1:** Lưu giá trị $w$ vào biến **A** và $b$ vào biến **B** để dễ dàng tính toán lặp đi lặp lại.

> [!TIP]
> **Mẹo 2:** Khi tính $(\hat{y} - y)$, hãy tính và lưu vào biến **C** vì giá trị này dùng chung cho cả hai công thức đạo hàm.

> [!TIP]
> **Mẹo 3:** Bấm máy theo công thức đã sắp xếp:
> 1. $\hat{y} = A \times x + B$ → Lưu vào **D**
> 2. $error = D - y$ → Lưu vào **C**
> 3. $dL/dw = 2 \times x \times C$
> 4. $dL/db = 2 \times C$
> 5. $A_{new} = A - \eta \times (dL/dw)$
> 6. $B_{new} = B - \eta \times (dL/db)$

---

## 7.3. Các lỗi thường gặp khi làm bài

| Lỗi | Nguyên nhân | Cách khắc phục |
|:---|:---|:---|
| Quên dấu trừ trong công thức cập nhật | Nhầm công thức | Nhớ: "Trừ đi để xuống đồi" |
| Nhầm lẫn $\hat{y}$ và $y$ | Không phân biệt | $\hat{y}$ = Dự đoán, $y$ = Thực tế |
| Quên nhân 2 trong đạo hàm | Đạo hàm sai | Luôn có hệ số 2 từ bình phương |
| Nhầm đạo hàm w và b | Không nhớ công thức | $w$ nhân thêm $x$, $b$ không nhân |
| Sai learning rate | Không đọc kỹ đề | Kiểm tra $\eta$ trước khi tính |

---

*Hết phần Giải thích đơn giản - Hồi quy tuyến tính*
