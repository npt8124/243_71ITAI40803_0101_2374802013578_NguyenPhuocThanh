# 243_71ITAI40803_0101_2374802013578_NguyenPhuocThanh
Bài 1: Nạp ảnh và lưu thành 3 màu khác nhau theo 3 kênh red, green, blue của hệ RGB bằng thư viện imageio
Kết quả cho thấy mỗi kênh chỉ giữ lại màu tương ứng.

Bài 2: Chương trình tạo ảnh đảo màu bằng cách lấy 255 - giá trị màu cho từng pixel, rồi hiển thị ảnh gốc và ảnh đảo màu cạnh nhau.
Kết quả cho thấy ảnh đảo màu có màu sắc đối lập với ảnh gốc, tạo hiệu ứng âm bản cho ảnh.

Bài 3: Chương trình chuyển ảnh từ không gian màu RGB sang HSV, tách riêng ba kênh H (màu sắc), S (độ bão hòa), và V (độ sáng). 
Kết quả hiển thị cho thấy từng đặc trưng màu được phân tách rõ ràng.

Bài 4: Chương trình điều chỉnh ảnh bằng cách giảm độ sáng (Value) còn 75% và xoay giá trị màu (Hue) về 1/3. 
Kết quả tạo ra ảnh có màu sắc thay đổi và tối hơn so với ảnh gốc, cho thấy hiệu ứng rõ rệt khi thao tác trên không gian màu HSV.

Bài 5: áp dụng bộ lọc trung bình (mean filter) với kích thước khác nhau (3×3, 5×5, 7×7) lên ảnh màu. Kết quả:
Mean 3×3: Giảm nhiễu nhẹ, giữ chi tiết tốt.
Mean 5×5: Hiệu quả lọc và giữ chi tiết cân bằng.
Mean 7×7: Khử nhiễu mạnh nhưng làm ảnh mờ, mất chi tiết nhỏ.
Đây là minh họa rõ ràng về ảnh hưởng của kích thước kernel đến chất lượng ảnh sau lọc.

Bài 6: Trong các bộ lọc (mean, median, max, min), median filter (bộ lọc trung vị) thường khử nhiễu tốt nhất, đặc biệt với nhiễu dạng salt-and-pepper (nhiễu muối tiêu).
+ Mean filter: Làm mịn ảnh, nhưng có thể làm mờ cạnh và không hiệu quả với nhiễu muối tiêu.
+ Median filter: Loại bỏ tốt nhiễu muối tiêu mà vẫn giữ được cạnh sắc nét.
+ Max/min filter: Chỉ phù hợp với một số loại nhiễu đặc biệt, không tốt bằng median filter cho đa số trường hợp, min filter có thể làm mất chi tiết ảnh làm tối ảnh, ngược lại max filter có thể làm sáng ảnh nhưng không khử nhiễu tốt.

Bài 7: Kết hợp lọc median để khử nhiễu và áp dụng các bộ lọc biên (Sobel, Prewitt, Laplacian) trên ảnh màu.
Median filter: Làm sạch ảnh hiệu quả trước khi phát hiện biên.
Sobel & Prewitt: Phát hiện biên theo hướng ngang và dọc, kết quả rõ nét, Sobel thường nhấn mạnh biên mạnh hơn.
Laplacian: Nhạy với nhiễu và phát hiện biên theo mọi hướng, nhưng dễ gây mờ chi tiết mịn.
Kết hợp khử nhiễu trước khi phát hiện biên giúp cải thiện kết quả, trong đó Sobel thường cho biên nổi bật nhất.

Bài 8: kết hợp lọc median để khử nhiễu và đổi màu RGB ngẫu nhiên bằng cách hoán vị kênh màu.
Median filter giúp làm sạch ảnh trước khi xử lý màu.
Việc hoán đổi kênh RGB tạo ra hiệu ứng màu ngẫu nhiên thú vị, dùng trong xử lý ảnh sáng tạo hoặc kiểm tra ảnh hưởng của kênh màu.

Bài 9: Median filter trước khi biến đổi giúp giữ chi tiết và loại bỏ nhiễu.
Việc hoán đổi thứ tự các kênh H-S-V tạo ra hiệu ứng màu mới lạ và ngẫu nhiên, phù hợp với mục tiêu sáng tạo hoặc thị giác máy tính.
Kết hợp colorsys.rgb_to_hsv và hoán vị đơn giản nhưng hiệu quả.
Nhận xét: Kết hợp tốt lọc nhiễu + đổi màu sáng tạo trong không gian màu HSV. Rất hữu ích để khám phá ảnh theo cách mới mẻ hoặc tạo hiệu ứng hình ảnh nghệ thuật.