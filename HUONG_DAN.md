# Spectrum Studio 1.2.4

Trên Windows, giải nén **toàn bộ** `SpectrumStudio-Windows-1.2.4-portable.zip`, mở thư mục `SpectrumStudio` rồi chạy `SpectrumStudio.exe`. Giữ `_internal` bên cạnh EXE. Không cần cài Python hoặc FFmpeg. Khi cập nhật, giải nén bản mới vào thư mục mới; thư viện preset được lưu riêng trong dữ liệu ứng dụng.

## Bộ đệm âm thanh — bản 1.2.4

Audio cache là dữ liệu âm thanh đã giải mã để phân tích sóng và tua, không phải tệp nhạc gốc. Dạng mono 48 kHz float32 hiện tại cần khoảng 11,52 MB mỗi phút nhạc. Cache dùng chung tại `%LOCALAPPDATA%\SpectrumStudio\AudioCache` và tự dọn tệp cũ không còn dùng để hướng tới giới hạn tổng 512 MiB.

Vào **Cài đặt → Bộ đệm âm thanh → Dọn bộ đệm không sử dụng** để giải phóng dữ liệu đã tạo. Nhạc gốc và preset được giữ nguyên. Bài đang mở được bảo vệ, có thể tạm vượt giới hạn; bài lớn hơn giới hạn sẽ được dọn khi đóng lần sử dụng cuối cùng. Các thư mục `.audio-cache` của bản cũ không được tự tìm hay tự xóa.

Bản này dùng ảnh hoàn chỉnh từ renderer GPU để hiển thị preview và không chờ tác vụ preview khi thay bài hát. Dữ liệu của bài cũ được giữ tới khi tác vụ đang đọc nó hoàn tất.

Preview, các nút Mở nhạc/Phát/Đánh dấu và ba thanh thời gian nằm gọn trong
phần bên trái 3/5 cửa sổ. Bảng chỉnh thành phần bên phải 2/5 kéo dài xuống dưới
để có thêm chỗ sửa sóng. Cài đặt cỡ chữ vẫn cho phép tăng/giảm mật độ thông tin.

## Hiệu ứng và tỷ lệ ảnh — bản 1.2

Trong Image, mở **Ảnh / Hiệu ứng suốt bài** và chọn Không, Đập theo nhạc,
Nhiễu méo ảnh, Nhiễu nước hoặc Glitch. Với các hiệu ứng lặp, **Chu kỳ** là thời
gian từ đầu lượt này đến đầu lượt sau; **Thời lượng** là phần có hiệu ứng trong
mỗi chu kỳ; **Lần đầu bắt đầu** là vị trí bắt đầu tính trên bài hát. Ví dụ chu kỳ 5 giây,
thời lượng 1 giây, bắt đầu 2 giây sẽ chạy ở giây 2–3, 7–8, 12–13… Có thể chỉnh
cường độ, kích cỡ vùng, tần số, tốc độ và hạt ngẫu nhiên. Các hiệu ứng tự chạy
theo thời gian cả bài, không cần thêm một thành phần cho mỗi lượt.

**Màu đầu / Màu đích** kết hợp chế độ cố định, theo nhạc hoặc theo chu kỳ. Theo
nhạc dùng Audio Spectrum đã chọn; đổi màu không tự phóng to ảnh. Chọn riêng
Đập theo nhạc khi muốn ảnh co/phóng theo beat.

Trong Nguồn, chọn **Vừa khung** để giữ đủ ảnh, **Phủ kín** để chủ động cắt phần
dư hoặc **Kéo giãn** để lấp khung tự do. Chọn tỷ lệ gốc hay tỷ lệ có sẵn và bật
khóa tỷ lệ để liên kết rộng/cao ở General và keyframe. Scale đồng đều tăng/giảm
toàn ảnh; nội dung vượt biên video vẫn bị cắt theo khung video. Dự án cũ giữ
nguyên kích thước đã lưu.

## Làm intro và chuyển động lặp bằng keyframe

Ảnh import vẫn là một thành phần Image. Mỗi keyframe lưu trạng thái của chính ảnh đó: **X/Y/Z, rộng/cao, scale đồng đều, xoay X/Y/Z, độ trong, độ sáng và tách RGB**. App tính các trạng thái ở giữa theo 12 kiểu nội suy; mặc định Mượt tăng tốc và giảm tốc nhẹ ở hai đầu.

1. Import ảnh vào Image, mở nhóm **Keyframe** và bật hoạt ảnh.
2. Đặt **thời điểm bắt đầu trên video** và **thời lượng**. Thời gian nhập dạng `phút:giây`, hỗ trợ phần nghìn giây, ví dụ `00:05.250`.
3. Nhập **Thời điểm đánh dấu trên video** rồi bấm **Thêm tại thời gian nhập**. Không cần phát bài nhạc đến vị trí đó. Chọn một mốc trên thanh hình thoi để tua tới nó; chỉnh các thông số của mốc để xem kết quả. **Lấy thời gian cả bài hát** lấy thời lượng nhạc và co giãn thời gian các mốc theo cùng tỷ lệ.
4. Thêm các mốc tiếp theo. Mỗi mốc có kiểu chuyển động cho đoạn đi tới mốc kế tiếp. Giá trị xoay nội suy trực tiếp: từ 0° tới 360° là một vòng đầy đủ.
5. Bật **ẩn ngoài đoạn** khi chỉ muốn ảnh xuất hiện trong đoạn intro. Bên trong đoạn, trạng thái trước mốc đầu và sau mốc cuối được giữ cho tới biên đoạn. Thời lượng luôn đủ chứa mốc cuối.

