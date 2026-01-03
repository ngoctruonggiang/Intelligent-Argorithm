# NỘI DUNG SLIDE: CHƯƠNG 6 - HỒI QUY TUYẾN TÍNH

## Slide 1
**Tiêu đề:** HỒI QUY TUYẾN TÍNH
**Nội dung:** (Trang bìa, chỉ có tiêu đề)

---

## Slide 2
**Tiêu đề:** Nội dung
**Danh sách:**
- Giới thiệu
- Bài toán hồi quy
- Ví dụ

---

## Slide 3
**Tiêu đề:** 1. Giới thiệu
**Nội dung:**
- **Hồi quy tuyến tính:** Là một phương pháp thống kê để hồi quy dữ liệu với biến phụ thuộc có giá trị liên tục trong khi các biến độc lập có thể có một trong hai giá trị liên tục hoặc là giá trị phân loại.
- Nói cách khác: "Hồi quy tuyến tính" là một phương pháp để dự đoán biến phụ thuộc (Y) dựa trên giá trị của biến độc lập (X).

---

## Slide 4
**Tiêu đề:** 1. Giới thiệu
**Nội dung:**
- **Ví dụ:** Xây dựng một chương trình tự động dự đoán tiền lương của nhân viên dựa trên số năm kinh nghiệm của họ.
- **Biểu đồ:** Trục tung là Salary (Million VND), trục hoành là Experience (Year). Các điểm dữ liệu phân bố theo xu hướng tăng dần.
- **Bảng dữ liệu:**
    | Experience | Salary |
    |---|---|
    | 3 | 60 |
    | 4 | 55 |
    | 5 | 66 |
    | 6 | 93 |
    | 7 | ? |

---

## Slide 5
**Tiêu đề:** 1. Giới thiệu
**Nội dung:**
- **Nhận xét:** Khi kẻ một đường qua một điểm dữ liệu - phương trình đường thẳng này có thể dùng để dự đoán chính xác tiền lương của nhân viên ứng với số năm kinh nghiệm của họ.
- **Hình ảnh:** Một đường thẳng màu đỏ đi qua các điểm dữ liệu.
- **Phương trình trên hình:** $Salary = w \times Experience + b$

---

## Slide 6
**Tiêu đề:** 1. Giới thiệu
**Nội dung:**
- Với một đường thẳng bất kỳ, ta có thể dùng nó để dự đoán tiền lương.
- Xét một phương trình đường thẳng $f(x) = wx + b$: mỗi đường thẳng khác nhau sẽ có số $w$ và $b$ khác nhau.
- **Hình ảnh:** Có 3 đường thẳng khác nhau (Tím, Đỏ, Vàng) cùng vẽ trên biểu đồ ban đầu, thể hiện các cách dự đoán khác nhau.
    - Tím: $Salary = w_1 \times Experience + b_1$ (?)
    - Đỏ: $Salary = w_2 \times Experience + b_2$ (?)
    - Vàng: $Salary = w_3 \times Experience + b_3$ (?)

---

## Slide 7
**Tiêu đề:** 1. Giới thiệu
**Nội dung:**
- **Câu hỏi:** Với các điểm dữ liệu cho trước, liệu có thể vẽ một đường thẳng xấp xỉ gần đúng nhất không? => Đường hồi quy.
- Để tìm đường thẳng xấp xỉ tối ưu nhất => Khoảng cách từ các điểm đến đường thẳng phải ngắn nhất.
- Gọi **Loss** là tổng các khoảng cách này.
- **Hình ảnh:** Các điểm dữ liệu và một đường thẳng tím. Các đoạn nét đứt đỏ ($error_1, error_2, ...$) thể hiện khoảng cách từ điểm đến đường thẳng.

---

## Slide 8
**Tiêu đề:** 1. Giới thiệu
**Nội dung:**
- **Làm thế nào để giảm loss:**
- Xét phương trình đường thẳng (PTĐT): $y = wx + b$
- Với $x$ là cố định (dữ liệu đầu vào) => Chỉ có thể thay đổi 2 giá trị $w$ và $b$.

---

