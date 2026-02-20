Hôm nay tôi muốn nói về một vài đặc điểm chí mạng của 1 Mobile App mà anh em cần biết. Kể cả là non-tech hay anh em dev mới vào nghề.

Anh em hãy tưởng tượng, app anh em làm xong, sau đó submit lên App Store và được duyệt.

Anh em đang rất hào hứng vì: Mình thật vãi đái, méo cần code gì hết vẫn submit được app lên store.

Anh em có chắc chắn 100% là:

- Cái app đó không bao giờ lỗi?

- Backend ( nếu có của anh em không bao giờ lỗi. )?

- Có những lỗi mà lúc App Store họ review, nó không xuất hiện, dần dần nó mới xuất hiện

- Khi anh em upgrade lên 1.2, đổi backend endpoint và một số user vẫn đang dùng Version 1.1.. Backend không đổi thì không được.

- Vân vân và mây mây …

Và hàng loạt những vấn đề , mà tôi chắc chắn là AI sẽ không nói cho các bạn biết. Vì nó chỉ tập trung giải quyết vấn đề của bạn đưa ra, chứ về kiến trúc tổng thể cho những cái tôi nói bên trên, nó không hề nói.

Tình huống số 1 ( Đa số các app sẽ gặp ). Theo anh em, khi app submit lên rồi, mà nó xuất hiện lỗi, ảnh hưởng tới trăm ngàn người dùng, thì anh em làm gì? App có thể fix ngay đấy, nhưng làm sao đưa lên store được đây? Vì phải chờ review mà? Giờ làm sao ta?

- Xin lỗi ngừoi dùng?

- Bắt người ta đợi anh em submit version mới, chờ review … ( quy trình này thường mất 1-2 ngày là nhanh nhất rồi )

Câu trả lời là không cần đâu. Anh em nên tìm hiểu về từ khoá Over-the-air (OTA) update để có thể xử lý việc này nhé. Đại loại đó là 1 kỹ thuật cho phép anh em cập nhật ứng dụng qua 1 bên thứ 3, mà không cần thông qua App Store. Tuy nhiên nó sẽ chỉ hõ trợ được khoảng 70%. Còn những phần can thiệp sâu liên quan tới native của thiết bị thì bắt buộc sẽ cần phải build lại app và submit lại app. Trước khi có Microsoft app center. Giờ nó EOL rồi. Công ty tôi đang code React Native thì dùng của Expo Updates.

Tình huống số 2 ( với app có backend ). Khi anh em có cập nhật gì đó ở phía backend, và đưa lên phiên bản mới cho app. VD thay đổi api, thay đổi payload Data thôi. Local thì chạy ngon luôn. Nhưng ngay thời điểm anh em deploy cái backend Version mới lên, thì toàn bộ app Version cũ sẽ lăn ra chết hết. Vậy thì chỗ này phải xử lý 2 chuyện.

- 1 là anh em cần phải đánh versioning cho API. Để khi release, cả v1.1 và v1.2 đều hoạt động được. Vd api/v1 ; api/v2. Dân chuyên thì họ có thể xử lý khéo léo để tránh trùng lặp, nhưng anh em non-tech Vibe code thì cứ lưu ý cái này và ra lệnh cho AI nó xử lý là được.

- Trước khi release thì lấy app version 1, test với backend mới nhất xem nó có hoạt động ổn định không. Sau đó hãy release backend -> web -> submit new app version

Tình huống số 3. App bắt buộc phải nâng cấp thì mới sử dụng được. ( anh em dùng app ngân hàng hay thấy cái này ). VD như anh em cần phải thay đổi toàn bộ app theo policy mới của App Store, hoặc có thay đổi cực lớn về System backend. thì mọi user phải cần được update lên version mới nhất để sử dụng. Xử lý cái này thế nào?

- Có 1 cái api check minimum version , hoặc là force update flag. Cứ mở app thì gọi vào api này.

- Nếu version app thấp hơn minimum version hoặc force update = true, thì anh em hiện cho user cái thông báo update, gắn link App Store vào. Là xong

Trên đây là 3 tình huống phổ biến mà tôi hay gặp . Còn rất nhiều quả kèo oái oăm khác mà anh em làm mobile app sẽ cần phải xử lý.

Với bài viết này, tôi hi vọng các anh em làm web/app sẽ có thêm nhiều góc nhìn về các vấn đề trong quá trình phát triển sản phẩm. Làm phần mềm không chỉ đơn giản là CODE!

Chúc anh em ngày mới vui và ngày càng build được những sản phẩm hay ho. Nếu thấy bài viết hữu ích thì giúp tôi lan toả nhé. Cảm ơn anh em.

