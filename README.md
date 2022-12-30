
### Docker container  

#### Overview về docker container
- [x] Cài đặt docker (trên linux)
- [ ] Cấu hình proxy
  - [ ] Cho docker daemon
  - [ ] Cho docker client
- [ ] Cấu hình trusted registry trong daemon.json tham khảo Local Repos
- [ ] Hello world với Docker
#### Các câu lệnh cơ bản
- [x] Docker tag: Tạo 1 image có tag mới từ image đã có
      
      Cú pháp: `docker image tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG]`
 
 Ví dụ: 
 ![Screenshot from 2022-12-27 08-09-53](https://user-images.githubusercontent.com/120613788/209635342-ab8b5dcf-2161-4fc0-81c2-93eedfc7db20.png)
- [x] Docker run: Khởi tạo 1 container dựa vào image có sẵn

      Cú pháp: `docker run [OPTIONS] IMAGE [COMMAND] [ARG...]

 Ví dụ:

Với 
    
    --name: tên container

    -h: tên host
    
    -t: cung cấp một giao diện để gõ command bên trong container
    
    -i: cung cấp một "con đường" giúp cho các chương trình bên trong container nhận được những command đã viết
- [x] Docker build: Tạo image từ Dockerfile
      Cú pháp: `docker build [OPTIONS] PATH | URL | -`
 
Ví dụ: 
![image](https://user-images.githubusercontent.com/120613788/209645752-0a615496-0eb6-4a64-8d05-817865e224bf.png)
- [x] Docker push: Đưa một image hoặc một repo lên Registry
      Đăng nhập vào Docker Hub:
      
      Cú pháp: `docker login`
![image](https://user-images.githubusercontent.com/120613788/210026315-00c3706c-4f69-4cea-8fc4-42e6caa01872.png)

      Cú pháp: `docker push [OPTIONS] NAME[:TAG]`
      
      Các lựa chọn:
      
            | Options |                |              Mô tả |
            | ------------- | ------------- | ------------- |
            | -a | --all-tags  | Push tất cả tagged images trong repository |
            |    | --disable-content-trust | Bỏ qua việc xác minh image |
            | -q | --quiet  | Ngăn chặn đầu ra dài dòng |
- [ ] Docker pull
#### Kiến thức thêm
- [ ] Docker CE/Docker EE
- [ ] Docker Engine
- [ ] Docker Compose - phải tìm hiểu
- [ ] Docker Registry
- [ ] Docker Daemon - phải tìm hiểu
- [ ] Docker network: Host, Bridge, Overlay, ...
- [ ] Docker volume, mount - phải tìm hiểu

### Docker-compose
- [ ] Định nghĩa
- [ ] Thực hành chạy file-config