## Slide 9
**Tiêu đề:** 1. Giới thiệu (Hình ảnh Loss vs Weight and Bias)
**Nội dung:**
- Khi giá trị $w$ và $b$ thay đổi dần theo hướng "tích cực" thì loss sẽ giảm dần.
- Khi $w$ và $b$ phù hợp sẽ tạo ra đường thẳng tối ưu nhất và loss nhỏ nhất.
- **Ví dụ trong hình:** $y = 13.47x + 5.58$ với $w=13.47, b=5.58$ thì có loss nhỏ nhất ($loss=300$).
- **Biểu đồ:** Biểu diễn việc giảm Loss khi thay đổi phương trình đường thẳng.

---

## Slide 10
**Tiêu đề:** 1. Giới thiệu
**Nội dung:**
- **Nhiệm vụ:** Tìm $w$ và $b$ để giá trị loss là nhỏ nhất.
- **Phương trình khoảng cách:** $loss = (f(x_i) - y_i)^2 = ((wx_i + b) - y_i)^2$
    - $y_i$: giá trị đúng (nhãn).
    - $f(x_i)$: giá trị dự đoán.
- Để tìm $b$ tối ưu, ta cố định $w$ và chỉ thay đổi $b$.
- **Mối quan hệ:** Giữa loss và $b$ là một hàm bậc 2 (Parabol).

---

## Slide 11
**Tiêu đề:** 1. Giới thiệu
**Nội dung:**
- Hàm loss là một đường Parabol, vị trí cực tiểu biểu trưng cho giá trị loss nhỏ nhất.
- Nếu tìm được giá trị $b$ tại điểm cực tiểu này, ta sẽ tìm được đường thẳng có loss thấp nhất.
- **Hình ảnh:** Đồ thị Parabol thể hiện mối quan hệ giữa Loss (trục tung) và $b$ (trục hoành).

---

## Slide 12
**Tiêu đề:** 1. Giới thiệu
**Nội dung:**
- Nếu coi giá trị bias ban đầu là một điểm nằm trên hàm loss, làm cách nào để di chuyển điểm đó tiến về phía cực tiểu?
- **Hình ảnh:** Một viên bi màu đỏ trên đồ thị Parabol đang lăn xuống đáy (cực tiểu).

---

## Slide 13
**Tiêu đề:** 1. Giới thiệu
**Nội dung:**
- Để thực hiện, ta có thể sử dụng công cụ **đạo hàm** (giá trị đạo hàm tại một vị trí cho biết độ dốc của hàm tại điểm đó).
- **Công thức:** $\frac{d}{dx}y(x) = \lim_{\Delta x \to 0} \frac{y(x + \Delta x) - y(x)}{\Delta x}$
- **Hình ảnh:** Minh họa đường tiếp tuyến và độ dốc (slope). Nếu dốc xuống ($\frac{d}{dx} < 0$), nếu dốc lên ($\frac{d}{dx} > 0$).

---

## Slide 14
**Tiêu đề:** 1. Giới thiệu
**Nội dung:**
- Nếu giá trị đạo hàm dương => hàm số đang tăng => điểm cực tiểu nằm bên trái => **đi ngược về hướng đạo hàm**.
- **Hình ảnh:** Minh họa việc di chuyển điểm $b$ về phía cực tiểu bằng cách đi ngược dấu đạo hàm.

---

## Slide 15
**Tiêu đề:** 1. Giới thiệu
**Nội dung:**
- Tiếp tục di chuyển ngược hướng đạo hàm.
- Dần dần điểm $b$ sẽ tiến gần đến điểm cực tiểu (Loss nhỏ nhất).
- Đây chính là nguyên lý của thuật toán **Gradient Descent** (Xuống đồi).

---

## Slide 16
**Tiêu đề:** 2. Bài toán hồi quy
**Nội dung:**
- Với các điểm dữ liệu có sẵn, thực hiện tính đạo hàm $b$ tại điểm đang xét và cập nhật lại giá trị $b$.
- Điều này dẫn đến việc tìm được đường thẳng tối ưu cho bài toán hồi quy (dự đoán tiền lương).

---

