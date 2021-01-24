# Mining-Massive-Data-Sets
Exercises on the field of Mining massive datasets

## Phần 1: Tìm hiểu về Spark và Mapreduce
### A. Apache Spark
#### *I. Đôi nét về Apache Spark*
<p align="justify"> &nbsp;&nbsp;&nbsp;&nbsp; Matei Zaharia, cha đẻ của Spark, sử dụng Hadoop từ những ngày đầu. Đến năm 2009 ông viết Apache Spark để giải quyết những bài toán học máy ở đại học UC Berkely vì Hadoop MapReduce hoạt động không hiệu quả cho những bài toán này. Rất sớm sau đó ông nhận ra rằng Spark không chỉ hữu ích cho học máy mà còn cho cả việc xử lý luồng dữ liệu hoàn chỉnh.

<p align="justify"> &nbsp;&nbsp;&nbsp;&nbsp; Apache Spark là một source cluster computing framework được phát triển sơ khởi vào năm 2009 bởi AMPLab tại đại học California. Sau này, Spark đã được trao cho Apache Software Foundation vào năm 2013 và được phát triển cho đến nay. Nó cho phép xây dựng các mô hình dự đoán nhanh chóng với việc tính toán được thực hiện trên một nhóm các máy tính, có có thể tính toán cùng lúc trên toàn bộ tập dữ liệu mà không cần phải trích xuất mẫu tính toán thử nghiệm. Tốc độ xử lý của Spark có được do việc tính toán được thực hiện cùng lúc trên nhiều máy khác nhau. Đồng thời việc tính toán được thực hiện ở bộ nhớ trong (in-memories) hay thực hiện hoàn toàn trên RAM. </p>

<p align="justify"> &nbsp;&nbsp;&nbsp;&nbsp; Spark cho phép xử lý dữ liệu theo thời gian thực, vừa nhận dữ liệu từ các nguồn khác nhau đồng thời thực hiện ngay việc xử lý trên dữ liệu vừa nhận được ( Spark Streaming). Spark không có hệ thống file của riêng mình, nó sử dụng hệ thống file khác như: HDFS, Cassandra, S3,…. Spark hỗ trợ nhiều kiểu định dạng file khác nhau (text, csv, json…) đồng thời nó hoàn toàn không phụ thuộc vào bất cứ một hệ thống file nào. </p>

<p align="center"> <img src ="https://user-images.githubusercontent.com/77878466/105625926-3d670d80-5e5f-11eb-97ef-798c88879d0e.png"/>
<p align="center"> <em>Quá trình hình thành và phát triển</em> </p>

#### *II. Cấu tạo của Spark*
