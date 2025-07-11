Thực hành Lab 4
2.1 Phân vùng theo histogram
2.1.1 Phương pháp Otsu
Thực hiện phân ngưỡng ảnh mức xám (fruit.jpg) sang ảnh nhị phân bằng phương pháp Otsu.

2.1.2 Phương pháp Adaptive Thresholding
Thực hiện phân ngưỡng cục bộ (adaptive thresholding) cho ảnh mức xám fruit.jpg bằng hàm threshold_local của skimage.
Cải tiến phân vùng chính xác hơn Otsu. Chia ảnh thành nhiều ảnh nhỏ và tính threshold cho từng ảnh nhỏ

2.2 Phân vùng theo region
Thực hiện phân vùng ảnh theo vùng (region-based segmentation) sử dụng phương pháp watershed trên ảnh fruit.jpg.
Phân vùng các vùng quả trên ảnh và vẽ đường viền phân vùng bằng màu đen.

2.3 Biến đổi đối tượng trong ảnh
2.3.1 Sử dụng binary_dilation
Thực hiện phép giãn (dilation) nhị phân trên ảnh dil_img.png sau khi phân ngưỡng Otsu.
Sử dụng ngưỡng Otsu tự động, phù hợp cho nhiều loại ảnh.
Hiển thị kết quả trực quan.

2.3.2 Sử dụng binary_opening
Quy trình đúng cho xử lý ảnh nhị phân.
Sử dụng ngưỡng Otsu tự động.
Có thể loại bỏ nhiễu nhỏ, làm mịn biên đối tượng.

2.3.3 Sử dụng binary_erosion
Thực hiện phép co (erosion) nhị phân trên ảnh dil_img2.png sau khi phân ngưỡng Otsu, sử dụng structuring element hình chữ thập và lặp 10 lần.
Phép erosion giúp loại bỏ các chi tiết nhỏ, làm co đối tượng lại.

2.3.4 Sử dụng binary_closing
Phép closing giúp lấp đầy lỗ nhỏ bên trong đối tượng và làm mịn biên.

Bài tập Lab 4
Áp dụng lại các phương pháp xử lý ảnh đã học để làm được 4 bài tập lab 4.