Bỏ **Lấy thời gian cả bài hát** để bật **Lặp keyframe suốt bài hát** và nhập
chu kỳ lặp. Đoạn 2 giây với chu kỳ 5 giây chạy lại mỗi 5 giây từ vị trí bắt đầu;
3 giây còn lại là khoảng nghỉ, ảnh ẩn hoặc giữ mốc cuối tùy ẩn ngoài đoạn. Nhập
mốc tại thời điểm của một lượt lặp sẽ chỉnh mốc cục bộ tương ứng. Muốn vòng
lặp nối êm, đặt mốc cuối cùng về trạng thái giống mốc đầu.

**Ví dụ vị trí trên video:** đặt bắt đầu `00:05`, thời lượng `00:03`; mốc cục bộ `00:00` là giây 5 của video, `00:00.600` là giây 5,6 và `00:03` là giây 8. Đổi thời điểm bắt đầu sẽ di chuyển toàn bộ hoạt ảnh, giữ nguyên khoảng cách giữa các mốc.

Chỉnh thông số trong nhóm Keyframe để sửa trạng thái đang chọn. General giữ thông số tĩnh của ảnh; chức năng chụp General cho phép đưa các thông số đó vào một mốc. Xóa hoặc di chuyển một mốc có thể Undo/Redo. Tắt hoạt ảnh sẽ dùng lại trạng thái General.

Có mẫu intro ngắn để bắt đầu nhanh và preset minh họa `examples/04-Intro-Image-Keyframes.TS`. Keyframe đi cùng ảnh khi lưu/mở `.TS`. Hiệu ứng ảnh, mask và phản ứng theo nhạc vẫn tiếp tục áp dụng. Khi dùng keyframe, thời gian và In/Out cũ của Image được ẩn và bỏ qua; tắt keyframe sẽ dùng lại dữ liệu cũ. Preview và xuất video cùng tính theo thời gian cảnh, nên tua ngược hoặc render từng đoạn không cần chạy lại từ đầu. Phần đặt ảnh và biến đổi GPU sử dụng lại nội dung ảnh khi có thể; FPS thực tế phụ thuộc kích thước ảnh, hiệu ứng và phần cứng.

**Sao chép mã keyframe** chép chuyển động dạng JSON; **Nhập / xem mã** cho phép dán vào Image khác hoặc bản Avee Android mới. Ảnh và General của thành phần đích được giữ nguyên. Xoay X/Y dùng để lật 3D, xoay Z xoay trên mặt phẳng; chiều sâu Z đưa ảnh gần hoặc xa. Scale 1 và độ sáng 1 giữ nguyên; tách RGB 0 tắt hiệu ứng, giá trị tính theo chiều rộng video. Xem `CHANGES_1.2.0.md` và `docs/image-keyframe-code-v2.md`.

## Các điều khiển mới ở 1.0.0

- Trong Sóng / Bar, bật **Flip input** để đảo thứ tự dải âm thanh trái/phải; dạng tròn đảo chiều đi quanh vòng. Hướng vươn của biên độ và tùy chọn đối xứng trên/dưới được giữ nguyên.
- Trong Dịch chuyển, nhập thời gian `phút:giây`: `01:30` là 90 giây, `02:05.250` là 2 phút 5,25 giây.
- Trong Ảnh / Nguồn, chọn **Hình có sẵn**: vuông trắng, tròn hoặc tròn viền mờ dần. Có thể tô màu bằng màu của thành phần.
- Trong **Ảnh / Nâng cao**, bật **Tách nền**, giữ màu đen mặc định hoặc chọn màu cần xóa. Dùng **+ Thêm màu cần xóa** để chọn nhiều màu. Dung sai 0 xóa đúng màu; tăng nhẹ nếu nền có nhiều sắc gần nhau. Điểm ảnh không khớp màu được giữ. Khi lưu `.TS`, danh sách màu đi cùng preset.
- Điều khiển **Uốn cong 2D & 3D** nằm trong một nhóm; hai chế độ vẫn bật/tắt và chỉnh độc lập.
- Khi kéo tới Composition nằm dưới, giữ con trỏ gần mép dưới cây để tự cuộn; rê giữ trên Composition thu gọn để mở nó rồi thả.
- Trong Cài đặt, chọn **FPS mục tiêu xem trước 30/60/120**. Chất lượng **Tự động** sẽ điều chỉnh độ phân giải theo khả năng máy. FPS đạt được tùy cảnh và phần cứng.
- Trong Export, **Bitrate video** chọn Tự động hoặc 0,1–200 Mbps. Đây là tốc độ bit trung bình; cảnh đơn giản có thể dùng ít hơn. Âm thanh AAC 192 kbps tính riêng. Giá trị cao thường tăng chất lượng và dung lượng, không làm cảnh render nhanh hơn.

Xem `CHANGES_1.0.0.md` để biết chi tiết và kết quả đo hiệu năng.

Trên Linux x86_64 (Debian 12 / Ubuntu 24.04 hoặc mới hơn, glibc 2.36+), cấp quyền chạy cho AppImage rồi mở. Xem `LINUX.md` về quyền chạy, FUSE và trình điều khiển đồ họa. Preset vẫn dùng `.TS`; thư viện mặc định ở `~/.local/share/AveeStudio/library-v1`.

## Tab dự án và render song song

Thanh tab trên đầu cửa sổ có **+** thêm, **×** đóng và kéo để đổi thứ tự. Mỗi tab giữ dự án, bài nhạc, vị trí phát, lựa chọn thành phần và Undo/Redo riêng. **Ctrl+T** thêm, **Ctrl+W** đóng, **Ctrl+Tab / Ctrl+Shift+Tab** chuyển tab; đổi phím trong Cài đặt. Mở lại một preset đã có tab sẽ chuyển về tab đó.

