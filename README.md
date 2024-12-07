## The JavaScript Engine and Runtime
### 1. JavaScript engine hoạt động như thế nào
 - ***JavaScript engine đơn giản là một chương trình máy tính thực thi Code JS từ dạng có thể đọc được của con người thành hướng dẫn mà phần cứng máy tính có thể hiểu và thực thi.***
 - ***Trình duyệt dựa vào v8 Engine (JavaScript engine), còn khi bạn chạy code ở local thì phần cần đến môi trường Node.js***
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
    
 ### 3. JIT trong JS hoạt động thế nào
  ![image](https://github.com/user-attachments/assets/dc6a50ef-5564-4ec5-b2b3-6085cf794253)

  ***Parsing (Phân tích cú pháp):***
  - Khi mã ```JavaScript``` được đưa vào engine, bước đầu tiên là parse mã để tạo ```AST (Abstract Syntax Tree)```.
  - ```AST``` là cấu trúc dữ liệu biểu diễn mã nguồn dưới dạng cây, giúp kiểm tra cú pháp và chuẩn bị cho quá trình dịch sang mã máy.

 ***Compilation (Biên dịch):***
  - Dựa trên ```AST```, mã ```JavaScript``` được biên dịch thành mã máy.
  - Trong quá trình này, mã máy ban đầu được tạo có thể không tối ưu để chương trình có thể thực thi ngay lập tức.

 ***Execution (Thực thi):***
  - Mã máy được chạy ngay lập tức trong ```call stack```.

***Optimization (Tối ưu hóa):***
  - ```JS engine``` tiếp tục tối ưu và biên dịch lại mã máy ngay cả khi chương trình đang chạy.
  - Quá trình này diễn ra ở hậu trường để cải thiện hiệu năng.
 
 ### 4. Runtime trong Broswer
***Trình duyệt là một môi trường, để thực thi ```Code JS```, và nó cũng cung cấp những ```API```có sẵn để thể tương tác với ```DOM``` hay ```CSSOM``` cũng như với  hệ điều hành hoặc phần cứng.***
 
 ***Giải thích một xíu về API mà trình duyệt cung cấp:***
 - Mặc dù nó được viết bằng JavaScript nhưng không phải là code JavaScript thông thường mà là các interface mà trình duyệt cung cấp để JavaScript có thể tương tác với các phần tử của trang web.
 - ```DOM API``` (Document Object Model API): Được cung cấp bởi trình duyệt, cho phép JavaScript tương tác với các phần tử HTML trên trang, truy cập, sửa đổi và tạo các phần tử mới.
 - ```CSSOM API``` (CSS Object Model API): Cung cấp các phương thức để thao tác với các quy tắc CSS của trang web.
 - Web API: Bao gồm ```window, fetch, localStorage, sessionStorage, WebSocket, Geolocation, v.v.,``` cung cấp các phương thức để giao tiếp với dịch vụ bên ngoài và dữ liệu lưu trữ.
    
 ![image](https://github.com/user-attachments/assets/c1dca981-09ef-4cfc-aeb0-e652d40ff787)

 ***Callback Queue (hay Task Queue):***
 - chứa các callback từ các sự kiện người dùng như ```click, keydown```, và các tác vụ bất đồng bộ như ```setTimeout```.
 - Callback Queue có độ ưu tiên thấp hơn ```Microtask Queue``` nên các ```callback``` trong ```Callback Queue``` được đưa vào sau khi các tác vụ từ ```Microtask Queue``` đã được xử lý xong và ngăn xếp gọi (Call Stack) trống.

 ***Microtask Queue:***
 - ```Microtask Queue``` chứa các callback từ các tác vụ như ```Promise, Async Awai, observable```.
 - Nó ưu tiên hơn ``Callback`` Queue nên thực thi ngay sau ```call task``` trống.
   
***[Xem thêm video để hiểu rõ hơn cách chúng thực thi](https://www.youtube.com/watch?v=eiC58R16hb8)***













