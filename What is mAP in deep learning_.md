# What is mAP in deep learning?
https://towardsdatascience.com/breaking-down-mean-average-precision-map-ae462f623a52

## 1. Intersection over Union (IoU)
![](https://i.imgur.com/nk9Knfc.png)
- IoU: Xác suất chồng chéo giữa real Boundary và predict boundary

## 2. Average Precision and mAP for Information Retrieval

![](https://i.imgur.com/VWa9AYe.png)
![](https://i.imgur.com/8jOaDDb.png)
![](https://i.imgur.com/vsiZKuJ.png)

- GPT: số ngưỡng (chia theo IoU - xác suất chồng chéo) 
    - ví dụ chia 3 ngưỡng:
        - =0  : False Negative
        - 0 < IoU < 0.5   : False Positive
        - 0.5 <= IoU <= 1 : True Positives

- P@k x rel@K = số lần xuất hiện nhãn là True Positives trên số lần dự đoán Positive cho tới thời điểm đang xét trong tập dữ liệu k (k: 1...n)

### Calculating mAP
![](https://i.imgur.com/3sp27hX.png)
- N: ở đây là số label
![](https://i.imgur.com/NRwLSHp.png)

