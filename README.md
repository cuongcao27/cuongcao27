# Tổng quan Prometheus Server
**Tổng quan về kiến trúc**
![Prometheus](https://user-images.githubusercontent.com/120613788/210294533-d604d359-d037-4d23-b812-618a1f9b4ef5.png)

* [x] **Giới thiệu cơ bản về Prometheus**
  * [x] Monitoring là gì? Khác gì với Logging và Tracing

|  Monitoring   |    Logging    | Tracing    |
| :------------:|:-------------:|:----------:|
| Kiểm tra, giám sát liên tục    |  Thu thập và lưu trữ dữ liệu trong một khoảng thời gian     | Theo dõi các quá trình của hệ thống   | 

  * [x] **Prometheus là gì?**
    - Prometheus là hệ thống giám sát mã nguồn mở. 
    - Prometheus thích hợp để giám máy chủ trung tâm, dịch vụ. 
    - Cho độ tin cậy cao và chạy độc lập, không phụ thuộc lưu trữ mạng. 
    - Có thể lấy dữ liệu từ các monitoring systems khác.
    - Hỗ trợ thu thập  multi-dimensional data.
    - Nhanh chóng phát hiện lỗi.
    - Cấu hình đơn giản.
  * [x] **Các khái niệm cơ bản của Prometheus**
    * [x] **Data model: Mô hình dữ liệu**
   
      Prometheus về cơ bản lưu trữ tất cả dữ liệu dưới dạng chuỗi thời gian: các luồng các giá trị được định thời theo cùng một số liệu và cùng một bộ kích thước được dán nhãn. Bên cạnh chuỗi thời gian được lưu trữ, Prometheus có thể tạo ra chuỗi thời gian xuất phát tạm thời là kết quả của các truy vấn. Có 3 kiểu dữ liệu:
        - Metric names and labels
        
          Mỗi chuỗi thời gian được xác định duy nhất bằng tên chỉ số và các cặp khóa-giá trị tùy chọn được gọi là nhãn. Tên chỉ số chỉ định tính năng chung của một hệ thống được đo lường (ví dụ: http_requests_total - tổng số yêu cầu HTTP nhận được). Nó có thể chứa các chữ cái và chữ số ASCII, cũng như dấu gạch dưới và dấu hai chấm. Nó phải phù hợp với regex [a-zA-Z_:][a-zA-Z0-9_:]*.  
          
          Lưu ý: Dấu hai chấm được dành riêng cho các quy tắc ghi do người dùng xác định. Chúng không nên được sử dụng bởi các nhà xuất khẩu hoặc thiết bị đo đạc trực tiếp.
          
          Nhãn kích hoạt mô hình dữ liệu của Prometheus: bất kỳ tổ hợp nhãn nhất định nào cho cùng một tên chỉ số đều xác định một khởi tạo chiều cụ thể của chỉ số đó (ví dụ: tất cả các yêu cầu HTTP đã sử dụng phương thức POST cho trình xử lý \/api\/tracks). Ngôn ngữ truy vấn cho phép lọc và tổng hợp dựa trên các kích thước này. Thay đổi bất kỳ giá trị nhãn nào, bao gồm thêm hoặc xóa nhãn, sẽ tạo ra một chuỗi thời gian mới. 
          
          Tên nhãn có thể chứa các chữ cái ASCII, số, cũng như dấu gạch dưới. Chúng phải khớp với regex [a-zA-Z_][a-zA-Z0-9_]*. Tên nhãn bắt đầu bằng __ được dành riêng để sử dụng nội bộ.  Giá trị nhãn có thể chứa bất kỳ ký tự Unicode nào.  Nhãn có giá trị nhãn trống được coi là tương đương với nhãn không tồn tại.
        - Samples

          Các mẫu tạo thành dữ liệu chuỗi thời gian thực tế. Mỗi mẫu bao gồm:
            - Giá trị float64
            - Dấu thời gian chính xác đến từng mili giây
        - Notation
        
          Với tên chỉ số và một tập hợp các nhãn, chuỗi thời gian thường được xác định bằng ký hiệu sau:
          
          `<metric name>{<label name>=<label value>, ...}`
          
          Ví dụ: một chuỗi thời gian có tên chỉ số api_http_requests_total và phương thức nhãn ='POST' và trình xử lý ='\/messages' có thể được viết như sau:
          
          `api_http_requests_total{method="POST", handler="/messages"}`
    * [x] **Metric types: Các kiểu số liệu**
    Các thư viện Prometheus client cung cấp bốn loại số liệu cốt lõi. Chúng hiện chỉ được phân biệt trong các thư viện client (để cho phép các API phù hợp với việc sử dụng các loại cụ thể) và trong wire protocol. 4 loại số liệu:
      - Counter
      - Gauge
      - Histogram
      - Summary

        **Counter: Bộ đếm**
        
        Bộ đếm là một số liệu tích lũy đại diện cho một bộ đếm tăng đơn điệu duy nhất có giá trị chỉ có thể tăng hoặc được đặt lại về 0 khi khởi động lại. Ví dụ: Có thể sử dụng bộ đếm để biểu thị số lượng yêu cầu được phân phát, nhiệm vụ đã hoàn thành hoặc lỗi. Không sử dụng bộ đếm để hiển thị giá trị có thể giảm. Ví dụ: Không sử dụng bộ đếm cho số lượng quy trình hiện đang chạy; thay vào đó sử dụng một máy đo. Tài liệu sử dụng thư viện client cho bộ đếm:
          - Go
          - Java
          - Python
          - Ruby
          - .Net
        **Gauge: Đồng hồ đo**
        
        Một thước đo là một số liệu đại diện cho một giá trị số duy nhất có thể tùy ý đi lên và xuống. Đồng hồ đo thường được sử dụng cho các giá trị đo như nhiệt độ hoặc sử dụng bộ nhớ hiện tại, nhưng cũng "tính" có thể tăng lên và xuống, giống như số lượng yêu cầu đồng thời. Tài liệu sử dụng thư viện client cho đồng hồ đo:
          - Go
          - Java
          - Python
          - Ruby
          - .Net

        **Histogram: Biểu đồ**
        
        Biểu đồ tần suất lấy mẫu các quan sát (thường là những thứ như thời lượng yêu cầu hoặc kích thước phản hồi) và đếm chúng trong các vùng lưu trữ có thể định cấu hình. Nó cũng cung cấp một tổng của tất cả các giá trị quan sát được.  
        
        Biểu đồ tần suất với tên số liệu cơ sở là `<basename>` hiển thị nhiều chuỗi thời gian trong một lần scrape: 
        - bộ đếm tích lũy cho các thùng quan sát, được hiển thị dưới dạng `<basename>_bucket{le='<giới hạn bao gồm trên>'}` 
        - tổng của tất cả các giá trị quan sát được, được hiển thị dưới dạng `<basename>_sum` 
        - đếm các sự kiện đã được quan sát, được hiển thị dưới dạng `<basename>_count` (giống hệt với `<basename> _bucket{le='+Inf'}` ở trên) 
        
        Sử dụng hàm `histogram_quantile()` để tính toán các lượng tử từ biểu đồ hoặc thậm chí tổng hợp các biểu đồ. Biểu đồ tần suất cũng phù hợp để tính Apdex score. Tài liệu sử dụng thư viện client cho biểu đồ:
          - Go
          - Java
          - Python
          - Ruby
          - .Net
          
          **Summary: Tóm tắt**
        
          Tương tự như biểu đồ, một bản tóm tắt lấy mẫu quan sát (thường là những thứ như thời lượng yêu cầu và kích thước phản hồi). Mặc dù nó cũng cung cấp tổng số quan sát và tổng của tất cả các giá trị quan sát được, nhưng nó tính toán các lượng tử có thể định cấu hình trong một khoảng thời gian của window.  
        
          Một bản tóm tắt với tên số liệu cơ bản của `<basename>` hiển thị nhiều chuỗi thời gian trong một lần scrape: 
          - phát trực tuyến φ-lượng tử (0 ≤ φ ≤ 1) các sự kiện quan sát được, được hiển thị dưới dạng `<basename>{quantile=''}` 
          - tổng của tất cả các giá trị quan sát được, được hiển thị dưới dạng `<basename>_sum` 
          - đếm các sự kiện đã được quan sát, được hiển thị dưới dạng `<basename>_count` 
    

    * [x] **Jobs and instances: Tác vụ và phiên bản**
    
    Theo thuật ngữ Prometheus, một điểm cuối bạn có thể scrape được gọi là một thể hiện, thường tương ứng với một quy trình duy nhất. Một tập hợp các trường hợp có cùng mục đích, một quy trình được sao chép cho khả năng mở rộng hoặc độ tin cậy chẳng hạn, được gọi là một công việc. Ví dụ: một công việc máy chủ API với bốn phiên bản sao chép:
    - job: api-server
      - instance 1: 1.2.3.4:5670
      - instance 2: 1.2.3.4:5671
      - instance 3: 5.6.7.8:5670
      - instance 4: 5.6.7.8:5671
      
    Nhãn được tạo tự động và chuỗi thời gian
    
    Khi Prometheus scrape một mục tiêu, nó sẽ tự động gắn một số nhãn vào chuỗi thời gian bị loại bỏ để xác định mục tiêu bị loại bỏ: 
    - `job`: tên công việc được cấu hình mà mục tiêu thuộc về. 
    - `instance`: the `<host>:<port>` một phần của URL của mục tiêu đã được scrape. 
    
    Nếu một trong hai nhãn này đã có trong dữ liệu bị xóa, hành vi này phụ thuộc vào tùy chọn cấu hình `honor_labels`. 
    
    Đối với mỗi trường hợp Scrape, Prometheus lưu trữ một mẫu trong chuỗi thời gian sau:
    - `up{job="<job-name>", instance="<instance-id>"}`: `1` nếu phiên bản khỏe mạnh, tức là có thể truy cập, hoặc `0` nếu truy cập không thành công
    - `scrape_duration_seconds{job="<job-name>", instance="<instance-id>"}`: thời lượng scrape
    - `scrape_samples_post_metric_relabeling{job="<job-name>", instance="<instance-id>"}`: số lượng mẫu còn lại sau khi áp dụng ghi nhãn lại số liệu
    - `scrape_samples_scraped{job="<job-name>", instance="<instance-id>"}`: số lượng mẫu mà mục tiêu tiếp xúc
    - `scrape_series_added{job="<job-name>", instance="<instance-id>"}`: số lượng gần đúng của series trong lần scrape này

    Chuỗi thời gian hoạt động rất hữu ích cho việc giám sát tính khả dụng của phiên bản.
  * [ ] Kiến trúc của Prometheus stack và các thành phần cơ bản.
  * [ ] Trường hợp nào sử dụng Prometheus? Trường hợp nào không nên sử dụng
* [ ] Cấu hình Prometheus
  * [ ] Cấu hình Prometheus server
  * [ ] Recording rules
  * [ ] Alerting rules
  * [ ] Templating
* [ ] Tìm hiểu về PromQL (Operators, Functions... + Example)
* [ ] Tìm hiểu về Labels
  * [ ] Labels là gì và để làm gì?
  * [ ] Instrumentation & Target labels
  * [ ] Relabel
* [ ] Lưu trữ
  * [ ] Các loại lưu trữ Prometheus
  * [ ] Làm thế nào để tính toán sizing?
* [ ] Tìm hiểu về Alertmanager
  * [ ] Tổng quan và cách thức hoạt động
  * [ ] Cấu hình
  * [ ] Silence Alerts
* [ ] Tìm hiểu về Service discovery
  * [ ] Tại sao phải có service discovery?
  * [ ] Một số loại service discovery cơ bản
    * [ ] File
    * [ ] OpenStack
    * [ ] Consul
