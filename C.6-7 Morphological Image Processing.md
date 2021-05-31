# C.6-7 Morphological Image Processing
- Là một nhánh sinh học kết hợp giữa các mẫu và cấu trức động - thực vật
- Trích xuất những cái vùng ảnh như: boundary..
## 1. Những cơ bản
![](https://i.imgur.com/FIF4qwg.png)
![](https://i.imgur.com/Ss0Lv4m.png)

## 2. Các kernels
![](https://i.imgur.com/TJ9aExK.png)

## 3. Erosion và Dilation
- Erosion: Phép dịch chuyển của kernel phải năm trọn trong tập A(những giá trị 1) -> sẽ cho ra kết quả ô trọng tâm

- Erosion: Khử nhiễu
![](https://i.imgur.com/X9c8djA.png)
![](https://i.imgur.com/pWTjknU.png)

- Dilation: Tăng nét
![](https://i.imgur.com/bLHvbbK.png)
![](https://i.imgur.com/3hPjFav.png)
![](https://i.imgur.com/JlVfd5J.png)

- Detect Edge bằng Dilation: bằng cách lấy output - input 
- ![](https://i.imgur.com/P0lttb3.png)

- Detect Edge bằng Erosion: bằng cách lấy input - output 
![](https://i.imgur.com/XksMPb2.png)
![](https://i.imgur.com/uB9JK2J.png)

![](https://i.imgur.com/VSNl1ru.png)

### Tính hai mặt 
![](https://i.imgur.com/PCZExzb.png)

## 4. Opening (đóng trước mở sau) và Closing (mở trước đóng sau)
![](https://i.imgur.com/7fnWflX.png)
- Opening: Làm rõ các cạnh, khử nhiễu
![](https://i.imgur.com/UoyoJLo.png)
![](https://i.imgur.com/oIlcLMQ.png)
![](https://i.imgur.com/JGj3mUZ.png)


- Closing: Lấp đầy lỗ trống (tăng nét)
![](https://i.imgur.com/UmVVvCQ.png)
![](https://i.imgur.com/y9uz7cd.png)

### Ví dụ:
- Khử nhiễu, tăng nét
![](https://i.imgur.com/5TtyM6M.png)

### Hit or miss
![](https://i.imgur.com/vZhTI6P.png)
- Phát hiện góc một cách hiệu quả
![](https://i.imgur.com/IpSePuK.png)
![](https://i.imgur.com/A8lXgUN.png)

## 5. Một vài giải thuật Morphology cơ bản
### 1. rút trích boundary
![](https://i.imgur.com/7Efbfhp.png)

### 2. Hole filling
![](https://i.imgur.com/Sqx3GiB.png)
- Dùng khử nhiễu lớn
- ![](https://i.imgur.com/EABcUxu.png)
- ![](https://i.imgur.com/hgz3vx6.png)

### 3. Trích xuất các thành phần được kết nối
![](https://i.imgur.com/ZdhDzds.png)
![](https://i.imgur.com/LGmb3N8.png)
![](https://i.imgur.com/ktDNWZg.png)
![](https://i.imgur.com/4mR2m2h.png)
![](https://i.imgur.com/xMN6lsB.png)

### 4. Convex Hull
![](https://i.imgur.com/xWuu4ic.png)
![](https://i.imgur.com/9EKsBwi.png)

### 5. Thinning
![](https://i.imgur.com/scDSKme.png)
![](https://i.imgur.com/XKT78Hp.png)

### 6. Thickening
![](https://i.imgur.com/xzc161x.png)
### 7. Skeletons
![](https://i.imgur.com/b4lDsch.png)
![](https://i.imgur.com/lFhSAK3.png)

### 8. Pruning
![](https://i.imgur.com/L33XcsN.png)

### 9. Reconstruction
- by Dilation
![](https://i.imgur.com/aiqQ3a3.png)
![](https://i.imgur.com/Xu49Vth.png)

- by Erosion
![](https://i.imgur.com/IU20Xuy.png)
![](https://i.imgur.com/C1OSb7z.png)
### 10. Đạo hàm dùng Morphology
![](https://i.imgur.com/pf6Pvyr.png)
![](https://i.imgur.com/a9Ja8iR.png)
### 11. Detect object với Top-hat và Bottom-hat trong ảnh xám
![](https://i.imgur.com/CLf3b15.png)
![](https://i.imgur.com/A12kWEP.png)
![](https://i.imgur.com/12M2Ivi.png)

### 12. Optical granulometry
![](https://i.imgur.com/bXXbv0h.png)

### tóm tắt
![](https://i.imgur.com/qLDe0Rd.png)
![](https://i.imgur.com/TDPlKIz.png)
![](https://i.imgur.com/KkdmZiT.png)
![](https://i.imgur.com/gwdHLZC.png)
![](https://i.imgur.com/zOZEO4L.png)

![](https://i.imgur.com/htEWKVa.png)
![](https://i.imgur.com/QlOWYmN.png)
![](https://i.imgur.com/bWJwA0o.png)
![](https://i.imgur.com/TFEoBQ9.png)
![](https://i.imgur.com/NanErFy.png)
![](https://i.imgur.com/kFWEBo3.png)
![](https://i.imgur.com/gFs7kVh.png)
![](https://i.imgur.com/Xr1KfXB.png)
