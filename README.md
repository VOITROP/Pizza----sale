# Pizza Order — Phân tích doanh thu và kiểm thử báo cáo bán hàng

**Dự án cá nhân | Ecommerce Intern | SQL Server · Power BI**

## Bài toán

Tôi thực hiện dự án để theo dõi kết quả bán hàng, nhận diện sự thay đổi về số đơn theo thời gian và so sánh hiệu suất sản phẩm. Báo cáo giúp tổng hợp các chỉ số bán hàng và xác định những nhóm sản phẩm cần phân tích thêm.

Dữ liệu gồm **48.620 dòng chi tiết, 21.350 đơn hàng**, từ **01/01/2015 đến 31/12/2015**. Tổng số pizza bán là **49.574**, doanh thu **817.860,05**, giá trị đơn trung bình **38,31** và số pizza trung bình mỗi đơn **2,32**. Giá trị tiền được giữ theo dữ liệu nguồn; đơn vị tiền tệ chưa được xác nhận.

Nguồn làm việc gồm file Excel `pizza_sales_excel_file.xlsx`, bảng SQL `dbo.pizza_sales` và báo cáo Power BI. Excel đã được kiểm tra độc lập; các KPI tổng hợp khớp SQL.

## Công việc của tôi

- Phân tích bài toán, viết 6 user story, 8 yêu cầu chức năng, 9 quy tắc nghiệp vụ và tiêu chí chấp nhận.
- Chuẩn hóa định nghĩa 5 KPI bán hàng, phạm vi bộ lọc và cách xử lý dữ liệu rỗng.
- Sử dụng SQL để tổng hợp, đối chiếu số liệu với Power BI.
- Trình bày báo cáo hai trang, theo dõi xu hướng thời gian, cơ cấu doanh thu và xếp hạng sản phẩm.
- Chạy bộ SQL A–L gồm 16 kết quả và một ví dụ lọc Classic; xây dựng 20 test case UAT có truy vết từ yêu cầu đến SQL và bằng chứng.

## Dashboard

### Tổng quan bán hàng

![Dashboard tổng quan bán hàng](06_Images/dashboard_overview.png)

### Hiệu suất sản phẩm

![Dashboard hiệu suất sản phẩm](06_Images/dashboard_products.png)

Ảnh báo cáo ở phạm vi toàn năm 2015, danh mục All. Các nhận xét dưới đây đã được đối chiếu SQL; một số chú thích tĩnh trong ảnh là nội dung cũ cần cập nhật.

## Quy trình thực hiện

**Yêu cầu nghiệp vụ → dữ liệu và SQL → Power BI → kiểm tra → nhận xét kinh doanh.**

Với câu hỏi “Tháng nào có nhiều đơn nhất?”, tôi định nghĩa số đơn bằng mã đơn duy nhất, tổng hợp SQL theo tên tháng trong nguồn năm 2015, thể hiện trên biểu đồ tháng và đối chiếu từng điểm. Tháng 7 dẫn đầu với 1.935 đơn. Nội dung được liên kết bằng FR03 → C → TC07.

## Ba nhận xét kinh doanh

### 1. Tháng 7 có số đơn cao nhất năm

Tháng 7 đạt **1.935 đơn**, cao nhất năm 2015; tháng 5 đứng thứ hai với **1.853 đơn**. Tháng 10 thấp nhất với **1.646 đơn**. Số đơn tháng 7 cao hơn tháng 10 **289 đơn, tương đương 17,56%**.

Số đơn thay đổi giữa các tháng, tạo cơ sở xem xét nhu cầu phục vụ theo từng giai đoạn. Tôi đề xuất phân tích thêm số đơn theo ngày hoạt động, ngày trong tuần và các chương trình bán hàng trước khi lập kế hoạch nhân sự hoặc chuẩn bị hàng. Một năm dữ liệu chưa đủ để khẳng định quy luật mùa vụ lặp lại.

### 2. Classic đóng góp doanh thu cao nhất trong các danh mục

Danh mục **Classic đạt 220.053,10**, chiếm **26,91% tổng doanh thu**. Đây là tỷ trọng cao nhất, tiếp theo là Supreme với **25,46%**; chênh lệch khoảng **1,45 điểm phần trăm** theo số hiển thị.

Classic là nhóm dẫn đầu về đóng góp doanh thu, nhưng cơ cấu doanh thu vẫn khá phân tán giữa các danh mục. Tôi đề xuất xem thêm lợi nhuận, tồn kho và mức độ sẵn có của sản phẩm trước khi ưu tiên nguồn lực hoặc triển khai ưu đãi cho nhóm này.

