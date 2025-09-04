2025-08-05 21:27
Status: #baby
Tags: [[system design]]
## Main
### What? 
Grafana và Prometheus là hai công cụ rất phổ biến và thường được sử dụng kết hợp để giám sát hệ thống (monitoring) và trực quan hóa dữ liệu (visualization).

|**Công cụ**|**Chức năng chính**|
|---|---|
|**Prometheus**|Hệ thống thu thập & lưu trữ dữ liệu thời gian (time-series)|
|**Grafana**|Công cụ trực quan hóa dữ liệu, tạo dashboard và alert|
### Prometheus

### ✅ Chức năng chính:

- Thu thập **metrics** theo định kỳ (pull-based model).
    
- Lưu trữ **time-series data** (dữ liệu theo thời gian).
    
- Hỗ trợ **PromQL** – ngôn ngữ truy vấn mạnh mẽ để phân tích dữ liệu.
    
- Hỗ trợ cảnh báo qua Alertmanager.
    

### 🛠 Cách hoạt động:

1. Prometheus định kỳ gửi request tới các endpoint như `http://<target>/metrics`.
    
2. Các ứng dụng/phần mềm expose metrics ở endpoint `/metrics` (thường qua exporter hoặc thư viện tích hợp).
    
3. Dữ liệu được lưu trữ trong cơ sở dữ liệu time-series nội bộ.
    
4. Người dùng truy vấn qua PromQL hoặc kết nối Grafana để hiển thị.
    

### 🔗 Ví dụ target:

yaml

Sao chépChỉnh sửa

`scrape_configs:   - job_name: 'node_exporter'     static_configs:       - targets: ['localhost:9100']`

---

### 📊 2. **Grafana – Trực quan hóa dữ liệu**

### ✅ Chức năng chính:

- Truy vấn dữ liệu từ Prometheus (và các nguồn khác như Loki, InfluxDB, MySQL...).
    
- Tạo dashboard, bảng biểu, đồ thị.
    
- Tạo cảnh báo (alerting).
    
- Tùy chỉnh giao diện người dùng dễ dàng.
    

### 🛠 Cách sử dụng:

- Kết nối **Data Source** đến Prometheus.
    
- Viết truy vấn PromQL trong giao diện đồ thị.
    
- Thiết lập các panel (line chart, gauge, bar, single stat...).
    
- Tạo dashboard chia sẻ được.


## Victoria metric
### What? 
**VictoriaMetrics** is a **fast, cost-efficient, and scalable** alternative to Prometheus for storing time-series data. It is fully compatible with **Prometheus** and **Grafana**, and is often used as a **drop-in replacement** or long-term storage backend.

|Feature|**Prometheus**|**VictoriaMetrics**|
|---|---|---|
|Time-series DB|Built-in|Optimized, custom TSDB|
|Data ingestion|Pull model|Compatible with pull & push|
|Retention|In-memory, limited by disk/RAM|Scalable retention (months to years)|
|Horizontal scalability|Difficult, federated Prometheus|Yes (via VictoriaMetrics Cluster)|
|Remote Write/Read|Supports|Fully compatible|
|Performance|Good|Excellent (lower disk, RAM usage)|
|Use case|Short-term monitoring (hours-days)|Long-term metrics, large-scale environments|
|Compatibility with Grafana|✅|✅|

## 🔄 Where VictoriaMetrics fits

You can use **VictoriaMetrics** in one of these roles:

1. **Drop-in Prometheus replacement** (standalone mode)
    
2. **Remote Write backend** (Prometheus writes to VictoriaMetrics)
    
3. **Long-term storage backend** via Thanos/Cortex style setup


## References

