[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=23574154&assignment_repo_type=AssignmentRepo)
# Day 10 Lab: Data Pipeline & Data Observability

**Student Email:** 26ai.trangntq@vinuni.edu.vn
**Name:** Nguyễn Thị Quỳnh Trang

---

## Mo ta

Bài lab "Data Pipeline & Data Observability" tập trung vào xây dựng một ETL pipeline tự động:

1. **Extract:** Đọc dữ liệu từ file JSON (raw_data.json)
2. **Validate:** Loại bỏ các bản ghi không hợp lệ (giá <= 0, category rỗng)
3. **Transform:** Tính giá giảm 10%, chuẩn hóa category về Title Case, thêm timestamp xử lý
4. **Load:** Lưu kết quả vào file CSV (processed_data.csv)

Tiếp theo, bài lab kiểm tra tác động của chất lượng dữ liệu đến quyết định của AI agent thông qua một "stress test" so sánh agent khi dùng dữ liệu sạch vs dữ liệu bẩn (garbage data).

---

## Cach chay (How to Run)

### Prerequisites
```bash
pip install pandas
```

### Chay ETL Pipeline
```bash
python solution.py
```

### Chay Agent Simulation (Stress Test)
```bash
# Tao du lieu garbage (co nhung issue nhu invalid prices, duplicates, outliers)
python generate_garbage.py

# Chay agent tren ca 2 bo du lieu
python agent_simulation.py
```

---

## Cau truc thu muc

```
├── solution.py              # ETL Pipeline script
├── processed_data.csv       # Output cua pipeline
├── experiment_report.md     # Bao cao thi nghiem
└── README.md                # File nay
```

---

## Ket qua

### ETL Pipeline Results
- **Input:** 5 records từ raw_data.json
- **Processed (Valid):** 3 records (Laptop $1200, Chair $45, Monitor $300)
- **Dropped (Invalid):** 2 records (Mystery Box: giá âm, Phone: category rỗng)
- **Output:** processed_data.csv với cột: id, product, price, category, discounted_price, processed_at

### Agent Simulation Results
- **Clean Data Test:** Agent chọn "Laptop" ✓ (sản phẩm hợp lý, giá $1200)
- **Garbage Data Test:** Agent chọn "Nuclear Reactor" ✗ (sản phẩm không thực tế, giá $999999)

### Key Findings
Chất lượng dữ liệu có tác động trực tiếp đến chất lượng quyết định của AI agent. Dữ liệu bẩn chứa outliers, duplicate IDs, sai kiểu dữ liệu, và null values khiến agent đưa ra quyết định sai lệch.
