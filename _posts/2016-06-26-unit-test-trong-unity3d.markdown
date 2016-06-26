---
layout:     post
title:      "Unit Test trong Unity"
subtitle:   "Unit Test"
date:       2016-06-26 02:30:00
author:     "Thiên Lê"
header-img: "img/post-bg-01.jpg"
---

<p>Lại cuối tuần rồi :D hôm nay mình sẽ tìm hiểu về Unit Test (UT) (khái niệm, lợi ích, …) và làm thế nào để ứng dụng Unit Test vào Unity.</p>

<h2 class="section-heading">Unit test là gì?</h2>

<p>UT là kỹ thuật kiểm nghiệm các hoạt động của mọi chi tiết mã (code) với một quy trình tách biệt với quy trình phát triển PM, giúp phát hiện sai sót kịp thời. UT còn có thể giúp phát hiện các vấn đề tiềm ẩn và các lỗi thời gian thực ngay cả trước khi chuyên viên kiểm định chất lượng (QA - Quality Assurance) tìm ra, thậm chí có thể sửa lỗi ngay từ ý tưởng thiết kế.</p>

<p>UT là các đoạn mã có cấu trúc giống như các đối tượng được xây dựng để kiểm tra từng bộ phận trong hệ thống. Mỗi UT sẽ gửi đi một thông điệp và kiểm tra câu trả lời nhận được đúng hay không, bao gồm: </p>
<p>     -	Các kết quả trả về mong muốn <br>
        -	Các lỗi ngoại lệ mong muốn
</p>
<p>Các đoạn mã UT hoạt động liên tục hoặc định kỳ để thăm dò và phát hiện các lỗi kỹ thuật trong suốt quá trình phát triển, do đó UT còn được gọi là kỹ thuật kiểm nghiệm tự động.</p>
<p>UT có các đặc điểm sau:</p>
<p>     -	Đóng vai trò như những người sử dụng đầu tiên của hệ thống. <br>
        -	Chỉ có giá trị khi chúng có thể phát hiện các vấn đề tiềm ẩn hoặc lỗi kỹ thuật.
</p>
<p>Tóm lại là mình test từ trong code luôn, code tới đâu, test tới đó chứ không phải làm xong tính năng nào thì build lên rồi chạy thử như cách trước giờ mình vẫn làm :v </p>

<h2 class="section-heading">Ứng dụng của Unit Test</h2>

<ul style="list-style-type:disc">
  <li>Kiểm tra mọi đơn vị nhỏ nhất là các thuộc tính, sự kiện, thủ tục và hàm. </li>
  <li>Kiểm tra các trạng thái và ràng buộc của đối tượng ở các mức sâu hơn mà thông thường chúng ta không thể truy cập được.</li>
  <li>Kiểm tra các quy trình (process) và mở rộng hơn là các khung làm việc(workflow - tập hợp của nhiều quy trình).</li>  
</ul>

<h2 class="section-heading">Lợi ích của Unit Test</h2>

<p>Thời gian đầu, người ta thường do dự khi phải viết UT thay vì tập trung vào viết mã cho các chức năng nghiệp vụ. Công việc viết UT có thể ngốn nhiều thời gian, tuy nhiên UT đem lại lợi ích to lớn như:</p>

<ul style="list-style-type:disc">
  <li>Tạo ra môi trường lý tưởng để kiểm tra bất kỳ đoạn mã nào, có khả năng thăm dò và phát hiện lỗi chính xác, duy trì sự ổn định của toàn bộ PM và giúp tiết kiệm thời gian so với công việc gỡ rối truyền thống.</li>
  <li>Phát hiện các thuật toán thực thi không hiệu quả, các thủ tục chạy vượt quá giới hạn thời gian.</li>
  <li>Phát hiện các vấn đề về thiết kế, xử lý hệ thống, thậm chí các mô hình thiết kế.</li>  
  <li>Phát hiện các lỗi nghiêm trọng có thể xảy ra trong những tình huống rất hẹp.</li>
  <li>Tạo hàng rào an toàn cho các khối mã: Bất kỳ sự thay đổi nào cũng có thể tác động đến hàng rào này và thông báo những nguy hiểm tiềm tàng.</li>
  <li>UT là môi trường lý tưởng để tiếp cận các thư viện API bên ngoài một cách tốt nhất. Sẽ rất nguy hiểm nếu chúng ta ứng dụng ngay các thư viện này mà không kiểm tra kỹ lưỡng công dụng của các thủ tục trong thư viện. Dành ra thời gian viết UT kiểm tra từng thủ tục là phương pháp tốt nhất để khẳng định sự hiểu đúng đắn về cách sử dụng thư viện đó. Ngoài ra, UT cũng được sử dụng để phát hiện sự khác biệt giữa phiên bản mới và phiên bản cũ của cùng một thư viện. </li>  
