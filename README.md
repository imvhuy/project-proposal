# Project Proposal

## Giải pháp Phân tích Dữ liệu Serverless cho Thông tin Thời tiết Thời gian Thực

**Mô tả dự án:**  
Xây dựng một pipeline dữ liệu thời tiết hoàn chỉnh sử dụng công nghệ serverless của AWS để thu thập, xử lý, phân tích và trực quan hóa dữ liệu thời tiết từ 6 thành phố Việt Nam.

**Người thực hiện:** Đặng Văn Huy

## Mục lục

1. [Executive Summary](#1-executive-summary)  
2. [Problem Statement](#2-problem-statement)  
3. [Solution Architecture](#3-solution-architecture)  
4. [Technical Implementation](#4-technical-implementation)  
5. [Timeline & Milestones](#5-timeline--milestones)  
6. [Budget Estimation](#6-budget-estimation)  
7. [Risk Assessment](#7-risk-assessment)  
8. [Expected Outcomes](#8-expected-outcomes)

## 1. Executive Summary

### Phát biểu Vấn đề:
Nhiều tổ chức và khu vực công tại Việt Nam thiếu một giải pháp có thể mở rộng, hiệu quả về chi phí và tự động để thu thập, xử lý và phân tích dữ liệu thời tiết thời gian thực cho thông tin kinh doanh, chuẩn bị thảm họa và tối ưu hóa hoạt động.

### Tổng quan Giải pháp:
Đề xuất một pipeline ETL hoàn toàn serverless trên AWS, tận dụng Lambda, S3, Athena và QuickSight để tự động hóa việc thu thập, xử lý, lưu trữ, phân tích và trực quan hóa dữ liệu thời tiết từ OpenWeatherMap.

### Tính năng Chính:
- Thu thập dữ liệu thời tiết tự động (24/7) thông qua Lambda và EventBridge  
- Chuyển đổi và làm giàu dữ liệu cho phân tích  
- Lưu trữ an toàn trên S3 (dữ liệu thô & đã xử lý)  
- Phân tích bằng Athena  
- Dashboard tương tác với QuickSight  
- Giám sát và kiểm soát chi phí tự động

### Lợi ích Kinh doanh & ROI:
- Thông tin thời gian thực hỗ trợ ra quyết định  
- Giảm công việc thủ công và rủi ro  
- Có thể mở rộng với chi phí tối thiểu  
- Mô hình trả theo sử dụng, chi phí thấp  
- Hỗ trợ phân tích nâng cao trong tương lai

### Đầu tư & Lịch trình:
- Chi phí AWS hàng tháng: ~$1–5 (nằm trong Free Tier)  
- Không yêu cầu phần cứng hay license

### Chỉ số Thành công:
- Trễ dữ liệu ≤ 1 giờ  
- Dashboard được người dùng kinh doanh sử dụng  
- Chi phí mỗi điểm dữ liệu < $0.01  
- Uptime pipeline 99.9%  
- Sự hài lòng của người dùng

## 2. Problem Statement

### Tình hình Hiện tại:
Phụ thuộc vào nguồn dữ liệu thủ công gây lỗi và không hiệu quả.

### Thách thức Chính:
- Thiếu tự động hóa  
- Chất lượng và định dạng dữ liệu không nhất quán  
- Khó khăn trong mở rộng  
- Trực quan hóa hạn chế  
- Gánh nặng vận hành

### Tác động Bên liên quan:
- Nhà phân tích: dữ liệu lỗi/thừa thiếu  
- IT: tốn thời gian bảo trì  
- Người ra quyết định: thiếu thông tin  
- Người dùng: trải nghiệm kém

### Hậu quả Kinh doanh:
- Lỡ cơ hội trong nông nghiệp, logistics, du lịch  
- Quản lý rủi ro kém  
- Chi phí vận hành tăng

## 3. Solution Architecture

### Tổng quan:
Một pipeline ETL serverless tích hợp OpenWeatherMap API, Lambda, S3, Athena, QuickSight.

![image](https://imvhuy.github.io/images/etl/architecture.png)

### Dịch vụ AWS Sử dụng:
- **Lambda:** thu thập và xử lý dữ liệu  
- **S3:** lưu trữ dữ liệu  
- **EventBridge:** lập lịch  
- **Athena:** truy vấn dữ liệu  
- **QuickSight:** dashboard  
- **CloudWatch:** giám sát  
- **IAM:** kiểm soát truy cập

### Thành phần:
- Lambda Collector: lấy dữ liệu hàng giờ  
- Lambda Processor: xử lý dữ liệu  
- S3: chứa dữ liệu thô và đã xử lý  
- Athena: phân tích SQL  
- QuickSight: trực quan hóa

### Bảo mật:
- IAM least privilege  
- Chính sách S3  
- Mã hóa SSE-S3 & HTTPS  
- API Key lưu trong Parameter Store

### Khả năng mở rộng:
- Lambda không trạng thái  
- S3 mở rộng tự động  
- Athena & QuickSight mở rộng theo nhu cầu

## 4. Technical Implementation

### Giai đoạn Triển khai:
1. Cấu hình IAM  
2. Tạo bucket S3  
3. Phát triển hàm Lambda  
4. Thiết lập EventBridge  
5. Tạo bảng Athena  
6. Thiết lập QuickSight  
7. Cấu hình giám sát

### Yêu cầu Kỹ thuật:
- AWS Free Tier  
- Python 3.11  
- API Key OpenWeatherMap  
- Athena & QuickSight kích hoạt

### Phát triển:
- Sử dụng Infrastructure as Code (tuỳ chọn)  
- Lambda module-based  
- Quản lý bằng Git

### Kiểm thử:
- Unit test cho Lambda  
- Test tích hợp S3, Athena  
- Test hiệu năng  
- Manual test dashboard

### CI/CD:
- Dùng GitHub Actions  
- Rollback qua backup S3 và Lambda version

## 5. Timeline & Milestones

### Thời gian:
**23/06/2025 – 15/07/2025**
link timeline: https://docs.google.com/spreadsheets/d/1QPgLRd18Ksj075rZ-wmasr--k9-lXuRwU3tm4gxQ2zM/edit?gid=1790630016#gid=1790630016

### Mốc Quan Trọng:
- Pipeline hoạt động ổn định  
- Dashboard đầu tiên xuất bản  
- Đào tạo người dùng hoàn tất

### Phụ thuộc:
- API OpenWeatherMap  
- Giới hạn AWS Free Tier

## 6. Budget Estimation

### Hạ tầng:
- Lambda: ~$0.20/tháng hoặc Free Tier  
- S3: ~$0.50/tháng hoặc Free Tier  
- Athena: ~$0.50/tháng  
- QuickSight: $9/user/tháng (sau dùng thử)

### Vận hành:
- Tối thiểu do serverless & trả theo sử dụng

### ROI:
- Hòa vốn trong < 1 tháng  
- Mở rộng dễ dàng với chi phí thấp

## 7. Risk Assessment

### Ma trận Rủi ro:

| Rủi ro                | Tác động | Xác suất | Giảm thiểu                          |
|-----------------------|----------|----------|-------------------------------------|
| Ngừng API             | Cao      | Thấp     | Logic retry, cảnh báo               |
| Vượt chi phí AWS      | Trung bình | Thấp   | Giới hạn ngân sách, lifecycle S3    |
| Dữ liệu sai lệch       | Trung bình | Trung bình | Giám sát & xác thực                |
| Vi phạm bảo mật       | Cao      | Thấp     | IAM, mã hóa, kiểm thử bảo mật       |

### Chiến lược:
- Cảnh báo tự động  
- Đánh giá định kỳ  
- Tài liệu hóa & đào tạo

### Kế hoạch Dự phòng:
- Thu thập thủ công nếu pipeline ngừng  
- Khôi phục từ backup S3

## 8. Expected Outcomes

### Chỉ số Thành công:
- Trễ dữ liệu < 1 giờ  
- 99.9% uptime  
- Tỷ lệ người dùng áp dụng > 80%  
- Chi phí < $0.01 / điểm dữ liệu

### Lợi ích Kinh doanh:
- Quyết định nhanh chóng  
- Tối ưu nguồn lực  
- Quản lý rủi ro tốt hơn

### Kỹ thuật:
- Cloud architecture hiện đại  
- Mở rộng đến ML & phân tích nâng cao

### Giá trị dài hạn:
- Hỗ trợ nhiều nguồn dữ liệu khác  
- Báo cáo & dashboard nâng cao
