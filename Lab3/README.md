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