</ul>

<p>Trong môi trường làm việc cạnh tranh, UT còn có tác dụng rất lớn đến năng suất làm việc:</p>
<ul style="list-style-type:disc">
  <li>Giải phóng chuyên viên QA khỏi các công việc kiểm tra phức tạp. </li>
  <li>Tăng sự tự tin khi hoàn thành một công việc. Chúng ta thường có cảm giác không chắc chắn về các đoạn mã của mình như liệu các lỗi có quay lại không, hoạt động của module hiện hành có bị tác động không, hoặc liệu công việc hiệu chỉnh mã có gây hư hỏng đâu đó... </li>
  <li>Là công cụ đánh giá năng lực của bạn. Số lượng các tình huống kiểm tra (test case) chuyển trạng thái "pass" sẽ thể hiện tốc độ làm việc, năng suất của bạn.</li>  
</ul>

<h2 class="section-heading">Thiết kế Unit Test</h2>
<p>Mỗi UT đều được tiết kế theo trình tự sau:</p>
<ul style="list-style-type:disc">
  <li>Thiết lập các điều kiện cần thiết: khởi tạo các đối tượng, xác định tài nguyên cần thiết, xây dựng các dữ liệu giả... </li>
  <li>Triệu gọi các phương thức cần kiểm tra. </li>
  <li>Kiểm tra sự hoạt động đúng đắn của các phương thức.</li>  
  <li>Dọn dẹp tài nguyên sau khi kết thúc kiểm tra.</li>
</ul>

<h2 class="section-heading">Chiến lược viết Unit Test hiệu quảt</h2>
<ul style="list-style-type:disc">
  <li>Mọi UT phải bắt đầu với trạng thái "fail" và chuyển trạng thái "pass" sau một số thay đổi hợp lý đối với mã chính. </li>
  <li>Mỗi khi viết một đoạn mã quan trọng, hãy viết các UT tương ứng cho đến khi bạn không thể nghĩ thêm tình huống nào nữa. </li>
  <li>Nhập một số lượng đủ lớn các giá trị đầu vào để phát hiện điểm yếu của mã theo nguyên tắc: Nếu nhập giá trị đầu vào hợp lệ thì kết quả trả về cũng phải hợp lệ và ngược lại.</li>  
  <li>Sớm nhận biết các đoạn mã không ổn định và có nguy cơ gây lỗi cao, viết UT tương ứng để khống chế.</li>
  <li>Ứng với mỗi đối tượng nghiệp vụ (business object) hoặc đối tượng truy cập dữ liệu (data access object), nên tạo ra một lớp kiểm tra riêng vì những lỗi nghiêm trọng có thể phát sinh từ các đối tượng này.</li>
  <li>Để ngăn chặn các lỗi có thể phát sinh trở lại thực thi tự động tất cả UT mỗi khi có một sự thay đổi quan trọng, hãy làm công việc này mỗi ngày. Các UT lỗi cho chúng ta biết thay đổi nào là nguyên nhân gây lỗi.</li>
  <li>Để tăng hiệu quả và giảm rủi ro khi viết các UT, cần sử dụng nhiều phương thức kiểm tra khác nhau. Hãy viết càng đơn giản càng tốt.</li>
  <li>Cuối cùng, viết UT cũng đòi hỏi sự nỗ lực, kinh nghiệm và sự sáng tạo như viết PM. </li>
