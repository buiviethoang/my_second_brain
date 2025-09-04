2025-08-30 09:31
Status: #baby
Tags: [[productivity]]
## Main




Giả sử bạn là người ra đề. Liệu bạn sẽ hỏi học sinh/ sinh viên câu hỏi gì?
Phương pháp ghi nhớ hiệu quả: Tưởng tượng và liên kết. 
Những cái gì quá trừu tượng thì ta liên kết với những thứ rõ ràng
Những ví dụ quá general thì ta làm cho nó specific thông qua những ví dụ rất là concrete

Luyện tập active recall như nào cho hợp lí? 
## 1. Luyện tập thói quen không nhìn vào tài liệu/ lời giải
Cái này khá tốt và khá hữu ích. Thay vì việc cứ chăm chăm nhìn vào lời giải thì ta bắt não bộ phải hoạt động và suy luận để trích xuất, lấy lại những dữ liệu cần thiết. Việc này sẽ giúp những thông tin được xử lí sẽ hằn sâu vào trong đầu ta hơn khi không làm như vậy. 
Một giải pháp khác là tra cứu theo keyword trên mạng để có thể hiểu hơn (cái này mình nghĩ phần nhiều sẽ dùng cho dân lập trình nhiều hơn) về đề tài, sau đó từ những dữ kiện thu được sẽ thực hiện giải bài. => Luyện tư duy khá tốt đó. 
## 2. Phần kiến thức rộng và phức tạp: Vẽ sơ đồ cho cả chương
Phần này thì mình chưa làm được. Chắc phải học cách vẽ Mindmap để giải quyết các vấn đề gặp phải thôi.
## 3. Tự hỏi và tự trả lời
Phần này good. Có lẽ cái khó nhất là đưa ra được bộ câu hỏi hợp lí và có ý nghĩa. Khi đó thì mới không để lọt kiến thức mà có khi lại còn tìm ra được rất nhiều ý mà bình thường học thụ động khó mà nghĩ ra được. 
Nhiệm vụ bây giờ: tìm ra bộ câu hỏi cho riêng mình. 
## 4. Làm flashcard
Đang thực hiện. Cái này để sau đi
## 5. Dạy lại cho người khác
Cái này sẽ thực hiện khi ôn tập. Sẽ tự hỏi vào tường và cố gắng dạy cho tường biết được những gì mình đã học. Nếu mà không đủ rõ, có nghĩa là kiến thức mình chưa đủ => Tìm hiểu thêm để hệ thống lại toàn bộ những gì mình có. Ok. Sẽ thực hiện 
## 6. Làm 1 bài test thử
Cái này chắc phải đến gần lúc thi thôi à. Chứ bình thường thì cũng không cần thiết phải như vậy. Điểm khó là tìm tài liệu và chọn lọc các câu hỏi có giá trị

# Các câu hỏi có thể đặt ra để hệ thống hóa kiến thức: 
? Phần đó nói về điều gì? Mục đích mà nó muốn hướng đến? Các khái niệm có thể có
? Tại sao phải nói về nó? 
? Nội dung chính là gì? Nếu là 1 quy trình thì các bước ở đây là gì. Giải thích ý nghĩa các bước?
? Ý nghĩa của nó trong 1 task/ 1 trường hợp là gì hay nó phục vụ cho bài toán/ task nào? 
? Ảnh hưởng/ tác động của nó lên cái task đó là ntn? Kể ra những ưu và nhược điểm của nó? 
? Nó có liên quan gì đến môn học và liên quan gì đến ta mà ta cần phải học? 

Ví dụ: Với bài phân tích trên trang: https://www.geeksforgeeks.org/object-detection-vs-object-recognition-vs-image-segmentation/ 

- Phần đó nói về điều gì? 
	-	So sánh giữa object detection vs object recognition vs image segmentation. 
	-	Mục đích là để phân biệt giữa chúng để ta không bị gọi nhầm tên các task
	-	Khái niệm: 3 khái niệm chính (tự liệt kê) 
- Tại sao phải nói về điều này? 
	-	Rất quan trọng. Giúp ta hiểu được rõ hơn giữa các task vụ trong CV
- Nội dung chính: 
	- Object recognition:
		- Sử dụng ML và image processing hoặc là sử dụng thuần CV:
			- Hog-SVM
			- Bag of features
			- Viola-Jones Algo
		- Sử dụng model Deep learning:
			- CNN
		- Những thách thức của object recognition: 
			- Output là single class label => CNN sẽ ko detect được nếu bài toán có nhiều hơn 1 class labels cho 1 image
			- Không biết được vị trí của object 
	- Object detection:
		- Image classification
		- Object localization
		- Những thách thức:
			- Object ko có hình dạng là hcn => rectangle bb ko ỏn
			- ko dùng để đo được những vùng, diện tích chiếm của object
	- Image segmentation:
		- Instance seg
		- Semantic seg
	- Ứng dụng: 
		- Tự liệt kê
- Nó phục vụ bài toán nào? 
	- Phần ứng dụng có nói
- Ưu và nhược điểm của các phương pháp được nói đến trong bài? 
	- Tự suy luận và rút ra từ việc đọc
- Nó có liên quan gì đến ta? 
	- Giúp ta phân biệt được rõ hơn 1 số task trong bài học của môn học CV


Nên lấy ví dụ ở các phần breakdown nhỏ nhất (ở mức node lá trong cây phân cấp)

## References
