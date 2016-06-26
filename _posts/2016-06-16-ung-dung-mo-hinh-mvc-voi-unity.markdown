---
layout:     post
title:      "Áp dụng mô hình MVC trong lập trình game với Unity 3D"
subtitle:   "Design Pattern"
date:       2016-06-16 01:40:00
author:     "Thiên Lê"
header-img: "img/post-bg-06.jpg"
---

<p>Một ngày cuối tuần buồn nhạt nhẽo, gấu thì đi làm, chơi game thì cứ thắng miết (cũng tại mình bá quá :v ), đành nằm vắt chân lên trán  suy nghĩ xem giờ làm gì cho nó bớt chán. Nghĩ mãi chả có trò gì chơi, đành mở project lên code vài dòng cho zui. Mình làm với Unity cũng được một thời gian rồi, cũng được vài project, kinh nghiệm không nhiều nhưng cũng không còn non và xanh như hồi mới vọc. Thế mà mỗi lần mở project lên để thêm thắt vài feature mới hay tìm mấy con bug cũng đều cảm thấy có gì đó rối rối mặc dù tổ chức source code cũng khá ổn. Có một câu nói rất hay như thê này: “The bigger the project, the bigger the spaghetti”.</p>

<img src="{{ site.baseurl }}/img/post/mvc_unity_1/image001.jpg"/>

<p>Unity với kiến trúc Component của nó thực sự rất mạnh mẽ, dễ học, dễ làm với mọi đối tượng. Thế nhưng một vấn đề chung mà hầu hết chúng ta đều gặp đó là phải tổ chức như thế nào để project dù có mở rộng tới mức nào vẫn rõ ràng, dễ nhìn, dễ bảo trì, sửa lỗi và dễ dàng nâng cấp. Chính vì vậy, mình đang tìm kiếm một giải pháp thực sự tốt cho vấn đề này, và giải pháp đầu tiên mà mình muốn thử nghiệm đó là áp dụng mô hình MVC vào Unity.</p>

<p>Đầu tiên thì mình sẽ tìm hiểu một tí về kiến trúc nền tảng của Unity, Entity-Component pattern, sau đó sẽ tìm hiểu về MVC và làm cách nào để ứng dụng MVC trên Unity.
<br>Okie! Cùng nghiên cứu nào.
</p>

<h2 class="section-heading">Mẫu thiết kế Entity-Component</h2>

<p>Entity-Component (EC) là một mẫu thiết kế mà ở đó ứng dụng sẽ bao gồm một hệ thống các Entity (thực thể :v dịch thấy chuối chuối sao í). Các thực thể là những đối tượng rỗng, không chứa bất kì dữ liệu nào riêng biệt và không có bất kỳ sự khác nào giữa chúng. Một thực thể có thể gắn lên nhiều Component (thành phần, có thể là tính năng hay dữ liệu …) khác nhau để thực hiện các mục đích riêng. Mỗi thực thể sẽ mang những thuộc tính và hành vi của component được thêm vào, khi đó các thực thể mới thực sự khác nhau.Trong Unity, các thực thể này gọi là GameObject. </p>

<p> Mỗi component thường có 2 thành phần là:</p>
<p>     -	Thuộc tính: dữ liệu riêng của component <br>
        -	Hành vi: các hàm xử lý
</p>

<p>Mỗi component trong một thực thể sẽ hoàn toàn độc lập với nhau và được thực thi trên những hệ thống riêng biệt, chính vì thế, tốc độ thực thi của kiến trúc EC rất nhanh.</p>

<img src="{{ site.baseurl }}/img/post/mvc_unity_1/image002.png"/>

<p>Một ví dụ khác về hệ thống sử dụng mẫu EC:</p>

<img src="{{ site.baseurl }}/img/post/mvc_unity_1/image003.png"/>

<p>EC là một mẫu thiết kế tốt để giảm bớt các vấn đề về kế thừa và đa kế thừa. Vì thế mẫu này rất thích hợp để làm kiến trúc nền tảng trong các game engine.</p>

