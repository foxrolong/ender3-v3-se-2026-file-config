FOXRO 5.0.0 - Hướng dẫn cài Klipper Ender 3 V3 SE

về main board máy in của tôi:
Ender 3 V3 SE
Main: CR4NS200320C14
Có chip CH340G
lưu ý - mã máy cho cài đặt sau này

cách thiết lập cài đặt
lưu ý trước khi làm:
nếu dùng Raspberry Pi mọi người nên dùng bản FOXRO KIAUH riêng của bạn thay cho bản gốc: <YOUR_FORK_URL>

BƯỚC 1:

Thiết lập Raspberry Pi
FOXRO KIAUH
Các bước cài đặt FOXRO KIAUH
Cài đặt Klipper và các gói cần thiết
Cài đặt Klipper
Cài đặt Moonraker
Lắp đặt buồm mũi hoặc buồm chính
Cấu hình
Tạo phần mềm máy in (tệp .bin)
Máy in 3D Flash
Hiệu chuẩn
Hiệu chỉnh hệ số PID
Hiệu chỉnh độ lệch Z
Các cài đặt và cấu hình bổ sung
TRẠI HÈ
Bù xoắn trục
Hiệu chỉnh áp suất tăng
Lời kết
Quyên góp Ko-fiGiúp giữ cho trang web không có quảng cáo
Tổng quan về dự ánLiên kết thường trực
Dự án này bao gồm việc thay đổi phần mềm Marlin mặc định đi kèm với Ender 3 V3 SE từ phiên bản gốc sang Klipper. Ngoài sự hỗ trợ khổng lồ mà bạn có thể tìm thấy trực tuyến, Klipper còn mang lại một số lợi ích khác, ví dụ:

Gửi mã Gcode trực tiếp từ máy tính của bạn thay vì chuyển thủ công từ thẻ SD
Giám sát từ xa và gửi lệnh
Giao diện web bạn có thể truy cập từ bất kỳ thiết bị nào trong nhà
Cải thiện khả năng cân bằng giường với TRẠI HÈ
Sự tăng áp suất và định hình đầu vào
Yêu cầuLiên kết thường trực
An Ender 3 V3 SE
Một chiếc Raspberry Pi (hoặc PC) chạy hệ điều hành Linux
Thẻ nhớ microSD cho Raspberry Pi
Bộ nguồn cho Raspberry Pi
Thẻ SD
Cáp USB C sang USB A để kết nối Ender và Pi
Tuyên bố miễn trừ trách nhiệm: Màn hình Ender 3 V3 SE hiện chưa tương thích với Klipper (chưa), vì vậy bạn sẽ mất khả năng điều khiển máy in từ núm xoay màn hình. Tuy nhiên, có một số giải pháp như sau: kho lưu trữ này để khôi phục một số chức năng của màn hình

Lắp đặtLiên kết thường trực
Thiết lập Raspberry PiLiên kết thường trực
Bước đầu tiên là phải có một chiếc Raspberry Pi (hoặc PC) hoạt động tốt mà bạn có thể kết nối SSH vào. Nếu bạn đã làm rồi, bạn có thể bỏ qua bước này. Nếu bạn không làm vậy, thì vẫn còn một hướng dẫn tuyệt vời Hướng dẫn thiết lập do nhóm Raspberry Pi thực hiện.

Các bước thực hiện mà không cần đi vào chi tiết là:

Cài đặt Raspberry Pi Imager
Chọn thiết bị của bạn (bạn đang sử dụng Raspberry Pi nào)
Hãy chọn hệ điều hành (tôi khuyên dùng phiên bản nhẹ của Raspberry Pi OS)
Chọn thiết bị lưu trữ của bạn (thẻ microSD mà bạn sẽ cài đặt vào Raspberry Pi)
Tùy chỉnh hệ điều hành để tạo tên người dùng và mật khẩu, thêm thông tin đăng nhập Wi-Fi, thiết lập tên máy chủ và bật SSH
Nhấp nháy thẻ nhớ microSD
Cắm thẻ nhớ microSD vào Raspberry Pi của bạn
Kết nối nguồn điện
Kết nối SSH vào Raspberry Pi của bạn
FOXRO KIAUH Liên kết thường trực
Sau khi thiết lập xong Raspberry Pi và kết nối SSH, bạn có thể tiến hành tải xuống và cài đặt FOXRO KIAUH. Đây là bản fork riêng để cài đặt Klipper và các thành phần cần thiết như Moonraker, Fluidd hoặc Mainsail.

