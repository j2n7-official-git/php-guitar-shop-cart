# PHP Guitar Shop Cart (New version for Chapter 2.8 - Web Techonology Course)

**[Changelog: Version exercise 2.8]:**
# PHP Guitar Shop Cart – Version Exercise 2.8

Cùng một dự án Guitar Shop với bản chapter 2.7, được cập nhật theo mục 2.8 (How to work with functions) trong giáo trình: gom hàm vào namespace `cart` và thêm tính năng sắp xếp giỏ hàng. Chạy thử bằng lệnh `php -S localhost:8000` rồi mở `localhost:8000`.

**index.php** – File điều khiển chính. So với bản trước, giỏ hàng lưu ở session `cart13`, và file đọc thêm tham số `sortkey` từ biểu mẫu (mặc định là `name`). Mọi hàm giỏ hàng giờ được gọi kèm namespace như `cart\add_item`, `cart\update_item` và `cart\sort`. Khi người dùng cập nhật hoặc xem giỏ, giỏ được sắp xếp theo khóa đã chọn trước khi nạp giao diện. Các action còn lại gồm add, show_add_item và empty_cart vẫn giữ nguyên.

**cart.php** – Thư viện hàm, nay nằm trong namespace `cart` để tránh trùng tên với hàm `sort` có sẵn của PHP. Ngoài ba hàm cũ là `add_item`, `update_item`, `get_subtotal`, file có thêm `compare_factory`, trả về một closure dùng `use ($sort_key)` để so sánh hai phần tử theo cột bất kỳ. Hàm `sort` dùng `uasort` với closure đó để sắp xếp giỏ hàng nhưng vẫn giữ nguyên khóa sản phẩm.

**add_item_view.php** – Trang Add Item, không thay đổi so với bản trước. Biểu mẫu gửi về `index.php` bằng POST với action là add, danh sách sản phẩm được tạo bằng vòng lặp qua mảng `$products`, danh sách số lượng chạy từ 1 đến 10. Phía dưới có liên kết View Cart để xem giỏ hàng.

**cart_view.php** – Trang Your Cart, được nâng cấp: mỗi tiêu đề cột (Item, Item Cost, Quantity, Total) có thêm một nút tròn `sortkey`, và nút của cột đang sắp xếp được đánh dấu `checked` dựa vào biến `$sort_key`. Người dùng chọn cột rồi bấm Update Cart để sắp xếp lại. Tổng phụ được lấy bằng `cart\get_subtotal()`, dữ liệu đọc từ session `cart13`.

**main.css** – Định dạng giao diện tông màu cam `#cc8420` cho cả hai trang, nền xám, khung nội dung trắng căn giữa tối đa 700 pixel. File giữ nguyên so với bản trước, vẫn phù hợp với các nút tròn mới nhờ định dạng chung cho bảng giỏ hàng.
<img width="1032" height="718" alt="image" src="https://github.com/user-attachments/assets/1302cf56-95fb-4eef-a567-e602990de4c3" />

----------------
**[Changelog: Version exercise 2.7]**
**index.php** – File điều khiển chính, mọi yêu cầu từ trình duyệt đều đi qua đây. File khởi tạo phiên làm việc (session) với cookie lưu hai tuần, tạo mảng giỏ hàng nếu chưa có và khai báo danh sách sản phẩm gồm Flute, Trumpet và Clarinet kèm giá. Sau đó file đọc tham số action từ biểu mẫu hoặc đường dẫn để quyết định việc cần làm: thêm sản phẩm, cập nhật số lượng, xem giỏ hàng, mở trang thêm sản phẩm hoặc làm trống giỏ. Sau cùng nó nạp giao diện phù hợp. Đây là điểm vào của web.

**cart.php** – File này chứa các hàm xử lý giỏ hàng và được index.php nạp vào bằng require_once. Hàm add_item thêm sản phẩm mới vào session, tính thành tiền bằng giá nhân số lượng; nếu sản phẩm đã có sẵn thì cộng dồn số lượng cũ với số lượng mới. Hàm update_item đổi số lượng của một sản phẩm, tính lại thành tiền, và xóa hẳn sản phẩm khỏi giỏ khi số lượng bằng 0 hoặc nhỏ hơn. Hàm get_subtotal cộng thành tiền của mọi sản phẩm rồi định dạng hai chữ số thập phân.

**add_item_view.php** – File này là trang Add Item, giao diện đầu tiên người dùng thấy khi vào web. Nó chứa một biểu mẫu gửi dữ liệu bằng phương thức POST về index.php với action là add. Danh sách chọn tên sản phẩm được tạo bằng vòng lặp foreach qua mảng sản phẩm, hiển thị tên cùng giá đã định dạng. Danh sách số lượng cho chọn từ 1 đến 10 nhờ vòng lặp for. Khi bấm nút Add Item, sản phẩm được đưa vào giỏ và trang giỏ hàng hiện ra. Phía dưới có liên kết View Cart để xem giỏ hàng.

**cart_view.php** – File này là trang Your Cart, hiển thị nội dung giỏ hàng lưu trong session. Nếu giỏ trống, trang báo chưa có sản phẩm nào. Nếu có hàng, trang vẽ một bảng gồm tên sản phẩm, giá, ô nhập số lượng và thành tiền của từng dòng, kèm tổng phụ ở cuối bảng. Người dùng sửa số lượng trong ô nhập rồi bấm Update Cart để gửi lên index.php với action là update; nhập 0 sẽ xóa sản phẩm đó. Hai liên kết phía dưới dẫn về trang Add Item hoặc làm trống toàn bộ giỏ hàng bằng Empty Cart.

**main.css** – File này định dạng giao diện cho cả hai trang bằng tông màu cam. Nền trình duyệt màu xám, nội dung nằm trong khung trắng căn giữa với bề rộng tối đa 700 pixel. Tiêu đề trong phần nội dung dùng màu cam #cc8420 lấy từ ảnh mẫu, còn tiêu đề đầu trang có đường kẻ đen phía dưới. Liên kết in đậm màu xanh đen. Bảng giỏ hàng có đường kẻ ngang ở dòng tiêu đề và dòng tổng phụ, cột số được căn phải, ô nhập số lượng thu nhỏ. Hai trang nối với file này bằng thẻ link.