Chuyển tab dừng nhạc/preview cũ và không tự phát tab mới. Tab nền không dựng preview, nhưng render vẫn chạy. Hàng tiến trình của từng tab nằm dưới toolbar: bấm tên để chuyển về tab, Hủy để dừng riêng lượt đó; × ẩn kết quả đã xong. Không đóng/thay nguồn nhạc hoặc preset của tab đang xuất; hãy hủy hoặc chờ xong trước. Chỉnh thông số trong khi render chỉ áp dụng cho lượt sau, vì mỗi lượt xuất dùng bản chụp dự án lúc bắt đầu.

Hộp Render kiểm tra kích thước, FPS, thời gian, số lượt đang chạy, RAM trống và RAM dự trù, tự cập nhật mỗi 2 giây. Ước tính dựa trên khung hình, hiệu ứng và bộ đệm; không phải cam kết chính xác. RAM thiếu sẽ chặn bắt đầu thêm; nhiều lượt chia sẻ CPU/GPU nên không đảm bảo nhanh hơn. Mỗi lượt phải có đường dẫn MP4 riêng.

Trong khi xuất, RAM cao làm giảm tốc dựng khung; RAM gần đầy sẽ nhả cache renderer và tạm dừng chờ. Nếu phục hồi, tiếp tục đúng khung mà không thay đổi chất lượng/FPS, không xuất lại từ đầu. Cơ chế này theo dõi RAM hệ thống trên Windows và Linux; không dùng phần trăm GPU làm dấu hiệu thiếu bộ nhớ.

Khi RAM thiếu nghiêm trọng liên tục và có nhiều lượt xuất, app cảnh báo ở hàng tiến trình rồi dừng **lượt mới mở nhất**. App chờ lượt đó giải phóng tài nguyên trước khi cân nhắc dừng thêm, ưu tiên giữ lượt cũ. Chỉ các lượt render của Spectrum Studio được dừng. Lượt còn lại tiếp tục khi RAM đủ; nếu chỉ còn một lượt mà RAM vẫn nguy cấp kéo dài, lượt cuối cũng phải dừng. Lượt đã bị dừng phải xuất lại; tệp tạm bị dọn, video cũ đã tồn tại ở đường dẫn đích được giữ nguyên. Có thể Hủy bất kỳ lúc nào trong khi chờ.

## Lưu tự động, Undo/Redo và phím tắt

Hai nút **↶ / ↷** nằm phía trên cây thành phần. Undo/Redo áp dụng cho thông số, thêm/xóa/nhân đôi, thứ tự lớp, mốc nhạc, intro và In/Out; bài nhạc đang phát không bị đổi. Trong ô đang nhập chữ, Ctrl+Z vẫn hoàn tác văn bản của ô đó.

**Cài đặt → Tự động lưu** bật lưu nền mỗi 30 giây khi có thay đổi. Mặc định tắt. Dự án mới được lưu vào thư viện; dự án có đường dẫn .TS còn cập nhật tệp đó. Các thay đổi phát sinh trong lúc đang lưu được giữ cho lượt tiếp theo.

**Cài đặt → Cấu hình phím tắt…** cho phép đặt tổ hợp riêng, xóa tổ hợp để tắt hoặc khôi phục mặc định. Không cho hai chức năng dùng trùng một tổ hợp. Mặc định: Ctrl+S lưu, Ctrl+Z/Ctrl+Y Undo/Redo, Ctrl+M mở nhạc, Ctrl+L thư viện nhạc, Space phát/dừng, Ctrl+Enter xuất video. Chọn thành phần rồi nhấn **Delete** để xóa hoặc **Ctrl+D** để nhân đôi; **Ctrl+Shift+D** dừng và đánh dấu. Xóa/nhân đôi không tác động đến thành phần khi đang nhập chữ hoặc chỉnh số. Nhấp chuột trái chọn thành phần; chỉ nhấp chuột phải mới mở menu Nhân đôi/Xóa.

## Preview ưu tiên mượt

Mặc định **Tự động · ưu tiên mượt**. App tự giảm độ phân giải khi có nhiều hiệu ứng, cập nhật khung mới nhất để tránh dồn hàng chờ. FPS và kích thước preview hiện bên dưới. Có thể chọn cố định 360 hoặc 640 px. Preview có thể mờ hơn khi cảnh nặng; video xuất vẫn dùng độ phân giải và FPS đã chọn trong Render.

Preview giảm chống răng cưa và số hạt hiển thị. Motion Blur lấy tối đa 3 mẫu trong khoảng shutter của chính thời điểm đó, không giữ bóng từ những khung đã phát. Export dùng số mẫu đã chọn (mặc định 12) và FPS xuất thực. Các tối ưu preview không thay đổi thông số lưu trong preset.

## Preset .TS được lưu trong app

- **Nhập .TS** nhận preset của bản PC, gồm cấu hình và phương tiện. App lưu một bản đầy đủ vào thư viện để tiếp tục chỉnh sửa độc lập với tệp đã nhập.
- **Preset đã lưu** mở thư viện có ảnh, tìm kiếm và số phương tiện. Có thể mở lại sau khi đóng app hoặc di chuyển/xóa `.TS` gốc.
- **Lưu dự án** cập nhật preset đang mở trong thư viện. **Lưu dự án hiện tại** trong thư viện cho phép đặt tên. **Xuất .TS** tạo bản mang sang máy khác, gồm ảnh, GIF, font, mask và video intro đang dùng. Preset/thư viện `.aveestudio` cũ vẫn mở được; lần lưu tiếp theo dùng `.TS`.
- Thư viện nằm ở `%LOCALAPPDATA%/AveeStudio/library-v1`, độc lập với thư mục EXE. Bài nhạc chọn để phát vẫn là tệp riêng; khi chuyển máy cần chép nhạc và chọn lại nếu đường dẫn thay đổi.
- Xóa preset trong thư viện cần xác nhận. Chuyển sang preset khác trước khi xóa preset đang mở.

