# 243_71ITAI40803_0101_2374802013578_NguyenPhuocThanh
Thực hành 3
1.1: Trích ảnh nhỏ trong ảnh lớn ban đầu, bmg = data[800:1200, 570:980], 800:1200 là vị trí của khu vực ảnh cần cắt, 570:980 là kích thước ảnh

1.2: Phép tịnh tiến đơn làm dịch chuyển ảnh tùy theo vector đưa vào.
bdata = nd.shift(data, (100, 25)): Ảnh dịch xuống 100 pixel và sang phải 25 pixel, nên phần lớn ảnh bị đẩy xuống dưới và sang phải, các vùng biên sẽ xuất hiện màu nền (đen).
(Giá trị dương dịch xuống/phải, giá trị âm dịch lên/trái.)

1.3: Tăng hoặc giảm pixel của ảnh vài lần, ảnh có thể sẽ mờ đi hoặc mất chi tiết tùy thuộc vào việc chỉnh sửa.

1.4: Hàm rotate dùng để xoay ảnh, khi tham số truyền không có reshape thì mặc định là True, nghĩa là sẽ tự tăng kích thước ảnh và lắp đầy phần nền trống, còn reshape = False thì sẽ chỉ lấy kích thước ảnh gốc, nên các góc bị thiếu do kích cỡ sẽ bị cắt mất.

1.5: Dilation và Erosion dùng để loại bỏ những pixel nhiễu. 

1.6: Thực hiện phép biến đổi ngẫu nhiên vị trí các pixel trong ảnh bằng cách cộng thêm một lượng dịch chuyển ngẫu nhiên (trong khoảng [-d, d]) cho mỗi tọa độ pixel. Ảnh sau biến đổi sẽ bị méo và nhiễu loạn vị trí các điểm ảnh, tạo hiệu ứng biến dạng ngẫu nhiên trên toàn ảnh.

1.7: Sử dụng hàm cos để làm biến dạng tọa độ của từng pixel. Kết quả là ảnh bị biến dạng theo dạng sóng cosine, các chi tiết trong ảnh bị uốn cong, lượn sóng theo cả chiều dọc và ngang.

Bài tập thực hành 3 (trên zalo)
Bài 1: V, H = data.shape[:2]: Lấy kích thước ảnh (chiều cao, chiều rộng).
M = np.indices((V, H)): Tạo lưới tọa độ cho từng pixel trong ảnh.
a = 10, f = 20: Đặt biên độ và tần số cho hiệu ứng sóng.
coords = np.array([map_y, map_x]): Gom các tọa độ mới thành mảng dùng cho biến đổi. 

Bài 2: is_papaya = ... / is_watermelon = ...: Tạo mặt nạ để xác định vùng quả đu đủ và dưa hấu dựa vào ngưỡng màu.
grad_papaya / grad_watermelon: Tạo gradient theo chiều ngang cho từng quả.
papaya_new[..., 0/1/2][is_papaya] = ...: Đổi màu vùng quả đu đủ thành gradient từ đỏ sang xanh lá.
watermelon_new[..., 0/1/2][is_watermelon] = ...: Đổi màu vùng dưa hấu thành gradient từ vàng sang tím.
alpha_papaya / alpha_watermelon: Tạo kênh alpha (độ trong suốt) cho từng quả.
canvas = ...: Tạo nền trong suốt đủ lớn để ghép hai quả.
Bài này thực hiện đổi màu hai loại quả thành các gradient màu khác nhau bằng cách tạo alpha mask cho từng quả, sau đó
ghép lên một nền trong suốt và lưu lại kết quả.

Bài 3: mountain_rot = nd.rotate(..., 45, reshape=False, ...): Xoay ảnh núi 45 độ, giữ nguyên kích thước gốc.
boat_rot = nd.rotate(..., 45, reshape=False, ...): Xoay ảnh thuyền 45 độ, giữ nguyên kích thước gốc.
mountain_mirror = np.flipud(mountain_rot): Tạo ảnh phản chiếu dọc (lật ngược) cho núi.
boat_mirror = np.flipud(boat_rot): Tạo ảnh phản chiếu dọc cho thuyền.
h1, w1 = ... / h2, w2 = ...: Lấy kích thước từng ảnh sau khi xoay.
canvas_h, canvas_w = ...: Tính toán kích thước canvas trắng đủ lớn để ghép cả hai đối tượng và phần phản chiếu.
canvas = np.ones(...) * 255: Tạo canvas trắng.

Bài 4: zoomed = nd.zoom(img, (5, 5, 1), order=1): Phóng to ảnh lên 5 lần theo cả chiều cao và rộng.
h, w = zoomed.shape[:2]: Lấy kích thước ảnh sau khi phóng to.
Y, X = np.meshgrid(...): Tạo lưới tọa độ cho từng pixel.
X_warped = X + 20 * np.sin(2 * np.pi * Y / 150): Biến đổi tọa độ X theo hàm sin để tạo hiệu ứng "uốn cong" (warping).
coords = [Y_warped.ravel(), X_warped.ravel()]: Gom các tọa độ mới thành mảng dùng cho biến đổi.
warped_img = np.zeros_like(zoomed): Tạo ảnh kết quả rỗng.
for i in range(3): ...: Lặp qua từng kênh màu, áp dụng biến đổi tọa độ với map_coordinates.

Bài 5: choose_image(): Hiển thị menu cho người dùng chọn 1 trong 3 ảnh mẫu, trả về ảnh đã chọn.
translate_image(img): Nhập số pixel tịnh tiến theo X, Y và thực hiện tịnh tiến ảnh bằng nd.shift.
rotate_image(img): Nhập góc xoay, hỏi giữ nguyên kích thước không, thực hiện xoay ảnh bằng nd.rotate.
zoom_image(img): Nhập hệ số phóng to/thu nhỏ, thực hiện bằng nd.zoom.
gaussian_blur(img): Nhập sigma, làm mờ ảnh bằng Gaussian filter.
wave_warp(img): Nhập biên độ sóng, thực hiện biến dạng sóng (wave effect) bằng biến đổi tọa độ với hàm sin.