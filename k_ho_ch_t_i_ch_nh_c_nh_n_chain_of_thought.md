# BẢN THIẾT KẾ PROMPT & KẾ HOẠCH TÀI CHÍNH CÁ NHÂN (CHAIN-OF-THOUGHT)

## 1. Mục tiêu bài toán

* **Ứng dụng Chain-of-Thought (CoT):** Buộc trợ lý AI thực hiện suy luận logic từng bước nhằm hạn chế tối đa sai sót số học khi tính toán dòng tiền biến động.

* **Kiểm soát ràng buộc:** Đảm bảo tuân thủ các nguyên tắc tài chính: tiết kiệm tối thiểu 20%, trả nợ đúng hạn, cân đối chi phí cố định và chi tiêu linh hoạt, tổng tỷ lệ phần trăm phân bổ bằng chính xác 100%.

* **Cấu trúc đầu ra trực quan:** Tách biệt rõ ràng giữa quá trình lập luận trung gian và bảng tổng hợp số liệu cuối cùng.

## 2. Thiết kế Prompt chuẩn (Dành cho AI)

```

Bối cảnh: Bạn là một chuyên gia lập kế hoạch tài chính cá nhân. Nhiệm vụ của bạn là xử lý dữ liệu tài chính của một cá nhân có thu nhập biến động, đang có nợ và các mục tiêu tiết kiệm rõ ràng để tối ưu hóa dòng tiền.

Dữ liệu đầu vào:
- Tổng thu nhập hàng tháng: [Nhập số tiền, ví dụ: 25.000.000 VNĐ]
- Chi phí cố định bắt buộc (nhà cửa, điện nước, bảo hiểm): [Nhập số tiền, ví dụ: 7.000.000 VNĐ]
- Các khoản nợ cần thanh toán tối thiểu: [Nhập số tiền, ví dụ: 4.000.000 VNĐ]
- Mục tiêu tiết kiệm: Tối thiểu 20% tổng thu nhập

Quy trình suy luận bắt buộc (Chain-of-Thought):
- Bước 1: Tính toán tổng thu nhập khả dụng sau khi trừ thuế (nếu có) và chi phí cố định bắt buộc.
- Bước 2: Phân bổ khoản tiền trả nợ tối thiểu từ phần thu nhập khả dụng.
- Bước 3: Trích lập quỹ tiết kiệm theo đúng tỷ lệ cam kết (tối thiểu 20% trên tổng thu nhập).
- Bước 4: Chia phần tiền còn lại cho chi tiêu linh hoạt (theo quy tắc 50/30/20 cải tiến) và kiểm tra tính cân đối tổng tỷ lệ phần trăm bằng đúng 100%.

Ràng buộc kỹ thuật & Định dạng đầu ra:
- Hiển thị đầy đủ các phép tính trung gian cộng, trừ, nhân, chia; tuyệt đối không nhảy cóc ra kết quả.
- Phần 1: Nhật ký suy luận logic (Reasoning Steps) chỉ ra công thức tính toán và số liệu trung gian.
- Phần 2: Bảng phân bổ ngân sách cuối cùng hiển thị dưới dạng Markdown Table gồm các cột: Hạng mục | Số tiền (VNĐ) | Tỷ lệ % | Ghi chú.

```

## 3. Kết quả triển khai thực tế (Minh họa số liệu chuẩn)

**Giả định dữ liệu đầu vào:**

* **Tổng thu nhập tháng (sau thuế):** 25.000.000 VNĐ

* **Chi phí cố định bắt buộc:** 7.000.000 VNĐ

* **Khoản trả nợ tối thiểu:** 4.000.000 VNĐ

* **Mục tiêu tiết kiệm:** 20% tổng thu nhập

### Phần 1: Nhật ký suy luận logic (Reasoning Steps)

* **Bước 1: Tính thu nhập khả dụng sau chi phí cố định bắt buộc**

  * Công thức: $\text{Thu nhập khả dụng} = \text{Tổng thu nhập} - \text{Chi phí cố định}$

  * Phép tính: $25.000.000 - 7.000.000 = 18.000.000\text{ VNĐ}$

  * Tỷ lệ chi phí cố định so với tổng thu nhập:
    

    $$
    \frac{7.000.000}{25.000.000} \times 100\% = 28\%
    $$

* **Bước 2: Phân bổ khoản tiền trả nợ tối thiểu**

  * Khoản trả nợ tối thiểu: $4.000.000\text{ VNĐ}$

  * Thu nhập còn lại sau khi trả nợ: $18.000.000 - 4.000.000 = 14.000.000\text{ VNĐ}$

  * Tỷ lệ trả nợ so với tổng thu nhập:
    

    $$
    \frac{4.000.000}{25.000.000} \times 100\% = 16\%
    $$

* **Bước 3: Trích lập quỹ tiết kiệm theo cam kết**

  * Tỷ lệ tiết kiệm mục tiêu: $20\%$ trên tổng thu nhập $25.000.000\text{ VNĐ}$

  * Phép tính: $25.000.000 \times 0.20 = 5.000.000\text{ VNĐ}$

  * Số dư tiền mặt còn lại sau khi tiết kiệm: $14.000.000 - 5.000.000 = 9.000.000\text{ VNĐ}$

* **Bước 4: Phân bổ chi tiêu linh hoạt và kiểm tra tỷ lệ 100%**

  * Số tiền dành cho chi tiêu linh hoạt (ăn uống, đi lại, giải trí, quỹ dự phòng phát sinh): $9.000.000\text{ VNĐ}$

  * Tỷ lệ chi tiêu linh hoạt so với tổng thu nhập:
    

    $$
    \frac{9.000.000}{25.000.000} \times 100\% = 36\%
    $$

  * **Kiểm tra tổng tỷ lệ phân bổ ngân sách:**
    

    $$
    \text{Chi phí cố định } (28\%) + \text{Trả nợ } (16\%) + \text{Tiết kiệm } (20\%) + \text{Chi tiêu linh hoạt } (36\%) = 100\%
    $$

    
    *Kết quả khớp chính xác tuyệt đối 100%, không có sai lệch số học.*

### Phần 2: Bảng phân bổ ngân sách cuối cùng

| Hạng mục | Số tiền (VNĐ) | Tỷ lệ % | Ghi chú | 
| ----- | ----- | ----- | ----- | 
| **Chi phí cố định** | 7.000.000 | 28% | Nhà cửa, điện nước, internet, bảo hiểm | 
| **Trả nợ tối thiểu** | 4.000.000 | 16% | Thanh toán các khoản nợ đúng hạn | 
| **Quỹ tiết kiệm** | 5.000.000 | 20% | Tích lũy và đầu tư đạt mục tiêu tối thiểu 20% | 
| **Chi tiêu linh hoạt** | 9.000.000 | 36% | Ăn uống, đi lại, sinh hoạt cá nhân và quỹ dự phòng | 
| **Tổng cộng** | **25.000.000** | **100%** | **Cân đối dòng tiền hoàn hảo** | 
