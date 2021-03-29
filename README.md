# Check_MK-2.0.0.
## Phần 1: Cài Đặt.
### 1.Cài đặt trên server Ubuntu 20.04.
### 1.1. Tải file cài đặt OMD - Check MK
```
wget https://download.checkmk.com/checkmk/2.0.0p1/check-mk-raw-2.0.0p1_0.focal_amd64.deb
```
![Screenshot from 2021-03-29 10-46-18](https://user-images.githubusercontent.com/71110126/112784480-0b02a800-907c-11eb-8e23-a730039c6091.png)

### 1.2. Cài đặt gói `gdebi`.
`Check MK` cần khá nhiều các gói dependence đi kèm, vì thế chúng ta cài đặt thêm gói này để có thể tự động cài một số gói đó.
```
apt install gdebi-core -y
apt-get update
```
Sau khi cài đặt `gdebi-core` xong, chúng ta sẽ được kết quả như hình.
![Screenshot from 2021-03-29 10-47-49](https://user-images.githubusercontent.com/71110126/112784622-5c129c00-907c-11eb-88ce-1c2d82bd7f9b.png)

### 1.3. Cài đặt OMD - Check MK
Chúng ta sử dụng `gdebi` để cài đặt gói DEB, mục đích là để GDEBI 'hoàn thiện' những gói dependence mà check mk cần.
```
gdebi check-mk-raw-2.0.0p1_0.focal_amd64.deb
```
Chọn `Y` để đồng ý cài đặt
![Screenshot from 2021-03-29 10-54-42](https://user-images.githubusercontent.com/71110126/112784999-2f12b900-907d-11eb-910b-48affb2fcd4e.png)

Chờ cho server tự động cài đặt khoảng 5p, chúng ta thấy kết quả như sau
![Screenshot from 2021-03-29 10-56-57](https://user-images.githubusercontent.com/71110126/112785135-80bb4380-907d-11eb-90d9-455a4b75de7a.png)

### 1.4. Tạo và khởi động site trên OMD
- **Bước 1**: Tạo site
```
omd create monitoring
```
**Chú ý**: `monitoring` là tên tùy chọn, bạn có thể đặt bất cứ tên gì bạn muốn
![Screenshot from 2021-03-29 11-00-25](https://user-images.githubusercontent.com/71110126/112785365-050dc680-907e-11eb-95b2-230cbdffd47e.png)

Thông tin `site` được mô tả ở hình.
   
- **Bước 2**: Khởi động site

```
omd start monitoring
```
![Screenshot from 2021-03-29 11-02-09](https://user-images.githubusercontent.com/71110126/112785458-3b4b4600-907e-11eb-9a50-d8ac35aba0e6.png)
- **Bước 3:** Mở port 80 cho HTTPD trên UFW

Nếu server của bạn có sử dụng UFW, hãy mở port cho apache2 bằng lệnh:

```
ufw allow 80/tcp
ufw reload
```

- **Bước 4**: Kiểm tra bằng trình duyệt Web

Dùng trình duyệt truy cập vào địa chỉ

```
http://10.5.92.179/monitoring
```

**Chú ý**: Thay địa chỉ IP của bạn vào đường dẫn và đăng nhập theo `omdadmin/omd`
![Screenshot from 2021-03-29 11-04-55](https://user-images.githubusercontent.com/71110126/112785644-aac13580-907e-11eb-8ab9-270c81e62491.png)
![Screenshot from 2021-03-29 11-05-09](https://user-images.githubusercontent.com/71110126/112785649-ae54bc80-907e-11eb-8cb3-64201eacac5e.png)