Khi lưu dự án portable, mỗi tệp phương tiện tối đa 128 MB, tổng tài nguyên tối đa 512 MB. Video intro cũng tính vào giới hạn này; nhạc chính không được nhúng vào gói.

## Chỉnh thành phần

Bên phải có cây thành phần và bảng thông số. Khi chọn một thành phần, các nhóm đều thu gọn; bấm tiêu đề nhóm cần sửa để mở. Nhóm đang mở được giữ trong lúc sửa và cập nhật bảng; chuyển sang thành phần khác sẽ thu gọn lại. **General** chứa Position, kích thước, góc xoay và độ trong. **Source** chọn nguồn Composition khi thành phần hỗ trợ. Sóng luôn có Audio Provider. Với ảnh/chữ/hiệu ứng, chỉ bật **Phản ứng theo nhạc** khi cần nhịp; lúc đó lựa chọn Audio Provider mới xuất hiện. RGB Split ở chế độ **Theo beat nhạc** luôn có Audio Provider. Thành phần tĩnh không cần phân tích âm thanh.

**+ Thêm** mở bảng nổi có tìm kiếm/lọc. Kéo thành phần vào dòng bất kỳ, vào Composition hoặc lên preview để đặt Position. Giữ tay nắm ở đầu dòng để đổi thứ tự. Audio Provider và Composition cũng kéo được; liên kết nguồn được cập nhật theo.

Giữ **tên thành phần** khoảng nửa giây hoặc nhấp chuột phải để chọn **Nhân đôi / Xóa**. Bản sao nằm ngay sau bản gốc, giữ thông số và nguồn nhưng chỉnh được độc lập. Với Composition, các lớp bên trong cũng được sao chép; liên kết sang Composition khác vẫn dùng nguồn cũ. Không xóa/nhân đôi Output và không xóa Audio Provider cuối cùng.

Bản 0.5 ghép các ô X/Y, rộng/cao, điểm neo và thời gian có liên quan trên cùng hàng. **General** mặc định thu gọn để dành chỗ cho thông số riêng của thành phần; bấm tiêu đề để mở. Ô tích có viền sáng, nền xanh và dấu tích khi bật. Từ bản 1.2, thanh sóng bài hát, intro và chuyển cảnh giữ cùng thang thời gian trong phần bên trái dưới preview.

Thành phần luôn mang tên **Sóng**, **Ảnh**, **Chữ**. Sóng có các kiểu cột, cột bo đỉnh, bar cong, đường mượt, đường vuông, sóng đặc, vòng tròn và dạng sóng âm. Sóng là thành phần cuối: chỉ chọn Audio Spectrum, không có nguồn Composition. Chữ giữ điểm bắt đầu ở Position khi nội dung dài thêm. Ô màu có hút màu màn hình.

**Sóng bar dạng cong** uốn từng thanh thành nét `)`, tâm các thanh cùng nằm trên một đường ngang. **Độ tròn** 0% cho thanh thẳng, 100% cho nửa đường tròn; chỉnh độ cong không làm đổi tâm hay độ vươn trên/dưới. Khi chọn kiểu này, đối xứng trên/dưới được bật để có hình giống mẫu tham chiếu.

**Sóng đường vuông** giữ hình hai đường gấp khúc đan nhau với các đỉnh sắc, mặc định bốn đỉnh thưa như ảnh tham chiếu. **Số đỉnh** điều khiển hình dạng (1–64), độc lập với **Số dải** phân tích trong Audio Spectrum. Mỗi đỉnh lấy mức lớn nhất của một nhóm dải không chồng nhau; nguồn mặc định vẫn phân tích đủ 199 dải. Chỉnh dải tần và **Audio Duration** trong Audio Spectrum đã chọn để thay đổi phản ứng của các đỉnh mà không biến hình thành hàng trăm đường răng cưa. **Vạch dọc tại đỉnh** và **Màu vạch tại đỉnh** điều khiển các nét dọc bên trong; **Độ dày / Thickness** thay đổi độ dày cả đường sóng lẫn vạch dọc. Hai đường là một cặp cố định, không cần bật đối xứng. **Sóng đặc** có cùng đường bao mượt như sóng dây và tô kín phần bên trong.

**Motion Blur → Cách làm mờ → Lóe sáng · Flare** tạo dải sáng kéo dài từ sóng như ảnh mẫu, giữ các cột gốc sắc nét. **Góc lóe** 0° là ngang; **Hướng lóe** chọn Hai bên, Lệch trái hoặc Lệch phải theo trục đã xoay. Điều chỉnh Độ dài tia, Bề rộng tia, Độ mềm tia, Cường độ lóe, Ngưỡng sáng và Màu lóe; mặc định cyan và lóe ngang hai bên. Cường độ 0 giữ nguyên nguồn. Để chỉ lóe phần sóng, đặt sóng trong một Composition riêng và chọn Composition đó làm nguồn của Motion Blur, tránh lấy cả ảnh nền làm vùng phát sáng. Hai chế độ Chuyển động · Shutter và Vector thủ công · Avee tiếp tục hoạt động như cũ.

Trong hộp chọn màu, thanh **Độ rõ / Độ mờ** chỉnh độ trong suốt: **0%** là trong suốt hoàn toàn, **100%** là rõ hoàn toàn. Thanh này độc lập với sáng–tối; alpha được giữ trong màu khi lưu preset `.TS`. Mức rõ thực tế còn nhân với độ trong của thành phần nếu bạn chỉnh cả hai.

