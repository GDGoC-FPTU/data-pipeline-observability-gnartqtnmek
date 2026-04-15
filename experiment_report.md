# Experiment Report: Data Quality Impact on AI Agent

**Student ID:** AI20K-2A202600406
**Name:** Nguyễn Thị Quỳnh Trang
**Date:** 15/04/2026

---

## 1. Ket qua thi nghiem

Chay `agent_simulation.py` voi 2 bo du lieu va ghi lai ket qua:

| Scenario | Agent Response | Accuracy (1-10) | Notes |
|----------|----------------|-----------------|-------|
| Clean Data (`processed_data.csv`) | Based on my data, the best choice is Laptop at $1200 | 9 | |
| Garbage Data (`garbage_data.csv`) | Based on my data, the best choice is Nuclear Reactor at $999999 | 2 | |

---

## 2. Phan tich & nhan xet

### Tai sao Agent tra loi sai khi dung Garbage Data?

Agent chọn "Nuclear Reactor" thay vì "Laptop" vì garbage data chứa nhiều vấn đề chất lượng dữ liệu:

**1. Extreme Outlier (Outliers):** Nuclear Reactor có giá $999999, gấp 833 lần so với Laptop ($1200). Agent chỉ xem xét giá cao nhất trong danh sách electronics mà không kiểm tra tính hợp lý của dữ liệu, nên nó nhận sản phẩm này là "tốt nhất".

**2. Duplicate IDs:** Dữ liệu garbage có hai bản ghi với id=1 (Laptop và Banana). Điều này tạo ra sự nhập nhằng trong dữ liệu gốc và khiến không rõ bản ghi nào là chính thức.

**3. Wrong Data Types:** Giá của "Broken Chair" là "ten dollars" (chuỗi ký tự) thay vì số. Nếu agent không xử lý lỗi kiểu dữ liệu, nó có thể cho kết quả sai hoặc crash.

**4. Null Values:** Bản ghi cuối cùng có id=None và category=None. Dữ liệu bị thiếu này làm cho agent không thể xác định sản phẩm đó thuộc danh mục nào.

Kết luận: Dữ liệu sạch đảm bảo agent lựa chọn sản phẩm hợp lý (Laptop $1200), nhưng dữ liệu bẩn khiến agent chọn sản phẩm không thực tế (Nuclear Reactor $999999).

---

## 3. Ket luan

**Quality Data > Quality Prompt?** **CÓ, tuyệt đối đúng.**

Ngay cả với cùng một agent logic đơn giản (tìm sản phẩm electronics có giá cao nhất), dữ liệu sạch cho kết quả hợp lý (Laptop $1200) còn dữ liệu bẩn cho kết quả vô lý (Nuclear Reactor $999999). Prompt và logic không thay đổi, nhưng dữ liệu đầu vào quyết định chất lượng đầu ra. Các vấn đề như outliers, duplicate IDs, null values, và sai kiểu dữ liệu trực tiếp ảnh hưởng đến quyết định của agent. Do đó, chất lượng dữ liệu là yếu tố quan trọng nhất để đảm bảo hệ thống AI hoạt động chính xác, thậm chí quan trọng hơn cả việc viết prompt hoàn hảo.
