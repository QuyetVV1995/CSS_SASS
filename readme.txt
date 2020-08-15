3 yếu tố quan trọng để có thể tạo nên 1 trang web tốt:
- Responsive design: chạy ổn định trên các màn hình thiết bị khác nhau
- Maintainable and scalable code: code rõ ràng, dễ hiểu, có thể tái sử dụng, tổ chức files, đặt tên classes, tổ chức code file html
- Web Performance: 
+ Giảm request lên website trong 1 khoảng thời gian
+ Giảm lượng dữ liệu phải tải khi load trang ( html, css, js, hình ảnh, videos, …)
+ Nén code CSS và JS
+ Đặc biết sử dụng ít hình ảnh và videos, sử dụng hình ảnh đã được nén bớt dung lượng và hiển thị phù hợp trên website .

Tổng quan về cách hoạt động của CSS
- Đầu tiên là browser sẽ load HTML, sau đó sẽ phân tích (parse) code HTML, từ đó browser tạo ra
 document object model (DOM) (có phân cấp theo theo: parent’s element, child’s element, …..)
- Sau khi phân tích code HTML tạo ra DOM, bắt đầu tìm file stylesheet để bắt đầu load CSS 
và rồi cũng phân tích code CSS và tạo ra CSS object model hay CSSOM (tương tự DOM) 
- CSSOM và DOM lưu (store)  trong 1 thứ gọi là render tree, và tiếp tục đến lượt website sẽ render sử dụng Visual formating model
- Và cuối cùng website được render (sinh ra, hiển thị) lên trên browser


Việc khai báo CSS gồm 2 phần:

Selector: gồm 1 hoặc nhiều element được khai báo
Declaration block: nơi mà để khai báo các thuộc tính (properties)
           Mỗi properties trong declaration block đều có declared value

Cascade ( trong Cascading Style Sheet CSS) là quá trình xử lý và kết hợp khi có nhiều thuộc tính được khai báo cùng nhau vào cùng 1 element.

Những nguồn khai báo CSS

User declaration (user style sheet): khi sử dụng trong 1 số browser cho phép user có thể chỉnh sửa CSS trên browser như Google Chrome (google development tool) ,…
Author declaration (author style sheet): Chính là những dòng code CSS do developer (chúng ta) tạo ra
Default value (user urgent style sheet): Những giá trị mặc định khi chúng ta không khai báo trong code CSS.
 (Ví dụ: font chữ mặc định sẽ là 16px nếu chúng ta không khai báo trong Author Style Sheet)


sử dụng phép so sánh vào 3 thông số lần lượt:

Độ quan trọng ( Importance) > Độ đặc trưng (Specificity) > Thứ tự dòng code (source order)

IMPORTANCE: Chắc các bạn đã quen với key word !important khi khai báo, khi đó ưu tiên đầu tiên sẽ những dòng khai báo có !important ở đó. 
Trong đó !important bởi User (hay reader của website) sẽ quan trọng hơn và được sử dụng là giá trị cuối cùng của properties. 
Ít quan trong nhất chính là các giá trị mặc định của browser (Default browser declaration).

SPECIFICITY: Khi được khai báo với cùng độ quan trọng ta sử dụng độ đặc trưng nhất đó chính là chúng ta sử dụng CSS inline styles ( khai báo CSS trong thẻ HTML).
 Quan trọng tiếp đến là ID, tiếp là class, pseudo-class của class và cuối cùng là element, pseudo-class của element. Ta sử dụng giá trị của từng hệ số để so sánh.

 Lưu ý
!important lúc nào cũng được ưu tiên cao nhất
Chỉ dùng !important như sự lựa chọn cuối cùng, tốt hơn nên níu vào SPECIFICITIES, nó sẽ dễ bảo trì và mở rộng hơn.
Sử dụng inline styles cũng được nhưng không nên ưu tiên sử dụng (giống !important là khó bảo trì)
1 id đặc trưng hơn 100 class và tương tự 1 class đặc trưng hơn 100 elements
Khai báo * có thông số so sánh là (0,0,0,0)
Khi sử dụng CSS từ file CSS ngoài (các thư viện, framework css) luôn để author code (code của bạn viết ) ở cuối


Việc tìm hiểu value processing quan trọng vì %, em, rem đều convert lại thành px khi webpage được load, 
chúng ta biết để có thể tính toán và sử dụng hiểu quả, tránh nhầm lẫn
để có thể giải thích value processing gồm 6 giai đoạn:
Declared value > Cascaded value > Specified value > Computed Value > Used Value >  Actual value
(Hình 4 tìm hiểu quá trình xử lý cuối cùng của CSS)
- DECLARED VALUE: chính là giá trị mà chúng ta khai báo trong CSS declaration block (ví dụ ở đây width của thẻ p có 2 khai báo là 66% (thông qua class .amazing)) và 140px ( element p).
 Đối với padding của element p hay font-size của section không được khai báo thì để trống
- CASCADED VALUE: thì đã được mình giải thích ở bài trước, thì ở đây witdh cascaded value của width sẽ là 66%, đặc biệt, font-size của webpage được mặc định là 16px do user urgent stylesheet
- SPECIFIED VALUE: Giá trị của CSS property được xác định (bắt buộc mọi property của CSS đều phải có giá trị) , 
do không được khai báo nên giá trị mặc định padding element p bằng 0px, font-size paragraph thì thừa kế giá trị computed của element cha 24px.
- COMPUTED VALUE: Convert những giá trị liên quan nhau (thường là font-size). Ở đây rem sẽ lấy giá trị root của web browser để qui đổi 1.5rem = 1.5 * root font-size. 
( Sẽ được giải thích kĩ hơn trong phần sau của bài học )
- USED VALUE: Tính toán cuối cùng dựa trên kích thước element, kích thước website. Ở đây width chiếm 66% width của element cha là .section 280px nên 184.8px.
- ACTUAL VALUE: số liệu thực tế hiển thị lên trên browser, do browser có đơn vị nhỏ nhất là 1px nên sử dụng 185px thay vì 184.8px
Đó là quá trình xử lí giá trị từ khi khai báo đến khi có thông số cuối cùng hiển thị lên trên browser

CSS convert các chỉ số sang px

html, body{
    font-size: 16px;
    width: 80vw;
}

.header{
    font-size: 150%;
    padding: 2em;
    margin-bottom: 10rem;
    height: 90vh;
    width: 1000px;
}

.header-child {    /*element con của .header*/   
    font-size: 3em;
    padding: 10%;
}
(hình 5 tìm hiểu quá trình xử lý cuối cùng của CSS)

- Fontsize sẽ dựa vào computed value của fontsize element cha để tính toán ở đây là 16px (body là element cha)
- Nếu sử dụng % để tính kích thước như (height, width, padding, margin,…) thì nó sẽ lấy width của element cha ở đây là 1000px để tính toán
- Với em khi sử dụng cho fontsize thì, nó sẽ lấy số liệu fontsize của element cha ( 24px = 150% của header)
- Chú ý với em khi sử dụng cho kích thước thì sử dụng giá trị fontsize của chính element đó (đừng nhầm với % nhé) ở ví dụ là fontsize : 24px của header với padding 2 em tương đượng 48px.
- Với rem thì với fontsize và kích thước là như nhau, đều sử dụng fontsize của browser (khai bảo ở thẻ html hoặc giá trị mặc định) để tính toán.
- Vh, vw thì khá là quen thuộc, tính toán dựa vào giá trị của viewport