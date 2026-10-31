# BigSix – Bản mô phỏng UI/UX

Bản giao diện độc lập được dựng từ frontend BigSix trong dự án. Mọi thao tác nghiệp vụ chạy bằng JavaScript và dữ liệu mẫu lưu trên trình duyệt. **Không cần Laravel, PHP, MySQL hoặc kết nối API backend.**

## Mở bản demo

Trên Windows, chạy **`START_DEMO.bat`** trong thư mục này. Cần cài Node.js trước; lần đầu chưa có thư viện thì chương trình sẽ cài bằng npm. Giữ cửa sổ lệnh mở khi trải nghiệm, nhấn `Ctrl+C` để dừng.

Hoặc chạy:

```powershell
cd C:\2026\TTCN\UIUX
npm ci
npm run dev
```

Mở **http://127.0.0.1:5173**. Lệnh `npm run dev` chỉ phục vụ giao diện tĩnh và tự cập nhật khi sửa mã; không cung cấp backend nghiệp vụ. Không mở trực tiếp `index.html` bằng cách nhấp đúp, vì mã React cần Vite xử lý.

## Tài khoản và thao tác nhanh

Thanh **UI/UX DEMO** trên cùng cho phép chuyển ngay giữa Khách, Người thuê, Chủ trọ và Admin. Trang đăng nhập có các nút điền nhanh tài khoản.

| Vai trò | Email | Mật khẩu |
|---|---|---|
| Người thuê | `user@bigsix.test` | `12345678` |
| Chủ trọ | `saler@bigsix.test` | `12345678` |
| Admin | `admin@bigsix.test` | `12345678` |

Các tài khoản phụ `owner2@bigsix.test` và `binh@bigsix.test` cũng dùng mật khẩu trên. Đăng ký mới dùng **OTP `123456`**, hết hạn sau 10 phút; không gửi email thật.

## Các màn hình và chức năng

- Danh sách phòng: tìm theo từ khóa, thành phố, giá và tiện ích; sắp xếp; phân trang; lưới/danh sách/bản đồ; yêu thích, lịch sử tìm kiếm và phòng vừa xem.
- Chi tiết phòng: thư viện ảnh, tiện ích, thông tin chủ trọ, bản đồ và biểu mẫu đặt phòng.
- Đăng ký, OTP, đăng nhập, đăng xuất; thông tin hồ sơ và đổi mật khẩu mẫu.
- Đăng phòng, chọn tọa độ, tải ảnh từ máy, xem trước, sửa và xóa tin.
- Đặt phòng: nhập thông tin người thuê, số tháng, ngày dự kiến; xem, chấp nhận, từ chối, hoàn thành và hủy đơn theo vai trò.
- Hồ sơ đăng ký chủ trọ; Admin xem, duyệt/từ chối, nhập ghi chú; người gửi theo dõi kết quả.
- Admin đổi vai trò và xóa tài khoản mẫu; dashboard hiển thị số liệu theo tài khoản.
- Kế hoạch đồ án; giao diện Việt/Anh và sáng/tối.

Các dữ liệu phòng, tài khoản, đơn và hồ sơ đều là giả lập. Ảnh phòng là hình minh họa SVG cục bộ. Bản đồ có thể kéo, phóng to/thu nhỏ, chọn điểm và mở marker; **nền bản đồ và tra cứu địa điểm chỉ là mô phỏng**, không phải dữ liệu địa lý chính xác. QR liên hệ là hình minh họa, không phải QR thực. Các liên kết chủ động mở Google Maps/Zalo/Facebook cần internet và không thuộc xử lý nội bộ của demo.

## Lưu và đặt lại

Dữ liệu được lưu trong `localStorage` với tiền tố `bigsix-uiux:` và giữ lại sau khi tải lại trang. Không dùng cơ sở dữ liệu hoặc dịch vụ lưu trữ máy chủ. Không nhập mật khẩu hoặc thông tin cá nhân thật vào bản mô phỏng.

Nút **Đặt lại mẫu → Đặt lại dữ liệu** khôi phục dữ liệu ban đầu, xóa các thay đổi và phiên đăng nhập của demo. Không xóa dữ liệu không mang tiền tố trên. Có 16 tin mẫu (14 tin còn trống), 5 tài khoản, 4 đơn và 1 hồ sơ chủ trọ chờ duyệt để thử các màn hình ngay.

Bản này giữ cách thao tác của website nguồn: hủy đơn hiện xóa bản ghi; hoàn thành đơn chưa tự trả phòng về còn trống; chưa bổ sung cơ chế chống đặt trùng. Đây là mô phỏng để trình bày giao diện, không thay thế hệ thống thật.

## Build và kiểm tra

```powershell
npm test
npm run test:ui
npm run build
npm run preview
```

`npm test` chạy các kịch bản dịch vụ mẫu. `npm run test:ui` chạy kiểm thử thao tác bằng Chrome/Edge cài trên Windows; có thể đặt biến `UIUX_CHROME_PATH` nếu trình duyệt ở đường dẫn khác. Kết quả và ảnh kiểm tra được ghi trong `test-results/`.

`npm run build` tạo bản giao diện tĩnh trong `dist/`. `npm run preview` phục vụ bản build tại http://127.0.0.1:4173. Có thể đưa thư mục `dist/` lên hosting tĩnh, không cần backend.

## Mã chính

- `src/pages/`, `src/components/`, `src/contexts/`: các màn hình, thanh điều hướng, ngôn ngữ và điều khiển demo.
- `src/api/services.js`: xử lý các thao tác trên dữ liệu trình duyệt, không gọi HTTP.
- `src/api/seed.js`: dữ liệu mẫu ban đầu.
- `src/demoEnvironment.js`: thay tra cứu địa điểm ngoài bằng dữ liệu mẫu cục bộ.
- `public/assets/`: ảnh phòng, nền bản đồ và QR minh họa.

Frontend gốc trong `../frontend` và backend trong `../backend` được giữ riêng, không bị thay bằng bản demo này.