Audio Provider giữ Audio Duration, Start/End Frequency, Frequency Bands, Maximum Height, Strength và Duration Averaging. Bản 0.4 khôi phục thuật toán và dáng sóng của bản 0.2 trước bản 0.3 theo yêu cầu: averaging Welch và đường nối bass PCHIP cũ. Dự án 0.3 mở lại cũng dùng dáng sóng đã khôi phục. Bản sửa Audio Offset âm/dương và im lặng ngoài thời lượng bài vẫn được giữ. Không khẳng định đây là thuật toán nội bộ của After Effects.

Với đường sóng, **Đoạn trống phía bass** kéo dài mép ngoài vùng tần số. Beat cho ảnh/hiệu ứng được chỉnh riêng với thông số sóng.

## Ảnh và GIF

Trong thành phần **Ảnh**, chọn một trong hai nguồn:

- **Tệp ảnh/GIF:** bấm **Chọn ảnh / GIF…**. Khi đã có tệp, lựa chọn Composition bị khóa; bấm **Xóa tệp ảnh** trước khi đổi sang Composition.
- **Composition:** chọn trong **Target Image · Composition**. Khi có liên kết, ô đường dẫn và nút chọn ảnh bị khóa; bấm **Bỏ liên kết Composition** trước khi chọn tệp.

Mở nhóm **GIF / Tốc độ phát** để kéo thanh tốc độ hoặc nhập từ **0,05× đến 8×**; nút **1×** trả về tốc độ gốc. 0,5× chậm một nửa, 2× nhanh gấp đôi. Nhóm này cũng có điểm bắt đầu GIF, lặp lại và đảo chiều; các ô chỉ bật khi nguồn ảnh là tệp `.gif`. GIF chạy theo thời gian bài nhạc trong preview và khi xuất, nên tua đến cùng một thời điểm sẽ chọn cùng khung GIF. Tốc độ được lưu trong preset `.TS`, có thể Undo/Redo. Khi tắt lặp lại, GIF giữ khung kết thúc của chiều phát đã chọn.

Mở nhóm **Ảnh / Mở rộng** để bật **Làm mờ ảnh**, **Đảo màu ảnh** (âm bản), **Xoay liên tục** hoặc **Sao băng chạy quanh viền**. Bo góc nằm trong cùng nhóm: 0 là góc vuông, 0,5 là bán kính bằng nửa cạnh ngắn. Sao băng đi theo đúng các góc bo, có cỡ, số vòng/giây, chiều chạy, độ dài đuôi, màu và độ sáng. Tốc độ xoay ảnh tính bằng độ/giây; dấu âm xoay ngược. Những lựa chọn này dùng được với ảnh, GIF và ảnh lấy từ Composition.

Nếu chọn ảnh lỗi hoặc không đọc được, nguồn ảnh cũ được giữ và có thông báo. Ảnh lớn được thu nhỏ lúc giải mã/dựng theo khung làm việc và giới hạn GPU, tệp gốc được giữ nguyên.

## Uốn cong ảnh và chữ qua Composition

Trong Ảnh có hai nhóm **Uốn cong 2D** và **Uốn cong 3D**, mặc định tắt. **Độ uốn** chạy từ 0 đến 100%: 0% thẳng, 50% nửa vòng, 100% vòng kín. Chọn **Hướng cong** để đảo chiều và **Ngang / Dọc** để chọn trục. Position vẫn là điểm neo. Các góc đã lưu ở bản 0.8 được hiển thị thành phần trăm tương ứng.

- **2D:** uốn hình/chữ theo cung tròn trong mặt phẳng. Bật **Xoay theo chiều uốn** để chữ đi theo tiếp tuyến như chữ chạy quanh vòng; bỏ tích để các lát ảnh giữ hướng ban đầu.
- **3D:** cuộn thành dải mặt trụ, có cả mặt trước và mặt sau. Phần trong suốt trên mặt trước cho nhìn thấy chữ ngược ở mặt sau. **Nghiêng vòng** thay đổi góc nhìn lên/xuống; **Phối cảnh** chỉnh cảm giác gần/xa. **Xoay theo chiều uốn** xoay dải quanh trục cong khi tăng độ uốn. Độ nghiêng tăng dần từ hình thẳng ở 0%, đạt giá trị đã chọn từ 25% trở lên. Đây là bề mặt ảnh có chiều sâu, không phải chữ khối dày.

Để uốn chữ, tạo Composition chứa Chữ, thêm Ảnh vào Output rồi chọn Composition ấy làm nguồn. Chỉnh Uốn cong trên Ảnh; nội dung/font/In–Out sửa tại Chữ. Phần lề trong suốt của Composition cũng được cuộn, nên hãy cho dòng chữ phủ phần chiều rộng mong muốn nếu cần vòng chữ khép kín. Có thể kết hợp hai kiểu uốn theo thứ tự 2D rồi 3D. Mask, bo góc và sao băng đi theo ảnh sau khi uốn.

### Quay chữ theo vòng

Trong mỗi nhóm **Uốn cong 2D / 3D**, bật **Quay quanh vòng**. **Tốc độ quay** tính bằng độ/giây: 30°/s = 12 giây/vòng, 60°/s = 6 giây/vòng. Nhập số âm để đảo chiều; 0 giữ đứng yên. **Góc bắt đầu** chọn vị trí của chữ trên vòng ở đầu bài. Thời gian một vòng được hiển thị ngay dưới các ô chỉnh.

2D quay theo cung tròn; 3D cho chữ chạy quanh mặt trụ, giữ nguyên tâm/độ nghiêng của vòng. Để dựng kiểu vòng chữ 3D xoay quanh ảnh, bắt đầu với **Độ uốn 100%**, **Nghiêng vòng 20–30°**, **Tốc độ 30°/s**. Nội dung ảnh/chữ cần nền trong suốt để thấy mặt sau. Phần vòng bị ảnh khác che phụ thuộc thứ tự Composition và các lớp.

