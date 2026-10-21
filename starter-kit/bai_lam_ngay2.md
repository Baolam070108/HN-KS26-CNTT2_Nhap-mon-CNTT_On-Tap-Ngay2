# BÀI LÀM – ÔN TẬP NGÀY 2

- Họ tên: Cao Bao Lam
- Lớp: CNTT2
- Link repository:
- Hệ điều hành (Windows/macOS): Windows**

## Bài 1. Lọc log thủ công

### Lệnh đã chạy

```shell

gc logs/access.log | sls "Error" | Add-content -Path logs/error_report.txt

```

### 2 dòng lỗi đầu tiên trong error\_report.txt

```text
2025-10-18 08:17:59 [ERROR] Khong tim thay trang /lich-thi (404)
2025-10-18 08:25:55 [ERROR] Het thoi gian cho (timeout)

```

## Bài 2. Đếm bằng pipeline

### Lệnh

```shell
sls "warning" -Path logs/access.log | Measure-Object -Line
sls "error" logs/payment.log | Measure-Object -Line
```

### Kết quả đếm (Windows: giá trị Count; macOS: con số in ra)

```text
WARNING trong access.log: 4
ERROR trong payment.log : 3
```

## Bài 3. Chạy script auto\_warning (.ps1 hoặc .sh)

### Lệnh chạy (Windows: nếu dùng Phụ lục 2 thì ghi cả 2 lệnh)

```shell
./auto_warning.ps1

```

### Nội dung file logs/warning\_report.txt

```text
=== CANH BAO THANH TOAN ===

2025-10-18 09:19:13 [WARNING] Cong thanh toan phan hoi cham
2025-10-18 09:28:16 [WARNING] Nhieu lan nhap sai ma OTP
2025-10-18 09:43:01 [WARNING] So du vi gan bang hoc phi
2025-10-18 09:46:22 [WARNING] So du vi gan bang hoc phi
2025-10-18 09:49:43 [WARNING] So du vi gan bang hoc phi



```

## Bài 4. Báo cáo tổng hợp

### Các lệnh đã chạy

```shell
"=== TONG HOP ACCESS LOG ===" | set-content  -Path ./logs/tong_hop_ngay2.txt 
 sls "error" logs/access.log | foreach-object { $_.Line } | add-content logs/tong_hop_ngay2.txt
(sls "warning" logs/payment.log | Measure-Object -Line).lines | add-content logs/tong_hop_ngay2.txt

```

### Nội dung file logs/tong\_hop\_ngay2.txt

```text
=== TONG HOP ACCESS LOG ===
2025-10-18 08:17:59 [ERROR] Khong tim thay trang /lich-thi (404)
2025-10-18 08:25:55 [ERROR] Het thoi gian cho (timeout)
2025-10-18 08:33:51 [ERROR] Ket noi may chu du lieu that bai
2025-10-18 08:37:19 [ERROR] Ket noi may chu du lieu that bai
2025-10-18 08:49:43 [ERROR] Het thoi gian cho (timeout)
2025-10-18 08:53:11 [ERROR] Het thoi gian cho (timeout)
5


```

## Bài 5. Câu hỏi ngắn

**a)** `>` ghi đè nội dung cũ, còn `>>` nối nội dung mới vào cuối file.

**b)** File chỉ còn các dòng `ERROR` của lệnh thứ hai, nội dung cũ bị mất.

**c)** Đường dẫn tương đối giúp dễ di chuyển, chia sẻ dự án và chạy script trên nhiều máy tính.

## Tự chấm (điền sau khi có đáp án)

- **Điểm tự chấm:** ..../100
- **Lỗi mình đã mắc và cách sửa:**