</ul>

<h2 class="section-heading">Unit Test vs Unity</h2>

<p>Mấy cái trên mình copy paste đó, đọc cho zui thôi :v chủ yếu là phần dưới này nè. </p>
<p>Thôi không nói dài dòng nữa, làm 1 cái ví dụ luôn là hiểu ngay ý mà. Okie! Lấy một ví dụ đơn giản về 1 con tàu vũ trụ với các thuộc tính và hành vi đơn giản sau:</p>
<p>Thuộc tính:</p>
<p>     -	Máu <br>
        -	Số đạn còn trong súng
</p>
<p>Hành vi:</p>
<p>     -	Di chuyển (trái, phải, lên, xuống) và khi phi thuyền còn ít máu thì bay chậm hơn so với lúc đầy máu <br>
        -	Bắn <br>
        -   Nạp đạn
</p>

<p>Script sẽ trông như thế này:</p>

<img src="{{ site.baseurl }}/img/post/unit_test_unity_1/image001.png"/>

<p>Đề viết các unit test, ta cần giải quyết 2 vấn đề sau:</p>
<ul style="list-style-type:disc">
  <li>MonoBehaviour là một lớp đặc biệt được xử lý bởi Unity theo một cách đặc biết (wtf?). Ta không thể tạo mới với những class này ( ví dụ: var ship = new SpaceshipMotor() !!!).</li>
  <li>Các đoạn code logic đều nằm trong Update() -> phụ thuộc vào thời gian -> không thể test được.</li>  
</ul>

<p>Vì vậy, đầu tiên ta cần phải refactor lại code sao cho các phương thức là tối giản và tách các phuong thức sử dụng Unity API riêng biệt. Sau khi làm xong, script của ta sẽ trông như thế này:</p>

<img src="{{ site.baseurl }}/img/post/unit_test_unity_1/image002.png"/>

<p>Bây giờ, ta đã có các phương thức riêng rẽ và phù hợp để test nếu có một đối tượng ảo SpaceshipMotor, nhưng điều đó là không thể vì class này vẫn đang kế thừa từ MonoBehaviour. </p>
<p>Vậy thì ta cần làm gì? Trước tiên, ta sẽ tách rời tất cả những đoạn code không liên quan tới Unity API ra thành một class riêng, rồi sau đó liên kết lại với class SpaceshipMotor. Nhìn lại ta sẽ thấy, trong class SpaceshipMotor chỉ có 2 phương thức TransformPosition() và InstanciateBullet() là có dung Unity API, những phần còn lại có thể tách ra được.</p>
<p>Vấn đề còn lại là làm sao để các logic bên lớp mới được tách ra đó có thể giao tiếp với phần còn lại. Câu trả lời đơn giản nhất là sử dụng interface như dưới đây:</p>

<img src="{{ site.baseurl }}/img/post/unit_test_unity_1/image003.png"/>

<img src="{{ site.baseurl }}/img/post/unit_test_unity_1/image004.png"/>

<p>Cùng bắt đầu với class SpaceshipMotor. Class này được cài đặt thêm các interface là ImovementController và IgunController (nghe tên là biết nó làm gì rồi hé). Trong class này có một field mới kiểu SpaceshipController (lớp chứa tất cả các logic được tách ra). Class SpaceshipController không biết gì về SpaceshipMotor, và việc duy nhất nó làm là gọi các phương thức thông qua interface.</p>
<p>UML diagram hiện tại sẽ trông như thế này:</p>

<img src="{{ site.baseurl }}/img/post/unit_test_unity_1/image005.png"/>

<p>Okay! Việc chuẩn bị để viết unit test đã xong (oh wtf? Nãy giờ mới là chuẩn bị thôi á? :v Đúng rồi đó)</p>

<h2 class="section-heading">Unit Test</h2>

<p>Đầu tiên, ta cần cài thêm <a href="https://www.assetstore.unity3d.com/en/#!/content/13802">Unity Test Tools</a> </p>