Quay dùng thời gian tuyệt đối của bài nhạc: dừng phát sẽ dừng quay, tua có thể đổi góc ngay, xuất từ giữa bài vẫn lấy đúng góc ở mốc đó. **Xoay theo chiều uốn** điều khiển hướng của bề mặt khi uốn; **Quay quanh vòng** điều khiển chuyển động theo thời gian. Mỗi hiệu ứng có tốc độ riêng. Với cung chưa khép kín, cả đoạn cung sẽ di chuyển quanh tâm; ở độ uốn nhỏ bán kính lớn nên cung có thể đi ra ngoài khung. Dùng 100% để tạo vòng chữ chạy liên tục như mẫu. Tắt quay bỏ cả tốc độ và góc bắt đầu; preset cũ mặc định tắt.

## Mask Image

Ảnh có nguồn **Mask Image** độc lập với nguồn ảnh chính. Chọn tệp ảnh/GIF hoặc một Composition làm mask; xóa nguồn hiện tại trước khi đổi loại. Mask được đặt trong khung ảnh rồi mới áp dụng Position, xoay và nhịp của ảnh.

Bốn chế độ theo Avee, với A là alpha của mask và L là giá trị lớn nhất trong ba kênh RGB:

| Mask Mode | Phần ảnh được giữ |
|---|---|
| Transparency | A |
| TransparencyAndBlacks | A × L; đen che, trắng giữ |
| TransparencyAndWhites | A × (1 − L); trắng che, đen giữ |
| InvertedTransparency | 1 − A |

Ảnh mask trong suốt, GIF và Composition đều dùng cùng quy tắc. GIF mask chạy theo thời gian bài nhạc. Tệp mask được giữ trong dự án portable/thư viện.

## Font và thời gian hiện chữ

**Chữ / Uốn cong 2D** và **Chữ / Uốn cong 3D** có đầy đủ độ uốn 0–100%, hướng uốn, phối cảnh/nghiêng vòng 3D và quay quanh vòng với tốc độ/góc bắt đầu độc lập. Toàn bộ dòng chữ được dựng trước khi uốn, nên chữ dài không bị cắt mất phần cuối ở mép video trước khi tạo vòng. Khi bật uốn, Position neo giữa dải chữ; Cỡ chữ và Size quyết định kích thước vòng. Khi tắt uốn, vị trí chữ giữ cách hoạt động cũ. Các thông số được lưu trong `.TS` và hỗ trợ Undo/Redo.

Trong **Chữ**, bấm **Tìm font / Chọn thư mục…** để tìm font đã cài, chọn thư mục chứa font hoặc chọn trực tiếp tệp TTF/OTF/TTC. Có ô tìm kiếm và mẫu chữ xem trước. Font từ tệp được dùng trong app mà không cần cài vào Windows và được giữ trong dự án portable.

Mặc định chữ hiện toàn bài. Khoảng thứ nhất có lựa chọn **Tự đặt / Đến hết bài**: chọn Đến hết bài để tự bám thời lượng nhạc và đặt Out ở cuối bài; chọn Tự đặt để dùng số giây đã nhập. Tùy chọn này cũng có ở ảnh, sóng và hạt. Bật **Chỉ hiện trong các khoảng đã chọn** để dùng tối đa 3 khoảng; tích riêng khoảng cần dùng rồi nhập bắt đầu/kết thúc bằng giây. Các khoảng chồng nhau được gộp, tránh chớp tắt giữa chúng. Khi chế độ giới hạn được bật nhưng không có khoảng hợp lệ được tích, chữ không hiện.

Chọn hiệu ứng **In** và **Out** độc lập: không, mờ, trượt trái/phải/lên/xuống hoặc thu/phóng; mỗi phía có số giây riêng. Hiệu ứng nằm trong khoảng hiển thị. Với chế độ toàn bài, In chạy từ đầu bài và Out kết thúc tại cuối bài. Position trong General vẫn là điểm neo, nội dung chữ dài lên không làm dịch điểm neo.

**Hiện · Biên mờ** có các hướng từ trái/phải/trên/dưới/giữa. Chọn biên **Thẳng / Tròn / Elip / Vuông**, chỉnh **Độ mềm** và **Bán kính**. Bán kính lớn làm vùng lộ ra rộng hơn trong cùng thời điểm chuyển cảnh; khi kết thúc In toàn bộ thành phần vẫn hiện đủ. Out chạy ngược quá trình hiện. Các lựa chọn này cũng nằm trong nhóm **Thời gian / Hiệu ứng Vào–Ra** của ảnh, sóng và hạt.

Riêng chữ có **So le từng chữ** (nhóm vị trí chẵn trước, nhóm lẻ sau), **Cuộn từng chữ** (từ chân chữ) và **Gõ từng chữ**. Cuộn có độ trễ giữa các chữ. Chọn độc lập cho Vào/Ra; dấu tiếng Việt đi cùng ký tự và không làm dịch điểm neo của cả dòng.

## Dịch chuyển theo mốc thời gian

**Dịch chuyển** là hiệu ứng riêng trong **+ Thêm**. Đặt hiệu ứng sau các lớp muốn di chuyển hoặc chọn một Composition làm nguồn. Thêm từng đoạn với thời gian đầu/cuối, tọa độ X/Y đầu và X/Y cuối, rồi chọn Linear, Smooth hoặc Smoother để làm mượt đầu/cuối.

Tọa độ là **độ dịch tương đối** theo kích thước khung: X = 0.1 dịch sang phải 10% chiều rộng; X âm sang trái, Y dương xuống và Y âm lên. Để đi A → B rồi về A, thêm đoạn thứ hai bắt đầu ở B và kết thúc ở A. Trước đoạn đầu giữ tọa độ đầu; giữa các đoạn và sau đoạn cuối giữ tọa độ kết thúc. Nếu các đoạn chồng nhau, đoạn bắt đầu sau được ưu tiên.

