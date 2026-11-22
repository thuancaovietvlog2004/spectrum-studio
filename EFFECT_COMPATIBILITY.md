# Thông số hiệu ứng 0.4 và Avee

Các nhóm giữ tên thuộc tính Avee khi có thể đối chiếu. Nguồn Composition, màu, opacity, blend và hình học nằm trong General/Source. Audio Provider chỉ cần cho Sóng và phần phản ứng theo nhạc; lớp tĩnh không phân tích âm thanh.

| Hiệu ứng | Phần đã đối chiếu/triển khai | Giới hạn |
|---|---|---|
| Sóng | Khôi phục thuật toán phổ và đường bass PCHIP của desktop 0.2, có bộ kiểm tra đầu ra đối chiếu bản lưu. Giữ sửa Audio Offset âm/dương và im lặng ngoài bài. | Dáng của dự án 0.3 cũng được đổi về bản trước theo yêu cầu. Không khẳng định là thuật toán Adobe. |
| Liquify | Simplex/FBM từ `LiquifyEffectElement.smali`; Intensity, Control, Complexity, Noise Scale, Blobs, Zoom, tốc độ và beat. | Biểu thức động riêng chưa chuyển đầy đủ; Desktop 0.2 giữ kiểu gợn cũ. |
| RGB Split | Vector X/Y, ba Split Color, nội dung trên/dưới từ Avee; thêm flash cố định/beat/chu kỳ với attack/hold/release smoothstep. X dương phải, Y dương xuống; lớp mới lóe về cùng hướng. | Flash theo thời gian là phần mở rộng desktop. Beat phát hiện lần vượt ngưỡng trên lưới 20 ms, được tính từ âm thanh và không phụ thuộc lịch sử preview. |
| Motion Blur | Manual giữ Gaussian 9 mẫu từ `buffer_motion_blur_frag.frag`. Chế độ chuyển động mới tích phân các khung trong khoảng shutter theo Angle/Phase và FPS thực. Mẫu alpha được cộng trong không gian premultiplied. | Mô phỏng phơi sáng, không tái tạo Adobe optical flow hoặc mọi camera expression. Preview tối đa 3 mẫu; export mặc định 12, tối đa 32. Nhiều blur lồng nhau dùng ngân sách mẫu chung để tránh tăng chi phí theo cấp số nhân. |
| Dịch chuyển | Hiệu ứng độc lập nhận Composition hoặc các lớp đứng trước, dịch theo chuỗi đoạn thời gian và độ dời X/Y; Linear/Smooth/Smoother, màu mốc. | Tọa độ là độ dời theo kích thước khung, không phải vị trí tuyệt đối. Giữ vị trí giữa các đoạn; đoạn bắt đầu sau thắng khi chồng. |
| Mask Image | Bốn mode từ `ImageMask.smali` và `buffer_fx_light_frag.frag`: A; A×maxRGB; A×(1−maxRGB); 1−A. Nhận file/GIF/Composition trong khung ảnh trước biến đổi ngoài. | Không thay bằng luminance có trọng số: Avee dùng kênh RGB lớn nhất. Mọi biểu thức mask động đặc thù điện thoại chưa chuyển được. |
| Chữ | Font đã cài hoặc TTF/OTF/TTC từ thư mục; ba khoảng tùy chọn, In/Out riêng; giữ Position khi nội dung dài. | Hiệu ứng theo thời gian áp dụng cho cả lớp chữ; không phải bộ animator từng ký tự của AE. Khoảng chồng nhau được gộp. |
| Mirror | Mode, Flip, Color, nguồn và vị trí trục. | Không tái tạo biểu thức hình học riêng. |
| Particle | Count, Scale, Spawn, Lifetime, Speed/Random, Gravity X/Y, hướng, sine, fade, màu/size theo tuổi, tỷ lệ, Mirror X/Y. | Mô phỏng 2D; perspective, force fields và bộ sinh 3D chưa tương đương. |
| Glow | Threshold, Gaussian blur, tint/intensity chạy GPU với CPU fallback; dùng cùng nền bloom giảm độ phân giải. | Shader Gaussian và Pillow có thể lệch nhẹ do kernel/làm tròn; không bảo đảm giống pixel với AE. |

Preview ưu tiên tốc độ bằng độ phân giải thấp hơn, ít mẫu shutter và giới hạn số hạt. Motion Blur không trộn bóng lưu từ lượt phát trước: tua đến cùng thời điểm cho cùng kết quả. Vật đứng yên trong chế độ Shutter giữ nguyên nét; Manual vẫn có thể làm mờ ảnh tĩnh. Export dùng độ phân giải, FPS, hạt và mẫu đã chọn; ngân sách lồng blur vẫn giới hạn chi phí.

`assets/avee_liquify.glsl` chứa fragment Liquify trích từ smali. CPU fallback giữ Simplex float32. Shader tùy chỉnh cần OpenGL 3.3 và báo lỗi biên dịch/driver thay vì âm thầm đổi thuật toán. GPU encoding QSV/NVENC/AMF là công đoạn khác với GPU effect; FFT và nhiều thao tác vẽ vẫn ở CPU.