Các bước cài đặt FOXRO KIAUH Liên kết thường trực
Điều kiện tiên quyết để cài đặt FOXRO KIAUH là phải cài đặt Git. Nếu bạn chưa cài đặt nó (hoặc nếu không chắc chắn), hãy chạy lệnh sau:

Sao chép mãsudo apt-get update && sudo apt-get install git -y
Sau khi cài đặt Git, hãy chạy lệnh sau để sao chép FOXRO KIAUH vào thư mục chính của bạn:

Sao chép mãcd ~ && git clone <YOUR_FORK_URL> kiauh
Sau khi sao chép thành công, hãy chạy FOXRO KIAUH bằng lệnh sau:

Sao chép mã./kiauh/kiauh.sh
Cài đặt Klipper và các gói cần thiếtLiên kết thường trực
Giờ bạn sẽ thấy một màn hình tương tự như hình bên dưới, đó là menu chính của FOXRO KIAUH, từ đó chúng ta sẽ cài đặt các gói cần thiết để chạy Klipper.

Ảnh chụp màn hình menu chính của FOXRO KIAUH
Menu chính của FOXRO KIAUH
Các gói cần thiết để cài đặt sẽ là:

Klipper
Moonraker
Buồm mềm hoặc buồm chính
Cài đặt KlipperLiên kết thường trực
Để cài đặt từng gói, chúng ta phải nhập: 1 (để cài đặt) và nhấn Enter, thao tác này sẽ đưa chúng ta đến màn hình sau:

Ảnh chụp màn hình menu cài đặt FOXRO KIAUH
Menu cài đặt FOXRO KIAUH
Bây giờ chúng ta phải gõ: 1 (cho Klipper) và nhấn Enter một lần nữa. Sau đó, hãy làm theo bất kỳ hướng dẫn nào xuất hiện để hoàn tất quá trình cài đặt.

Cài đặt MoonrakerLiên kết thường trực
Để cài đặt Moonraker, chúng ta phải lặp lại các bước ở trên nhưng chọn Moonraker ở màn hình thứ hai. Các bước sẽ như sau:

Chạy FOXRO KIAUH hoặc vào Menu chính nếu đang chạy
Nhập “1” (không có dấu ngoặc kép) và nhấn Enter
Nhập “2” (không có dấu ngoặc kép) và nhấn Enter
Hãy làm theo hướng dẫn để cài đặt
Lắp đặt buồm mũi hoặc buồm chínhLiên kết thường trực
Fluidd và Cánh buồm chính Đây là giao diện người dùng của Klipper, chúng ta sẽ tương tác với chúng để gửi lệnh đến máy in của mình. Việc lựa chọn hoàn toàn phụ thuộc vào sở thích cá nhân, vì vậy bạn có thể truy cập trang web của họ và xem trang nào bạn thích nhất, chức năng của chúng về cơ bản là giống nhau.

Để cài đặt một trong số chúng, chúng ta phải lặp lại các bước ở trên nhưng chọn tùy chọn của mình ở màn hình thứ hai. Các bước sẽ như sau:

Chạy FOXRO KIAUH hoặc vào Menu chính nếu đang chạy
Nhập “1” (không có dấu ngoặc kép) và nhấn Enter
Nhập “3” HOẶC “4” (không có dấu ngoặc kép) và nhấn Enter
Hãy làm theo hướng dẫn để cài đặt
Cấu hìnhLiên kết thường trực
Sau khi hoàn tất các bước trên, bạn có thể truy cập giao diện web của mình bằng cách vào http://[hostname-of-your-pi].local và bạn sẽ thấy điều tương tự như thế này:

Ảnh chụp màn hình menu chính của Fluidd
Menu chính Fluid
Tiếp theo, bạn cần vào tab Cấu hình (hình bên dưới) và bạn sẽ thấy một printer.cfg tệp và một macro.cfg tài liệu. Nếu không thấy các tệp đó, bạn có thể tạo chúng bằng cách nhấp vào nút ‘+’ ở đầu danh sách tệp.

Ảnh chụp màn hình menu cấu hình Fluidd
Menu cấu hình Fluidd
Sau đó, hãy truy cập một trong nhiều kho lưu trữ Github để lấy tệp cấu hình đã được thiết lập sẵn. Tôi khuyên bạn nên thử bootuz-dinamon. Sao chép và dán nội dung của printer.cfg và macro.cfg vào của bạn.

