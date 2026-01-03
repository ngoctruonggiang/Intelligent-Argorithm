# PHẦN 5: KẾT QUẢ THỰC NGHIỆM
# (Mô tả kết quả và phân tích ưu nhược điểm)

---

## 📚 MỤC LỤC

1. [Thiết lập thực nghiệm](#1-thiết-lập-thực-nghiệm)
2. [Kết quả trên bộ dữ liệu nhỏ](#2-kết-quả-trên-bộ-dữ-liệu-nhỏ)
3. [Kết quả trên bộ dữ liệu TSPLIB](#3-kết-quả-trên-bộ-dữ-liệu-tsplib)
4. [Phân tích và so sánh](#4-phân-tích-và-so-sánh)
5. [Ưu nhược điểm của từng thuật toán](#5-ưu-nhược-điểm-của-từng-thuật-toán)

---

# 1. THIẾT LẬP THỰC NGHIỆM

## 1.1. Môi trường thực nghiệm

| Thông số | Giá trị |
|:---|:---|
| **CPU** | Intel Core i5-10400 @ 2.9GHz |
| **RAM** | 16 GB DDR4 |
| **Hệ điều hành** | Windows 11 |
| **Ngôn ngữ** | Python 3.10 |
| **IDE** | VS Code |

## 1.2. Cài đặt thuật toán

| Thuật toán | Tham số |
|:---|:---|
| **Brute Force** | Không có tham số |
| **Nearest Neighbor** | Thử tất cả điểm xuất phát |
| **Genetic Algorithm** | pop_size=100, generations=500, mutation_rate=0.1 |

## 1.3. Phương pháp đo lường

- Mỗi thuật toán chạy **10 lần** (với GA)
- Ghi nhận: **Chi phí tốt nhất, trung bình, thời gian**
- Tính **Gap** so với nghiệm tối ưu (nếu biết)

---

# 2. KẾT QUẢ TRÊN BỘ DỮ LIỆU NHỎ (10 thành phố)

## 2.1. Dữ liệu test

**Nguồn:** Tự sinh ngẫu nhiên

**Nghiệm tối ưu (Brute Force):** 285.6

## 2.2. Bảng kết quả

| Thuật toán | Chi phí | Gap | Thời gian |
|:---|:---:|:---:|:---:|
| **Brute Force** | **285.6** | 0% | 0.15s |
| **Nearest Neighbor** | 342.8 | 20.0% | < 0.001s |
| **Genetic Algorithm** | 289.2 | 1.3% | 0.8s |

## 2.3. Nhận xét

- ✅ **Brute Force**: Tìm được nghiệm tối ưu, thời gian chấp nhận được với n=10
- ⚠️ **Nearest Neighbor**: Nhanh nhất nhưng Gap khá cao (20%)
- ✅ **GA**: Gap thấp (1.3%), thời gian hợp lý

---

# 3. KẾT QUẢ TRÊN BỘ DỮ LIỆU TSPLIB

## 3.1. berlin52 (52 thành phố)

**Nghiệm tối ưu đã biết:** 7,542

| Thuật toán | Chi phí tốt nhất | Chi phí TB | Gap | Thời gian |
|:---|:---:|:---:|:---:|:---:|
| **Brute Force** | - | - | - | Không khả thi |
| **Nearest Neighbor** | 8,980 | 8,980 | 19.1% | 0.01s |
| **Genetic Algorithm** | 7,698 | 7,850 | 2.1% | 15s |

## 3.2. kroA100 (100 thành phố)

**Nghiệm tối ưu đã biết:** 21,282

| Thuật toán | Chi phí tốt nhất | Chi phí TB | Gap | Thời gian |
|:---|:---:|:---:|:---:|:---:|
| **Brute Force** | - | - | - | Không khả thi |
| **Nearest Neighbor** | 26,524 | 26,524 | 24.6% | 0.05s |
| **Genetic Algorithm** | 21,890 | 22,350 | 2.9% | 45s |

## 3.3. Biểu đồ so sánh Gap

```
Gap (%)
    ^
 25%│  ████████████████████████  Nearest Neighbor
    │
 20%│
    │
 15%│
    │
 10%│
    │
  5%│
    │
  3%│  ███  Genetic Algorithm
  0%├───────────────────────────────> Thuật toán
```

---

# 4. PHÂN TÍCH VÀ SO SÁNH

## 4.1. Về chất lượng nghiệm

| Tiêu chí | Brute Force | Nearest Neighbor | Genetic Algorithm |
|:---|:---:|:---:|:---:|
| Gap trung bình | **0%** | 20-25% | 2-5% |
| Độ ổn định | Cố định | Cố định | Dao động |

**Nhận xét:**
- GA cho nghiệm **gần tối ưu** với Gap chỉ 2-5%
- NN nhanh nhưng Gap lên đến 20-25%

## 4.2. Về thời gian chạy

```
Thời gian (log scale)
    ^
100s│                          ▲ Brute Force (n>12)
    │
 10s│              ▲ GA
    │
  1s│
    │
0.1s│
    │
0.01│  ▲ NN
    +────────────────────────> Kích thước n
       10    50   100
```

## 4.3. Scalability (Khả năng mở rộng)

| n | Brute Force | Nearest Neighbor | GA |
|:---:|:---:|:---:|:---:|
| 10 | ✅ | ✅ | ✅ |
| 50 | ❌ | ✅ | ✅ |
| 100 | ❌ | ✅ | ✅ |
| 500 | ❌ | ✅ | ⚠️ Chậm |
| 1000 | ❌ | ✅ | ⚠️ Rất chậm |

---

# 5. ƯU NHƯỢC ĐIỂM CỦA TỪNG THUẬT TOÁN

## 5.1. Brute Force

| ✅ Ưu điểm | ❌ Nhược điểm |
|:---|:---|
| Đảm bảo tối ưu 100% | Chỉ dùng được với n ≤ 12 |
| Đơn giản, dễ hiểu | Độ phức tạp O(n!) |
| Làm baseline để so sánh | Không thực tế cho bài toán lớn |

## 5.2. Nearest Neighbor

| ✅ Ưu điểm | ❌ Nhược điểm |
|:---|:---|
| Rất nhanh O(n²) | Không đảm bảo tối ưu |
| Dễ cài đặt | Gap thường 20-25% |
| Mở rộng được với n lớn | Phụ thuộc điểm xuất phát |

## 5.3. Genetic Algorithm

| ✅ Ưu điểm | ❌ Nhược điểm |
|:---|:---|
| Nghiệm gần tối ưu (Gap 2-5%) | Cần tuning tham số |
| Cân bằng chất lượng/tốc độ | Kết quả không cố định (stochastic) |
| Mở rộng được với n vừa | Chậm hơn NN nhiều lần |

---

## 5.4. Kết luận tổng quát

> [!IMPORTANT]
> **Khuyến nghị sử dụng:**
> - **n ≤ 12:** Brute Force (nếu cần chính xác)
> - **n lớn, cần nhanh:** Nearest Neighbor
> - **n vừa, cần chất lượng:** Genetic Algorithm

---

*Hết Phần 5 - Kết quả thực nghiệm*
