# Unity Doesn't Recreate FirebaseApp.dll in Plugins/Android

## Vấn đề: 
- Khi tôi làm một sản phẩm game mới và sử dụng lại template của một game cũ trước đó. Trong folder `Assets/Plugins/Android/FirebaseApp.dll` nó sẽ không tạo lại file `FirebaseApp.dll` mặc dù đã Force Resolve nhưng không được (có đôi lần tôi xoá đi và play game trên editor thì nó tự tạo lại fire `FirebaseApp.dll` và vô tình lại xử lý được vấn đề này =))) ), còn phần lớn các lần khác thì xoá đi là mất hút luôn và không tự tạo lại.

<img width="846" alt="Screenshot 2025-03-23 at 19 54 33" src="https://github.com/user-attachments/assets/addccf6f-36bd-417a-854b-5cc3976f1209" />

## Hậu quả
- Nếu xoá `FirebaseApp.dll` đi khỏi folder Plugins thì tất cả dịch firebase sẽ không sử dụng được
- Nếu không xoá đi đồng thời Unity không làm mới lại `FirebaseApp.dll` thì các dịch vụ firebase của game mới tạo sẽ không được đẩy lên firebase console (nó có thể sẽ đẩy lên console của game trước đó)
## Mong muốn
- `FirebaseApp.dll` của game mới được tạo phải mang đúng thông tin của game này để có thể đẩy được tracking hoặc fetch được giá trị remote config từ firebase console (hoặc các dịch vụ khác cũng tương tự)
## Cách xử lý
- Mở file FirebaseApp.dll theo đường dẫn `Assets/Plugins/Android/FirebaseApp.androidlib/res/values/google-services.xml` bằng ide hoặc các công cụ text editor
- Mở file `google-service.xml`
<img width="1403" alt="Screenshot 2025-03-23 at 20 03 38" src="https://github.com/user-attachments/assets/528e4654-31f1-44d8-bce3-879aed71fb74" />

- Mở tiếp file `google-service.json` theo đường dẫn `Assets/google-service.json`

<img width="1403" alt="Screenshot 2025-03-23 at 20 08 10" src="https://github.com/user-attachments/assets/e8b8e471-36d4-4f72-af4a-05da5e7a4e27" />

- Đối chiếu thông tin và sửa lại file `google-service.xml` của `FirebaseApp.dll` sao cho thông tin đồng nhất với `google-service.json`

|google-service.xml|google-service.json|
|gcm_defaultSenderId|tương ứng với gcm_defaultSenderId|