<p><b>Ưu điểm</b><p>
<ul style="list-style-type:disc">
  <li>Tái sử dụng code tốt, giảm độ phức tạp của dự án. Một component có thể được sử dụng cho nhiều thực thể khác nhau có chung một số đặc điểm về component đó.</li>
  <li>Tốc độ xử lý cực nhanh vì mỗi component sẽ chạy trên một hệ thống riêng biệt nhau và không phải trả chi phí cho các hàm thừa kế trừu tượng như trong cấu trúc cây thừa kế.</li>
  <li>Dễ vận hành và bảo trì game: mỗi component gần như hoàn toàn độc lập với nhau nên rất dễ thích nghi với những thay đổi trong game, ít ảnh hưởng tới các component còn lại.</li>
  <li>Dễ dàng cho các dự án có nhiều người cùng tham gia khi mỗi người có thể quản lý mỗi component riêng biệt.</li>
</ul>
<p><b>Nhược điểm</b><p>
<ul style="list-style-type:disc">
  <li>Không thích hợp với các dự án nhỏ.</li>
  <li>Thời gian phát triển ban đầu lớn.</li>  
</ul>

<p>Rõ ràng có thể thấy, EC là một mẫu thiết kế tốt hơn so với kiểu hướng đối tượng truyền thống. Nó giúp chống phân mảnh và tổ chức kiến trúc source code tốt hơn. Dù vậy, với những dự án lớn, sẽ hơi khó khăn trong việc tìm đúng thực thể hay component cần tìm khi mà có hàng tỷ cách để lắp ráp các component vào các thực thể để thực hiện một nhiệm vụ nào đó. Vì thế, chúng ta cần một cách nào đó để tổ chức kiến trúc source code tốt hơn nữa.</p>

<h2 class="section-heading">Mẫu thiết kế Model-View-Controller (MVC)</h2>

<p>Mẫu thiết kế MVC chia ứng dụng thành 3 phần bao gồm:</p>
<ul style="list-style-type:disc">
  <li>Model: chứa thông tin, dữ liệu</li>
  <li>View: giao diện, UI, …</li>
  <li>Controller: điều hướng quyết định, hành động</li>
</ul>

<figure>
  <img src="{{ site.baseurl }}/img/post/mvc_unity_1/image004.png"/>
  <figcaption><i>Hình ảnh chỉ mang tính minh họa thôi, đừng xem :v</i></figcaption>
</figure>

<p>MVC đủ linh hoạt để hiện thực trên các hệ thống Entity-Component hay Hướng đối tượng thông thường.</p>
<p>Game và UI thường có quy trình làm việc kiểu đợi phản hổi từ người chơi, hoặc là đợi một điều kiện xảy ra, sau đó gửi thông báo các sự kiện đó đến nơi thích hợp để quyết định xử lý như thế nào và đáp lại, cuối cùng là cập nhật lại các dữ liệu phù hợp. Những hành động đó cho thấy rõ khả năng tương thích với MVC.</p>

<h2 class="section-heading">Áp dụng mô hình MVC vào Unity</h2>

<p>Sau một lúc lang thang trên mạng thì mình tìm được cái hình này.</p>

<figure>
  <img src="{{ site.baseurl }}/img/post/mvc_unity_1/image005.jpg"/>
  <figcaption><i>Mô hình AMVCC (Application-Model-View-Controller-Component)</i></figcaption>
</figure>

<p>Thôi nói nhiều mệt quá, thử làm đại một cái ví dụ hay ho xem thử nào :3</p>

<p><br>...Một ngày sau...</p>

<p>Haizz, nghĩ mãi mới ra một ý tưởng để làm ví dụ. Mình sẽ làm một cái game nhảm nhảm kiểu như trên màn hình có 1 cái bong bóng hiện ngẫu nhiên, nhiệm vụ của người chơi là chọc vào cho nó nổ để ghi điểm, được 10 điểm là win :( </p>

<p>B1: Đầu tiên là tạo các GameObject theo cấu trúc như thế này<p>

<img src="{{ site.baseurl }}/img/post/mvc_unity_1/image006.png"/>

<p>B2: Lên mạng kiếm đại 1 cái hình bong bóng nào đó.<p>

<img src="{{ site.baseurl }}/img/post/mvc_unity_1/image007.png"/>

<p>B3: Tạo các thư mục theo cấu trúc như thế này:<p>

<img src="{{ site.baseurl }}/img/post/mvc_unity_1/image008.png"/>

<p>Rồi, bắt đầu code thôi =))</p>