Mỗi đoạn có màu riêng; hai mốc A/B cùng thời gian và màu hiện trên thanh sóng bài hát. Bấm mốc để tua đến điểm đó. Sửa thời gian trong bảng hiệu ứng sẽ cập nhật mốc; tắt đoạn để bỏ chuyển động và mốc của nó.

## Chỉnh màu nâng cao

Trong **+ Thêm → Hiệu ứng**, chọn **Chỉnh màu**. Đặt thành phần sau các lớp cần chỉnh hoặc chọn một Composition làm nguồn. Chỉnh sáng/tối và màu không làm mất alpha của ảnh trong suốt.

Các nhóm gồm phơi sáng, độ sáng, tương phản, vùng sáng/vùng tối, trắng/đen, gamma; nhiệt độ/tint, bão hòa, vibrance, hue; HSL theo vùng màu; và **Curves**. Phơi sáng dùng đơn vị stop; tăng 1 stop là nhân đôi ánh sáng. Curves có kênh chung RGB và các kênh Đỏ/Lục/Lam. Thêm và kéo điểm để chỉnh vùng tối/trung gian/sáng, xóa điểm hoặc đưa đường cong về mặc định. Undo/Redo và preset .TS giữ cả đường cong.

Các thông số mặc định giữ màu gốc. Chỉnh màu chạy trên GPU; CPU dùng khi GPU không khả dụng. Kết quả là xử lý video RGB của app, không phải quy trình chỉnh RAW/HDR có quản lý màu chuyên dụng.

## Hiệu ứng gần Avee gốc

- **Liquify:** chọn `Avee · Simplex Noise` để dùng shader trích từ smali, với Intensity, Control, Control Speed/Beat, Complexity, Noise Scale, Blobs và Zoom. `Desktop 0.2` giữ kiểu cũ.
- **RGB Split:** có ba cách lóe: **Cố định**, **Theo beat nhạc**, **Theo chu kỳ**. X dương lóe phải, X âm lóe trái; Y dương xuống, Y âm lên; phối hợp X/Y tạo hướng chéo. **Lóe về cùng hướng** bật mặc định cho lớp mới; bỏ tích để tách đối xứng như trước. **Đường lóe mượt** chỉnh thời gian tăng lên đỉnh, giữ đỉnh và thu về; **Độ mạnh đỉnh** chỉnh mức tách. Chu kỳ có thời điểm bắt đầu và khoảng lặp; khoảng lặp quá ngắn sẽ được nâng bằng tổng ba pha để tránh cắt đột ngột. Theo beat kích hoạt khi Beat vượt ngưỡng; chỉnh Audio Provider và ngưỡng nếu ít/nhiều lần lóe. Màu ba kênh, Blend Mode Content và ảnh gốc phía trên/dưới vẫn có. Chế độ cố định không cần Audio Provider.
- **Motion Blur:** chế độ **Chuyển động · Shutter** lấy mẫu chuyển động thật trong khoảng phơi sáng ngắn: **Shutter Angle** càng lớn vệt càng dài; **Shutter Phase** đặt khoảng phơi sáng trước/sau thời điểm khung; **Samples** điều khiển độ mịn. Mặc định 180°/−90°/12 mẫu; tại 30 FPS là khoảng 1/60 giây, tại 60 FPS là 1/120 giây. Đặt sau hiệu ứng Dịch chuyển hoặc chọn Composition đang chuyển động. Vật đứng yên giữ nguyên nét, không lưu bóng kiểu Echo. Đây là mô phỏng shutter theo nguyên lý chuyển động, không phải bản sao thuật toán Adobe hoặc ước lượng optical flow. **Vector thủ công · Avee** vẫn dùng Gaussian 9 mẫu và có thể làm mờ cả ảnh tĩnh.
- **Mirror:** Mirror Mode, Flip Mirror, tâm trục, màu và nguồn Composition.
- **Particle:** Count Limit, Particle Scale, Spawn Area/Time, Lifetime, Speed/Random, Gravity X/Y, Side Sine Wave, Color From/To, Start/End Size, Fade và Mirror X/Y. Hiện dựng hạt 2D; perspective/force field 3D và biểu thức đặc thù được giữ dữ liệu và báo khi nhập.
- **Glow:** Threshold, Intensity, Radius và giữ ảnh gốc; bước threshold/blur/tint được đưa lên GPU, có CPU fallback khi driver không hỗ trợ. Điều khiển theo kiểu AE, không bảo đảm kết quả giống từng pixel.
- **Shader:** biên dịch GLSL thực trên GPU; xem `SHADERS.md`. Cần OpenGL 3.3. Hiệu ứng tích hợp có CPU fallback; shader tự viết báo lỗi biên dịch/driver.

Xem `EFFECT_COMPATIBILITY.md` để biết mức tương thích. Một số shader vertex, biểu thức chuyển động, video texture trong preset điện thoại và tài nguyên nội bộ chưa dựng đầy đủ trên laptop. `.viz` vẫn giữ các phương tiện này. Chèn video qua track Intro và GIF qua thành phần Ảnh là các tính năng riêng đã được hỗ trợ.

## Nhạc, đánh dấu và video intro

Nút **Nhạc** mở **Gần đây** (10 bài mở thành công gần nhất) và playlist theo thư mục. Thêm thư mục để quét cả thư mục con, tìm kiếm theo tên và chọn bài; thư mục được nhớ cho lần mở app sau. Tệp đã mất được bỏ khỏi danh sách gần đây. Alt+Trái/Alt+Phải chuyển bài trong playlist; phát hết bài tự chuyển sang bài tiếp theo và dừng ở cuối danh sách.

