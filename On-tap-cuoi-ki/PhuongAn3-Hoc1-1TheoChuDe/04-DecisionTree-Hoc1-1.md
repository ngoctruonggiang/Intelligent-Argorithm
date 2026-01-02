# 📚 HỌC 1-1 THEO CHỦ ĐỀ: CÂY QUYẾT ĐỊNH (ID3)
## Phương án 3: Câu hỏi tương tác và kiểm tra hiểu biết

---

> **Phương pháp học:**
> Đọc câu hỏi → Suy nghĩ → Trả lời → Xem đáp án
> Đừng vội nhìn đáp án trước khi suy nghĩ!

---

# 🎯 PHẦN 1: KIỂM TRA HIỂU BIẾT CƠ BẢN

## Câu 1: Entropy nghĩa là gì?
**Trong ngữ cảnh Decision Tree, Entropy đo lường điều gì?**

<details>
<summary>💡 Xem gợi ý</summary>
Nghĩ về độ "hỗn loạn" hoặc "không chắc chắn" của dữ liệu...
</details>

<details>
<summary>✅ Xem đáp án</summary>

**Entropy** đo lường **độ hỗn loạn** (impurity) của tập dữ liệu:
- **Entropy = 0:** Dữ liệu hoàn toàn thuần nhất (tất cả cùng lớp)
- **Entropy = 1:** Dữ liệu hoàn toàn hỗn loạn (50-50)

**Mục tiêu của ID3:** Giảm Entropy càng nhanh càng tốt!
</details>

---

## Câu 2: Entropy = 0 có ý nghĩa gì?

<details>
<summary>✅ Xem đáp án</summary>

**Entropy = 0** nghĩa là tập dữ liệu **hoàn toàn thuần nhất**.

**Ví dụ:**
- 10 người, tất cả đều "Đồng ý" → Entropy = 0
- 10 người, tất cả đều "Không đồng ý" → Entropy = 0

Khi đạt Entropy = 0, ta **dừng chia** và tạo nút lá.
</details>

---

## Câu 3: Information Gain là gì?

<details>
<summary>✅ Xem đáp án</summary>

**Information Gain** đo lường **mức độ giảm Entropy** khi chia dữ liệu theo một thuộc tính.

**Công thức:**
```
Gain = Entropy(trước chia) - Entropy(sau chia)
```

**Gain CAO = Thuộc tính TỐT** → Nên chọn làm nút!
</details>

---

## Câu 4: Tại sao chọn thuộc tính có Gain cao nhất?

<details>
<summary>✅ Xem đáp án</summary>

Vì Gain cao nghĩa là:
1. Giảm Entropy nhiều nhất
2. Phân loại dữ liệu tốt nhất
3. Cây sẽ ngắn hơn, đơn giản hơn

**Ví dụ:** Nếu hỏi "Có mưa không?" mà 100% người trả lời "Có" đều không đi chơi → Câu hỏi rất tốt (Gain cao)!
</details>

---

# 🧮 PHẦN 2: KIỂM TRA TÍNH TOÁN

## Câu 5: Tính Entropy

**Bài toán:** Tập S có 6 mẫu "Yes" và 6 mẫu "No". Entropy(S) = ?

<details>
<summary>💡 Gợi ý</summary>
Đây là trường hợp 50-50...
</details>

<details>
<summary>✅ Xem đáp án</summary>

- p(Yes) = 6/12 = 0.5
- p(No) = 6/12 = 0.5
- log₂(0.5) = -1

```
Entropy = -0.5 × (-1) - 0.5 × (-1)
        = 0.5 + 0.5
        = 1
```

**Đáp án: Entropy = 1** (hỗn loạn nhất)
</details>

---

## Câu 6: Tính Entropy (nâng cao)

**Bài toán:** Tập S có 8 mẫu "Yes" và 2 mẫu "No". Entropy(S) ≈ ?

<details>
<summary>💡 Gợi ý</summary>
p(Yes) = 0.8, p(No) = 0.2
</details>

<details>
<summary>✅ Xem đáp án</summary>

- p(Yes) = 8/10 = 0.8
- p(No) = 2/10 = 0.2

Tra bảng:
- -0.8 × log₂(0.8) ≈ 0.258
- -0.2 × log₂(0.2) ≈ 0.464

```
Entropy ≈ 0.258 + 0.464 = 0.72
```

**Đáp án: Entropy ≈ 0.72**
</details>

---

## Câu 7: So sánh Gain

**Bài toán:** Cho Entropy(S) = 1. Hai thuộc tính chia như sau:
- Thuộc tính A: Tạo 2 nhánh, mỗi nhánh có Entropy = 0.5
- Thuộc tính B: Tạo 2 nhánh, mỗi nhánh có Entropy = 0

Thuộc tính nào tốt hơn?

<details>
<summary>✅ Xem đáp án</summary>

**Thuộc tính A:**
```
Gain(A) = 1 - (0.5×0.5 + 0.5×0.5) = 1 - 0.5 = 0.5
```

**Thuộc tính B:**
```
Gain(B) = 1 - (0.5×0 + 0.5×0) = 1 - 0 = 1
```

**Đáp án: Thuộc tính B tốt hơn** (Gain = 1 > 0.5)

B tạo ra các nhánh thuần nhất ngay lập tức!
</details>

---

# 🤔 PHẦN 3: TÌNH HUỐNG NÂNG CAO

## Câu 8: Overfitting là gì?

<details>
<summary>✅ Xem đáp án</summary>

**Overfitting** xảy ra khi cây **quá chi tiết**, học thuộc lòng dữ liệu huấn luyện nhưng dự đoán kém trên dữ liệu mới.

**Dấu hiệu:**
- Cây có rất nhiều tầng
- Mỗi lá chỉ có 1-2 mẫu
- Độ chính xác trên tập huấn luyện rất cao nhưng trên tập test thấp

**Giải pháp:** Cắt tỉa cây (Pruning).
</details>

---

## Câu 9: Điều gì xảy ra nếu tất cả thuộc tính có Gain = 0?

<details>
<summary>✅ Xem đáp án</summary>

Điều này xảy ra khi **không có thuộc tính nào giúp phân loại tốt hơn**.

**Giải pháp:**
1. Tạo nút lá với nhãn của **lớp đa số**
2. Hoặc dừng thuật toán và chấp nhận độ chính xác hiện tại
</details>

---

*Hết phần Học 1-1: Decision Tree*
