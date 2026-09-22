# LAB 3 – NHẬN DIỆN VÀ ỨNG PHÓ CÁC MỐI ĐE DỌA ĐẾN AN TOÀN THÔNG TIN

## 1. Thông tin sinh viên

- Họ và tên: Võ Quỳnh Chi
- MSSV: 1150070004
- Lớp: 11_TTMT
  
## 2. Môi trường thực hành

- Máy ảo: VMware Workstation
- Hệ điều hành máy ảo: Windows 11 x64
- Network Adapter: Host-only
- Tên tài khoản Windows: quynhchi
- Thư mục thực hành: C:\LAB3
- Python: 3.14.7
- Wireshark: 4.6.8
- Sysmon: 15.22
- Autoruns: 14.3
- Process Explorer: 17.14
- HTTP Server thử nghiệm: 127.0.0.1:8080
- Snapshot: LAB3_CLEAN_20260914

## 3. Cách dựng môi trường

1. Tạo máy ảo Windows 11 bằng VMware Workstation.
2. Thiết lập Network Adapter ở chế độ Host-only.
3. Tạo thư mục C:\LAB3 để lưu công cụ, dữ liệu và bằng chứng.
4. Chuẩn bị bộ dữ liệu lab3_assets do giảng viên cung cấp.
5. Cài đặt Python 3.14.7.
6. Cài đặt Wireshark 4.6.8 và Npcap.
7. Cài đặt Sysmon 15.22, Autoruns 14.3 và Process Explorer 17.14.
8. Tạo snapshot LAB3_CLEAN_20260914 trước khi thực hiện bài Lab.

## 4. Các tình huống đã thực hiện

### Tình huống 1 – Xác định tài sản, lỗ hổng, mối đe dọa và rủi ro

- Lập Risk Register cho môi trường thực hành.
- Xác định Asset → Vulnerability → Threat → Risk → Control.
- Phân loại các nguồn đe dọa theo 5 nhóm của bài học.

Kết quả: PASS.

### Tình huống 2 – Kiểm chứng phát hiện EICAR

- Kiểm tra trạng thái Windows Defender.
- Sử dụng EICAR Test File để kiểm tra khả năng phát hiện.
- Kiểm tra lịch sử phát hiện của Windows Defender.
- Không tắt Real-time Protection và không tạo exclusion.

Kết quả: PASS.

### Tình huống 3 – Tấn công mật khẩu và nguy cơ Keylogging

- Tạo tài khoản thử nghiệm lab3user.
- Thực hiện đăng nhập đúng và đăng nhập sai có kiểm soát.
- Kiểm tra các sự kiện xác thực trong Windows Security Log.
- Thay đổi mật khẩu của tài khoản thử nghiệm và kiểm chứng lại.

Kết quả: PASS.

### Tình huống 4 – Backdoor và Persistence

- Cài đặt và kiểm tra Sysmon.
- Tạo các artefact thử nghiệm LAB3_Run_Demo và LAB3_Persistence_Demo.
- Sử dụng Autoruns để phát hiện persistence.
- Khởi chạy HTTP Server cục bộ bằng Python.
- HTTP Server chỉ bind tại 127.0.0.1:8080.
- Sử dụng Sysmon và các công cụ hệ thống để kiểm tra tiến trình.

Kết quả: PASS.

### Tình huống 5 – Sniffing, MITM và Spoofing

- Sử dụng Wireshark để capture traffic của chính máy ảo.
- Capture HTTP traffic trên loopback 127.0.0.1:8080.
- Quan sát HTTP GET và HTTP response trong Wireshark.
- Phân tích sự khác biệt giữa HTTP và HTTPS.
- Không thực hiện MITM, spoofing hoặc chuyển hướng traffic chủ động.

Kết quả: PASS.

### Tình huống 6 – DoS, DDoS và Mail Bombing

