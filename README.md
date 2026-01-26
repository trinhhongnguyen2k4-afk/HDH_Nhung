# TUẦN 1 – XÂY DỰNG TOOLCHAIN BIÊN DỊCH CHÉO CHO ARM BẰNG CROSSTOOL-NG

## Giới thiệu
Trong hệ thống nhúng Linux, việc tự xây dựng toolchain biên dịch chéo đóng vai trò rất quan trọng, giúp kiểm soát tốt kiến trúc, thư viện và trình biên dịch sử dụng cho vi xử lý mục tiêu.  
Ở tuần này, bài lab tập trung vào việc sử dụng **Crosstool-NG** để tạo một toolchain dành cho **vi xử lý ARM**, sử dụng **thư viện C musl**, sau đó kiểm tra hoạt động của toolchain thông qua **QEMU**.

---

## Nội dung chính thực hiện
- Thiết lập môi trường phát triển cho Crosstool-NG  
- Cấu hình và xây dựng toolchain cross-compile cho ARM  
- Kiểm tra toolchain bằng cách biên dịch chương trình C  
- Chạy thử chương trình ARM trên máy host thông qua QEMU  

---

## Chuẩn bị môi trường và dữ liệu
Bộ dữ liệu phục vụ cho bài lab đã được chuẩn bị sẵn, bao gồm các tập tin cần thiết cho quá trình thực hành sau này.  
Sau khi tải và giải nén, toàn bộ dữ liệu sẽ được lưu trữ trong thư mục làm việc chính và được sử dụng xuyên suốt các bài tiếp theo.

Bên cạnh đó, hệ thống cần được cập nhật đầy đủ và cài đặt các gói công cụ cần thiết để đảm bảo quá trình build toolchain diễn ra ổn định.  
Yêu cầu phần cứng tối thiểu là **4GB RAM** do quá trình biên dịch tiêu tốn nhiều tài nguyên.

---

## Cài đặt và build Crosstool-NG
Crosstool-NG được tải về từ kho mã nguồn chính thức và sử dụng phiên bản đã được kiểm chứng về độ ổn định.  
Do build trực tiếp từ mã nguồn Git, cần thực hiện bước bootstrap trước khi cấu hình và biên dịch.

Sau khi hoàn tất, Crosstool-NG sẽ được cài đặt cục bộ và sẵn sàng cho việc cấu hình toolchain.

---

## Cấu hình toolchain cho ARM
Toolchain được cấu hình thông qua giao diện `menuconfig` của Crosstool-NG.  
Một số lựa chọn quan trọng trong quá trình cấu hình bao gồm:

- Kiến trúc mục tiêu: **ARM**
- Hỗ trợ FPU phần cứng với chuẩn **vfpv3**
- Sử dụng **musl** làm thư viện C
- Trình biên dịch GCC phiên bản **13.2.0**
- Bật hỗ trợ ngôn ngữ C++
- Không tích hợp các thành phần debug để giảm độ phức tạp

Các thiết lập này nhằm tạo ra một toolchain gọn nhẹ, phù hợp cho môi trường nhúng.

---

## Xây dựng chuỗi công cụ
Sau khi cấu hình hoàn tất, toolchain được tiến hành xây dựng tự động bằng Crosstool-NG.  
Quá trình này mất khá nhiều thời gian (khoảng **30–60 phút**) tùy thuộc vào cấu hình hệ thống.

Sau khi build thành công, toolchain sẽ được cài đặt tại thư mục mặc định trong `$HOME/x-tools`.

---

## Kiểm tra và sử dụng toolchain
Toolchain sau khi xây dựng được thêm vào biến môi trường `PATH` để tiện sử dụng.  
Việc kiểm tra được thực hiện bằng cách gọi trình biên dịch ARM GCC và xác nhận thông tin phiên bản.

Tiếp theo, một chương trình C đơn giản được biên dịch bằng toolchain vừa tạo để kiểm tra khả năng sinh mã cho kiến trúc ARM.

---

## Chạy chương trình ARM bằng QEMU
Để kiểm tra chương trình ARM ngay trên máy host, QEMU ở chế độ user-mode được sử dụng.  
Chương trình ARM sau khi biên dịch sẽ được chạy thử thông qua QEMU cùng với sysroot của toolchain, giúp xác nhận rằng toolchain hoạt động chính xác.

---

## Nhận xét
Thông qua bài lab này, toolchain cross-compile cho ARM đã được xây dựng thành công từ Crosstool-NG và hoạt động đúng như mong đợi.  
Kết quả đạt được là nền tảng quan trọng cho các bài thực hành tiếp theo liên quan đến kernel, root filesystem và hệ thống nhúng Linux hoàn chỉnh.

---

## Ghi chú
Sau khi chắc chắn toolchain đã build thành công, có thể xóa các tệp trung gian để giải phóng dung lượng ổ đĩa nếu cần thiết.
