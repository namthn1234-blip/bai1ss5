# THIẾT KẾ PROMPT: LẬP KẾ HOẠCH TÀI CHÍNH CÁ NHÂN BẰNG CHAIN-OF-THOUGHT

## 1. Mục tiêu

Thiết kế một prompt giúp AI lập ngân sách hằng tháng từ thu nhập biến động, chi phí bắt buộc, các khoản nợ và mục tiêu tiết kiệm. Prompt buộc AI tính toán theo quy trình, trình bày **công thức, số liệu trung gian và kiểm tra kết quả** trước khi đưa ra bảng phân bổ cuối cùng.

> Lưu ý: “Nhật ký suy luận” trong bài là **bản giải trình các bước tính có thể kiểm chứng**, không yêu cầu công bố suy nghĩ nội bộ ẩn của mô hình.

## 2. Prompt hoàn chỉnh (có thể sao chép để sử dụng)

**Vai trò:** Bạn là trợ lý lập kế hoạch tài chính cá nhân, ưu tiên sự chính xác số học, khả năng thanh toán nợ đúng hạn và dòng tiền an toàn.

**Dữ liệu đầu vào:**
- Tháng lập kế hoạch: [THÁNG/NĂM].
- Thu nhập: [TỪNG NGUỒN, SỐ TIỀN, MỨC ĐỘ ỔN ĐỊNH]; thu nhập dự kiến thấp nhất nếu có: [SỐ TIỀN].
- Thuế, bảo hiểm và các khoản khấu trừ bắt buộc: [CHI TIẾT].
- Chi phí cố định bắt buộc: [TIỀN NHÀ, ĐIỆN NƯỚC, HỌC PHÍ, ...].
- Các khoản nợ: [TÊN NỢ, DƯ NỢ, LÃI SUẤT, SỐ TIỀN PHẢI TRẢ TỐI THIỂU, NGÀY ĐẾN HẠN].
- Mục tiêu tiết kiệm: tối thiểu 20% thu nhập sau thuế hoặc [TỶ LỆ CAO HƠN]; số dư quỹ dự phòng hiện có: [SỐ TIỀN]; đích quỹ dự phòng: [SỐ THÁNG CHI PHÍ THIẾT YẾU].
- Các giới hạn đặc biệt: [NẾU CÓ]. Đơn vị tiền tệ: VND.

**Nhiệm vụ:** Hãy suy nghĩ từng bước một và tính toán chi tiết trước khi đưa ra quyết định. Thực hiện phép tính theo 4 bước sau, nhưng chỉ trình bày **công thức, kết quả trung gian, các giả định và kiểm tra số học có thể xác minh**; không cần trình bày suy nghĩ nội bộ không quan sát được.

1. **Thu nhập khả dụng:** Tính thu nhập ròng = tổng thu nhập − thuế/khấu trừ bắt buộc; tiền còn sau chi phí cố định = thu nhập ròng − tổng chi phí cố định.
2. **Trả nợ:** Liệt kê các khoản tối thiểu phải trả theo hạn; trích đủ tổng tiền trả nợ tối thiểu trước khi phân bổ chi tiêu khác. Nếu dư, ưu tiên trả thêm nợ có lãi suất cao, nhưng không làm mất khả năng thanh toán tối thiểu và quỹ an toàn.
3. **Tiết kiệm:** Trích tối thiểu 20% **thu nhập ròng sau thuế** (không tính trên phần tiền còn lại), trừ khi nguồn lực không đủ trả các nghĩa vụ bắt buộc; phân chia phần tiết kiệm thành quỹ dự phòng và mục tiêu khác. Nêu rõ nếu mục tiêu 20% chưa đạt.
4. **Chi tiêu linh hoạt:** Lấy phần ngân sách còn lại sau chi phí cố định, trả nợ tối thiểu và tiết kiệm; áp dụng **50/30/20 cải tiến cho riêng khoản linh hoạt**: 50% nhu cầu thiết yếu biến đổi, 30% mong muốn, 20% đệm tiền mặt/chi phí phát sinh. Không áp dụng máy móc tỷ lệ 50/30/20 lên tổng thu nhập khi tiền nợ và chi phí cố định đã ràng buộc ngân sách.

**Kiểm tra bắt buộc:**
- Tổng mọi khoản phân bổ phải đúng bằng thu nhập ròng sau thuế (sai số làm tròn tối đa 1 VND).
- Tổng tỷ lệ phần trăm phải bằng 100% sau khi xử lý sai số làm tròn.
- Không được phân bổ âm, không được tính trùng chi phí cố định vào chi tiêu linh hoạt.
- Đánh dấu từng khoản nợ có đủ tiền thanh toán đúng hạn hay không.
- Với thu nhập không ổn định, lập thêm kịch bản thu nhập thấp; không coi thu nhập chưa chắc chắn là tiền đã có.
- Nếu không đủ tiền cho chi phí bắt buộc và nợ tối thiểu, nêu thiếu hụt, xếp thứ tự ưu tiên sinh hoạt thiết yếu và nghĩa vụ đến hạn, khuyến nghị liên hệ chủ nợ để thương lượng; **không tạo ra một bảng ngân sách giả cân bằng bằng cách bịa thêm thu nhập**.
- Nếu dữ liệu thiếu, liệt kê giả định rõ ràng; không tự bịa dư nợ, lãi suất hay hạn thanh toán.

