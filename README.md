
### Docker container  

#### Overview về docker container
- [x] Cài đặt docker (trên linux)
- [ ] Cấu hình proxy
  - [ ] Cho docker daemon
  - [ ] Cho docker client
- [ ] Cấu hình trusted registry trong daemon.json tham khảo Local Repos
- [ ] Hello world với Docker
#### Các câu lệnh cơ bản
- [x] **Docker tag**: Tạo 1 image có tag mới từ image đã có
      
      Cú pháp: `docker image tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG]`
 
 Ví dụ: 
 ![Screenshot from 2022-12-27 08-09-53](https://user-images.githubusercontent.com/120613788/209635342-ab8b5dcf-2161-4fc0-81c2-93eedfc7db20.png)
- [x] **Docker run**: Khởi tạo 1 container dựa vào image có sẵn

      Cú pháp: `docker run [OPTIONS] IMAGE [COMMAND] [ARG...]

 Ví dụ:

Với 
    
    --name: tên container

    -h: tên host
    
    -t: cung cấp một giao diện để gõ command bên trong container
    
    -i: cung cấp một "con đường" giúp cho các chương trình bên trong container nhận được những command đã viết
- [x] **Docker build**: Tạo image từ Dockerfile
      Cú pháp: `docker build [OPTIONS] PATH | URL | -`
 
Ví dụ: 
![image](https://user-images.githubusercontent.com/120613788/209645752-0a615496-0eb6-4a64-8d05-817865e224bf.png)
- [x] **Docker push**: Đưa một image hoặc một repo lên Registry
      Đăng nhập vào Docker Hub:
      
      Cú pháp: `docker login`
![image](https://user-images.githubusercontent.com/120613788/210026315-00c3706c-4f69-4cea-8fc4-42e6caa01872.png)

      Cú pháp: `docker push [OPTIONS] NAME[:TAG]`
      
- Các lựa chọn:
            
|       Options       |              | Mô tả     |
| :------------:|:-------------:|:-----:|
|    -a          |      --all-tags      | Push tất cả tagged images trong repository    |
|     -a         |       --disable-content-trust      |   Bỏ qua việc xác minh image   |
|     -q         | --quiet             |    Thu gọn log của lệnh  |
- [x] **Docker pull**: Pull 1 image hoặc 1 Repo từ Registry

Cú pháp : `docker pull [OPTIONS] NAME[:TAG|@DIGEST]
- Các lựa chọn:
            
|       Options       |              | Mô tả     |
| :------------:|:-------------:|:-----:|
|    -a          |      --all-tags      | Push tất cả tagged images trong repository    |
|     -a         |       --disable-content-trust      |   Bỏ qua việc xác minh image   |
|     -a         |       --flatform string      |  Thiết lập platform nếu server cho phép nhiều platform   |
|     -q         | --quiet             |    Thu gọn log của lệnh  |

Ví dụ:
![image](https://user-images.githubusercontent.com/120613788/210030711-5a578af8-9352-40ba-998c-e23d14718470.png)
#### Kiến thức thêm
- [x] **Docker CE/Docker EE**

 Có 2 phiên bản phổ biến của Docker Engine:
- **Docker Community Edition (CE)**: Là phiên bản miễn phí và chủ yếu dựa vào các sản phẩm nguồn mở khác.
- **Docker Enterprise (EE)**: Khi sử dụng phiên bản này sẽ nhận được sự hỗ trợ của nhà phát hành, có thêm các tính năng quản lý và bảo mật.

- [x] **Docker Engine**
![image](https://user-images.githubusercontent.com/120613788/210030832-14903b70-67fa-488d-9855-6814ba133839.png)
Docker Engine: Là một ứng dụng client-server

Các thành phần chính của Docker Engine gồm có:
- **Server (hay còn gọi là Docker Daemon)**: chịu trách nhiệm tạo, quản lý các Docker objects như images, containers, networks, volume.
- **REST API**: docker daemon cung cấp các api cho Client sử dụng để thao tác với Docker
- **Client**: là thành phần đầu cuối cung cấp một tập hợp các câu lệnh sử dụng api để người dùng thao tác với Docker.
- [x] **Docker Compose**

Docker Compose là công cụ dùng để định nghĩa và run multi-container cho Docker application. Với compose bạn sử dụng file YAML để config các services cho application của bạn. Sau đó dùng command để create và run từ những config đó. Sử dụng cũng khá đơn giản chỉ với ba bước:
- Khai báo môi trường của chương trình trong Dockerfile.
- Khai báo các services cần thiết để chạy application trong file docker-compose.yml.
- Run docker-compose up để start compose và chạy chương trình.
Compose có những câu lệnh cho phép quản lý lifecycle của chương trình:
- Start, Stop và Build lại service
- Xem status của các service đang chạy
- Xem log output của service đang chạy
Như vậy Docker compose giúp ta tự động tải các image, thiết lập cấu hình tốt hơn rất nhiều so với docker. Nó sẽ cần một file cấu hình docker-compose.yml để chạy theo các image và cấu hình trong đó.

**Đặc điểm**
Không giống như Dockerfile (build các image). Docker compose dùng để build và run các container. Các thao tác của docker-compose tương tự như lệnh: docker run.

Docker compose cho phép tạo nhiều service(container) giống nhau bằng lệnh:

`$ docker-compose scale <tên service> = <số lượng>`

**Những lợi ích khi sử dụng Compose**

- Tạo ra nhiều môi trường độc lập (isolated environments) trong một host: Compose cô lập môi trường của các project để đảm bảo chúng không bị xung đột lẫn nhau, cũng như dễ dàng tạo những bản sao của một môi trường nào đó.

- Chỉ tạo lại các container đã thay đổi: Compose sẽ nhận biết được các service chưa thay đổi và sử dụng lại các container tương ứng với service đó.

- Điều chỉnh các biến sử dụng cho các môi trường: Compose sử dụng các biến trong Compose file cho các môi trường. Vì vậy với môi trường hay người dùng khác nhau, có thể điều chỉnh các biến khi sử dụng Compose để thiết lập các service.

**Một số trường hợp thường gặp khi sử dụng Compose**

Compose có thể được sử dụng cho nhiều trường hợp. Dưới đây sẽ là hai trường hợp sử dụng Compose trong việc phát triển chương trình.

- Môi trường phát triển

Khi phát triển một chương trình, việc chạy một chương trình trong một môi trường cô lập và tương tác là rất cần thiết. Compose cho phép thiết lập và chạy tất cả các service cần thiết cho chương trình. Chỉ với một câu lệnh docker-compose up, các service đó sẽ được chạy với các container tương ứng.

- Môi trường cho automated test

Với automated test, việc tạo ra một môi trường cho việc sử dụng các gói test bằng compose trở nên rất đơn giản. Tạo một môi trường với Compose, chạy các gói test, sau đó hủy môi trường đó chỉ với ba dòng lệnh:

`$ docker-compose up`

`$ ./run_tests` (Chạy gói automated test)

- [x] **Docker Registry**
![image](https://user-images.githubusercontent.com/120613788/210033358-ec87b778-7f5c-47da-8884-7c1b3f7243f3.png)
Docker Registry là một dịch vụ máy chủ cho phép lưu trữ các docker image của cá nhân, công ty, team... hay nói cách khác Docker Registry là nơi chứa các image trong quá trình khởi động các container. Hình ảnh sẽ được push vào registry và client sẽ pull images từ registry. Bạn có thể sử dụng registry của riêng mình hoặc registry của các nhà cung cấp lớn như: AWS, Google Cloud, Microsoft, Azure.
- [x] **Docker Daemon**
Đây là nơi lắng nghe các yêu cầu đến từ Docker client với mục đích quản lý các đối tượng thông qua REST API như Image, Container, Network hay Volumes. Bên cạnh đó, các Docker Daemon cũng giao tiếp với nhau nhằm quản lý các Docker Services.
- [x] **Docker network**: Host, Bridge, Overlay, ...
Docker network sẽ đảm nhiệm nhiệm vụ kết nối mạng giữa các container với nhau, kết nối giữa container với bên ngoài, cũng như kết nối giữa các cụm (swarm) docker containers.

Với container và service của Docker, bạn có thể kết nối chúng lại với nhau hoặc kết nối chúng với các mạng khác nằm ngoài docker.

**Các loại network drivers của Docker**

Hệ thống network Docker là dạng plugable, sử dụng drivers. Hầu hết các driver được cung cấp mặc định, với các chức năng cốt lõi của các chức năng mạng thông thường.

Docker network có thể cung cấp hầu hết các chức năng mà một hệ thống mạng bình thường cần có.

- BRIDGE

Đây là driver mạng default của Docker. Nếu không chỉ định driver thì bridge sẽ là driver mạng mặc định khi khởi tạo.

Khi chúng ta cài đặt Docker, virtual bridge docker0 sẽ được tạo ra, docker tìm một subnet chưa được dùng trên host và gán một địa chỉ cho docker0
![image](https://user-images.githubusercontent.com/120613788/210043098-eec5ad01-8e07-418f-8ea7-fcaaf2ab84c3.png)

Bridge network thường được sử dụng khi cần chạy ứng dụng dưới dạng các container độc lập cần giao tiếp với nhau. Các container trong cùng mạng có thể giao tiếp với nhau qua địa chỉ IP. Docker không hỗ trợ nhận diện host ở mạng này, vì vậy muốn connect thì phải dùng options links để docker có thể hiểu được địa chỉ của các service.

Bridge là driver tốt nhất cho việc giao tiếp multiple containers ở một host đơn.

- HOST

Dùng khi container cần giao tiếp với host và sử dụng luôn mạng ở host, vì sử dụng mạng của máy chủ đang chạy nên không còn lớp mạng nào giữa container với Docker Host phù hợp khi cần connect từ container ra thẳng ngoài host

- OVERLAY

Mạng lớp phủ - Overlay network tạo một mạng phân tán giữa nhiều máy chủ Docker. Kết nối nhiều Docker daemons với nhau và cho phép các cụm services giao tiếp với nhau. Chúng ta có thể sử dụng overlay network để giao tiếp dễ dàng giữa cụm các services với một container độc lập, hay giữa 2 container với nhau ở khác máy chủ Docker daemons.

Nhờ Overlay network, không cần các công việc thiết lập routing giữa các container thông qua hệ điều hành. Overlay network tạo nên một lớp phủ trên mạng của máy chủ và cho phép container kết nối đến (bao gồm cả các cụm containers) để giao tiếp một cách bảo mật. Docker đảm bảo định tuyến các gói tin đến và đi đúng container đích.

- MACVLAN

Mạng Macvlan cho phép chúng ta gán địa chỉ MAC cho container, điều này làm cho mỗi container như là một thiết bị vật lý trong mạng. Docker daemon định tuyến truy cập tới container bởi địa chỉ MAC. Sử dụng driver macvlan là lựa chon tốt khi các ứng dụng khác cần phải connect đến theo địa chỉ vật lý hơn là thông qua các lớp mạng của máy chủ.

- NONE

Với container không cần networking hoặc cần disable đi tất cả mọi networking, chúng ta sẽ chọn driver này. Thường được dùng với mạng tùy chỉnh. Driver này không thể dùng trong cụm swarm.

**Một vài cách sử dụng Docker Network**

**Khởi tạo một Docker Network**
`$docker network create [OPTIONS] NETWORK`
`$docker network create -d bridge my-bridge-network`

Trong đó options `-d` là driver, để tạo mạng overlay thì có thể dùng `-d overlay` .Ngoài ra còn một số options
--gateway: Địa chỉ Ip của Gateway (IPv4 hay IPv6) cho mạng con
--ip-range: Xác định một dải IPs sử  dụng trong mạng
--internal: Hạn chế  access từ bên ngoài vào mạng
--ipv6: Bật IPv6
--subnet: Chọn mạng con

Ví dụ: Khởi tạo mạng my-bridge-network1 với driver bridge có subnet 10.11.0.0/16, ip gateway là 10.11.0.1
![image](https://user-images.githubusercontent.com/120613788/210045924-d2158f89-2bf4-48e8-8f12-089ace28b5a6.png)
![image](https://user-images.githubusercontent.com/120613788/210045977-012fc02a-a409-4e3e-ba44-3185c5a886ba.png)

**Sử dụng network khi chạy một container**

Sử dụng option --network để chạy một container trên network bridge đó

Cú pháp: `docker run --network=bridge -itd --name=container1 <tên container>`
![image](https://user-images.githubusercontent.com/120613788/210046567-9ca3e234-34b4-45b7-8851-255750197806.png)

**Sử dụng network qua docker-compose**

Khi dùng docker-compose thì nếu không khai báo network, docker sẽ tự động khởi tạo một mạng dành cho app và driver sẽ là bridge.

Cú pháp: `docker-compose up`

Nếu muốn khai báo mạng cho từng containers trong một cụm chúng ta có thể dùng 2 cách sau:
- Khai báo driver host cho container app qua network_mode, cách khai báo này có thể thay đổi driver cho container

Trường hợp chúng ta muốn app sử dụng luôn mạng của host mà không dùng mạng docker, hãy khai báo như sau:
![image](https://user-images.githubusercontent.com/120613788/210048787-f8606fa5-899d-49ca-ba57-d7c57e7363db.png)
- Khai báo qua networks trong docker-compose.yml
![image](https://user-images.githubusercontent.com/120613788/210048805-2e2043c1-e448-4be2-b2ad-d7bd1e38085b.png)
**Sử dụng network trong cụm docker swarm**

Docker swarm thường sử dụng file docker-compose.yml để deploy, và trong file này cần lựa chọn mạng overlay để docker có thể connect multiple networks host với nhau.
![image](https://user-images.githubusercontent.com/120613788/210048830-4834a14c-7f08-431a-a556-dbb5d026cd87.png)

**Xóa network**

Cú pháp: `docker network rm <tên network>`
![image](https://user-images.githubusercontent.com/120613788/210049135-b306913e-13b6-4480-ac36-90f3f9172b44.png)

Kiểm tra lại các network đang có:
![image](https://user-images.githubusercontent.com/120613788/210049904-6f29a8ec-6624-4c2d-a0e0-be6f23152d49.png)

- [ ] **Docker volume, mount** 

Volume trong Docker là một cơ chế được Docker sử dụng để cung cấp khả năng lưu trữ liên tục (persistent data storage). Chúng mang lại những lợi ích đáng kể trong quá trình phát triển và triển khai ứng dụng của bạn với Docker.
![image](https://user-images.githubusercontent.com/120613788/210050821-6bb97e6c-5fb2-4afb-aa06-b74654ddd54c.png)

Volume trong Docker được dùng để chia sẻ dữ liệu cho container.

**Tại sao lại cần Docker Volume?**
- Volumes giản hóa việc backup hoặc migrate hơn bind mount.
- Bạn có thể quản lý volumes sử dụng các lệnh Docker CLI và Docker API.
- Volumes làm việc được trên cả Linux và Windows container.
- Volumes có thể an toàn hơn khi chia sẻ dữ liệu giữa nhiều container.
- Volume drivers cho phép bạn lưu trữ volumes trên remote hosts or cloud providers, để mã hóa nội dung của volumes, hoặc thêm các chức năng khác.
- Các nội dung của volume mới có thể được điền trước bởi một container.

**Dùng Docker Volume khi nào?**
- Sử dụng volume để gắn (mount) một thư mục nào đó trong host với container.
- Sử dụng volume để chia sẻ dữ liệu giữa host và container
- Sử dụng volume để chia sẽ dữ liệu giữa các container
- Backup và Restore volume.

**Tạo volumes**

Tạo volume với docker bằng lệnh sau:

`docker volume create [volume_name]`

Lệnh này sẽ tạo ra một volume lưu trữ dữ liệu có thể được sử dụng bởi một container cụ thể hoặc một được chia sẻ giữa một nhóm các container. Có thể gắn volume này vào một vị trí bên trong container. Sau khi hoàn tất, bạn có thể dễ dàng lưu trữ hoặc truy cập dữ liệu container từ máy chủ.

Ví dụ:
![image](https://user-images.githubusercontent.com/120613788/210052546-0c7a4be5-3952-4f5c-a7db-c0d1c8b7fde2.png)

**Hiển thị volumes**

Khi phải quản lý một số lượng lớn các volume dữ liệu, cần xác định được đúng các volume. Liệt kê tất cả các volume hiện đang được khai báo bằng lệnh: `docker volume ls`

Lệnh này sẽ hiển thị danh sách tên tất cả các docker volume cùng với docker volume drivers tương ứng của chúng đang có trên máy chủ. Ngoài ra, đối với Linux thì các volume của sẽ được lưu trữ tại /var/lib/docker/volumes trên máy chủ.

Ví dụ:
![image](https://user-images.githubusercontent.com/120613788/210052981-ccc81ce7-dce1-4ff8-abf0-ea9d12a10e26.png)

**Kiểm tra volunes**

Lệnh kiểm tra docker volume sẽ cung cấp thông tin chi tiết về một volume cụ thể. Nó hiển thị các thông tin về volume driver, mount point, scope hay labels (nhãn) của volume.

Cú pháp: `docker volume inspect [volume_name]`

Ví dụ:
![image](https://user-images.githubusercontent.com/120613788/210053120-6161d05e-fdcb-4e72-998a-2b2894cc9a7b.png)

**Xoá volumes**

Xoá đi các volume không cần thiết giúp giải phóng không gian lưu trữ cho máy chủ.
- Xoá 1 volume cụ thể: 

`docker volume rm [volume_name]`
- Xoá nhiều volume cùng lúc:

`docker volume rm [volume_name_1] [volume_name_2] [volume_name_3] [...]`

- Khi có một số lượng volume rất lớn cần phải xoá đi thì docker daemon còn cung cấp một lệnh rất hữu ích nữa đó là:

`docker volume prune`

Lệnh này không xoá đi bất cứ volume nào đang được sử dụng bởi một container hiện có. Nó sẽ chỉ xoá đi các volume đang không được sử dụng. Do đó, lệnh này là an toàn để sử dụng và rất hiệu quả trong việc giải phóng không gian lưu trữ trên các môi trường phát triển.

**Tạo một container với volumes**

Lệnh sau đây sẽ tạo một docker container và mount volume vào container này. Nếu volume liên kết không tồn tại sẵn thì Docker Engine sẽ tạo một volume mới:
- Cách 1: Sử dụng tùy chọn `--volume`

Cú pháp: `docker run --name [container_name] --volume "[volume_name]":/tmp [docker_image]`
### Docker-compose
- [ ] Định nghĩa
- [ ] Thực hành chạy file-config
