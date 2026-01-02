# 📚 TỔNG HỢP KIẾN THỨC: K-NEAREST NEIGHBOR (KNN)
## Phương án 5: Kết hợp tất cả - Tài liệu in ấn

---

# 📌 PHẦN 1: TÓM TẮT LÝ THUYẾT

## 1.1. Định nghĩa
**KNN (K-Nearest Neighbor)** là thuật toán phân loại dựa trên việc tìm K điểm dữ liệu gần nhất, sau đó gán nhãn theo **đa số phiếu bầu**.

## 1.2. Đặc điểm chính
| Đặc điểm | Mô tả |
|----------|-------|
| **Loại** | Supervised Learning (Học có giám sát) |
| **Phương pháp** | Instance-based / Lazy Learning |
| **Không huấn luyện** | Chỉ lưu trữ dữ liệu |
| **Tham số chính** | K (số láng giềng) |

---

# 📌 PHẦN 2: CÔNG THỨC QUAN TRỌNG

## 2.1. Khoảng cách Euclidean

### Công thức 2D:
$$d(A, B) = \sqrt{(x_2-x_1)^2 + (y_2-y_1)^2}$$

### Công thức nD:
$$d(A, B) = \sqrt{\sum_{i=1}^{n}(b_i - a_i)^2}$$

---

# 📌 PHẦN 3: BẢNG TRA CỨU CĂN BẬC 2

| Số | √ | | Số | √ |
|:--:|:-:|:-:|:--:|:-:|
| 1 | 1.00 | | 10 | 3.16 |
| 2 | 1.41 | | 13 | 3.61 |
| 3 | 1.73 | | 16 | 4.00 |
| 4 | 2.00 | | 17 | 4.12 |
| 5 | 2.24 | | 18 | 4.24 |
| 6 | 2.45 | | 20 | 4.47 |
| 7 | 2.65 | | 25 | 5.00 |
| 8 | 2.83 | | 32 | 5.66 |
| 9 | 3.00 | | 50 | 7.07 |

---

# 📌 PHẦN 4: QUY TRÌNH LÀM BÀI

## ✅ Checklist 5 bước

- [ ] **Bước 1:** Đọc đề, xác định **tọa độ điểm mới** và **K**
- [ ] **Bước 2:** Lập bảng tính khoảng cách từ điểm mới đến TẤT CẢ các điểm
- [ ] **Bước 3:** Sắp xếp khoảng cách từ **BÉ đến LỚN**
- [ ] **Bước 4:** Chọn **K điểm** có khoảng cách nhỏ nhất
- [ ] **Bước 5:** Đếm nhãn, gán theo **ĐA SỐ**

---

# 📌 PHẦN 5: VÍ DỤ MẪU (ĐỀ THI)

**Đề:** Cho các điểm: A(0,0)-Đỏ, B(1,0)-Đỏ, C(3,3)-Xanh, D(4,3)-Xanh. Với K=3, điểm P(2,1) thuộc lớp nào?

**Giải:**

| Điểm | Công thức | d |
|:----:|:---------:|:-:|
| A | √(4+1) | **√5 ≈ 2.24** |
| B | √(1+1) | **√2 ≈ 1.41** |
| C | √(1+4) | **√5 ≈ 2.24** |
| D | √(4+4) | **√8 ≈ 2.83** |

**3 điểm gần nhất:** B(1.41), A(2.24), C(2.24)
**Đếm:** Đỏ = 2, Xanh = 1
**→ P thuộc lớp ĐỎ** ✅

---

# 📌 PHẦN 6: LƯU Ý QUAN TRỌNG

> ⚠️ **Chọn K là số LẺ** để tránh hòa phiếu
> 
> ⚠️ **K quá nhỏ** → Nhạy với nhiễu
> 
> ⚠️ **K quá lớn** → Mất thông tin vị trí

---

*Hết tổng hợp KNN - In mang vào phòng thi*