Cập nhật năm 2025: Tôi khuyên bạn nên thử shubham0x13’s Tệp cấu hình này có một số nâng cấp so với tệp cấu hình của Bootuz. Sao chép và dán nội dung của printer.cfg và macro.cfg vào của bạn.

Tạo phần mềm máy in (tệp .bin)Liên kết thường trực
Hãy đảm bảo thẻ SD của bạn được định dạng FAT32 với kích thước phân bổ là 4096, nếu không bạn có thể gặp sự cố và không thể flash

Bản cập nhật năm 2025 cảm ơn @derlaft: Trên màn hình máy in, hãy kiểm tra “phiên bản phần cứng” của bạn. Nếu đó là “CR4NS200320C14” thì bạn đang sử dụng phiên bản bo mạch chủ mới. Hãy ghi nhớ điều này cho bước 2:

Để tạo firmware thực tế sẽ chạy trong máy in 3D của bạn, bạn cần biên dịch firmware trên Raspberry Pi. Để thực hiện điều này, bạn cần làm theo các bước sau:

Đi đến /klipper Mở thư mục và chạy lệnh menuconfig bằng cách chạy đoạn mã sau:

Sao chép mãcd ~/klipper/
make menuconfig
Chọn các thiết lập sau tùy thuộc vào bo mạch chủ của bạn:

Sao chép mãOriginal motherboard:
- Micro-controller architecture: STMicroelectronics STM32
- Processor model: STM32F103
- Bootloader offset: 28KiB
- Communication interface: Serial (on USART1 PA10/PA09)

New motherboard:
- Micro-controller architecture: STMicroelectronics STM32
- Processor model: STM32F401
- Bootloader offset: 64KiB
- Communication interface: Serial (on USART1 PA10/PA9)
Sau khi chọn tất cả các tùy chọn, hãy nhấn phím q và lưu các thay đổi, sau đó chạy lệnh:

Sao chép mãmake
Máy in 3D FlashLiên kết thường trực
Sau khi hoàn thành, sẽ có một klipper.bin tệp trong klipper/out/ thư mục. Để lấy được tập tin, bạn cần sao chép nó từ Raspberry Pi sang máy tính, nhưng trước tiên chúng ta phải di chuyển nó từ nơi nó được tạo ra đến một thư mục mà Fluidd/Mainsail có thể truy cập.

Để di chuyển tập tin, hãy kết nối SSH vào Raspberry Pi của bạn và điều hướng đến trang sau: klipper/out/ Mở thư mục bằng cách chạy lệnh sau:

Sao chép mãcd ~/klipper/out
Sau đó chạy ls Lệnh này dùng để xác nhận tệp tin có tồn tại hay không, và nếu có, bạn có thể gửi nó đến địa chỉ của mình config để thư mục hiển thị từ Fluidd/Mainsail bằng cách chạy lệnh sau:

Sao chép mãcp klipper.bin ~/printer_data/config/
Lưu ý: Nếu bạn gặp lỗi “Không tìm thấy tệp hoặc thư mục”, bạn cần xác minh rằng các bước trước đó (biên dịch firmware) đã được thực hiện chính xác và tìm vị trí của tệp đó klipper/out/ hoặc printer_data/config/ Trong Raspberry Pi của bạn, hãy sửa đổi các lệnh trước đó cho phù hợp.

Giờ đây, khi bạn vào tab cấu hình của giao diện người dùng Fluid/Mainsail, klipper.bin Tệp tin sẽ nằm ở đó để bạn chỉ cần nhấp chuột phải và tải xuống máy tính của mình. Sau khi tải xuống tệp, các bước tiếp theo là:

Nếu bạn có phiên bản bo mạch chủ mới: hãy tạo một thư mục có tên là STM32F4_UPDATE trong thẻ SD của bạn và di chuyển klipper.bin Hãy lưu tệp vào đó, sau đó chuyển sang bước 2. Nếu bạn có bo mạch chủ cũ, hãy thực hiện theo các bước dưới đây.

Chuyển klipper.bin sao chép tệp vào thẻ SD của máy in
Tắt máy in
Lắp thẻ SD
Bật máy in và đợi 15 giây
Tắt máy in
Tháo thẻ SD ra và xóa tệp .bin
Lắp thẻ SD trống vào máy in
Bật máy in (màn hình sẽ hiển thị hình ảnh bảo vệ màn hình màu xanh lam)
Kết nối Raspberry Pi của bạn với máy in thông qua cáp USB
Truy cập giao diện web Fluidd hoặc Mainsail của bạn
Máy in sẽ ở đó và bạn sẽ thấy một cái gì đó tương tự như thế này:

