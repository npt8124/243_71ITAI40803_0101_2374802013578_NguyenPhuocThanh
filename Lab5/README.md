Thực hành Lab 5
2.1 Gán nhãn ảnh
thres = threshold_otsu(a): Áp dụng thuật toán ngưỡng Otsu để tự động tìm một giá trị ngưỡng toàn cục tối ưu cho ảnh a.
b = a > thres: Tạo ra một ảnh nhị phân (b) bằng cách so sánh từng pixel của ảnh a với giá trị ngưỡng thres. Các pixel lớn hơn ngưỡng sẽ là True (tiền cảnh), còn lại là False (hậu cảnh).
Hàm label() từ skimage.morphology sẽ tìm tất cả các thành phần pixel được kết nối trong ảnh nhị phân b và gán cho mỗi thành phần một giá trị nhãn duy nhất.
properties = ['Area', 'Centroid', 'BoundingBox']: Định nghĩa danh sách các thuộc tính mà bạn quan tâm từ mỗi vùng (đối tượng).

2.2 Dò tìm cạnh theo chiều dọc
bmg = abs(data - nd.shift(data, (0, 1), order=0)): Dòng này áp dụng một bộ lọc sai phân đơn giản (tương tự như một dạng của bộ lọc Sobel hoặc Prewitt cho hướng ngang) để phát hiện các cạnh. Các giá trị pixel cao trong bmg sẽ tương ứng với các vị trí có cạnh ngang rõ rệt trong ảnh gốc.

2.3 Dò tìm cạnh với Sobel Filter
a = nd.sobel(data, axis=0): Áp dụng bộ lọc Sobel lên ảnh data để phát hiện các cạnh theo hướng dọc (axis=0). 
b = nd.sobel(data, axis=1): Áp dụng bộ lọc Sobel lên ảnh data để phát hiện các cạnh theo hướng ngang (axis=1).
bmg = abs(a) + abs(b): Kết hợp kết quả từ hai phép toán Sobel.
Sử dụng bộ lọc Sobel để thực hiện phát hiện cạnh. Bằng cách tính toán gradient theo cả hai hướng ngang và dọc, sau đó tổng hợp chúng, chương trình có thể xác định và làm nổi bật tất cả các cạnh trong ảnh, mang lại một cái nhìn tổng thể về các ranh giới đối tượng và chi tiết trong hình ảnh.

2.4 Xác định góc của đối tượng
x = nd.sobel(indata, 0)
Nội dung: Tính toán đạo hàm ảnh theo hướng dọc (gradient theo trục Y) bằng bộ lọc Sobel. Kết quả x biểu thị sự thay đổi cường độ theo chiều dọc.
Ý nghĩa: Phát hiện các cạnh ngang.

y = nd.sobel(indata, 1)
Nội dung: Tính toán đạo hàm ảnh theo hướng ngang (gradient theo trục X) bằng bộ lọc Sobel. Kết quả y biểu thị sự thay đổi cường độ theo chiều ngang.
Ý nghĩa: Phát hiện các cạnh dọc.

x1 = nd.gaussian_filter(x1, 3)
Nội dung: Áp dụng bộ lọc Gauss (làm mờ) với sigma=3 lên x1.

bmg = Harris(data): Gọi hàm Harris với ảnh đã tải làm đầu vào. Kết quả bmg là một mảng NumPy chứa các giá trị đáp ứng Harris cho mỗi pixel.

Bài này thực hiện phát hiện góc Harris để tìm các điểm đặc trưng trong ảnh. Nó tính toán gradient ảnh theo hai hướng, sau đó sử dụng chúng để xây dựng và phân tích ma trận cấu trúc cục bộ, từ đó tạo ra một bản đồ "độ nhạy góc". Các điểm ảnh có giá trị cao trong bản đồ này là các ứng viên tiềm năng cho các góc.

2.5 Dò tìm hình dạng cụ thể trong ảnh với Hough Transform
2.5.1 Dò tìm đường thẳng trong ảnh
Chương trình định nghĩa một hàm LineHough nhận một ảnh (hoặc ma trận cường độ) và một ngưỡng gama. Hàm này sẽ lặp đi lặp lại, tìm điểm có cường độ cao nhất trong ảnh đầu vào.
V, H = data.shape: Lấy kích thước (chiều cao V và chiều rộng H) của ảnh đầu vào data. Dùng để xác định phạm vi của không gian Hough.
while ok:: Vòng lặp chính của thuật toán.

mx = w.max(): Tìm giá trị pixel lớn nhất còn lại trong ảnh w.

if mx < gama: ok = 0: Nếu giá trị pixel lớn nhất nhỏ hơn ngưỡng gama, dừng vòng lặp.

else:: Nếu có một điểm nổi bật.

v,h = divmod(w.argmax(), H): Tìm tọa độ (hàng v, cột h) của pixel có giá trị lớn nhất trong w.

y = V - V và x = h: Có vẻ như y = 0 và x = h. Điều này ngụ ý rằng tọa độ (x, y) được sử dụng là (h, 0) trong hệ tọa độ mới (với gốc ở dưới cùng bên trái, hoặc một chuyển đổi nào đó). Thông thường, tọa độ của pixel được sử dụng trực tiếp là (h, v). Nếu y = 0 luôn, điều này chỉ xem xét các đường đi qua hàng đầu tiên của điểm ảnh (nếu V-V là 0 và V là chiều cao ảnh). Điều này có thể là một sai sót hoặc một cách triển khai rất đặc biệt. Trong biến đổi Hough tiêu chuẩn, x và y sẽ là tọa độ của điểm (h, v) đang được xét.

rh = x*np.cos(theta) + y*np.sin(theta): Tính toán giá trị ρ (khoảng cách từ gốc) cho tất cả các góc θ đi qua điểm (x, y) hiện tại. Đây là công thức của đường thẳng trong dạng chuẩn tắc: ρ=xcosθ+ysinθ.

for i in range(len(rh)):: Lặp qua tất cả các giá trị ρ và θ cho điểm hiện tại.

if 0 <= rh[i] < R and 0 <= tp[i] < 90:: Kiểm tra xem các giá trị ρ và θ có nằm trong phạm vi hợp lệ của bộ tích lũy ho không.

ho[int(rh[i]), int(tp[i])] += mx: Tích lũy giá trị cường độ mx của điểm ảnh hiện tại vào ô tương ứng (rho, theta) trong bộ tích lũy ho. Đây là bước "bình chọn".

w[v, h] = 0: Đặt giá trị của pixel đã xử lý về 0 trong bản sao w để nó không được chọn lại trong các vòng lặp tiếp theo.

return ho: Trả về ma trận tích lũy Hough.

2.5.2 Dò tìm đường tròn trong ảnh
Minh họa một cách hiệu quả quy trình phát hiện góc Harris trong xử lý ảnh. Hai dòng quan trọng nhất là việc chuyển đổi ảnh sang thang độ xám (image_gray = rgb2gray(data)) và áp dụng hàm phát hiện góc Harris (coordinate = corner_harris(image_gray, k=0.001)). Dòng đầu tiên đảm bảo dữ liệu đầu vào phù hợp cho thuật toán, trong khi dòng thứ hai thực hiện toàn bộ logic phát hiện góc một cách hiệu quả. Kết quả là một bản đồ "độ nhạy góc" có thể được sử dụng để xác định các điểm đặc trưng trong ảnh, vốn rất hữu ích trong nhiều ứng dụng thị giác máy tính như theo dõi đối tượng, ghép ảnh, hoặc nhận dạng đối tượng.
