# 📚 HỌC 1-1 THEO CHỦ ĐỀ: K-NEAREST NEIGHBOR (KNN)
## Phương án 3: Câu hỏi tương tác và kiểm tra hiểu biết

---

> **Phương pháp học:**
> Đọc từng phần, trả lời câu hỏi rồi mới xem đáp án. Đừng vội nhìn đáp án!

---

# 🎯 PHẦN 1: KIỂM TRA HIỂU BIẾT CƠ BẢN

## Câu 1: KNN là gì?
**Hãy giải thích bằng lời của bạn: KNN hoạt động như thế nào?**

<details>
<summary>💡 Xem gợi ý</summary>
Nghĩ về việc hỏi ý kiến những người xung quanh bạn...
</details>

<details>
<summary>✅ Xem đáp án</summary>

KNN phân loại một điểm dữ liệu mới bằng cách:
1. Tìm K điểm gần nhất với nó
2. Xem những điểm đó thuộc lớp nào
3. Gán nhãn theo đa số

**Ví dụ:** Nếu 3 người gần bạn nhất đều đội mũ đỏ, bạn có thể cũng thuộc "team đỏ"!
</details>

---

## Câu 2: Tại sao K thường là số lẻ?

<details>
<summary>✅ Xem đáp án</summary>

Để tránh trường hợp **hòa phiếu**.

**Ví dụ với K=4:**
- 2 phiếu Xanh
- 2 phiếu Đỏ
→ Không biết chọn ai!

**Với K=3 hoặc K=5:** Luôn có bên thắng!
</details>

---

## Câu 3: Lazy Learning là gì?

<details>
<summary>✅ Xem đáp án</summary>

KNN được gọi là **"lazy learning"** (học lười) vì:
- Không có giai đoạn huấn luyện (training)
- Chỉ **lưu trữ** tất cả dữ liệu
- Khi cần dự đoán mới bắt đầu **tính toán**

→ "Lười" ở chỗ không học trước, đợi đến lúc cần mới làm!
</details>

---

# 🧮 PHẦN 2: KIỂM TRA TÍNH TOÁN

## Câu 4: Tính khoảng cách

**Bài toán:** Cho A(0, 0) và B(3, 4). Tính d(A, B).

<details>
<summary>💡 Gợi ý</summary>
Đây là tam giác vuông nổi tiếng 3-4-5!
</details>

<details>
<summary>✅ Xem đáp án</summary>

```
d = √[(3-0)² + (4-0)²]
  = √[9 + 16]
  = √25
  = 5
```
</details>

---

## Câu 5: Phân loại điểm mới

**Bài toán:** Cho các điểm:
- A(0,0) - Đỏ
- B(1,1) - Đỏ
- C(4,4) - Xanh
- D(5,5) - Xanh

Điểm P(2,2) thuộc lớp nào với K=3?

<details>
<summary>💡 Gợi ý</summary>
Tính khoảng cách từ P đến A, B, C, D trước.
</details>

<details>
<summary>✅ Xem đáp án</summary>

1. d(P,A) = √8 ≈ 2.83
2. d(P,B) = √2 ≈ 1.41
3. d(P,C) = √8 ≈ 2.83
4. d(P,D) = √18 ≈ 4.24

3 điểm gần nhất: **B (Đỏ), A (Đỏ), C (Xanh)**

Đếm: 2 Đỏ > 1 Xanh → **P thuộc lớp ĐỎ**
</details>

---

# 🤔 PHẦN 3: TÌNH HUỐNG NÂNG CAO

## Câu 6: Điều gì xảy ra nếu K = N (số điểm trong tập)?

<details>
<summary>✅ Xem đáp án</summary>

Mọi điểm mới đều được gán nhãn của **lớp đa số** trong tập huấn luyện.

**Ví dụ:** Nếu tập có 70% Xanh, 30% Đỏ → Tất cả điểm mới đều được gán là Xanh!

→ KNN trở nên **vô nghĩa** vì không còn phụ thuộc vị trí.
</details>

---

## Câu 7: Khi nào KNN hoạt động kém?

<details>
<summary>✅ Xem đáp án</summary>

1. **Dữ liệu lớn:** Phải tính khoảng cách với TẤT CẢ điểm → Chậm
2. **Dữ liệu nhiều chiều:** "Curse of dimensionality" - khoảng cách mất ý nghĩa
3. **Dữ liệu có nhiễu:** Điểm sai ở gần có thể làm sai kết quả
4. **Dữ liệu mất cân bằng:** Lớp đông sẽ "lấn át" lớp ít
</details>

---

*Hết phần Học 1-1: KNN*
