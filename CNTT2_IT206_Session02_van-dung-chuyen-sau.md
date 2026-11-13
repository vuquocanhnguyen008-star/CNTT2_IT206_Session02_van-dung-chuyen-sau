# Bài 1: Thiết kế giải pháp Prompting tự động hóa (CREATE + Few-shot + JSON/Table)

> Tình huống giả định (vì đề bị cắt): tự động trích xuất thông tin đơn hàng từ tin nhắn khách thành JSON. Nếu đề của bạn có tình huống khác thì đổi lại cho khớp.

## Bước 1: Thiết kế giải pháp (Input/Output)

- **Input:** tin nhắn khách hàng (văn bản tự do), có thể thiếu hoặc sai thông tin.
- **Output:** JSON gồm `ten_khach`, `san_pham`, `so_luong`, `sdt`, `trang_thai`.
- **Xử lý lỗi:**
  - Thiếu trường thì để `null`.
  - Dữ liệu rỗng hoặc sai lệch thì trả `{"loi": "du_lieu_khong_hop_le"}`.
  - Không được tự bịa thông tin.

## Bước 2: Prompt hoàn chỉnh

```
[C] Bạn là hệ thống xử lý đơn hàng tự động của cửa hàng TechShop.
[R] Trích xuất thông tin đơn hàng từ tin nhắn khách và trả về JSON.
[E] (Few-shot)
Input: "Mình là Lan, lấy 2 chuột Logitech, sđt 0901234567"
Output: {"ten_khach":"Lan","san_pham":"Chuột Logitech","so_luong":2,"sdt":"0901234567","trang_thai":"hop_le"}

Input: "Cho mình đặt bàn phím"
Output: {"ten_khach":null,"san_pham":"Bàn phím","so_luong":null,"sdt":null,"trang_thai":"thieu_thong_tin"}
[A] Chỉ trả về JSON thuần, không giải thích. Trường nào không có thì để null, không tự đoán. Nếu tin nhắn rỗng hoặc không liên quan đơn hàng, trả {"loi":"du_lieu_khong_hop_le"}.
[T] JSON đúng cấu trúc ở trên.
[E] Tin nhắn cần xử lý: "[dán tin nhắn vào đây]"
```

## Kết quả chạy thử

Dán prompt vào AI, thử 3 trường hợp (đủ thông tin, thiếu thông tin, tin nhắn rỗng) rồi copy kết quả vào đây:

- Trường hợp 1 (đủ thông tin): _[dán kết quả]_
- Trường hợp 2 (thiếu thông tin): _[dán kết quả]_
- Trường hợp 3 (tin nhắn rỗng): _[dán kết quả]_
