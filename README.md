# How JavaScript Works Behind the Scenes
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

## Scope and The Scope Chain

***1. Các loại Scope trong JavaScript***

- ***Global Scope:*** Biến khai báo ngoài mọi hàm hoặc block, có thể truy cập từ mọi nơi trong chương trình.
  
```
  var message = "Global message";

function showMessage() {
  var message = "Local message"; // This "shadows" the global variable
  console.log(message); // Accessing the local variable => Local message
}

showMessage();
console.log(message); // Accessing the global variable
```

- ***Function Scope:*** Mỗi hàm tạo ra một scope riêng. Các biến khai báo trong hàm chỉ truy cập được trong hàm đó.

```
  function myFunction() {
  if (true) {
    var localVariable = "I'm in block scope";
    let blockVariable = "I'm also in block scope";
  }
  console.log(localVariable); // Accessible
  console.log(blockVariable); // Error: blockVariable is not defined
}
```

- ***Block Scope (từ ES6):*** Các block (cặp ngoặc {} như trong if, for) tạo scope riêng, nhưng chỉ áp dụng cho các biến khai báo bằng let và const.

```
if (true) {
  let blockVariable = "I'm in block scope";
  console.log(blockVariable);
}
// Accessing blockVariable here would result in an error
```
***2. Scope Chain***
- Mỗi scope luôn có thể truy cập tất cả các biến từ các ```outer scope``` của nó, nhưng không thể truy cập vào các ```inner scope```.
Quá trình tìm biến: ```Variable Lookup```
- Nếu không tìm thấy biến trong scope hiện tại, JavaScript sẽ tìm trong ``scope chain`` (các ```outer scope```).
- ```Một chiều:``` Scope không thể truy cập biến từ các inner scope hoặc sibling scope.

```
function testScope() {
    let outerVar = "Outer Scope";

    if (true) {
        let innerVar = "Inner Scope";
        console.log(outerVar); // Có thể truy cập outerVar
        console.log(innerVar); // Có thể truy cập innerVar
    }

    console.log(outerVar); // Có thể truy cập outerVar
    // console.log(innerVar); // Lỗi: innerVar is not defined
}

testScope();

Giải thích:
Scope của innerVar:

innerVar được khai báo bằng let trong block {} của if.
Nó chỉ tồn tại và có thể truy cập trong phạm vi block đó.
Scope của outerVar:

outerVar thuộc phạm vi toàn bộ hàm testScope.
Mọi scope bên trong testScope đều có thể truy cập outerVar.
```
## Variable Environment: Hoisting 

***1. Hoisting***
- Là hành vi đưa phần khai báo của ***hàm (Function)***, ***biến (let, const, var)*** hoặc ***lớp(class)*** lên đầu phạm vi mà chúng được định nghĩa và gán giá trị.
- Thực chất: Trình biên dịch JavaScript quét mã để tìm các khai báo biến trước khi thực thi, và các biến được thêm vào Variable Environment Object trong giai đoạn tạo Execution Context.

***Biến (Variable)***
- Với ```var:``` Chỉ khai báo được hoisted, không phải giá trị. Giá trị mặc định là ```undefined.```
```
console.log(x); // Output: undefined
var x = 5;
console.log(x); // Output: 5
```

```
x = 5;
console.log(x); // Output: 5
var x = 5;
```

- Với let và const: ```let``` và ```const``` được hoisted nhưng không thể truy cập trước dòng khai báo.

```
console.log(y); // ReferenceError: Cannot access 'y' before initialization
let y = 10;

console.log(z); // ReferenceError: Cannot access 'z' before initialization
const z = 15;
```

  
***Hàm (Function)***
- có 2 loại ```function declarations``` và ```function expressions```
- Các ```function declarations``` được hoisted hoàn chỉnh, nghĩa là bạn có thể sử dụng chúng trước khi khai báo.
```
sayHello(); // Output: "Hello!"

function sayHello() {
    console.log("Hello!");
}
```
- Các ```function expressions``` không hoạt động giống như vậy mà nó tương tự như (let, const, var).
```
console.log(multiply(2, 3)); // ReferenceError: Cannot access 'multiply' before initialization
const multiply = function(a, b) {
  return a * b;
};
```

```
sayHello(); // Kết quả: undefined is not a function

var sayHello = function() {
    console.log("Hello, world!");
};
```

***Lớp (Class)***
- Các ```class``` được ```hoisted```, nhưng không thể sử dụng trước khi khai báo.

