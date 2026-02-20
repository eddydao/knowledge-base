#  Note
Debugging là thứ mà ta làm sau khi thực hiện thành công một test case
> Một test case thành công là test case cho thấy chương trình không thực hiện đúng những gì chương trình đó cần làm

Debugging có 2 bước
- Bước 1: Xác định nơi nghi ngờ lỗi xảy ra trong chương trình
- Bước 2: Sửa lỗi đó

Debugging thường là hoạt động mà lập trình viên không thích nhất, vì:
- Việc debug ra lỗi là bằng chứng lập trình viên không đủ hoàn hảo
- Trong các hoạt động phát triển phần mềm, debug tốn năng lượng tinh thần nhất. Thông thường, các lỗi cần được sửa nhanh nhất có thể, và đôi khi có những lỗi xảy ra ở rất nhiều nơi trong chương trình.
- So với các hoạt động khác trong phát triển phần mềm, quá trình debugging có rất ít nghiên cứu, tài liệu và quy trình chuẩn.

# Các phương pháp debugging:

## Vét cạn
Là một phương pháp thông dụng trong gỡ lỗi
Không cần suy nghĩ quá nhiều nhưng có hiệu suất thấp và thường khó thành công
Có thể được chia thành 3 danh mục chính:

### Gỡ lỗi với Memory dump
Là phương pháp Vét cạn có hiệu quả thấp nhất:
- Khó để biết được kết nối giữa vị trí ô nhớ và biến trong chương trình
- Với các chương trình lớn, memory dump cho ra một lượng lớn data, phần lớn data không liên quan đến vấn đề
- Memory dump là một bản snapshot của chương trình tại thời điểm tạo ra, nhưng khi gỡ lỗi, thường cần đến trạng thái động của chương trình ( trạng thái thay đổi theo thời gian)
- Thường không phản ánh chính xác điểm/ thời điểm gây lỗi, có thể che giấu mất manh mối để tìm ra lỗi
- Không có phương pháp thích hợp để tìm ra lỗi với memory dump

### Gỡ lỗi với việc "ghi log khắp chương trình"
Hiệu quả hơn memory dump vì cho thấy trạng thái động của chương trình và cho phép theo dõi thông tin có liên quan đến chương trình
Vẫn có các vấn đề xảy ra:
- Hit-or-missed: thay vì củng cố việc tìm kiếm lỗi sai theo hướng logic, phương pháp này dựa vào may mắn
- Cho ra một lượng lớn data cần được phân tích
- Yêu cầu thay đổi code chương trình, có thể gây ra lỗi khác
- Sự đánh đổi khi sử dụng ở các chương trình lớn là khá cao, không phù hợp với một số loại chương trình

### Gỡ lỗi với công cụ tự động
Công cụ gỡ lỗi tự động có cách hoạt động tương tự bằng cách thêm các dòng lệnh "in" vào trong chương trình, nhưng thay vì làm thay đổi code chương trình, ta theo dõi các thông tin, thông số thông qua tính năng debug của ngôn ngữ hoặc tương tác với công cụ gỡ lỗi.
Công cụ của ngôn ngữ thường là việc cho phép in `stacktrace` hay các biến đặc tả.
Công cụ gỡ lỗi tương tác cho phép đặt `breakpoint` trong code để chương trình có thể dừng tại một điểm cụ thể khi một đoạn code được thực hiện hoặc một biến số bị thay đổi, cho phép LTV theo dõi trạng thái của chương trình.

### Điểm chung của vét cạn
- Loại bỏ quá trình suy nghĩ

> Recommend Vét cạn khi (1) các phương pháp khác không có tác dụng, (2) làm hỗ trợ cho phương pháp Quy nạp

## Phương pháp Quy nạp
Thực hiện với việc từ một manh mối ( một biểu hiện của lỗi, kết quả `failed` của một hay nhiều test case), tìm kiếm mối liên hệ giữa các manh mối để suy ra lỗi đang xảy ra và fix nó.

Các bước thực hiện:
- Bước 1: thu thập dữ liệu liên quan: liệt kê các thông tin đã biết về việc chương trình đã thực hiện đúng và sai, những triệu chứng mà ta tin có thể có lỗi
- Bước 2: Tổ chức dữ liệu: sắp xếp dữ liệu theo cách có thể giúp nhận ra mẫu hình `pattern` và tìm kiếm các điểm mâu thuẫn
- Bước 3: đưa ra giả thuyết: đưa ra giả thuyết dựa trên các thông tin đã có
- Bước 4: kiểm chứng giả thuyết: so sánh giả thuyết với dữ liệu ban đầu xem nó có giải thích toàn bộ các triệu chứng hay không. Nếu sai, gỉa thuyết sai/ chưa đầy đủ/ có nhiều lỗi xảy ra
- Bước 5: sửa lỗi: chỉ khi hoàn tất các bước trên, mới nên tiến hành sửa lỗi. Sau khi sửa, hãy tiến hành kiểm thử để đảm bảo việc fix lỗi ko tạo ra các lỗi mới.




## Phương pháp Suy diễn
