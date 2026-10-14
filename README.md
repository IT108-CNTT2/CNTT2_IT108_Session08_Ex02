# Báo cáo xử lý tìm kiếm nội dung tệp tin

## Phần 1: Phân tích lỗi của An

### 1. Nhầm lẫn về tư duy
- An đang bị nhầm lẫn cơ bản giữa việc **tìm kiếm tệp tin** (tìm tên file/đường dẫn trên ổ cứng) với việc **tìm kiếm nội dung bên trong tệp** (quét các dòng chữ nằm sâu trong tệp log).

### 2. Sự khác biệt giữa `Get-ChildItem` và `Select-String`
- **`Get-ChildItem`** (tương đương `dir` hoặc `ls`): Dùng để liệt kê danh sách tệp tin và thư mục. Tham số `-Filter "*404*"` chỉ tìm những **tên tệp** có chứa từ khóa "404". Vì không có tệp nào mang tên này, lệnh không trả về kết quả và tuyệt đối không đọc nội dung bên trong `access.log`.
- **`Select-String`** (tương đương `grep` trên Linux hay `findstr` trên CMD): Mới chính là công cụ chuyên dụng để quét và tìm kiếm **văn bản/chuỗi ký tự bên trong** tệp tin.

---

## Phần 2: Hoàn thiện câu lệnh PowerShell chuẩn

Để lọc từ khóa "error" trong tệp `access.log` mà không cần bận tâm chữ hoa hay chữ thường, đồng thời tự động hiển thị số thứ tự dòng, ta dùng lệnh:

```powershell
Select-String -Path access.log -Pattern "error"
