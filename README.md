# BTL Nhóm 3 -- Hệ thống phân loại sản phẩm theo màu sắc

## 1. Giới thiệu

Đây là repository của **BTL Nhóm 3** về đề tài **thiết kế hệ thống phân
loại sản phẩm theo màu sắc**.

Hệ thống sử dụng băng tải để vận chuyển sản phẩm, cảm biến hồng ngoại để
phát hiện sản phẩm, camera để thu nhận hình ảnh và xử lý màu sắc, cùng
các cơ cấu chấp hành để đưa sản phẩm vào vị trí tương ứng.

Trung tâm điều khiển của hệ thống là **ESP32**. Hệ thống sử dụng
**driver TMC2209 2A** để điều khiển động cơ bước và các servo cho cơ cấu
chấp hành. PC/Laptop được sử dụng để giám sát, thống kê và xử lý ảnh.

## 2. Chức năng chính

-   Khởi động và dừng hệ thống bằng các nút điều khiển.
-   Chọn chế độ **AUTO/MANUAL**.
-   Điều chỉnh tốc độ băng tải bằng núm vặn **SPEED**.
-   Phát hiện sản phẩm bằng cảm biến hồng ngoại.
-   Thu nhận hình ảnh trong buồng chụp camera.
-   Xử lý ảnh và phân biệt màu sắc trên PC/Laptop.
-   Điều khiển băng tải và các cơ cấu chấp hành để phân loại sản phẩm.
-   Có chức năng RESET và EMERGENCY STOP để vận hành an toàn.

## 3. Sơ đồ khối tổng thể

``` text
                         ┌─────────────────┐
                         │    PC / Laptop  │
                         │ Giám sát,       │
                         │ thống kê,       │
                         │ xử lý ảnh       │
                         └────────┬────────┘
                                  │
┌─────────────────┐               ▼
│ Các nút điều    │      ┌──────────────────┐
│ khiển           ├─────►│ Mạch điều khiển  │
│ START / STOP    │      │      ESP32       │
│ RESET / E-STOP  │      └────────┬─────────┘
│ AUTO / MANUAL   │               │
│ SPEED           │               │
└─────────────────┘               │
                                  ▼
                         ┌─────────────────┐
                         │ Các cơ cấu      │
                         │ chấp hành       │
                         └────────┬────────┘
                                  │
                 ┌────────────────┼────────────────┐
                 ▼                ▼                ▼
             Băng tải       Cơ cấu đẩy       Cơ cấu trượt
                            bằng servo        hứng vật

          Cảm biến hồng ngoại ──► phát hiện sản phẩm

          Buồng chụp camera ──► camera + đèn
```

## 4. Các khối của hệ thống

### Mạch điều khiển

Trung tâm điều khiển là **ESP32**.

Các thành phần liên quan gồm:

-   Driver điều khiển động cơ bước: **TMC2209 2A**.
-   Mạch điều khiển servo **MG946R**.
-   Các tín hiệu từ nút điều khiển và cảm biến.
-   Tín hiệu điều khiển đến các cơ cấu chấp hành.

### Các nút điều khiển

  Nút / công tắc   Chức năng
  ---------------- ------------------------------------
  START            Khởi động hệ thống
  STOP             Dừng hệ thống
  RESET            Đưa hệ thống về trạng thái ban đầu
  EMERGENCY STOP   Dừng khẩn cấp
  AUTO/MANUAL      Chọn chế độ tự động hoặc thủ công
  SPEED            Điều chỉnh tốc độ băng tải

### Cảm biến hồng ngoại

Cảm biến hồng ngoại có nhiệm vụ **phát hiện vật đến gần**, từ đó cung
cấp tín hiệu cho hệ thống điều khiển để thực hiện quá trình nhận dạng và
phân loại.

### Buồng chụp camera

Buồng chụp gồm **đèn và camera**, tạo môi trường chụp ổn định để phục vụ
quá trình nhận dạng màu sắc.

Camera dự kiến sử dụng **OV7670 + FIFO AL422**.

### Cơ cấu đẩy bằng servo

Cơ cấu đẩy sử dụng servo và cơ cấu bánh răng để **biến chuyển động quay
thành chuyển động thẳng**, từ đó đẩy sản phẩm sang vị trí cần thiết.

### Cơ cấu trượt hứng vật

Cơ cấu trượt có nhiệm vụ hứng và dẫn sản phẩm sau khi được phân loại.

## 5. Phần mềm và xử lý

PC/Laptop thực hiện:

-   Giám sát hệ thống.
-   Thống kê dữ liệu.
-   Xử lý hình ảnh.
-   Hỗ trợ giao tiếp với hệ thống điều khiển.

ESP32 thực hiện:

-   Nhận tín hiệu từ cảm biến và nút điều khiển.
-   Điều khiển động cơ bước thông qua TMC2209.
-   Điều khiển servo.
-   Thực hiện logic điều khiển của hệ thống.

## 6. Thành viên nhóm

  ------------------------------------------------------------------------
  Thành viên                                    MSSV Phân công
  --------------------- ---------------------------- ---------------------
  **Phạm Thanh Triều**                  **23021363** Thiết kế app giao
                                                     diện, cơ cấu chấp
                                                     hành, truyền thông

  **Nguyễn Đình Trung**                 **23021367** Điều chỉnh hệ thống
                                                     phân biệt màu sắc,
                                                     truyền thông với
                                                     camera

  **Nguyễn Hoàng Tuyển**                **23021351** Thiết kế mạch điện
                                                     tử, thuật toán điều
                                                     khiển
                                                     
  ------------------------------------------------------------------------

## 7. Thông tin nhóm

**BTL -- Nhóm 3**

Đề tài: **Hệ thống phân loại sản phẩm theo màu sắc**

### Thành viên

-   Phạm Thanh Triều -- 23021363
-   Nguyễn Đình Trung -- 23021367
-   Nguyễn Hoàng Tuyển -- 23021351

------------------------------------------------------------------------

> Repository phục vụ quá trình phát triển, thử nghiệm và hoàn thiện BTL
> của Nhóm 3.
