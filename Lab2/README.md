# 243_71ITAI40803_0101_2374802013578_NguyenPhuocThanh
Thực hành 2
1.1: Biến đổi cường độ ảnh tự tối sang sáng và ngược lại. 

1.2: Đoạn mã thực hiện biến đổi logarit ngược (inverse log) với hệ số gamma = 5 lên ảnh xám. Biến đổi này làm tăng độ tương phản ở vùng tối và giảm ở vùng sáng. Các chi tiết ở vùng tối sẽ được làm sáng lên, giúp dễ quan sát hơn.
Thường được dùng để tăng chất lượng của ảnh.

1.3: Biến đổi logarit giúp làm sáng các vùng tối và nén các vùng sáng, tăng cường chi tiết ở vùng tối. Hệ số 128.0 giúp điều chỉnh mức sáng tổng thể của ảnh kết quả.
Ảnh kết quả sẽ có độ tương phản tốt hơn ở vùng tối, các chi tiết mờ sẽ rõ hơn.
Phương pháp này thường dùng cho các ảnh có độ tương phản thấp ở vùng tối.

1.4: Ảnh sau cân bằng lược đồ sẽ rõ nét hơn, dễ quan sát các chi tiết ở cả vùng tối và sáng.
Đây là một kỹ thuật tăng cường ảnh phổ biến trong xử lý ảnh số.

1.5: Đoạn mã thực hiện biến đổi co giãn mức xám (contrast stretching) cho ảnh xám.
Công thức: im2 = 255 * (c - a) / (b - a)
Biến đổi này sẽ kéo dãn toàn bộ dải mức xám của ảnh về khoảng [0, 255]. Ảnh kết quả sẽ có độ tương phản cao hơn, các chi tiết ở vùng tối và sáng đều được làm rõ hơn.
Sau biến đổi, ảnh sẽ sáng hơn, tối hơn ở các vùng tương ứng, giúp dễ quan sát chi tiết. Đây là kỹ thuật tăng cường ảnh đơn giản nhưng hiệu quả trong xử lý ảnh số.

1.6.1: Dùng để biến đổi ảnh theo miền tần suất, giúp phân tích các đặc trưng về cấu trúc, họa tiết, nhiễu trong ảnh.

1.6.2: Bộ lọc thông thấp Butterworth làm mượt ảnh, loại bỏ các chi tiết tần số cao (nhiễu, biên sắc nét). Ảnh kết quả sẽ mờ hơn so với ảnh gốc, các chi tiết nhỏ bị làm mờ, chỉ giữ lại các thành phần lớn (tần số thấp).
Thích hợp cho các ứng dụng làm mượt, giảm nhiễu ảnh.

Butterworth highpass Filter: Bộ lọc này làm mượt ảnh, loại bỏ các chi tiết tần số cao (nhiễu, biên sắc nét). Ảnh sau lọc sẽ mượt, ít chi tiết nhỏ, phù hợp cho các bài toán làm mượt ảnh hoặc giảm nhiễu.

Bài tập Lab 2
Bài 1: Khi chọn các chữ cái trong menu thì sẽ thực hiện biến đổi trên cả 3 ảnh và lưu 3 ảnh vừa được biến đổi vào folder exercise.

Bài 2: Tương tự như bài 1 nhưng thay thành 3 phép biến đổi là Fast Fourier, Butterworth Low pass và Butterworth High pass.

Bài 3: Xử lý ảnh bằng ngẫu nhiên các phép biến đổi ở bài 1.

Bài 4: Xử lý ảnh bằng ngẫu nhiên các phép biến đổi ở bài 2 kèm thêm Max Filter.