# Zero-Width String Encoder

> Embed invisible text inside any string using zero-width Unicode characters.

**[Tiếng Việt](#tiếng-việt)** · **[English](#english)**

---

## English

### What is this?

Zero-Width String Encoder is a single-file web application that lets you hide a secret string inside any visible text using zero-width Unicode characters. The resulting string looks completely identical to the original — no visual difference — but carries hidden data that can be extracted with the built-in decoder.

This technique is a form of text-based steganography, useful for watermarking text, embedding metadata, or passing hidden messages through plain-text channels.

### Features

- **Encode** — embed a hidden string into any original string
- **Decode** — extract hidden strings from any text that contains zero-width characters
- **Insert position control** — choose to insert at the start, end, or a custom character offset
- **Visual preview** — see exactly where the hidden content sits within the output string
- **Copy to clipboard** — one-click copy with `execCommand` fallback for iframe environments
- **Bilingual UI** — switch between Vietnamese and English at any time
- **Zero dependencies** — pure HTML, CSS, and JavaScript; no build step, no libraries

### How it works

Each character in the hidden string is UTF-8 encoded into bytes. Each byte is then serialized as 8 zero-width characters:

| Character | Unicode | Meaning   |
|-----------|---------|-----------|
| Zero Width Space | `U+200B` | bit `0` |
| Zero Width Non-Joiner | `U+200C` | bit `1` |
| Zero Width Joiner | `U+200D` | byte separator |

**Example:** The character `A` (ASCII 65 = `01000001`) is encoded as:
```
U+200B U+200C U+200B U+200B U+200B U+200B U+200B U+200C U+200D
  0      1      0      0      0      0      0      1    (separator)
```

The encoded block is then inserted into the original string at the chosen position. The result is visually indistinguishable from the original.

### Usage

1. Open `zero-width-encoder.html` in any modern browser — no server required.
2. **Encode tab**: enter the visible string and the string to hide, choose an insert position, then click *Generate hidden string*. Copy the result.
3. **Decode tab**: paste any text into the input, then click *Decode hidden string* to reveal any embedded content.
4. Use the **VI / EN** toggle in the top-right corner to switch the interface language.

### Compatibility

Works in any modern browser (Chrome, Firefox, Safari, Edge). The clipboard copy uses the `Clipboard API` with an `execCommand` fallback, so it works in sandboxed iframe environments such as embedded chat interfaces.

### Limitations

- The output string is longer in terms of raw bytes (each hidden character adds ~9 invisible characters). The visual length remains unchanged.
- Some text platforms strip zero-width characters on paste or save. Test your target platform before relying on this for sensitive use cases.
- Not a security tool — zero-width characters can be detected by anyone who inspects the raw bytes.

### File structure

```
zero-width-encoder.html   # Single-file application (HTML + CSS + JS)
README.md                 # This file
```

### License

MIT — free to use, modify, and distribute.

---

## Tiếng Việt

### Giới thiệu

Zero-Width String Encoder là ứng dụng web đơn file cho phép bạn ẩn một chuỗi bí mật bên trong bất kỳ đoạn văn bản nào, sử dụng các ký tự Unicode zero-width (độ rộng bằng không). Chuỗi kết quả trông hoàn toàn giống chuỗi gốc — không có bất kỳ sự khác biệt nào về mặt hiển thị — nhưng chứa dữ liệu ẩn có thể được trích xuất bằng bộ giải mã tích hợp sẵn.

Kỹ thuật này là một dạng steganography văn bản, hữu ích cho việc đánh dấu bản quyền nội dung, nhúng metadata, hoặc truyền tin nhắn ẩn qua các kênh văn bản thuần túy.

### Tính năng

- **Mã hóa** — nhúng chuỗi ẩn vào bất kỳ chuỗi gốc nào
- **Giải mã** — trích xuất chuỗi ẩn từ văn bản chứa ký tự zero-width
- **Kiểm soát vị trí chèn** — chèn vào đầu, cuối, hoặc vị trí ký tự tùy chỉnh
- **Xem trước trực quan** — hiển thị chính xác vị trí nội dung ẩn trong chuỗi kết quả
- **Sao chép vào clipboard** — sao chép một chạm, có fallback `execCommand` cho môi trường iframe
- **Giao diện song ngữ** — chuyển đổi giữa tiếng Việt và tiếng Anh bất cứ lúc nào
- **Không phụ thuộc thư viện** — HTML, CSS và JavaScript thuần; không cần build, không cần thư viện ngoài

### Nguyên lý hoạt động

Mỗi ký tự trong chuỗi ẩn được mã hóa UTF-8 thành các byte. Mỗi byte sau đó được biểu diễn bằng 8 ký tự zero-width:

| Ký tự | Unicode | Ý nghĩa |
|-------|---------|---------|
| Zero Width Space | `U+200B` | bit `0` |
| Zero Width Non-Joiner | `U+200C` | bit `1` |
| Zero Width Joiner | `U+200D` | phân cách byte |

**Ví dụ:** Ký tự `A` (ASCII 65 = `01000001`) được mã hóa thành:
```
U+200B U+200C U+200B U+200B U+200B U+200B U+200B U+200C U+200D
  0      1      0      0      0      0      0      1    (phân cách)
```

Khối mã hóa sau đó được chèn vào chuỗi gốc tại vị trí đã chọn. Kết quả không thể phân biệt về mặt hiển thị so với chuỗi gốc.

### Hướng dẫn sử dụng

1. Mở `zero-width-encoder.html` trên bất kỳ trình duyệt hiện đại nào — không cần server.
2. **Tab Mã hóa**: nhập chuỗi hiển thị và chuỗi muốn ẩn, chọn vị trí chèn, rồi nhấn *Tạo chuỗi ẩn*. Sao chép kết quả.
3. **Tab Giải mã**: dán văn bản vào ô nhập, nhấn *Giải mã chuỗi ẩn* để xem nội dung được nhúng.
4. Dùng nút **VI / EN** ở góc trên bên phải để chuyển ngôn ngữ giao diện.

### Tương thích

Hoạt động trên mọi trình duyệt hiện đại (Chrome, Firefox, Safari, Edge). Chức năng sao chép sử dụng `Clipboard API` với fallback `execCommand`, đảm bảo hoạt động trong môi trường iframe như các giao diện chat nhúng.

### Hạn chế

- Chuỗi kết quả dài hơn về số byte thô (mỗi ký tự ẩn thêm khoảng 9 ký tự vô hình). Độ dài hiển thị không thay đổi.
- Một số nền tảng tự động xóa ký tự zero-width khi dán hoặc lưu. Hãy kiểm tra nền tảng mục tiêu trước khi sử dụng cho các trường hợp quan trọng.
- Đây không phải công cụ bảo mật — ký tự zero-width có thể bị phát hiện bởi bất kỳ ai kiểm tra byte thô của văn bản.

### Cấu trúc file

```
zero-width-encoder.html   # Ứng dụng đơn file (HTML + CSS + JS)
README.md                 # File này
```

### Giấy phép

MIT — tự do sử dụng, chỉnh sửa và phân phối.
