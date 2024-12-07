## The JavaScript Engine and Runtime
### 1. Công cụ JavaScript hoạt động như thế nào
 
<img width="2230" alt="jsen" src="https://github.com/user-attachments/assets/ed870a64-2ef7-42e6-b035-05d2494f2551">

- Khi bạn chạy một ứng dụng ```JavaScript```, trình duyệt (hoặc môi trường thực thi như ```Node.js```) sử dụng một phần bộ nhớ RAM để cấp phát cho ```JavaScript Engine```.
- Bộ nhớ này được chia thành các phần như ```Heap``` và ```Stack```.
- Heap là một khu vực trong ```RAM``` được dùng để lưu trữ các ```Objects``` và dữ liệu phức tạp.

### 2. Compilation (Biên dịch) và Interpretation (Thông dịch)

***Hai phương pháp để chuyển đổi mã nguồn của một chương trình thành mã máy mà máy tính có thể hiểu và thực thi.***

 ***a. Biên dịch - Source code được biên dịch thành mã máy, sau đó mới được thực thi khi chạy chương trình.***
  ![image](https://github.com/user-attachments/assets/1f4903cf-023d-476d-844e-73ed5f48c5a5)
  - Toàn bộ source code được chuyển đổi thành mã máy (machine code) một lần và được ghi vào một tệp nhị phân có thể chạy trực tiếp trên máy tính.
  - C, C++, Java (phần bytecode), Rust
  
  ***b. Thông dịch - Source code được chuyển đổi thành mã máy và thực thi đồng thời từng dòng.***
  ![image](https://github.com/user-attachments/assets/91b6859d-8f35-4414-8294-63cf9f76d78f)
  -  Bộ thông dịch sẽ đọc và thực thi source code từng dòng một. Mã vẫn cần được chuyển đổi thành machine code và quá trình này diễn ra từng dòng khi chương trình đang chạy.
  -  Python, Ruby, PHP, JavaScript (truyền thống).

  ***c. Biên dịch JIT (just-in-time)- Source code được biên dịch thành mã máy và thực thi ngay sau khi biên dịch.***
   ![image](https://github.com/user-attachments/assets/4e41474e-cdea-4050-aa67-235ca1ac0e10)

  - Toàn bộ Source code được chuyển đổi thành machine code một lần và sau đó được thực thi ngay lập tức.
  - ***JavaScript với các engine hiện đại như V8 (trong Chrome và Node.js).***
  - Java với JVM (Java Virtual Machine).
    
![image](https://github.com/user-attachments/assets/3a2890db-bccd-4d2e-af65-225a6f64249d)