<p>Tạo script trong thư mục Core và đặt tên là Element</p>

<pre>
//Base class for all elements
public class Element : MonoBehaviour
{
    AppManager app;
	
	void Start ()
    {
        app = GameObject.FindObjectOfType&lt;AppManager&gt;();
	}

    public AppManager App
    {
        get
        {
            return app;
        }
    }
}
</pre>

<p>Đây là lớp cơ sở cho tất cả các phần tử trong game. Cái này sau khi làm xong thì mình lại thấy không cần thiết, thay vào đó có thể sử dụng Singleton cho class AppManager thì hay hơn :3</p>
<p>Tiếp theo là lớp AppManager cũng trong thư mục Core luôn.</p>

<pre>
public class AppManager : MonoBehaviour
{
    //Reference to the root instances of MVC
    public Model model;
    public View view;
    public Controller controller;

	// Use this for initialization
	void Start ()
    {
        
    }
}
</pre>

<p>Tiếp theo là các class Model, View và Controller</p>

<pre>
//Model.cs
//Contain all data related to the app
public class Model : Element
{
    public BubbleModel bubbleModel;
    public int score;
    public int winCondition;
    public bool isGameEnd;
}
</pre>
<pre>
//BubbleModel.cs
[Serializable]
public class BubbleModel
{
    public float timeRespawn;
    public float timer;
}
</pre>
<pre>
//View.cs
public class View : Element
{
    public BubbleView bubbleView;
    public ScoreView scoreView;
}
</pre>
<pre>
//ScoreView.cs
public class ScoreView : Element
{
    public Text txtScore;
}
</pre>
<pre>
//BubbleView.cs
public class BubbleView : Element
{
    public void OnMouseDown()
    {
        App.controller.OnBubbleHit();
    }

    float timer;
    public void Update()
    {
        if (App.model.isGameEnd)
            return;

        timer += Time.deltaTime;
        if (timer > App.model.bubbleModel.timeRespawn)
        {
            timer = 0;
            App.controller.OnRandomBubblePosition();
        }
    }
}
</pre>
<pre>
//Controller.cs
public class Controller : Element
{
    public void OnBubbleHit()
    {
        App.model.score++;
        App.view.scoreView.txtScore.text = App.model.score.ToString();
        Debug.Log("Score: " + App.model.score);

        if (App.model.score >= App.model.winCondition)
        {
            App.view.bubbleView.GetComponent&lt;Collider2D&gt;().enabled = false;
            OnGameVictory();
            Application.Quit();
        }
        else
        {
            OnRandomBubblePosition();
        }
    }

    public void OnRandomBubblePosition()
    {
        Vector3 randPosition = Camera.main.ScreenToWorldPoint(new Vector3(Random.Range(0, Screen.width), Random.Range(0, Screen.height), 0));
        randPosition.z = 0;
        App.view.bubbleView.transform.position = randPosition;
    }

    public void OnGameVictory()
    {
        Debug.Log("Victory!");
        App.view.scoreView.txtScore.text = "Victory!";
        App.model.isGameEnd = true;
    }
}
</pre>

<p>Các Class nhớ để trong đúng thư mục cho đẹp nhé :D </p>

<p>Tiếp theo chúng ta sẽ kéo các scripts đó vào các object đã tạo lúc đầu. Hierarchy sẽ trông như thế này:</p>

<pre>
-Application [AppManager]
	-Model [Model]
	-Controller [Controller]
	-View [View]
		-Bubble [BubbleView]
		-Score [ScoreView]
</pre>

<p>Trong Model chúng ta set các thông số:</p>

<img src="{{ site.baseurl }}/img/post/mvc_unity_1/image009.png"/>

<p>Okay, như vậy là xong cái game rồi :v </p>