Thanh sóng toàn bài chạy hết chiều ngang. Bấm/kéo để tua; **Dừng & đánh dấu** hoặc Shift+bấm tạo mốc; thời gian hiện phía trên, chuột phải để xóa mốc.

Hai nút **+ In / + Out** ở đầu/cuối thanh sóng thêm **Biến dạng + mờ** hoặc **Xoay ảnh + mờ**. Track In/Out nằm dưới Intro và tác động lên toàn hình chính. Bấm khối để mở bảng nổi; kéo để dịch thời gian hoặc nhập đầu/cuối. Mặc định 3 giây; cho phép 0,5 giây. Nếu đầu không nhỏ hơn cuối, cuối được sửa thành đầu + 1 giây trong giới hạn khoảng trống/bài hát. Hai khối không chồng nhau. Chọn **Xoay biến dạng · Giữ khung** để biến dạng nội dung trong khung cố định, hoặc **Xoay cả ảnh** để quay toàn hình quanh tâm. Hiệu ứng mới mặc định 0,5 vòng và tỷ lệ 1×: In xoay cả ảnh từ lật ngược 180° về gốc; với xoắn trong khung, góc xoắn mạnh ở tâm và giảm dần đến mép cố định. Out theo chiều ngược. Chỉnh thêm zoom, số vòng (âm để đổi chiều) và **Độ mờ · px tại 1080p**. Blur dùng cùng Gaussian với mục Ảnh, giảm về rõ khi In kết thúc; không tạo vệt nhiều ảnh xoay. Thông số đã lưu trong hiệu ứng cũ được giữ, có thể đặt lại số vòng thành 0,5. Intro luôn che phía trên các hiệu ứng này; nhạc chính tiếp tục phát.

Track **INTRO** nằm dưới thanh sóng bài hát:

1. Bấm **+ Video** để chèn tại thời điểm đang phát, hoặc thả tệp video vào vị trí mong muốn trên track.
2. Kéo khối video sang trái/phải để căn thời gian; ô **Bắt đầu (s)** cho phép nhập chính xác. Bấm khối để chọn và chỉnh nó.
3. Chọn **Lấp đầy** hoặc **Vừa khung**. Chọn **Out**: Không, Mờ dần, Trượt trái, Trượt phải hoặc Thu nhỏ; nhập thời gian hiệu ứng tính bằng giây.
4. Bấm **Xóa** để bỏ intro đang chọn. Lưu dự án để giữ video và vị trí đã căn.

Intro xuất hiện ngay tại điểm bắt đầu, không có hiệu ứng vào. Nó che hình chính trong khi nhạc chính tiếp tục phát; âm thanh sẵn có của video intro không được trộn vào. Khi video chạy hết, app giữ khung cuối để thực hiện hiệu ứng Out rồi trở về hình chính. Phần Out được thể hiện ở cuối khối trên track và làm dài tổng thời gian khối. Nếu các intro chồng thời gian, clip được thêm sau nằm trên.

## Xuất MP4 và fade âm thanh

Mở **Render**, nhập đoạn xuất theo `HH:MM:SS` hoặc `HH:MM:SS.mmm`, chọn kích thước và FPS. Hai ô âm thanh tính bằng giây:

- **Âm thanh đầu bài · To dần:** tăng âm lượng từ im lặng đến mức gốc.
- **Âm thanh cuối bài · Nhỏ dần:** giảm âm lượng về im lặng.

Giá trị **0 = tắt**, tối đa 60 giây mỗi phía và tự giới hạn theo độ dài đoạn xuất. Khi chỉ xuất một đoạn giữa bài, fade được tính từ đầu/cuối **đoạn xuất** đó. Nếu hai khoảng fade chồng nhau, cả hai mức giảm được áp dụng. Fade chỉ thay đổi âm thanh trong tệp MP4, không đổi nhạc phát trong preview và không làm hình ảnh mờ dần.

Mặc định **Tự động · Ưu tiên GPU**: app thử mã hóa thật bằng Intel Quick Sync (QSV), NVIDIA NVENC hoặc AMD AMF trước khi sử dụng. Nếu không hỗ trợ hoặc lỗi mã hóa, app chuyển sang CPU. Có lựa chọn CPU thủ công; tiến trình hiển thị bộ mã hóa thực đang dùng.

Preview tạm dừng trong lúc render. Video xuất offline, không đợi nhạc phát theo thời gian thực. Bản 0.6 ghép Composition, ảnh, mask, biến đổi và chuỗi hiệu ứng trên GPU; chỉ lấy khung hoàn chỉnh về một lần ở cảnh thông thường. Preview dùng OpenGL để thu/phóng và hiển thị. Phân tích nhạc và tạo nét sóng/chữ/hạt vẫn dùng CPU; hạt lấy ảnh từ Composition cần đọc thêm nguồn về. Có đường dự phòng khi GPU không khả dụng. Tiến trình phân biệt **Dựng hình** và **Mã hóa**, còn preview hiện **GPU/CPU** đang dựng. Trong Task Manager, **Video Encode** và **3D/Compute** là các phần khác nhau. Tốc độ phụ thuộc cảnh, độ phân giải và phần cứng.

Trên Windows, cache nhạc nằm trong `.audio-cache`. AppImage dùng thư mục cache người dùng (`$XDG_CACHE_HOME/AveeStudio/audio` hoặc `~/.cache/AveeStudio/audio`) để có thể ghi khi AppImage được gắn chỉ đọc. Có thể đổi bằng `AVEE_CACHE_DIR` hoặc xóa cache sau khi đóng app. Thư viện preset là dữ liệu riêng, không phải cache.