P/s: Nay không dùng AI format nữa không anh em lại bảo content AI. =))))))))) Anh em chịu khó đọc vậy

[#ai](https://www.facebook.com/hashtag/ai?__eep__=6&__cft__[0]=AZZgMXwnSs6bD0uTYyX7dZlX4y6GyDzAXse51YIx9CcHj4nAFtiS5G9KSbHuu062_wry6XvuhLOuuW3krcINEN1vyumlhNvq9t3QmCCjIVzFCKVdvDGfklViLivRILoOJcYCFzmGAxY6C4frFZ9Hn9kuVtlz7ixP5ENLwcpC4OviF-Dr7yK9USO9XOJAD-j9b3PiFZSHQQujTu_uSwscuflV&__tn__=*NK-R) [#mobile](https://www.facebook.com/hashtag/mobile?__eep__=6&__cft__[0]=AZZgMXwnSs6bD0uTYyX7dZlX4y6GyDzAXse51YIx9CcHj4nAFtiS5G9KSbHuu062_wry6XvuhLOuuW3krcINEN1vyumlhNvq9t3QmCCjIVzFCKVdvDGfklViLivRILoOJcYCFzmGAxY6C4frFZ9Hn9kuVtlz7ixP5ENLwcpC4OviF-Dr7yK9USO9XOJAD-j9b3PiFZSHQQujTu_uSwscuflV&__tn__=*NK-R) [#dev](https://www.facebook.com/hashtag/dev?__eep__=6&__cft__[0]=AZZgMXwnSs6bD0uTYyX7dZlX4y6GyDzAXse51YIx9CcHj4nAFtiS5G9KSbHuu062_wry6XvuhLOuuW3krcINEN1vyumlhNvq9t3QmCCjIVzFCKVdvDGfklViLivRILoOJcYCFzmGAxY6C4frFZ9Hn9kuVtlz7ixP5ENLwcpC4OviF-Dr7yK9USO9XOJAD-j9b3PiFZSHQQujTu_uSwscuflV&__tn__=*NK-R) [#vibe](https://www.facebook.com/hashtag/vibe?__eep__=6&__cft__[0]=AZZgMXwnSs6bD0uTYyX7dZlX4y6GyDzAXse51YIx9CcHj4nAFtiS5G9KSbHuu062_wry6XvuhLOuuW3krcINEN1vyumlhNvq9t3QmCCjIVzFCKVdvDGfklViLivRILoOJcYCFzmGAxY6C4frFZ9Hn9kuVtlz7ixP5ENLwcpC4OviF-Dr7yK9USO9XOJAD-j9b3PiFZSHQQujTu_uSwscuflV&__tn__=*NK-R) [#coding](https://www.facebook.com/hashtag/coding?__eep__=6&__cft__[0]=AZZgMXwnSs6bD0uTYyX7dZlX4y6GyDzAXse51YIx9CcHj4nAFtiS5G9KSbHuu062_wry6XvuhLOuuW3krcINEN1vyumlhNvq9t3QmCCjIVzFCKVdvDGfklViLivRILoOJcYCFzmGAxY6C4frFZ9Hn9kuVtlz7ixP5ENLwcpC4OviF-Dr7yK9USO9XOJAD-j9b3PiFZSHQQujTu_uSwscuflV&__tn__=*NK-R) [#bip](https://www.facebook.com/hashtag/bip?__eep__=6&__cft__[0]=AZZgMXwnSs6bD0uTYyX7dZlX4y6GyDzAXse51YIx9CcHj4nAFtiS5G9KSbHuu062_wry6XvuhLOuuW3krcINEN1vyumlhNvq9t3QmCCjIVzFCKVdvDGfklViLivRILoOJcYCFzmGAxY6C4frFZ9Hn9kuVtlz7ixP5ENLwcpC4OviF-Dr7yK9USO9XOJAD-j9b3PiFZSHQQujTu_uSwscuflV&__tn__=*NK-R) [#buildinpublic](https://www.facebook.com/hashtag/buildinpublic?__eep__=6&__cft__[0]=AZZgMXwnSs6bD0uTYyX7dZlX4y6GyDzAXse51YIx9CcHj4nAFtiS5G9KSbHuu062_wry6XvuhLOuuW3krcINEN1vyumlhNvq9t3QmCCjIVzFCKVdvDGfklViLivRILoOJcYCFzmGAxY6C4frFZ9Hn9kuVtlz7ixP5ENLwcpC4OviF-Dr7yK9USO9XOJAD-j9b3PiFZSHQQujTu_uSwscuflV&__tn__=*NK-R)