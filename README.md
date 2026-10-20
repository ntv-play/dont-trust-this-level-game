# Trang web giới thiệu game (NTV Play)

Trang giới thiệu "Don't Trust This Level" / "Đừng Tin Màn Này", hai thứ tiếng, cùng phong cách với game ([STYLE-GUIDE.md](../STYLE-GUIDE.md)). Đăng lên GitHub Pages, Cloudflare Pages hoặc Netlify. Trang này cũng là chỗ đặt chính sách riêng tư và `app-ads.txt` mà Google Play và AdMob yêu cầu ([docs/PUBLISH.md](../docs/PUBLISH.md), mục 2).

| File | Là gì |
| --- | --- |
| `index.html` | Trang chính: tên game, nút Google Play, tính năng, ảnh chụp, danh sách "những thứ không nên tin" |
| `privacy.html` | Chính sách riêng tư (tiếng Việt + tiếng Anh) |
| `app-ads.txt` | Dòng xác minh của AdMob |
| `img/` | Logo hạt đậu (`logo.svg`) và ảnh chụp game `<vi|en>-<menu|trap|replay|win>.jpg` |

## Ngôn ngữ

Trang tự chọn tiếng Việt nếu trình duyệt để tiếng Việt, còn lại tiếng Anh. Nút 🌐 đổi ngôn ngữ và nhớ lựa chọn. Link `?lang=vi` hoặc `?lang=en` ép ngôn ngữ (tiện cho link trong clip TikTok).

Chữ nằm trong object `T` ở cuối `index.html` (`T.vi`, `T.en`). Chữ viết sẵn trong HTML là bản tiếng Anh, cho máy tìm kiếm và khi trình duyệt tắt JavaScript.

## Trước khi đăng

1. `npm run site`: chụp lại ảnh game trong `img/` ở cả hai thứ tiếng (chạy lại mỗi khi giao diện game thay đổi). Lệnh này build một bản web không quảng cáo vào `.site-build/` chỉ để chụp ảnh; bản đó không đăng lên trang.
2. `privacy.html`: thay `[TÊN NHÀ PHÁT TRIỂN]`, `[DEVELOPER NAME]`, `[EMAIL]`.
3. `app-ads.txt`: thay bằng đúng dòng AdMob đưa ([docs/ADMOB.md](../docs/ADMOB.md), bước 7).
4. `index.html`, object `CONFIG` ở đầu thẻ `<script>`:
   - `email`: email liên hệ (để trống thì ẩn link "Liên hệ");
   - `storeLive`: đổi thành `true` khi app đã lên Google Play. Nút xám "Sắp có trên Google Play" sẽ thành nút "Tải trên Google Play" trỏ tới `storeUrl`.
5. `index.html`, thẻ `og:image`: đổi thành link đầy đủ (`https://<tên-miền>/img/en-menu.jpg`) để Facebook, Zalo, Messenger hiện ảnh khi chia sẻ link.

## Đăng lên GitHub Pages

1. Tạo repo công khai tên đúng `<tên-github>.github.io`.
2. Chép **toàn bộ nội dung** thư mục `site/` (trừ file README này nếu muốn) vào gốc repo, commit, push.
3. Repo → Settings → Pages → Source: nhánh `main`, thư mục `/ (root)`.
4. Vài phút sau trang chạy ở `https://<tên-github>.github.io`. Kiểm tra:
   - `https://<tên-github>.github.io/` mở trang chính, bấm 🌐 đổi được ngôn ngữ;
   - `https://<tên-github>.github.io/privacy.html` và `/app-ads.txt` mở được.
5. Điền `https://<tên-github>.github.io/privacy.html` vào `PRIVACY_URL` trong [src/platform/adConfig.ts](../src/platform/adConfig.ts) và vào Play Console. Điền `https://<tên-github>.github.io` vào mục Website trên trang Play Store.

## Xem thử trên máy

```powershell
npx vite preview --outDir site --port 4300
```

Rồi mở http://localhost:4300.