Ảnh chụp màn hình menu chính của Fluidd
Menu chính Fluid
Trong trường hợp máy in không được nhận diện, hãy kết nối SSH vào Raspberry Pi của bạn và chạy lệnh sau:

Sao chép mãdmesg | grep usb
Sau khi chạy, kết quả sẽ hiển thị như thế này:

ảnh chụp màn hình của một thiết bị đầu cuối
Dòng bạn nên tìm
Sau đó điều hướng đến máy in của bạn printer.cfg tệp và tìm kiếm [mcu] khối mã. Phải có 2 dòng bên dưới bắt đầu bằng “serial:”. Chú thích dòng dài bằng cách thêm “#” vào đầu (không có dấu ngoặc kép) và bỏ chú thích dòng ngắn, thay đổi giá trị thành giá trị bạn nhận được khi chạy lệnh trước đó.

Giờ thì bạn đã có một chiếc Ender 3 V3 SE hoạt động tốt với Klipper được cài đặt rồi, chúc mừng! Giờ bạn có thể tiếp tục đến phần hiệu chuẩn để hiệu chỉnh máy in và bắt đầu in.

Hiệu chuẩnLiên kết thường trực
Hiệu chỉnh hệ số PIDLiên kết thường trực
Vào giao diện web chính của Fluidd hoặc Mainsail và cuộn xuống mục “Macro”. Sau đó chạy PID_BED và PID_EXTRUDER. Chạy một cái trước, và sau khi nó kết thúc, hãy chạy cái còn lại.

ảnh chụp màn hình hộp macro
Hộp macro
Lưu ý: Nếu macro không xuất hiện trên màn hình chính hoặc không chạy, hãy vào printer.cfg và thêm vào [include macro.cfg] ở đâu đó trong tập tin

Hiệu chỉnh độ lệch ZLiên kết thường trực
Để hiệu chỉnh Z-Offset, hãy vào tab Tune ở bên trái và nhấp vào “Hiệu chỉnh” để tạo ma trận lưới của giường.

ảnh chụp màn hình menu lưới giường
Menu lưới giường
Sau khi quá trình tạo hoàn tất, hãy vào tab Trang chủ, sau đó vào hộp công cụ và chọn PROBE_CALIBRATE trong menu thả xuống “Công cụ”.

ảnh chụp màn hình hộp công cụ
Hộp dụng cụ
Lấy một tờ giấy và chạy thử bài kiểm tra giấy Để hiệu chỉnh độ lệch Z chính xác cho máy in của bạn, hãy điều chỉnh các giá trị bằng cách nhấp vào các nút ‘+’ hoặc ‘-‘ xuất hiện. Bạn có thể di chuyển tờ giấy nhưng cần có lực cản nhất định. Tôi đã đạt được kết quả tốt hơn khi làm việc này khi máy in nguội, nhưng một số người khuyên nên làm khi vòi phun và đế in ở nhiệt độ hoạt động, hãy thử xem cái nào phù hợp nhất với bạn.

ảnh chụp màn hình menu thăm dò thủ công
Menu thăm dò thủ công
Các cài đặt và cấu hình bổ sungLiên kết thường trực
TRẠI HÈLiên kết thường trực
Tôi đặc biệt khuyên bạn nên cài đặt Klipper Adaptive Meshing & Purging (TRẠI HÈ) để tận dụng tối đa lợi ích của việc cải thiện độ bằng phẳng của giường và hệ thống làm sạch thích ứng. Các bước cài đặt trên trang web của họ khá đơn giản nhưng tôi cũng sẽ cung cấp chúng ở đây.

Trước tiên bạn cần định nghĩa [exclude_object] trong của bạn printer.cfg tài liệu.

Hãy đến chỗ bạn printer.cfg tệp và thêm một dòng có nội dung như sau: [exclude_object]
ảnh chụp màn hình của mô-đun đối tượng loại trừ
Loại trừ mô-đun đối tượng
Hãy đến chỗ bạn moonraker.conf tệp và thêm 2 dòng

Sao chép mã[file_manager]
enable_object_processing: True
Hãy đảm bảo vào trình cắt lát của bạn và bật tùy chọn “Label Objects”. Tôi sử dụng Cura và nó tự động gắn nhãn cho các đối tượng.

