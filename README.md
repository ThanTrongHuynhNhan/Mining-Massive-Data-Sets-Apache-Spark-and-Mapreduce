# Mining-Massive-Data-Sets
Exercises on the field of Mining massive datasets

## Phần 1: Tìm hiểu về Spark và Mapreduce
### A. Apache Spark
#### *I. Đôi nét về Apache Spark*
<p align="justify"> &nbsp;&nbsp;&nbsp;&nbsp; Matei Zaharia, cha đẻ của Spark, sử dụng Hadoop từ những ngày đầu. Đến năm 2009 ông viết Apache Spark để giải quyết những bài toán học máy ở đại học UC Berkely vì Hadoop MapReduce hoạt động không hiệu quả cho những bài toán này. Rất sớm sau đó ông nhận ra rằng Spark không chỉ hữu ích cho học máy mà còn cho cả việc xử lý luồng dữ liệu hoàn chỉnh.

<p align="justify"> &nbsp;&nbsp;&nbsp;&nbsp; Apache Spark là một source cluster computing framework thực thi dữ liệu dựa trên Hadoop HDFS (nhưng không thay thế cho Hadoop) được phát triển sơ khởi vào năm 2009 bởi AMPLab tại đại học California. Sau này, Spark đã được trao cho Apache Software Foundation vào năm 2013 và được phát triển cho đến nay. Nó cho phép xây dựng các mô hình dự đoán nhanh chóng với việc tính toán được thực hiện trên một nhóm các máy tính, có có thể tính toán cùng lúc trên toàn bộ tập dữ liệu mà không cần phải trích xuất mẫu tính toán thử nghiệm. Tốc độ xử lý của Spark có được do việc tính toán được thực hiện cùng lúc trên nhiều máy khác nhau. Đồng thời việc tính toán được thực hiện ở bộ nhớ trong (in-memories) hay thực hiện hoàn toàn trên RAM. </p>

<p align="justify"> &nbsp;&nbsp;&nbsp;&nbsp; Spark cho phép xử lý dữ liệu theo thời gian thực, vừa nhận dữ liệu từ các nguồn khác nhau đồng thời thực hiện ngay việc xử lý trên dữ liệu vừa nhận được ( Spark Streaming). Spark không có hệ thống file của riêng mình, nó sử dụng hệ thống file khác như: HDFS, Cassandra, S3,…. Spark hỗ trợ nhiều kiểu định dạng file khác nhau (text, csv, json…) đồng thời nó hoàn toàn không phụ thuộc vào bất cứ một hệ thống file nào. </p>

<p align="center"> <img src ="https://user-images.githubusercontent.com/77878466/105625926-3d670d80-5e5f-11eb-97ef-798c88879d0e.png"/>
<p align="center"> <em>Quá trình hình thành và phát triển</em> </p>

#### *II. Cấu tạo của Spark*
<p align="justify"> &nbsp;&nbsp;&nbsp;&nbsp; Nhìn chung thì cấu tạo của Apache Spark gồm có 5 thành phần chính: Spark Core, Spark Streaming, Spark SQL, MLlib và GraphX, với thành phần trung tâm của Spark là Spark Core. Spark có thể chạy trên nhiều loại Cluster Managers như Hadoop YARN, Apache Mesos hoặc trên chính cluster manager được cung cấp bởi Spark được gọi là Standalone</p>

<p align="center"> <img src ="https://user-images.githubusercontent.com/77878466/105628034-fe3fb900-5e6c-11eb-91d4-637f6b2b5845.png" width="50%"/>
<p align="center"> <em>Thành phần của Spark</em> </p>