<p>Tuy nhiên, có gì đó không ổn lắm trong ví dụ này. Khi click vào quả bóng, trong view ta gọi hàm App.controller.OnBubbleHit(), mặc dù không phải là sai, nhưng nếu cứ làm như vậy với tất cả những thông báo thì lại dở đi. Ta nên xây dựng một hệ thống thông báo để làm việc này.
<br>Đầu tiên là khai báo 1 cái enum 
</p>

<pre>
public enum Notification
{
    BubbleHit,
    Victory,
    GameStart
        //....
}
</pre>

<p>Thêm thắt class AppManager 1 xíu</p>
<pre>
public void Notify(Notification noty, Object target, params object[] data)
{
    Controller[] controller_list = GetAllControllers();
    foreach (Controller c in controller_list)
    {
        c.OnNotification(noty, target, data);
    }
}

// Fetches all scene Controllers.
public Controller[] GetAllControllers()
{        
    // :v 
    return new Controller[] { controller };
}
</pre>

<p>Cái này là ví dụ nên mình chỉ có 1 cái controller thôi, thực tế thì mình có thể có nhiều cái để quản lý rõ ràng hơn.</p>

<p>Trong Controller thêm vào:</p>

<pre>
public void OnNotification(Notification noty, UnityEngine.Object target, object[] data)
{
    switch (noty)
    {
        case Notification.BubbleHit:
            OnBubbleHit();
            break;
        case Notification.Victory:
            OnGameVictory();
            break;
        case Notification.GameStart:
            break;
        default:
            break;
    }
}
</pre>

<p>Cuối cùng là bên BubbleView sửa lại thành:</p>

<pre>
public void OnMouseDown()
{
    App.Notify(Notification.BubbleHit, this);
}
</pre>

<h2 class="section-heading">Một số quy tắc khi làm việc với MVC</h2>

<h3>1. Models</h3>

<ul style="list-style-type:disc">
  <li>Chứa các dữ liệu và trạng thái chính của game.</li>
  <li>Serialize, deserialize và chuyển đổi giữa các dữ liệu.</li>
  <li>Load / Save data.</li>
  <li>Thông báo đến các Controller về các tiến trình.</li>
  <li>Lưu trạng thái game.</li>
  <li>Tuyệt đối không truy xuất trực tiếp tới các Views.</li>
</ul>

<h3>2. Views</h3>

<ul style="list-style-type:disc">
  <li>Có thể lấy dữ liệu từ Model. Ví dụ, trong hàm Player.Run() của PlayerView có thể truy xuất thông tin speed trong Model.</li>
  <li>Không thay đổi Model.</li>
  <li>Chỉ thực hiện các chức năng chính của object view đó phụ trách mà thôi. Ví dụ, PlayerView thì không nên xử lý Input hay chỉnh sửa GameState.</li>
  <li>Mỗi View nên là một hộp đen và chỉ giao tiếp thông qua interface với notification thôi.</li>
  <li>Không chứa các dữ liệu chính ( như speed, health, lives … , những cái phụ nhỏ xíu thì ok).</li>  
</ul>

<h3>3. Controllers</h3>

<ul style="list-style-type:disc">
  <li>Không lưu các dữ liệu chính.</li>
  <li>Có thể lọc thông báo từ các View không liên quan.</li>
  <li>Cập nhật và sử dụng dữ liệu của Model.</li>
  <li>Quản lý các màn hình Unity.</li>  
</ul>

<h2 class="section-heading">Kết luận</h2>

<p>Cảm nhận đầu tiên sau khi tìm hiểu cái này là “Umm cũng hay ho phết đấy, tìm hiểu kỹ thêm xem sao”.<br>
Mình chỉ mới làm demo nhỏ thôi nên chưa biết hay dở thế nào nên không dám chém bừa :v Mình sẽ áp dụng trong dự án sắp tới và lúc đó mình sẽ nói lại sau, hehe.<br>
Tuần sau mình sẽ thử tìm một vài framework sử dụng MVC để nghiên cứu, nếu không có thì mình sẽ tự viết lại, ahihi :v
</p>

<p><br>Tài liệu tham khảo: <a href="https://www.toptal.com/unity-unity3d/unity-with-mvc-how-to-level-up-your-game-development">Unity with MVC: How to Level Up Your Game Development</a></p>
