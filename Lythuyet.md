#Tổng Quan giao thức HTTP
## Mục lục
[1.Khái Niệm] (#1)

[2.Các Thành Phần] (#2)

[2.1.Thông báo HTTP] (#2.1)

[2.2.Các phương thức HTTP] (#2.2)

[2.3.Mã trạng thái] (#2.3)

[3.Cơ chế hoạt động] (#3)

[4.Tham Khảo] (#4)

<a name="1"></a>
### 1.Khái Niệm
- HTTP là giao thức tầng ứng dụng.
- Nó dùng để trao đổi dữ liệu(files HTML, files ảnh, kết quả các truy vấn...) trên hệ thống World Wide Web.
- Nó dùng port mặc định là 80, nhưng những port khác cũng có thể được dùng.
- HTTP quy định rõ cách mà các yêu cầu của client được xây dưng, gửi tới server và cách mà các server trả lời các yêu cầu đó.
- Các đặc trưng cơ bản của HTTP:
<ul>
	<li>HTTP kết nối không liên tục: Khi các HTTP client (browser) gửi 1 request xong, nó ngắt kết nối đến server và đợi server phản hồi.Server giải quyết xong yêu cầu và thiết lập lại kết nối để gửi cho client.</li>
	<li>HTTP là phương tiện độc lập: bất kì loại dữ liệu nào cũng có thể được gửi bởi HTTP miễn là server cũng như client biết cách kiểm soát nội dung dữ liệu.</li>
	<li>HTTP là stateless: Cả server và client chỉ biết nhau trong kết nối hiện tại, sau đó sẽ quên nhau đi.</li>
</ul>

<a name="2"></a>
### 2.Các Thành Phần

<a name="2.1"></a>
### 2.1.Thông báo HTTP
- HTTP được xây dựng trên cơ sở mô hình cấu trúc Client-Server và giao thức Stateless các Yêu cầu/Phản hồi mà điều hành bởi việc trao đổi các thông báo (Message) dọc theo một kết nối TCP/IP.
- Định dạng chung cho 1 thông báo gồm 4 mục:
<ul>
	<li>1 dòng đầu tiên.</li>
	<li>Không có hoặc nhiều trường header theo sau.</li>
	<li>1 dòng trống.</li>
	<li>1 thông báo body tùy ý.</li>
</ul>
- Trường HTTP header cung cấp các thông tin về request, response hay về các đối tượng được gửi trong thông báo body.
- Có 4 loại header:
<ul>
	<li>General-header:Áp dụng thông thường cho cả request và response. </li>
	<li>Client Request-header: chỉ áp dụng cho request.</li>
	<li>Server Response-header: chỉ áp dụng cho response.</li>
	<li>Entity-header: Các trường này xác định thông tin về thực thể body.</li>
</ul>
- Giờ chúng ta sẽ tìm hiểu 2 thông báo chính là HTTP-Request và HTTP-Response.

#### a.HTTP-Request
- 1 mẫu thông báo Request sẽ có dạng
<ul>
	<li>1 dòng yêu cầu.</li>
	<li>Không có hoặc nhiều trường header (General|Request|Entity) theo sau.</li>
	<li>1 dòng trống chỉ phần kết thúc của trường Header.</li>
	<li>1 thân thông báo tùy ý.</li>
</ul>
- Dòng yêu cầu: được bắt đầu với 1 thủ tục method, được theo sau bởi 1 Request-URI và phiên bản giao thức, và kết thúc với CLFR.
```sh
Request-Line= Method Request-URI HTTP-Version CLFR
```
- Method: 
<ul>
	<li>Các phương thức để được thực hiện được nhận diện bởi Request-URI đã cung cấp.<li>
	<li>Các method luôn được viết hoa.</li>
	<li>Các method trong request: GET, HEAD, POST, PUT, DELETE, CONNECT, OPTIONS, TRACE.</li>
</ul>
- Request-URI là 1 bộ nhận diện nguồn đồng nhất (URI) và xác định nguồn mà áp dụng Request.
- Header-Request:
<ul>
	<li>Cho phép client truyền thêm thông tin về Request, và về chính client đó tới server.</li>
	<li>Những trường này hoạt động như các bộ chỉnh sửa request.</li>
	<li>Các header quan trọng: Accept-Charset, Accept-Encoding, Accept-Language,Authorization, Expect, From, Host, If-Match, If-Modified-Since, If-None-Match, If-Range, If-Unmodified-Since, Max-Forwards, Proxy-Authorization, Range, Referer, TE ,User-Agent.</li>
</ul>

#### b.HTTP-Response
- 1 mẫu thông báo Response sẽ có dạng
<ul>
	<li>1 dòng trạng thái.</li>
	<li>Không có hoặc nhiều trường header (General|Response|Entity) theo sau.</li>
	<li>1 dòng trống chỉ phần kết thúc của trường Header.</li>
	<li>1 thông báo body tùy ý.</li>
</ul>
- Dòng trạng thái: bao gồm phiên bản HTTP, 1 số mã hóa trạng thái và 1 cụm từ văn bản.
- Mã hóa trạng thái
<ul>
	<li>1 số nguyên 3 kí tự:kí tự đầu tiên của mã hóa trạng thái định nghĩa hạng(loại) Response và 2 kí tự sau không có vai trò phân loại nào.</li>
	<li>5 giá trị cho kí tự đầu tiên:1xx(Thông tin), 2xx(Thành Công), 3xx(Sự điều hướng lại), 4xx(Lỗi client), 5xx(Lỗi server).</li>
</ul>
- Header-Response:
<ul>
	<li>Cho phép Server truyền thông tin thêm về phản hồi mà không thể được đặt trong dòng trạng thái.<li>
	<li>Cung cấp thông tin về Server và truy cập từ xa tới nguồn được xác định bởi Request-URI.<li>
	<li>Các Header quan trọng:Accept-Ranges, Age, ETag, Location, Proxy-Authenticate, Retry-After, Server, Vary, WWW-Authenticate</li>
</ul>

<a name="2.2"></a>
#### 2.2.Các phương thức HTTP

| Tên | Mô tả |
| --- | --- |
| GET *| Lấy 1 tài nguyên hiện có từ server. |
| HEAD | Tương tự như GET, nhưng nó truyền tải dòng trạng thái và khu vực Header. |
| POST *| Tạo ra 1 nguồn tài nguyên mới, ví dụ: thông tin khách hàng, file tải lên, …, sử dụng các mẫu HTML. |
| PUT *| Cập nhật 1 nguồn tài nguyên hiện có. |
| DELETE *| Xóa nguồn tài nguyên hiện có. |
| CONNECT | Được sử dụng bởi Client để thành lập một kết nối mạng tới Server. |
| OPTIONS | tìm ra các phương thức HTTP và các chức năng được hỗ trợ bởi một Server. |
| TRACE | Trình bày một vòng lặp kiểm tra thông báo song song với path tới nguồn mục tiêu. |

`*:Các phương thức hay dùng.`

<a name="2.2"></a>
#### 2.3.Mã trạng thái
##### a.1xx: Thông tin
- Nghĩa là yêu cầu đã được nhận và tiến trình đang tiếp tục.

| Thông báo | Mô tả |
| --- | --- |
| 100 Continue | Chỉ một phần của yêu cầu được nhận bởi Server, nhưng miễn là nó không bị loại bỏ, Client nên tiếp tục với yêu cầu. |
| 101 Switching Protocols | Server chuyển đổi giao thức. |

##### b.2xx: Thành công
- Nghĩa là hoạt động đã được nhận, được hiểu, và được chấp nhận một cách thành công.

| Thông báo | Mô tả |
| --- | --- |
| 200 OK | Yêu cầu là OK. |
| 201 Created | Yêu cầu là hoàn thành, và một nguồn mới được tạo. |
| 202 Accepted | Yêu cầu được chấp nhận để xử lý, nhưng xử lý vẫn chưa hoàn thành |
| 203 Non-authoritative Information | Thông tin từ 1 bên thứ 3 không được xác thực |
| 204 No content | 1 mã trạng thái và header được gửi trong response. nhưng không có phần thân thông báo. |

##### c.3xx: Chuyển hướng
- Các hoạt động phải được thực hiện để hoàn thành Request.

| Thông báo | Mô tả |
| --- | --- |
| 301 Moved Permanently | Trang được yêu cầu đã di chuyển sang url mới |
| 302 Found | Trang được yêu cầu đã di chuyển tạm thời sang url mới |
| 303 See other, 307 Temporary Redirect | Trang được yêu cầu có thể được tìm thấy với url khác |
| 304 Not Modified | Đây là mã phản hồi tới một If-Modified-Since hoặc If-None-Match header, nơi mà URL không được chỉnh sửa từ ngày cụ thể. |s
| 305 Use Proxy | URL được yêu cầu phải được truy cập thông qua proxy được chú thích trong Location header |

##### d.4xx: Lỗi client
- Nghĩa là yêu cầu bao gồm các cú pháp sai hoặc không thể hoàn thành.

| Thông báo | Mô tả |
| --- | --- |
| 400 Bad Request | Server không hiểu được request |
| 401 Unauthorized | Trang được yêu cầu cần username, password |
| 403 Forbidden | Truy cập tới trang yêu cầu bị cấm |
| 404 Not Found | Server không thể tìm được trang đã yêu cầu |
| 408 Request Timeout | Yêu cầu mất nhiều thời gian hơn server sẵn sàng đơi. |
| 410 Gone | Trang được yêu cầu không khả dụng. |

##### e.5xx: Lỗi server
- Nghĩa là server không thể hoàn thành các yêu cầu hợp lệ

| Thông báo | Mô tả |
| --- | --- |
| 500 – Internal Server Error | Yêu cầu không được hoàn thành, server gặp phải trường hợp không mong muốn |
| 502 Bad Gateway | Yêu cầu không được hoàn thành, server nhận được 1 phản hồi không có giá trị từ server cấp trên |
| 503 Service Unavailable | Yêu cầu không được hoàn thành, server tạm thời bị quá tải hoặc bị down. |
| 504 Gateway Timeout | Gateway bị trễ. |

<a name="3"></a>
### 3.Cơ chế hoạt động
<img src="http://i.imgur.com/PBh056p.gif" align="centre" />

- Web browser tách địa chỉ website làm 3 phần:
<ul>
	<li>Phần giao thức: (“http”).</li>
	<li>Máy chủ tên miền: (www.howstuffworks.com)</li>
	<li>Tên tệp: (“web-server.htm”)</li>
</ul>
- Browser liên hệ với DNS để chuyển đổi tên miền "www.howstuffworks.com" ra địa chỉ IP.
- Sau đó, browser sẽ gửi tiếp một kết nối tới máy chủ có địa chỉ IP tương ứng qua cổng 80.
- Browser gửi yêu cầu GET đến máy chủ, yêu cầu tệp "http://computer.howstuffworks.com/web-server.htm.", cookies cũng được gửi kèm theo.
- Server sẽ gửi đoạn text dạng HTML đến browser của bạn kèm theo cookies.
- Browser đọc các thẻ HTML, định dạng trang web và kết xuất ra màn hình của bạn.

<a name="4"></a>
### 4.Tham Khảo
- http://www.tutorialspoint.com/http/http_header_fields.htm
- http://open.ptit.edu.vn/clbsv/showthread.php?t=6871
- http://www.hongkiat.com/blog/common-http-errors/