<ul align="justify">
  <li><b>Spark Core:</b> Là nền tảng cho các thành phần còn lại và các thành phần này muốn khởi chạy được thì đều phải thông qua Spark Core do Spark Core đảm nhận vai trò thực hiện công việc tính toán và xử lý trong bộ nhớ (In-memory computing) đồng thời nó cũng tham chiếu các dữ liệu được lưu trữ tại các hệ thống lưu trữ bên ngoài. Spark Core cung cấp những chức năng cơ bản nhất của Spark như lập lịch cho các tác vụ, quản lý bộ nhớ, fault recovery, tương tác với các hệ thống lưu trữ…Đặc biệt, Spark Core cung cấp API để định nghĩa RDD (Resilient Distributed DataSet) là tập hợp của các item được phân tán trên các node của cluster và có thể được xử lý song song.</li></br>

  <li><b>Spark SQL:</b> cho phép truy vấn dữ liệu cấu trúc qua các câu lệnh SQL. Spark SQL có thể thao tác với nhiều nguồn dữ liệu như Hive tables, Parquet, và JSON. Bên cạnh đó, Spark SQL cung cấp một kiểu data abstraction mới (SchemaRDD) nhằm hỗ trợ cho cả kiểu dữ liệu có cấu trúc (structured data) và dữ liệu nửa cấu trúc (semi-structured data). Spark SQL còn hỗ trợ DSL (Domain-specific language) để thực hiện các thao tác trên DataFrames bằng ngôn ngữ Scala, Java hoặc Python và nó cũng hỗ trợ cả ngôn ngữ SQL với giao diện command-line và ODBC/JDBC server.</li></br>
  
  <li><b>Spark Streaming:</b> được sử dụng để thực hiện việc phân tích stream bằng việc coi stream là các mini-batches và thực hiệc kỹ thuật RDD transformation đối với các dữ liệu mini-batches này. Qua đó cho phép các đoạn code được viết cho xử lý batch có thể được tận dụng lại vào trong việc xử lý stream, làm cho việc phát triển lambda architecture được dễ dàng hơn. Tuy nhiên điều này lại tạo ra độ trễ trong xử lý dữ liệu (độ trễ chính bằng mini-batch duration) và do đó nhiều chuyên gia cho rằng Spark Streaming không thực sự là công cụ xử lý streaming giống như Storm hoặc Flink.</li></br>
  
  <li><b>MLlib (Machine Learning Library):</b> Cung cấp rất nhiều thuật toán của học máy như: classification, regression, clustering, collaborative filtering...là một nền tảng học máy phân tán bên trên Spark do kiến trúc phân tán dựa trên bộ nhớ</li></br>
  
  <li><b>GraphX:</b> là nền tảng xử lý đồ thị dựa trên Spark. Nó cung cấp các Api để diễn tảcác tính toán trong đồ thị bằng cách sử dụng Pregel Api.</li></br>
</ul>

#### *III. Lợi ích nổi bật mà Spark mang lại*
<ul align="justify">
  <li><em>Xử lý dữ liệu</em>: Spark xử lý dữ liệu theo lô và thời gian thực</li>
  <li><em>Tính tương thích</em>: Có thể tích hợp với tất cả các nguồn dữ liệu và định dạng tệp được hỗ trợ bởi cụm Hadoop.</li>
  <li><em>Hỗ trợ ngôn ngữ</em>: hỗ trợ Java, Scala, Python và R.</li></br><li style="list-style-type: none">
      <p align="center"> <img src ="https://user-images.githubusercontent.com/77878466/105629301-c89ece00-5e74-11eb-853c-79337c833eda.png"/>
      <p align="center"> <em>Cơ cấu các ngôn ngữ Spark hỗ trợ (2014-2015)</em> </p></li>
    
  <li><em>Phân tích thời gian thực</em>: Apache Spark có thể xử lý dữ liệu thời gian thực tức là dữ liệu đến từ các luồng sự kiện thời gian thực với tốc độ hàng triệu sự kiện mỗi giây. Bên cạnh đó, Spark còn được sử dụng để xử lý phát hiện gian lận trong khi thực hiện các giao dịch ngân hàng. Đó là bởi vì, tất cả các khoản thanh toán trực tuyến được thực hiện trong thời gian thực và chúng ta cần ngừng giao dịch gian lận trong khi quá trình thanh toán đang diễn ra.</li>
  <li><em>Quản lý bộ nhớ</em>: Spark giải quyết các vấn đề vấn đề xung quanh định nghĩa Resilient Distributed Datasets (RDDs). RDDs hỗ trợ hai kiểu thao tác thao tác: transformations và action. Thao tác chuyển đổi(tranformation) tạo ra dataset từ dữ liệu có sẵn. Thao tác actions trả về giá trị cho chương trình điều khiển (driver program) sau khi thực hiện tính toán trên dataset.</li> 
