# Sơ qua về project

## Cơ sở lý thuyết 
### Phát hiện gương mặt

- Các gương mặt trên được cắt trực tiếp nhờ model phát hiện gương mặt người được train trên mạng YOLO dựa theo dataset về gương mặt con người đã được gán nhãn theo format của YOLO v11

  > YOLO là một mô hình mạng CNN cho việc phát hiện, nhận dạng, phân loại đối tượng. Yolo được tạo ra từ việc kết hợp giữa các convolutional layers và connected layers.Trong đóp các convolutional layers sẽ trích xuất ra các feature của ảnh, còn full-connected layers sẽ dự đoán ra xác suất đó và tọa độ của đối tượng. Thông tin về YOLO có thể tìm thấy ở [đây](https://docs.ultralytics.com/#what-are-the-licensing-options-available-for-ultralytics-yolo)


   ![](https://oditeksolutions.com/wp-content/uploads/2025/01/Fashionable-Blog-Banner.webp)
  <p align = 'center'> Phát hiện gương mặt với YOLO </p>

### Nhận diện các gương mặt
- Ứng dụng mô hình CNN để train dữ liệu nhận diện các gương mặt. Các gương mặt được thu thập, gán nhãn, sau đó tiền xử lý dữ liệu và đưa vào CNN để train tạo ra model có thể phân biệt gương mặt mỗi người

  > Layer cuối cùng là lớp Dense có số unit bằng số người cần phân biệt và activation là hàm softmax. Từ đó có thể phát triển code nhận diện gương mặt (nếu độ tin cậy < 90% thì gán nhãn là 'unknow' ngược lại thì ghhi nhãn của nó lên màn hình)

  ![](https://cdn.analyticsvidhya.com/wp-content/uploads/2024/10/59954intro-to-CNN.webp)
    <p align = 'center'> Minh họa cấu trúc CNN </p>

# Cách chạy
## 1. Cài đặt các thư viện cần thiết (python 3.10)

- Clone dự án về và chạy dòng lệnh sau trên command Prompt để cài thư viện cần thiết:

  ``` bash
  pip install -r 'requirements.txt'
  ```

## 2. Chuẩn bị data
- **Bước 1:** Xóa sạch các thư mục trong foder `data_image_raw` nếu nó có tồn tại

- **Bước 2:**

  - Nếu đã có data về các gương mặt, chỉ cần thêm vào thư mục `data_image_raw` theo cấu trúc sau:

    Mỗi thư mục của mỗi người là ảnh cắt gương mặt của người đó:

    ```
    data_image_raw   
            ├── tên người thứ 1    
            ├── tên người thứ 2
            ├──  -------------    
            └── tên người thứ n
    ```

    > Số lượng các ảnh mỗi người nên đồng đều nhau và nên thu thập dữ liệu ở cùng một ví trí 


  - Nếu chưa có bất kỳ data nào (cần ít nhất 2 người để lấy data):

    - Vào file `main code\make_data_face` và chỉnh tên người cần lấy dữ liệu:
      
      > Truyền tên người cần lấy data vào dòng này trong file: 
        ```python
        MakeDataFace('Viet Anh')
        ```

      Nhìn thẳng vào camerea rồi bấm `run` để chương trình tự động lấy đủ 500 gương mặt. Nên quay nhiều hướng khác nhau để data đa dạng, tránh overfitting. Code tự điều chỉnh ánh sáng và tương phản nên không nhất thiết cần thu thập gương mặt mọi người ở cùng vị trí (nhưng có vẫn là hơn)

    - Làm tương tự cho những người còn lại đến khi hết.

      ![](https://raw.githubusercontent.com/vietanhlee/Face-Recognizer/refs/heads/main/display_github/thu%20thap.png)
      <p align = 'center'> Thu thập hình ảnh gương mặt </p>
    
      > Ảnh sau khi được thu thập sẽ được lưu vào thư mục `data_image_raw/ten_người_đó`


## 3. Xử lý data

- Chạy file `training_data.ipynb` để tiến hành xử lý dữ liệu thô sau đó training và xuất ra model cuối ở: `model/model_cnn.h5`.

## 4. Chạy code

Chỉ cần chạy file `main code\main.py` để bắt đầu sử dụng.
![](https://raw.githubusercontent.com/vietanhlee/Face-Recognizer/refs/heads/main/display_github/chay.png)
    <p align = 'center'> Chạy thử </p>

# Nhận xét

## Ưu điểm
- Mô hình huấn luyện tương đối hiệu quả trong phạm vi tập data lớn gồm nhiều gương mặt được train, 

- Phân loại hiểu quả hơn so với phương pháp chiết xuất đặc trưng của từng gương mặt và so sánh sự giống nhau của nó và chiết xuất đặc trưng dữ liệu cần được dự đoán khi đưa vào.

## Nhược điểm
- Dễ bị overfiting hoặc kém hiệu quả hơn với tập data ít, số người ít vì mô hình học được rất dễ bị một đặc điểm trội nào đó (màu sắc, góc độ) từ 1 gương mặt làm sai lệch đi kết quả dự đoán mặc dù đã tăng cường làm giàu dữ liệu như tăng giảm độ sáng và độ tương phản.

# Tích hợp thêm trên Qt5

Project tích hợp trên PyQt5 [tại đây](https://github.com/vietanhlee/face-recognition-Qt5)

![](https://github.com/vietanhlee/face-recognition-Qt5/blob/main/display_github/Screenshot%202025-02-10%20200413.png?raw=true)

<p align = 'center'> Demo Qt5 </p>