- Chạy local_load_test.py với tải giới hạn trên 127.0.0.1:8080.
- Phân tích dataset ddos_sample.csv.
- Kết quả dữ liệu DDoS ghi nhận 66 GET và 54 SYN.
- Phân tích dataset mailbomb_sample.csv.
- Ghi nhận 80 bản ghi có trạng thái accepted.
- Không tạo DDoS hoặc gửi email hàng loạt ra bên ngoài.

Kết quả: PASS.

### Tình huống 7 – Social Engineering, Phishing và Spear Phishing

- Phân tích mẫu phishing_email.txt.
- Nhận diện các dấu hiệu của email phishing.
- Phân loại 6 tình huống Social Engineering trong social_engineering_cases.csv.
- Phân biệt Phishing, Spear Phishing, Pretexting, Baiting, Quid Pro Quo và Watering Hole.

Kết quả: PASS.

### Tình huống 8 – Cleanup, phục hồi và kiểm tra lại

- Xóa LAB3_Run_Demo.
- Xóa LAB3_Persistence_Demo.
- Dừng HTTP Server trên cổng 8080.
- Xóa tài khoản thử nghiệm lab3user.
- Kiểm tra lại Windows Defender.
- AntivirusEnabled = True.
- RealTimeProtectionEnabled = True.
- IsTamperProtected = True.
- Tạo autoruns_after.csv.
- Tính SHA-256 cho các file Evidence.
- Tạo evidence_sha256.csv.
- Sao lưu Evidence ra máy thật.
- Khôi phục VM về snapshot LAB3_CLEAN_20260914.
- Máy ảo Windows 11 khởi động lại thành công.

Kết quả: PASS.

## 5. Bằng chứng thu thập

Các bằng chứng của bài thực hành được lưu trong thư mục Evidence.

Một số file đã thu thập:

- autoruns_after.csv
- baseline_time.txt
- ddos_analysis.txt
- defender_device.txt
- evidence_sha256.csv
- http_loopback_8080.pcapng
- local_load_test.txt
- mailbomb_analysis.txt
- task_ran.txt

Các file bằng chứng đã được tính SHA-256 để phục vụ kiểm tra tính toàn vẹn.

## 6. Lỗi gặp phải và cách khắc phục

### Lỗi thiếu script ddos_analyze.py

Khi chạy:

python C:\LAB3\lab3_assets\scripts\ddos_analyze.py

hệ thống báo không tìm thấy file.

Cách khắc phục:
Kiểm tra thư mục scripts và xác định chỉ có local_load_test.py. Sau đó sử dụng PowerShell để đọc và phân tích trực tiếp file ddos_sample.csv.

### Lỗi khôi phục snapshot VMware

Khi khôi phục snapshot LAB3_CLEAN_20260914, VMware không thể khôi phục trạng thái bộ nhớ đã lưu do vấn đề tài nguyên.

Cách khắc phục:
Discard trạng thái đã lưu, đưa VM về trạng thái Powered off và khởi động lại máy ảo từ snapshot LAB3_CLEAN_20260914.

Kết quả:
Windows 11 khởi động lại bình thường.

### Thiếu autoruns_before.csv

Trong quá trình thực hành không có file autoruns_before.csv nên không thể tạo kết quả so sánh autoruns_diff.txt đúng nghĩa.

Cách xử lý:
Giữ nguyên các bằng chứng thực tế đã thu được và không tạo giả baseline trước cleanup.

## 7. Kết luận

Bài Lab 3 đã thực hiện các nội dung nhận diện và ứng phó với nhiều nhóm mối đe dọa an toàn thông tin trong môi trường máy ảo cô lập.

Các hoạt động có khả năng tạo tải chỉ được thực hiện trên localhost 127.0.0.1. Các tình huống DDoS, Mail Bombing và Social Engineering được phân tích bằng dữ liệu huấn luyện/offline.

Sau khi hoàn thành thực hành, các artefact thử nghiệm được cleanup, bằng chứng được tính SHA-256 và máy ảo được khôi phục về snapshot sạch.