### 3. Sản phẩm dẫn đầu doanh thu khác sản phẩm dẫn đầu số lượng

**The Thai Chicken Pizza** có doanh thu cao nhất với **43.434,25**, trong khi **The Classic Deluxe Pizza** có số lượng bán cao nhất với **2.453 pizza**.

Hai tiêu chí cho thấy sản phẩm bán nhiều nhất chưa chắc tạo doanh thu cao nhất. Tôi đề xuất theo dõi riêng doanh thu và số lượng khi đánh giá sản phẩm; bổ sung giá bán, giảm giá, chi phí và tồn kho trước khi lựa chọn sản phẩm chủ lực hoặc xây dựng chương trình bán kèm.

## Kết quả kiểm tra

Đã chạy thành công 17 câu SELECT trong file SQL hiện tại. Doanh thu làm tròn là **817.860,05**, AOV **38,31**, số pizza **49.574**, số đơn **21.350**, số pizza trung bình mỗi đơn **2,32**. Doanh thu và AOV nguyên bản có nhiều chữ số thập phân.

Phần F chỉ lấy tháng 2: Classic **1.178**, Supreme **964**, Veggie **944**, Chicken **875** pizza. Kết quả này không cùng phạm vi với ảnh dashboard toàn năm.

Bộ UAT hiện có **0 Pass, 2 Fail, 1 Blocked, 17 Not Run** và **6 lỗi mở**. Test cần kiểm tra cả SQL và Power BI; chạy SQL thành công chưa đủ để ghi Pass. Hai test Fail là TC10 khác phạm vi và TC17 lỗi nội dung trên ảnh. Những Pass lưu trước đây thuộc phiên bản SQL cũ.

Xem [kết quả SQL hiện tại](04_UAT/Test_Evidence/Current_SQL_Results.txt), [kịch bản UAT](04_UAT/UAT_Test_Cases.md) và [số liệu cho nhận xét kinh doanh](04_UAT/Test_Evidence/Business_Insights_Evidence.md).
## Phạm vi và phần còn hoàn thiện

Đây là dự án cá nhân về phân tích bán hàng, vận dụng các kỹ năng liên quan đến Ecommerce. Phạm vi không bao gồm vận hành gian hàng trên sàn, quảng cáo hoặc xử lý đơn thực tế.

Kiểm tra giao diện TC17 đang Fail: chú thích tháng phải đổi January thành May; nhận định về buổi tối chưa có biểu đồ giờ chứng minh; tiêu đề phần danh mục cần cập nhật; nhiều tên sản phẩm bị cắt và đơn vị tiền chưa rõ. Các tình huống bộ lọc, ranh giới Top 5, dữ liệu rỗng và refresh chưa được kiểm tra đầy đủ. Dữ liệu hiện chưa đủ để đánh giá lợi nhuận, tỷ lệ chuyển đổi hoặc hiệu quả quảng cáo.

## Báo cáo và tài liệu chi tiết

1. [Yêu cầu nghiệp vụ](01_Documents/Business_Requirements.md) và [định nghĩa KPI](01_Documents/KPI_Definitions.md).
2. [Dữ liệu Excel](02_Data/pizza_sales_excel_file.xlsx), [dữ liệu mẫu](02_Data/sample_data.csv) và [từ điển dữ liệu](02_Data/Data_Dictionary.md).
3. [SQL phân tích bán hàng](03_SQL/03_business_analysis.sql), [kiểm tra dữ liệu](03_SQL/01_data_quality.sql), [chuẩn hóa](03_SQL/02_data_cleaning.sql) và [thứ tự chạy](03_SQL/README.md).
4. [Kịch bản UAT](04_UAT/UAT_Test_Cases.md), [kết quả kiểm tra](04_UAT/Test_Summary.md) và [tài liệu UAT gốc](04_UAT/UAT_Original.docx).
5. [Dashboard Power BI](05_PowerBI/Pizza_Order_Dashboard.pbix) và [ghi chú rà soát](05_PowerBI/Review_Notes.md).

## Cách xem dự án

Đọc README để xem bài toán, hai ảnh và ba nhận xét. Mở báo cáo Power BI để xem sản phẩm. Xem Test_Summary để biết phạm vi đã kiểm tra. Các tài liệu và SQL được đánh số theo trình tự thực hiện.

Đây là bộ bàn giao cục bộ. Nguồn công khai và giấy phép của dữ liệu cần được xác nhận trước khi đăng dữ liệu đầy đủ lên GitHub.

