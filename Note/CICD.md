---
Created by: liemgumball
Created time: 2024-08-04T17:42
---
# Dockerfile

1. Sử dụng node version 18
2. working directory bên trong image
3. copy các file package.json và package.lock.jsọn vào working directory
4. chạy npm installl để tải module
5. copy các file còn lại vào
6. chỉ rằn appp sẽ chạy ở cổng 3000
7. chạy command npm start

# File cicd

1. run workflows khi có lệnh push lên main hoặc là có pulll request merge vào main
2. job đầu tiên là ci
    1. checkout để thực hiện action
    2. đặng nhập vào dockerhub
    3. build image từ dockerfile và run container
    4. sleep 10 giây là show log của container đang chạy
    5. push image vủa build thành công lên dockerhub
3. Job tiếp theo là cd
    1. đăng nhập vào aws ec2 instance bằng ssh
    2. pull image vừa mới tạo trên dockerhub
    3. run container bằng image mới tạo trên cổng 3000 cùng với các biến từ trong file /home/ubuntu/.env

# Giải thích truyền biến

khi run container thì thêm flag —env-file và đừng dẫn tới file chứa biến môi trường