</ul>

### B. MapReduce
#### *I. Đôi nét về MapReduce*
<p align="center"> <img src ="https://user-images.githubusercontent.com/77878466/105629891-4c0dee80-5e78-11eb-9892-6a9cfe16b770.png"/>
<p align="center"> <em>Mô hình MapReduce</em> </p>

<p align="justify"> &nbsp;&nbsp;&nbsp;&nbsp; MapReduce là mô hình được thiết kế độc quyền bởi Google, nó có khả năng lập trình xử lý các tập dữ liệu lớn song song và phân tán thuật toán trên 1 cụm máy tính. MapReduce trở thành một trong những thành ngữ tổng quát hóa trong thời gian gần đây. MapReduce sẽ bao gồm 2 thủ tục là một thủ tục Map() và 1 thủ tục Reduce(). Thủ tục Map() bao gồm lọc (filter) và phân loại (sort) trên dữ liệu khi thủ tục khi thủ tục Reduce() thực hiện quá trình tổng hợp dữ liệu. Đây là mô hình dựa vào các khái niệm biển đối của bản đồ và reduce những chức năng lập trình theo hướng chức năng. Thư viện của thủ tục Map() và Reduce() sẽ được viết bằng nhiều loại ngôn ngữ khác nhau. Thủ tục được cài đặt miễn phí và được sử dụng phổ biến nhất là là Apache Hadoop.</p>

#### *II. Mô hình MapReduce*
<p align="center"> <img src ="https://user-images.githubusercontent.com/77878466/105629766-86c35700-5e77-11eb-98e4-e1e47a5d0d2b.png"/>
<p align="center"> <em>Mô hình các hàm chính của MapReduce</em> </p>

<p align="justify"> &nbsp;&nbsp;&nbsp;&nbsp; MapReduce có 2 hàm chính là Map() và Reduce(), đây là 2 hàm đã được định nghĩa bởi người dùng và nó cũng chính là 2 giai đoạn liên tiếp trong quá trình xử lý dữ liệu của MapReduce.</p>

<ul align="justify">
  <li><b>Hàm Map():</b>  có nhiệm vụ nhận Input cho các cặp giá trị/khóa và output chính là tập những cặp giá trị/khóa trung gian. Sau đó, chỉ cần ghi xuống đĩa cứng và tiến hành thông báo cho các hàm Reduce() để trực tiếp nhận dữ liệu. </li></br>
  
  <li><b>Hàm Reduce():</b> có nhiệm vụ tiếp nhận từ khóa trung gian và những giá trị tương ứng với lượng từ khóa đó. Sau đó, tiến hành ghép chúng lại để có thể tạo thành một tập khóa khác nhau. Các cặp khóa/giá trị này thường sẽ thông qua một con trỏ vị trí để đưa vào các hàm reduce. Quá trình này sẽ giúp cho lập trình viên quản lý dễ dàng hơn một lượng danh sách cũng như  phân bổ giá trị sao cho  phù hợp nhất với bộ nhớ hệ thống. </li></br>
  
  <li><b>Shuffle:</b> là bước  trung gian ở giữa Map và Reduce. Sau khi Map hoàn thành  xong công việc của mình thì Shuffle sẽ làm nhiệm vụ chính là thu thập cũng như tổng hợp từ khóa/giá trị trung gian đã được map sinh ra trước đó rồi chuyển qua cho Reduce tiếp tục xử lý.</li></br>
</ul>