```
const obj = new MyClass(); // ReferenceError: Cannot access 'MyClass' before initialization

class MyClass {
    constructor() {
        this.name = "Test Class";
    }
}
```
## Regular Functions và Arrow Functions
- ```Arrow Functions``` - một tính năng mới được giới thiệu trong ```ES6```
- Nếu bạn muốn viết code ngắn gọn hoặc làm việc với các phương thức xử lý mảng, thì ```Arrow functions``` sẽ là lựa chọn tốt hơn.

***1. Syntax***
- Syntax của một fuction bình thuờng:
```
let x = function function_name(parameters){ 
   // body of the function 
}; 
```

- Syntax của arrow functions:
```
let x = (parameters) => { 
    // body of the function 
}; 

```

***2. Từ khóa this***
```
let user = { 
    name: "GFG", 
    gfg1:() => { 
        console.log(this.name)
        console.log("hello " + this.name); // no 'this' binding here 
    }, 
    gfg2(){        
        console.log("Welcome to " + this.name); // 'this' binding works here 
    }   
 }; 
user.gfg1(); 
user.gfg2(); 
```
![image](https://github.com/user-attachments/assets/471dfd56-471c-4583-bd87-80fe09f94808)

***3. Arguments***
- ```Regular functions```
```
let user = {       
    show(){ 
        console.log(arguments); 
    } 
}; 
user.show(1, 2, 3); 
```
![image](https://github.com/user-attachments/assets/2847bac0-259e-492c-9a84-b4b03e576197)

- ```Arrow function```

```
let user = {      
        show_ar : () => { 
        console.log(...arguments); 
    } 
}; 
user.show_ar(1, 2, 3); 
```
![image](https://github.com/user-attachments/assets/7af215e0-e964-4b5e-84de-d6dfbd2da61d)

***4. Từ khóa new***
- ```Regular Function```
```
let x = function(){ 
    console.log(arguments); 
}; 
new x(1,2,3); 
```
![image](https://github.com/user-attachments/assets/04b44142-3202-4ad9-a61d-52f2e38a4f71)

- ```Arrow Function```
```
let x = ()=> { 
    console.log(arguments); 
}; 
new x(1,2,3); 
```
![image](https://github.com/user-attachments/assets/cdbe322e-61bd-47cd-838c-c6a6f382f0c8)

## Primitives và Objects (Kiểu nguyên thuỷ và Kiểu tham chiếu)

- ***Primitives***:  ```Number```, ```String```, ```Boolean```, ```Undefined```, ```Null```, ```Symbol```, ```BigInt```
- ***Objects***: ```Objects```, ```Array```, ```Functions``` 

## Toán tử(Operators) và chuỗi(String) 

***1. Destructuring Arrays***
- tính năng cho phép ***lấy các phần tử từ một mảng và gán chúng trực tiếp vào các biến riêng biệt.*** Thay vì sử dụng cú pháp truyền thống để chỉ ra chỉ số của từng phần tử trong mảng.
```
const [a, b, c, d] = numbers;
```

```
Có thể sử dụng default values để tránh lỗi undefined

const [first, second = 'default', third = 'default'] = [1, 2]; // third sẽ có giá trị là 'default'
```

***2. Destructuring Objects***
- ***Tính năng cho phép bạn lấy các thuộc tính từ một đối tượng và gán chúng trực tiếp vào các biến riêng biệt.***
```
const person = {
  name: 'John Doe',
  age: 30,
  location: 'New York'
};

const { name, age, location } = person;


const { name, age = 25, job = 'unemployed' } = person;
```
***3. Rest Pattern***
- ***Pattern rest trông giống hệt như operator spread. Cả hai đều có cú pháp giống nhau với ba dấu chấm nhưng thực hiện công việc ngược lại.***
 - ```Operator spread``` dùng để mở rộng một mảng hoặc truyền nhiều giá trị vào một hàm, biến nó thành các phần tử riêng lẻ.
 - ```Pattern rest``` dùng để gom các phần tử lại và đóng chúng vào một mảng, ngược lại so với operator spread.

```
const [a, b, ...others] = [2, 3, 4, 5];
console.log(a, b, others); // Kết quả: 2, 3, [4, 5]
```

```
const orderPizza = (mainIngredient, ...otherIngredients) => {
  console.log(mainIngredient, otherIngredients); // "mushrooms", ["onion", "olives", "spinach"]
};

orderPizza("mushrooms", "onion", "olives", "spinach");
```
***4. Nullish Coalescing (??)***
- Nếu toán hạng bên trái của toán tử ```??``` là ```null``` hoặc ```undefined,``` nó ```trả về toán hạng bên phải (giá trị mặc định)```
- Nếu toán hạng bên trái ```không phải là null hoặc undefined,``` nó ```trả về toán hạng bên trái.```
- Khác với toán tử ```OR (||)``` thông thường, chỉ trả về giá trị mặc định nếu biến là ```falsy (như 0, false, '', NaN).```

***5. Logical Assignment***

- ```&&=``` (Logical AND Assignment)
   - Sử dụng: ```x &&= y``` có nghĩa là ```x = x && y.```
   - Chỉ gán lại giá trị cho ```x nếu nó true``` và ```y khác false``` (```true hoặc null```, ```ndefined```, 0, ```NaN```, hoặc ```""``` sẽ là ```false```).
   - 
   ```
   let x = 5;
   x &&= 3; // x = 3, vì x là true và y khác false
   ```
- ```||=``` (Logical OR Assignment)
   - Sử dụng: ```x ||= y``` có nghĩa là ```x = x || y```.
   - Chỉ gán lại giá trị cho ```x nếu nó false và y không phải ```false``` (tức là y không phải ```null```, ```undefined```, 0, ```NaN, hoặc ""```).
   ```
   let x = 0;
   x ||= 3; // x = 3, vì x là false và y không phải false

   ```

- ```??=``` (Logical Nullish Assignment)
    - Sử dụng: ```x ??= y``` có nghĩa là ```x = x ?? y```.
    - Chỉ gán lại giá trị cho x nếu nó ```null``` hoặc ```undefined``` và y không phải ```null``` hoặc ```undefined```.
    ```
    let x = null;
    x ??= 3; // x = 3, vì x là null
    ```
***6. Set***
- Được sử dụng để lưu trữ các giá trị duy nhất. Các giá trị trong một ```Set``` không lặp lại và không có chỉ số, ```tương tự như mảng nhưng loại bỏ các giá trị trùng lặp.```
```
let numbers = [1, 2, 2, 3, 4, 4];
let uniqueNumbers = new Set(numbers); // uniqueNumbers sẽ chứa 1, 2, 3, 4
```
- ***Lợi ích của Set***
  - ```Loại bỏ trùng lặp:``` Set tự động loại bỏ các giá trị trùng lặp, giúp bạn dễ dàng kiểm soát và duy trì dữ liệu duy nhất.
  - ```Hiệu suất:``` Các phương thức của ```Set``` (như ```add, delete, has```) có thời gian phức tạp gần như O(1), tức là rất nhanh chóng.
  - ```Dễ dàng chuyển đổi sang mảng:``` Bạn có thể dễ dàng chuyển đổi một Set thành một mảng sử dụng Array.from() hoặc ...spread operator.


- Tạo 1 custom ```Set```
```
function MySet() {
    this.items = {};  // Dùng một đối tượng để lưu trữ các giá trị
    this.size = 0;    // Số lượng các giá trị trong `Set`

    // Thêm một giá trị vào `Set`
    this.add = function(value) {
        if (!this.has(value)) {
            this.items[value] = true;  // Đánh dấu giá trị là có trong `Set`
            this.size++;
        }
    };

   // Kiểm tra xem một giá trị có tồn tại trong `Set` hay không
    this.has = function(value) {
        return this.items.hasOwnProperty(value);
    };
.....
```
***7. Map***
- Khi bạn cần các khóa không phải chuỗi hoặc các khóa có thể lặp lại:
```
let map = new Map();
map.set(1, 'a');
map.set(1, 'b'); // Cập nhật giá trị của khóa 1
console.log(map.get(1)); // 'b'
```

- Khi bạn cần giữ thứ tự:
```
let map = new Map();
map.set('c', 3);
map.set('a', 1);
map.set('b', 2);

for (let [key, value] of map) {
  console.log(key, value);
}
// Output:
// 'c' 3
// 'a' 1
// 'b' 2
```
- ```Map``` cung cấp các phương thức hữu ích như ```has, get, set, delete, và clear``` giúp dễ dàng thao tác với dữ liệu.
```
let map = new Map();
map.set('apple', 1);
map.set('banana', 2);

console.log(map.has('apple')); // true
console.log(map.delete('banana')); // true
console.log(map.size); // 1
```
- Khi bạn muốn sử dụng ```entries``` hoặc ```forEach```
```
let map = new Map([
  ['apple', 1],
  ['banana', 2],
]);

map.forEach((value, key) => {
  console.log(key, value);
});
// Output:
// 'apple' 1
// 'banana' 2
```
- Khi bạn cần làm việc với các cặp ```khóa/giá trị``` phức tạp hoặc các dữ liệu liên kết:

## Lập trình Hướng Đối Tượng (OOP) Với JavaScript 

***1. OOP***
- OOP cho phép chúng ta mô phỏng các khía cạnh của thế giới thực bằng cách sử dụng các đối tượng có chứa dữ liệu (thuộc tính) và hành vi (phương thức). Nó giúp tổ chức code, làm cho mã trở nên linh hoạt và dễ duy trì hơn.

- Đối tượng: Các đối tượng là những khối mã tự chứa, có thể coi như những ứng dụng nhỏ. Chúng bao gồm dữ liệu và hành vi.
 ```
const user = {
  username: 'john_doe',
  password: '123456',
  email: 'john@example.com',
  login: function() {
    console.log(`${this.username} has logged in.`);
  },
  sendMessage: function(message) {
    console.log(`${this.username} sent a message: ${message}`);
  }
};
```
- Lớp : Các ```Class``` đóng vai trò là bản thiết kế để tạo ra các đối tượng. Chúng định nghĩa những gì mà một đối tượng cần chứa và hành vi của nó.
```
class User {
  constructor(username, password, email) {
    this.username = username;
    this.password = password;
    this.email = email;
  }

  login() {
    console.log(`${this.username} has logged in.`);
  }

  sendMessage(message) {
    console.log(`${this.username} sent a message: ${message}`);
  }
}

```
- Đóng gói: Đóng gói liên quan đến việc giữ một số thuộc tính và phương thức riêng tư bên trong một lớp học, ngăn không cho mã bên ngoài thao tác trực tiếp vào trạng thái bên trong.
 ```
class User {
  constructor(username, password, email) {
    this.username = username;
    this.password = password;
    this.email = email;
  }

  login() {
    console.log(`${this.username} has logged in.`);
  }

  // Method is private, cannot be accessed outside the class
  #checkSpam(message) {
    // Logic to check if message is spam
    return false;
  }
}
```
- Kế thừa: Kế thừa cho phép một lớp (lớp con) thừa kế các thuộc tính và phương thức từ một lớp khác (lớp cha), thúc đẩy việc tái sử dụng mã.
 ```
class Admin extends User {
  constructor(username, password, email, adminLevel) {
    super(username, password, email); // Thừa kế các thuộc tính từ lớp cha
    this.adminLevel = adminLevel;
  }

  manageSystem() {
    console.log(`${this.username} manages the system.`);
  }
}
```
- Đa hình: Đa hình cho phép một lớp con ghi đè phương thức được thừa kế từ lớp cha, cung cấp các triển khai khác nhau cho các đối tượng khác nhau.
```
class Author extends User {
  constructor(username, password, email, books) {
    super(username, password, email); // Thừa kế các thuộc tính từ lớp cha
    this.books = books;
  }

  login() {
    console.log(`${this.username} logged in as an author.`);
  }
}
```
***2. Setters và Getters***
- ```Getters``` dùng để lấy giá trị (như thuộc tính bình thường nhưng có thể bao gồm logic).
- ```Setters``` dùng để đặt giá trị và thường được sử dụng để ***kiểm tra hoặc xử lý dữ liệu trước khi lưu***.

```
class Person {
  constructor(birthYear) {
    this.birthYear = birthYear;
  }
  get age() {
    return new Date().getFullYear() - this.birthYear;
  }
}
const jessica = new Person(1990);
console.log(jessica.age); // Output: 34 (năm 2024)
```

```
class Person {
  set fullName(name) {
    if (name.includes(' ')) {
      this._fullName = name;
    } else {
      console.error('Not a valid full name');
    }
  }
  get fullName() {
    return this._fullName;
  }
}
const walter = new Person();
walter.fullName = 'Walter White';
console.log(walter.fullName); // Output: "Walter White"
walter.fullName = 'Walter';
// Output: "Not a valid full name"
```

***3. Static Methods***
- Dùng để cung cấp các tiện ích hỗ trợ hoặc xử lý dữ liệu chung cho lớp/hàm tạo mà không cần liên quan đến các instance cụ thể.
- Không thể truy cập từ instance, chỉ thông qua lớp hoặc hàm tạo.
```
class Person {
  constructor(name) {
    this.name = name;
  }
  static hey() {
    console.log('Hey there! 👋');
  }
}
Person.hey(); // Output: Hey there! 👋
```












