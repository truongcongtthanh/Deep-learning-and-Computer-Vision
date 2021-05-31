# Báo cáo Deep learning 
## 1. Mô tả đề tài
- Face Detection and Recognition: Bài toán phát hiện khuôn mặt có trong ảnh và nhận diện khuôn mặt đó từ dữ liệu đã train
- Giới hạn đề tài Detect and Recognize:
    - Một khuôn mặt đối với test realtime bằng camera laptop
    - Nhiều khuôn mặt đối với test bằng video
## 2. Các kỹ thuật giải quyết bài toán
- Có nhiều kỹ thuật giúp giải quyết bài toán trên. Em xin giới thiệu kỹ thuật
    - Facenet model để phát hiện và căn chỉnh khuôn mặt
    - MTCNN model để nhận diện khuôn mặt
    
### 2.1. Multi-task Cascaded Convolutional Networks (MTCNN)
#### 2.1.1 Khái quát mạng MTCNN
![](https://i.imgur.com/ECgJGs4.png)
**Ảnh 1**
- Là một kỹ thuật dùng để phát hiện khuôn mặt trải qua 3 giai đoạn:
    - Trước tiên ta cần resize bức thành Image pyramid để chuẩn bị cho dữ liệu đầu vào
    - Giai đoạn 1: Chúng ta sẽ sử dụng một **fully convolutional network** đơn giản được gọi là **Proposal Network (P-Net)** để đề xuất nhanh ra các **windows** chứa đối tượng. Sau đó, chúng ta sử dụng 2 kỹ thuật kết hợp là **Bounding box regression và Non-maximum suppression (NMS)** để giảm số đề xuất trùng lặp xuống.
    - Giai đoạn 2: Đầu ra của giai đoạn 1 sẽ được đưa vào một mạng **CNN** phức tạp hơn được gọi là **Refine Network (R-Net)** để loại bỏ số lượng lớn các đề xuất nữa (giảm các đối tượng không phải là khuôn mặt), rồi sử dụng tiếp **Bounding box regression và Non-maximum suppression (NMS)** để giảm trùng lặp
    - Giải đoạn 3: Tương tự như giai đoạn 2, chỉ khác mạng **Output Network (O-Net)** đưa ra 5 điểm cụ thể trên gương mặt:
        - Mắt trái
        - Mắt phải
        - Mũi 
        - Góc miệng trái
        - Góc miệng phải
![](https://i.imgur.com/kIM27WY.png)
**Ảnh 2**

#### 2.1.2 Kiến trúc mạng MTCNN:
![](https://i.imgur.com/ddjCLOh.png)
**Ảnh 3**
    - **Face classification**: Chúng ta sẽ sử dụng **Cross-entropy loss** để tiến hành phân loại **face/non-face**
            ![](https://i.imgur.com/WzgvfV1.png)
    - **Bounding box regression**:
            ![](https://i.imgur.com/FDQUyQI.png)
    - **Facial landmark localization**: 
            ![](https://i.imgur.com/nBoYOwV.png)
            - landmarks ở đây là 5 điểm keypoints 


#### 2.1.3 Ưu điểm mạng MTCC:
    - Nhận diện được mặt ở nhiều góc khác nhau
    - Nhận diện có độ chính xác cao
    - Tốc độ nhanh: 16fps trên máy 2.60GHz CPU

#### 2.1.4 Đánh giá
- So sánh tốc độ và độ chính xác giữa **MTCNN** và mạng **CNN** trước[1]
![](https://i.imgur.com/OKFLODO.png)

- Đánh giá hiệu năng **phát hiện khuôn mặt** của **MTCNN** và một vài phương pháp khác
![](https://i.imgur.com/xcHzRLr.png)
**Ảnh 4**
- Đánh giá **liên kết khuôn mặt** của **MTCNN** và một vài phương pháp khác
![](https://i.imgur.com/gcSK5y0.png)
**Ảnh 5**
### 2.2 Facenet
- Facenet chính là một dạng **siam network** có tác dụng biểu diễn các bức ảnh trong một không gian eucledean n chiều (thường là 128) sao cho khoảng cách giữa các véc tơ **embedding càng nhỏ**, mức độ tương đồng giữa chúng càng lớn.
- **Siam Network** là kiến trúc mạng mà khi bạn đưa vào 2 bức ảnh và mô hình sẽ trả lời chúng thuộc về cùng 1 người hay không

#### 2.2.1 Khái quát thuật toán
- Hầu hết các thuật toán **nhận diện khuôn mặt** trước **Facenet** đều tìm cách biểu diễn một vector embedding thông qua một **layer bottle neck** để giảm chiều dữ liệu
    - Hạn chế: số chiều embedding lớn (>=1000), anh hướng tới tốc độ. Thường áp dụng thêm thuật toán **PCA** giảm chiều dữ liệu để tăng tốc độ tính toán
    - Hàm loss function chỉ đo lường khoảng cách giữa 2 bức ảnh **=>** một đầu vào huấn luyện chỉ học được **Hoặc là sự giống nhau hoặc là khác nhau** mà không học được cùng lúc cả 2

- **Facenet** ra đời để giải quyết 2 hạn chế trên
    - **Base network** áp dụng một mạng CNN và giảm chiều dữ liệu còn 128. 
    - Sử dụng **loss function** là hàm **Triple loss** có khả năng học đồng thời cả sự giống nhau và khác nhau

#### 2.2.2 Hàm Triple Loss
![](https://i.imgur.com/EnSxrqU.png)
**Ảnh 6**
- Tính **Triplet loss** là khoảng cách giữa các embbeding vector **anchor** và **positive** **trừ** cho khoảng cách giữa các embbeding vector **anchor và negative** (tức ta tìm cách làm giảm khoẳng cách từ các vector positive tới anchor và ngược lại đẩy các vector negative đi xa khỏi anchor)
- Để áp dụng triple loss, chúng ta cần **lấy ra 3 bức ảnh** trong đó có **một bức ảnh là anchor** được cố định trước, 1 ảnh là **Positive** (cùng một người với anchor), 1 ảnh là **Negative** (người khác so với Anchor).
- Kí hiệu ảnh Anchor, Positive, Negative lần lượt là **A, P, N**.
- Mục tiêu của hàm loss function là tối thiểu hóa khoảng cách giữa 2 ảnh khi chúng là negative và tối đa hóa khoảng cách khi chúng là positive. Như vậy chúng ta cần lựa chọn các bộ 3 ảnh sao cho:
    - Ảnh Anchor và Positive khác nhau nhất: cần lựa chọn để khoảng cách **d(A,P)**  lớn. Điều này cũng tương tự như bạn lựa chọn một ảnh của mình hồi nhỏ so với hiện tại để thuật toán học khó hơn. Nhưng nếu nhận biết được thì nó sẽ thông minh hơn.
    - Ảnh Anchor và Negative giống nhau nhất: cần lựa chọn để khoảng cách **d(A,N)** nhỏ. Điều này tương tự như việc thuật toán phân biệt được ảnh của một người anh em giống bạn với bạn.

- Triplot loss function luôn lấy 3 bức ảnh làm input và trong mọi trường hợp ta kì vọng:
    ![](https://i.imgur.com/PUSCBxU.png)
- Để làm cho khoảng cách giữa vế trái và vế phải lớn hơn, chúng ta sẽ cộng thêm vào vế trái một hệ số  không âm rất nhỏ. Khi đó **(1)** trở thành:
    ![](https://i.imgur.com/GQ5kbeE.png)
- Như vậy hàm loss function sẽ là:
    ![](https://i.imgur.com/soqBEhB.png)
- Sẽ không ảnh hưởng gì nếu ta nhận diện đúng ảnh Negative và Positive là cùng cặp hay khác cặp với Anchor. Mục tiêu của chúng ta là giảm thiểu các trường hợp hợp mô hình nhận diện sai ảnh Negative thành Postive nhất có thể. Do đó để loại bỏ ảnh hưởng của các trường hợp nhận diện đúng Negative và Positive lên hàm loss function. Ta sẽ điều chỉnh giá trị đóng góp của nó vào hàm loss function về 0. Khi đó hàm loss function trở thành:
    ![](https://i.imgur.com/JbD9hSY.png)

## 3. Tài liệu tham khảo
[] Joint Face Detection and Alignment using
Multi-task Cascaded Convolutional Networks: https://arxiv.org/ftp/arxiv/papers/1604/1604.02878.pdf

[] FaceNet: A Unified Embedding for Face Recognition and Clustering: https://arxiv.org/pdf/1503.03832.pdf

[] Mô hình Facenet trong face recognition :https://phamdinhkhanh.github.io/2020/03/12/faceNetAlgorithm.html#32-learning-similarity

[] Deep learning và bài toán Face Recognition: https://forum.machinelearningcoban.com/t/deep-learning-va-bai-toan-face-recognition/1776

[] Nhận diện khuôn mặt bằng MTCNN - hướng dẫn tách khuôn mặt tập trung vào tốc độ: https://ichi.pro/vi/nhan-dien-khuon-mat-bang-mtcnn-huong-dan-tach-khuon-mat-tap-trung-vao-toc-do-13663800405321

[] Nhận diện khuôn mặt trong video bằng MTCNN và Facenet: https://miai.vn/2019/09/11/face-recog-2-0-nhan-dien-khuon-mat-trong-video-bang-mtcnn-va-facenet/