(Các bước tiếp theo được sao chép từ KAMP Github)

Kết nối SSH vào Raspberry Pi của bạn và thực hiện các lệnh sau:

Sao chép mã cd

 git clone https://github.com/kyleisah/Klipper-Adaptive-Meshing-Purging.git

 ln -s ~/Klipper-Adaptive-Meshing-Purging/Configuration printer_data/config/KAMP

 cp ~/Klipper-Adaptive-Meshing-Purging/Configuration/KAMP_Settings.cfg ~/printer_data/config/KAMP_Settings.cfg
Lưu ý: Thao tác này sẽ chuyển đến thư mục chính, sao chép kho lưu trữ KAMP, tạo liên kết tượng trưng của kho lưu trữ đến thư mục cấu hình máy in của bạn và tạo một bản sao của KAMP_Settings.cfg Trong thư mục cấu hình của bạn, sẵn sàng để chỉnh sửa.

Cũng có khả năng với các thiết lập cũ hơn của klipper hoặc moonraker, đường dẫn cấu hình của bạn sẽ khác. Hãy đảm bảo sử dụng đường dẫn cấu hình chính xác cho máy của bạn khi tạo liên kết tượng trưng và khi sao chép KAMP_Settings.cfg vào thư mục cấu hình của bạn.

Mở của bạn moonraker.conf Tệp và thêm cấu hình này:

Sao chép mã[update_manager Klipper-Adaptive-Meshing-Purging]
type: git_repo
channel: dev
path: ~/Klipper-Adaptive-Meshing-Purging
origin: https://github.com/kyleisah/Klipper-Adaptive-Meshing-Purging.git
managed_services: klipper
primary_branch: main
Lưu ý: Mỗi khi cấu hình Moonraker thay đổi, cần phải khởi động lại hệ thống để các thay đổi có hiệu lực. Nếu bạn không muốn Moonraker thông báo cho bạn về các bản cập nhật trong tương lai của KAMP, hãy bỏ qua bước này.

Tùy thuộc vào những tính năng bạn muốn từ KAMP, bạn sẽ cần phải [include] một số tệp trong KAMP_Settings.cfg:



Lưu ý: Các tệp cấu hình KAMP được chia nhỏ như vậy để những người không sử dụng đầu dò giường có thể hưởng lợi từ tính năng làm sạch thích ứng và các tính năng khác.

Sau bạn [include] Đối với các tính năng bạn muốn, hãy nhớ khởi động lại firmware để các tính năng đó có hiệu lực. Đừng quên thêm [include KAMP_Settings.cfg] đến của bạn printer.cfg!
Bù xoắn trụcLiên kết thường trực
Tôi nhận thấy nhiều người dường như gặp vấn đề với việc san bằng giường ngay cả sau khi đã xem xét tất cả các giải pháp khả thi. Vấn đề tôi gặp phải là hầu hết các máy in Ender 3 V3 SE đều có một chút độ xoắn ở thanh chữ X, làm sai lệch kết quả về độ cân bằng của bàn in. Video này Nero3D giải thích vấn đề khá chi tiết. Tôi khuyên bạn nên bật Bù xoắn trục Hãy thiết lập mô-đun và cài đặt nó để máy in của bạn hoạt động trơn tru.

Hiệu chỉnh áp suất tăngLiên kết thường trực
Pressure Advance là một cách tuyệt vời khác để cải thiện chất lượng bản in của bạn, tôi khuyên bạn nên làm theo tài liệu hướng dẫn của Klipper Áp suất tăng để điều chỉnh cho đúng.

Lời kếtLiên kết thường trực
Tôi hy vọng hướng dẫn này hữu ích với bạn và giúp bạn cài đặt và vận hành được Ender 3 V3 SE bằng Klipper. Tôi cũng muốn ghi nhận những hướng dẫn và video mà tôi đã làm theo để thiết lập ban đầu:

arismelachroinos tuyệt vời bài đăng trên Reddit
Video BootUse UA (Tiếng Ukraina có phụ đề tiếng Anh)
Ender 3 V3 SE của pblvsky hướng dẫn
Nếu bạn gặp bất kỳ vấn đề nào trong quá trình làm theo hướng dẫn này, đừng ngần ngại liên hệ với tôi và tôi sẽ cố gắng hết sức để giúp bạn. Chúc bạn in ấn vui vẻ!