## Slide 17
**Tiêu đề:** 2. Bài toán hồi quy
**Nội dung:**
- **Quy trình tính toán (Pipeline):**
    1. Khởi tạo $w$ và $b$ ngẫu nhiên.
    2. Lấy mẫu dữ liệu từ "Dữ liệu huấn luyện".
    3. Tính Output $\hat{y}$.
    4. Tính Loss.
    5. Tính đạo hàm riêng cho từng tham số.
    6. Cập nhật tham số.
    7. Quay lại bước 2 (Vòng lặp).

---

## Slide 18
**Tiêu đề:** 2. Bài toán hồi quy
**Nội dung:**
- **Giải thuật chi tiết:**
    1. Khởi tạo ngẫu nhiên $w$ và $b$.
    2. Với mỗi mẫu dữ liệu thứ $i$:
        (a) Dự đoán output: $\hat{y}_i = f(x_i) = w x_i + b$
        (b) Tính sự chênh lệch (Loss): $L(\hat{y}_i, y_i) = (\hat{y}_i - y_i)^2$
        (c) Tìm giá trị đạo hàm tại mẫu $i$ để cập nhật $w, b$:
            - $\frac{\partial L}{\partial b} = 2(\hat{y}_i - y_i)$
            - $\frac{\partial L}{\partial w} = 2x_i(\hat{y}_i - y_i)$

---

## Slide 19
**Tiêu đề:** 2. Bài toán hồi quy
**Nội dung:**
- (d) Cập nhật giá trị mới cho hai tham số với công thức:
    - $w = w - \eta \frac{\partial L}{\partial w}$
    - $b = b - \eta \frac{\partial L}{\partial b}$
- Với $\eta$ là hằng số **learning rate** (tốc độ học).
- Lặp lại bước 2 cho đến khi xử lý hết các mẫu dữ liệu.

---

## Slide 20
**Tiêu đề:** 3. Ví dụ
**Nội dung:**
- **Bài toán:** Xây dựng hàm dự đoán tiền lương dựa theo số năm kinh nghiệm.
- **Dữ liệu:**
    | Index | Experience | Salary (.million VND) |
    |---|---|---|
    | 0 | 3 | 60 |
    | 1 | 4 | 55 |
    | 2 | 5 | 66 |
    | 3 | 6 | 93 |

---

## Slide 21
**Tiêu đề:** 3. Ví dụ
**Nội dung:**
1. Khởi tạo: $w = 10$, $b = 5$, $\eta = 0.01$.
2. Áp dụng công thức dự đoán và tính loss.
3. Thử dự đoán cho nhân viên 7 năm kinh nghiệm:
    - $\hat{y} = 10 \times 7 + 5 = 75$ (triệu).
    - Giả sử lương thực tế là 100 -> Loss = $(75 - 100)^2 = 625$. -> Giá trị loss cao.
4. Cần điều chỉnh $w$ và $b$ để cải thiện.

---

## Slide 22
**Tiêu đề:** 3. Ví dụ
**Nội dung:**
- Duyệt qua mẫu dữ liệu thứ 0 ($x_0=3, y_0=60$).
- (a) Output: $\hat{y}_0 = 3 \times 10 + 5 = 35$.
- (b) Loss: $L = (35 - 60)^2 = 625$.
- **Hình ảnh:** Sơ đồ minh họa quá trình tính Forward qua Model ($w=10, b=5$) ra output 35 và tính Loss.

---

## Slide 23
**Tiêu đề:** 3. Ví dụ
**Nội dung:**
- Hình ảnh tiếp tục minh họa sơ đồ tính toán.
- (Lưu ý: Trên hình vẽ các hộp parameters có giá trị $w=11.5$ và $b=5.5$, đây là giá trị SAU khi cập nhật ở bước tiếp theo, hình ảnh này có thể minh họa cho kết quả sau bước update).

---

## Slide 24
**Tiêu đề:** 3. Ví dụ
**Nội dung:**
- (c) Tính đạo hàm:
    - $\frac{\partial L}{\partial w} = 2 \times 3 \times (35 - 60) = -150$
    - $\frac{\partial L}{\partial b} = 2 \times (35 - 60) = -50$