**Định dạng kết quả — đúng 2 phần:**

**Phần 1. Nhật ký suy luận logic (Reasoning Steps):** Bảng/đoạn liệt kê từng bước, công thức, số thế vào, kết quả trung gian; có đối soát tổng và cảnh báo rủi ro.

**Phần 2. Bảng phân bổ ngân sách cuối cùng:** Xuất Markdown Table với 4 cột **Hạng mục | Số tiền | Tỷ lệ % | Ghi chú**. Tỷ lệ tính trên thu nhập ròng; có dòng tổng cộng. Sau bảng, kết luận ngắn về khả năng trả nợ, tỷ lệ tiết kiệm và quỹ dự phòng.

## 3. Ví dụ minh họa với dữ liệu giả định

**Dữ liệu mẫu:** Tổng thu nhập 25.000.000 VND; thuế và khấu trừ 2.000.000 VND; chi phí cố định 9.000.000 VND; khoản trả nợ tối thiểu 3.000.000 VND; cam kết tiết kiệm 20% thu nhập ròng. Giả định các khoản nợ đến hạn đều nằm trong mức trả tối thiểu nêu trên. Chưa có dữ liệu lãi suất/dư nợ để tối ưu trả thêm nợ.

### Phần 1. Nhật ký suy luận logic (Reasoning Steps)

1. **Thu nhập ròng:** 25.000.000 − 2.000.000 = **23.000.000 VND**.
2. **Sau chi phí cố định:** 23.000.000 − 9.000.000 = **14.000.000 VND**.
3. **Sau trả nợ tối thiểu:** 14.000.000 − 3.000.000 = **11.000.000 VND**.
4. **Tiết kiệm cam kết:** 20% × 23.000.000 = **4.600.000 VND**.
5. **Ngân sách linh hoạt còn lại:** 11.000.000 − 4.600.000 = **6.400.000 VND**.
6. **Chia 50/30/20 cải tiến:** nhu cầu thiết yếu biến đổi = 50% × 6.400.000 = **3.200.000 VND**; mong muốn = 30% × 6.400.000 = **1.920.000 VND**; đệm phát sinh = 20% × 6.400.000 = **1.280.000 VND**.
7. **Đối soát:** 9.000.000 + 3.000.000 + 4.600.000 + 3.200.000 + 1.920.000 + 1.280.000 = **23.000.000 VND**. Tiết kiệm đạt **20% thu nhập ròng**.

### Phần 2. Bảng phân bổ ngân sách cuối cùng

| Hạng mục | Số tiền | Tỷ lệ % | Ghi chú |
|---|---:|---:|---|
| Chi phí cố định bắt buộc | 9.000.000 VND | 39,13% | Nhà ở, hóa đơn và nghĩa vụ cố định |
| Trả nợ tối thiểu | 3.000.000 VND | 13,04% | Ưu tiên theo ngày đến hạn |
| Tiết kiệm và quỹ dự phòng | 4.600.000 VND | 20,00% | Đạt mức cam kết 20% |
| Chi thiết yếu biến đổi | 3.200.000 VND | 13,91% | Ăn uống, đi lại, nhu yếu phẩm |
| Chi tiêu mong muốn | 1.920.000 VND | 8,35% | Giải trí, mua sắm không bắt buộc |
| Đệm chi phí phát sinh | 1.280.000 VND | 5,57% | Giữ thanh khoản cho tình huống bất ngờ |
| **Tổng cộng** | **23.000.000 VND** | **100,00%** | **Đối soát khớp thu nhập ròng** |

**Nhận xét:** Với dữ liệu giả định, ngân sách đủ trả nợ tối thiểu và đạt tiết kiệm 20%. Khoản đệm phát sinh khác với quỹ dự phòng dài hạn; nên ưu tiên xây quỹ dự phòng đạt khoảng 3–6 tháng chi phí thiết yếu tùy mức độ ổn định thu nhập. Nếu thu nhập thực tế thấp hơn dự kiến, cần tính lại toàn bộ ngân sách trước khi chi tiêu.

## 4. Tiêu chí đánh giá chất lượng prompt

- **Rõ dữ liệu đầu vào:** Có thu nhập, thuế, chi phí cố định, khoản nợ, hạn nợ, tiết kiệm và quỹ dự phòng.
- **Rõ trình tự xử lý:** Thu nhập ròng → chi phí bắt buộc → nợ tối thiểu → tiết kiệm → linh hoạt.
- **Kiểm chứng được:** Có công thức, phép thế số, đối soát tiền và phần trăm.
- **Quản trị rủi ro:** Có kịch bản thu nhập thấp và cách xử lý khi thiếu tiền.
- **Đầu ra nhất quán:** Hai phần riêng biệt; bảng Markdown đúng bốn cột.

*Kết luận: Prompt có cấu trúc từng bước giúp kiểm soát phép tính và giảm rủi ro bỏ sót ràng buộc. Các con số trong ví dụ chỉ dùng để minh họa, không đại diện cho tình hình tài chính của người sử dụng.*