<p>Tạo 1 folder mới đặt tên là Tests để chứa những script test.</p>
<p>Sau đó, click phải vào folder đó, chọn Create/Editor Test C# Script, đặt tên SpaceshipControllerTests cho script mới tạo.</p>
<p>Trong class mới tạo có sẵn một phương thức test mẫu, trông như thể này:</p>

<img src="{{ site.baseurl }}/img/post/unit_test_unity_1/image006.png"/>

<p>Nhìn qua ta có thể dễ dàng nhận ra cấu trúc chung của một phương thức test có dạng:</p>

<pre>
[Test]
    public void Tên phương thức()
    {
        //Khai báo và khởi tạo

        //Các hành động

        //Thực hiện so sánh, xác nhận
    }
</pre>

<p>Unity mặc định sử dụng thư viện NUnit, tham khảo thêm về thư viện này tại <a href="http://www.nunit.org/">ĐÂY</a></p>
<p>Ngoài ra ta còn sử dụng thư viện NSubstitute, thao khảo thêm tại  <a href="http://nsubstitute.github.io/help.html ">ĐÂY</a></p>

<p>Okie! Sau khi đã nghiên cứu thì ta thử viết 1 đoạn test xem nào!</p>
<p>Ví dụ 1 cái thôi nhé. Giã sử ta cần test xem lúc hết đạn có bắn được không, ta viết như sau:</p>

<img src="{{ site.baseurl }}/img/post/unit_test_unity_1/image007.png"/>

<p>Cú pháp: Substitute.For<Tên class or Interface>() trong thư viện NSubstutite sẽ tạo ra và trả về một đối tượng ảo (Mock object) với các hành vi và thuộc tính như một đối tượng thật.</p>
<p>Để ý phương thức Test của chúng ta. Đầu tiên, sau khi khởi tạo các đối tượng ảo, ta xét giá trị bulletLeft của đối tượng motor về 0 (nghĩa là lấy hết đạn ra). Sau đó gọi hàm bắn ApplyFire() của đối tượng đó. Trong phần kiểm tra, xác nhận, nếu như gunController không nhận được bất kỳ lệnh bắn (Fire()) nào thì có nghĩa là test của chúng ta đã pass (rõ ràng rồi, vì ta đã lấy hết đạn ra rồi mà bắn sao được nữa :v ).</p>

<p>Tương tự, chúng ta có thể viết thêm nhiều test khác nữa như: test xem sau khi hết đạn rồi reload có bắn tiếp được không? Hay test xem tốc độ của phi thuyền có bị giảm khi còn ít máu không? …</p>

<p>Sau khi đã viết các unit test rồi, việc còn lại là chạy thử các test đó xem có đúng không :D </p>

<p>Chúng ta chỉ cần mở cửa sổ Editor test bằng cách chọn Window->Editor test runner</p>

<p>Cửa sổ Editor test hiện lên và chứa tất cả các phương thức test chúng ta đã viết:</p>

<img src="{{ site.baseurl }}/img/post/unit_test_unity_1/image008.png"/>

<p>Để chạy thử, ta nhấn vào Run All là xong :v quá dễ đúng không.</p>

<img src="{{ site.baseurl }}/img/post/unit_test_unity_1/image009.png"/>

<p>Màu xanh là Passed, đỏ là Failed. Như trên thì dễ thấy hàm reload có vấn đề :v fix that bugs now!</p>

<br>

<p>Download project tại <a href="https://github.com/trongthien18/unit-test-in-unity3d">ĐÂY</a></p>

<p>Tài liệu tham khảo:</p>
<p><a href="http://blogs.unity3d.com/2014/05/21/unit-testing-part-1-unit-tests-by-the-book/">Unit test by the book</a></p>
<p><a href="http://blogs.unity3d.com/2014/06/03/unit-testing-part-2-unit-testing-monobehaviours/">Unit testing MonoBehaviours</a></p>
<p><a href="http://www.pcworld.com.vn/articles/cong-nghe/cong-nghe/2005/12/1188434/unit-test-voi-phat-trien-phan-mem-hien-dai/">Unit Test với phát triển phần mềm hiện đại</a></p>