- (d) Cập nhật tham số:
    - $w = 10 - 0.01 \times (-150) = 11.5$
    - $b = 5 - 0.01 \times (-50) = 5.5$
- **Kết quả:** Sau khi cập nhật, bộ tham số mới là $w=11.5$ và $b=5.5$.

---

## Slide 25
**Tiêu đề:** 3. Ví dụ
**Nội dung:**
- 3. Lặp lại cho mẫu dữ liệu tiếp theo ($x_1=4, y_1=55$).
- (a) Output: $\hat{y}_1 = 4 \times 11.5 + 5.5 = 51.5$.
- (b) Loss: $L = (51.5 - 55)^2 = 12.25$.
- **Hình ảnh:** Sơ đồ minh họa quá trình tính Forward qua Model ($w=11.5, b=5.5$).

---

## Slide 26
**Tiêu đề:** 3. Ví dụ
**Nội dung:**
- Sơ đồ tiếp tục, hiển thị giá trị tham số cập nhật kế tiếp là $w=11.78, b=5.57$.

---

## Slide 27
**Tiêu đề:** 3. Ví dụ
**Nội dung:**
- (c) Tính đạo hàm tại mẫu 1:
    - $\frac{\partial L}{\partial w} = -28$.
    - $\frac{\partial L}{\partial b} = -7$.
- (d) Cập nhật tham số:
    - $w = 11.5 - 0.01 \times (-28) = 11.78$
    - $b = 5.5 - 0.01 \times (-7) = 5.57$
- **Kết quả:** Bộ tham số mới là $w=11.78$ và $b=5.57$.

---

## Slide 28
**Tiêu đề:** 3. Ví dụ
**Nội dung:**
- 4. Thực hiện tương tự với mẫu dữ liệu ($x_2=5, y_2=66$).
- (a) Output: $\hat{y}_2 = 5 \times 11.78 + 5.57 = 64.47$.
- (b) Loss: $L = (64.47 - 66)^2 = 2.3409$.
- (c) Tính đạo hàm:
    - $\frac{\partial L}{\partial w} = -15.3$.
    - $\frac{\partial L}{\partial b} = -3.06$.

---

## Slide 29
**Tiêu đề:** 3. Ví dụ
**Nội dung:**
- (d) Cập nhật tham số:
    - $w = 11.78 - 0.01 \times (-15.3) = 11.933$
    - $b = 5.57 - 0.01 \times (-3.06) = 5.6006$
- **Kết quả:** Bộ tham số mới là $w=11.933$ và $b=5.6006$.

---

## Slide 30
**Tiêu đề:** 3. Ví dụ
**Nội dung:**
- 5. Với mẫu dữ liệu cuối cùng ($x_3=6, y_3=93$).
- (a) Output: $\hat{y}_3 = 6 \times 11.933 + 5.6006 = 77.1986$.
- (b) Loss: $L = (77.1986 - 93)^2 = 249.6842$.
- (c) Tính đạo hàm: $w: -189.6168$, $b: -31.6028$.

---

## Slide 31
**Tiêu đề:** 3. Ví dụ
**Nội dung:**
- (d) Cập nhật tham số:
    - $w = 11.933 - 0.01 \times (-189.6168) = 13.82916$
    - $b = 5.6006 - 0.01 \times (-31.6028) = 5.916628$
- **Kết quả:** Sau khi cập nhật, bộ tham số mới là $w=13.82916$ và $b=5.916628$.

---

## Slide 32
**Tiêu đề:** 3. Ví dụ
**Nội dung:**
- 6. Sau khi duyệt qua tất cả các mẫu dữ liệu, tham số $w$ và $b$ đã được điều chỉnh phù hợp.
- **Kiểm chứng:** Dự đoán lại cho nhân viên 7 năm kinh nghiệm.
    - $\hat{y} = 13.82916 \times 7 + 5.916628 \approx 102.72$
- **Loss kiểm chứng:** $L = (102.72 - 100)^2 = 7.3984$.
- **Kết luận:** So với loss ban đầu (625), loss mới (7.3984) đã giảm đáng kể -> Mô hình đã học tốt và có thể dùng để dự đoán chính xác cao.
