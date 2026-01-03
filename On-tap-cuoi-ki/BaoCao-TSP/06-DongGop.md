# PHẦN 6: ĐÓNG GÓP CỦA NHÓM
# (Tổng kết các công việc đã thực hiện)

---

## 📚 MỤC LỤC

1. [Tổng quan công việc](#1-tổng-quan-công-việc)
2. [Chi tiết đóng góp](#2-chi-tiết-đóng-góp)
3. [Sản phẩm đầu ra](#3-sản-phẩm-đầu-ra)
4. [Hướng phát triển](#4-hướng-phát-triển)

---

# 1. TỔNG QUAN CÔNG VIỆC

## 1.1. Mục tiêu dự án

- ✅ Nghiên cứu và trình bày bài toán TSP
- ✅ Cài đặt 3 thuật toán: Brute Force, Nearest Neighbor, Genetic Algorithm
- ✅ Thực nghiệm trên nhiều bộ dữ liệu
- ✅ So sánh và đánh giá các thuật toán

## 1.2. Kết quả đạt được

| Mục tiêu | Trạng thái |
|:---|:---:|
| Giới thiệu bài toán TSP | ✅ Hoàn thành |
| Mô tả dữ liệu và tiền xử lý | ✅ Hoàn thành |
| Cài đặt 3 thuật toán | ✅ Hoàn thành |
| Đánh giá độ phức tạp | ✅ Hoàn thành |
| Thực nghiệm và phân tích | ✅ Hoàn thành |

---

# 2. CHI TIẾT ĐÓNG GÓP

## 2.1. Nghiên cứu lý thuyết

- Tìm hiểu định nghĩa và lịch sử bài toán TSP
- Phân loại các phương pháp giải (Exact, Heuristic, Metaheuristic)
- Nghiên cứu độ phức tạp NP-hard của bài toán

## 2.2. Cài đặt thuật toán

| Thuật toán | Nội dung cài đặt |
|:---|:---|
| **Brute Force** | Duyệt hoán vị với itertools.permutations |
| **Nearest Neighbor** | Thuật toán tham lam với tối ưu điểm xuất phát |
| **Genetic Algorithm** | Toàn bộ GA: Selection, Crossover (OX), Mutation |

## 2.3. Thực nghiệm

- Tạo bộ dữ liệu test ngẫu nhiên (10, 20 thành phố)
- Sử dụng dữ liệu chuẩn TSPLIB (berlin52, kroA100)
- Chạy thực nghiệm 10 lần, thống kê kết quả

## 2.4. Phân tích và báo cáo

- So sánh chất lượng nghiệm (Gap)
- Phân tích thời gian chạy
- Đánh giá ưu nhược điểm từng thuật toán

---

# 3. SẢN PHẨM ĐẦU RA

## 3.1. Tài liệu báo cáo

| File | Nội dung | Số trang ước tính |
|:---|:---|:---:|
| `01-GioiThieu.md` | Giới thiệu bài toán TSP | ~6 trang |
| `02-DuLieu.md` | Dữ liệu và tiền xử lý | ~8 trang |
| `03-ThuatToan.md` | 3 thuật toán chi tiết | ~12 trang |
| `04-DanhGia.md` | Độ đo và đánh giá | ~4 trang |
| `05-ThucNghiem.md` | Kết quả thực nghiệm | ~6 trang |
| `06-DongGop.md` | Đóng góp của nhóm | ~2 trang |

**Tổng cộng:** ~38 trang

## 3.2. Code nguồn

- `brute_force_tsp.py` - Thuật toán vét cạn
- `nearest_neighbor_tsp.py` - Thuật toán hàng xóm gần nhất
- `genetic_algorithm_tsp.py` - Giải thuật di truyền
- `utils.py` - Các hàm tiện ích (đọc file, tính khoảng cách)

---

# 4. HƯỚNG PHÁT TRIỂN

## 4.1. Cải tiến thuật toán

- **GA:** Thêm các toán tử crossover khác (PMX, CX)
- **Hybrid:** Kết hợp NN làm khởi tạo cho GA
- **2-opt:** Thêm local search để cải thiện nghiệm

## 4.2. Mở rộng bài toán

- **CVRP:** Capacitated Vehicle Routing Problem (có ràng buộc tải trọng)
- **TSP động:** Thành phố xuất hiện/mất đi theo thời gian
- **Multi-depot TSP:** Nhiều điểm xuất phát

## 4.3. Công cụ hỗ trợ

- Xây dựng **giao diện đồ họa** visualize tour
- Phát triển **web app** cho người dùng thử nghiệm
- Tích hợp với **Google Maps API** cho ứng dụng thực tế

---

> [!NOTE]
> **Kết luận:** Báo cáo đã trình bày đầy đủ bài toán TSP từ lý thuyết đến thực nghiệm, so sánh 3 thuật toán phổ biến và rút ra các nhận xét hữu ích cho việc lựa chọn phương pháp giải phù hợp.

---

*Hết Phần 6 - Đóng góp của nhóm*

---

# 📎 PHỤ LỤC: DANH SÁCH TÀI LIỆU THAM KHẢO

1. TSPLIB: http://comopt.ifi.uni-heidelberg.de/software/TSPLIB95/
2. Applegate, D. L., et al. (2006). The Traveling Salesman Problem: A Computational Study.
3. Michalewicz, Z. (1996). Genetic Algorithms + Data Structures = Evolution Programs.
4. Cormen, T. H., et al. (2009). Introduction to Algorithms (3rd Edition).

---

*Hết báo cáo nghiên cứu bài toán TSP*
