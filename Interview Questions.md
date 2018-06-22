# <p align="center"> **14**
## <p align="center"> Java
Trong khi các câu hỏi liên quan đến Java được tìm thấy xuyên suốt quyển sách này, thì chương này dành cho các câu hỏi liên quan về ngôn ngữ và cú pháp. Những câu hỏi như vậy không phổ biến ở các công ty lớn vì những công ty đó thích kiểm tra năng lực ứng viên hơn là kiến thức của họ (và vì họ sẽ dành thời gian và nguồn lực để dạy cho ứng viên một ngôn ngữ cụ thể). Tuy nhiên, các câu hỏi này có thể lại phổ biến ở một số công ty khác.

**Hướng tiếp cận**

Vì những câu hỏi như thế này sẽ tập trung chủ yếu vào kiến thức, nên việc nói về cách tiếp cận vấn đề sẽ không được hay lắm. Nhưng nói cho cùng thì có phải chỉ cần biết được câu trả lời chính xác là được hay không?

Phải mà cũng chưa phải. Dĩ nhiên, việc tốt nhất có thể làm để có thể vượt qua những câu hỏi như vậy là phải học Java kỹ lưỡng cả bên trong lẫn ngoài. Tuy nhiên, nếu vẫn còn mơ hồ, bạn có thể thử bàn luận về chúng bằng cách tiếp cận dưới đây:
1.	Cho một ví dụ về kịch bản (scenario), và tự hỏi bản thân có những trường hợp nào xảy ra
2.	Tự hỏi bản thân các ngôn ngữ khác nhau sẽ giải quyết cùng một kịch bản này như thế nào
3.	Thử tưởng tượng nếu là một người tạo ra ngôn ngữ (language designer), bạn sẽ thiết kế như thế nào trong tình huống này. Ý nghĩa của mỗi lựa chọn thiết kế là gì?

Nhà tuyển dụng sẽ ấn tượng nhiều hơn nếu bạn có thể rút ra được câu trả lời thay vì biết kiến thức đó một cách cứng nhắc. Đừng nói dối để qua mặt nhà tuyển dụng, hãy trả lời họ rằng “Tôi không chắc là nhớ được câu trả lời, nhưng để thử xem tôi có hiểu đúng hay không. Giả sử chúng ta có đoạn code như thế này…”

**Từ khóa final**

Từ khóa final trong Java có một nghĩa khác tùy thuộc xem nó là một biến, lớp hay phương thức
*	_Biến_: Giá trị của biến này không thay đổi được một khi được khởi tạo
*	_Phương thức_ (method): Các phương thức có từ khóa final sẽ không cho phương thức từ lớp con (subclass) ghi đè lên được
*	_Lớp_ (class): Một lớp có từ khóa final là lớp không có bất kỳ lớp con nào

**Từ khóa finally**

Từ khóa finally được dùng trong trong khối lệnh try/catch và đảm bảo cho đoạn code bên trong được thực thi, ngay cả khi có lỗi biệt lệ (exception). Khối lệnh finally sẽ được thực thi sau khối lệnh try và catch, nhưng lại trước khi điều khiển chuyển ngược về gốc

Hãy xem ví dụ dưới đây diễn ra thế nào: 
```java
public static String lem() {
   System.out.println("lem");
   return "return from lem";
 }

 public static String foo() {
    int x = 0;
    int y = 5;
    try {
        System.out.println("start try");
        int b = y / x;
        System.out.println("end try");
        return "returned from try";
    } catch (Exception ex) {
        System.out.println("catch");
        return lem() + " | returned from catch";
    } finally {
        System.out.println("finally");
    }
 }

 public static void bar() {
    System.out.println("start bar");
    String v = foo();
    System.out.println(v);
    System.out.println("end bar");
 }

 public static void main(String[] args) {
    bar();
 }
```
Kết quả của đoạn code sẽ là: 
```
start bar
start try
catch
lem
finally
return from lem | returned from catch
end bar
```
Chú ý kỹ tại dòng thứ 3 và 5 của output. Khối lệnh catch được thực thi toàn bộ (bao gồm lời gọi hàm và lệnh return), sau đó đến khối lệnh finally, sau cùng là hàm trả về giá trị.

**Phương thức finalize**

Cơ chế gom rác tự động gọi đến phương thức finalize() ngay trước khi hoàn toàn loại bỏ đối tượng. Vì thế một lớp có thể ghi đè phương thức finalize() từ lớp Object để định nghĩa các hành động tùy chỉnh trong quá trình gom rác.
```java
protected void finalizeQ throws Throwable {
 /* Close open files, release resources, etc */
}
```
**Overloading vs Overriding**

Nạp chồng (overloading) là thuật ngữ để diễn tả có hai phương thức có cùng tên nhưng khác về số lượng hoặc kiểu dữ liệu của tham số đầu vào.
```java
public double computeArea(Circle c) { ... }
public double computeArea(Square s) { ... }
```
Mặt khác, ghi đè (Overriding) xảy ra khi một phương thức viết lại cả tên lẫn dấu hiệu phân biệt cho một phương thức có trong lớp cha của lớp hiện tại
```java
public abstract class Shape {
    public void printMe() {
        System.out.println("I am a shape.");
    }
public abstract double computeAreaQ;
}

public class Circle extends Shape {
    private double rad = 5;
    public void printMeQ {
    System.out.println("I am a circle.");
    }

    public double computeAreaQ {
    return rad * rad * 3.15;
    }
}

public class Ambiguous extends Shape {
    private double area = 10;
    public double computeAreaQ {
    return area;
    }
}

public class IntroductionOverriding {
    public static void main(String[] args) {
        Shape[] shapes = new Shape[2];
        Circle circle = new CircleQ;
        Ambiguous ambiguous = new Ambiguous();

        shapes[0] = circle;
        shapes[l] = ambiguous;

        for (Shape s : shapes) {
            s.printMeQ;
            System.out.println(s.computeArea());
        }
    }
}
```
Đoạn code trên sẽ in ra kết quả
```
I am a circle.
78.75
I am a shape.
10.0
```
Để ý rằng lớp Circle đã ghi đè phương thức printMe(), trong khi lớp Ambiguous sử dụng phương thức này như bình thường

**Collection Framwork**

Nền tảng tập hợp của Java (Java’s collection framework) hữu ích đến không ngờ, và bạn sẽ thấy nó được sử dụng xuyên suốt quyển sách. Dưới đây là một vài phần hữu ích nhất:
ArrayList: Một ArrayList là một mảng có thể thay đổi kích thước một cách linh động, tự động tăng khi thêm một phần tử.
```java
ArrayList<String> myArr = new ArrayList<String>();
myArr.add("one");
myArr.add("two");
System.out.println(myArr.get(0)); /* prints <one> *
```
_Vector_: vector rất giống với ArrayList, nhưng khác ở điểm nó được đồng bộ hóa. Cú pháp của nó cũng giống ArrayList.
```java
Vector<String> myVect = new Vector<String>();
myVect.add("one");
myVect.add("two");
System.out.println(myVect.get(0));
```
_LinkedList_: LinkedList là một lớp có sẵn trong Java. Mặc dù nó hiếm khi có trong các buổi phỏng vấn, nhưng lại hữu ích trong học tập bởi vì chúng minh họa một vài cú pháp cho Iterator
```java
LinkedList<String> myLinkedList = new LinkedList<String>();
myLinkedList.add("two");
myLinkedList.addFirst("one");
Iterator<String> iter = myLinkedList.iteratorQ;
while (iter.hasNextQ) {
    System.out.printIn(iter.next());
}
```
_HashMap_: Tập hợp Hashmap được sử dụng rất rộng rãi, cả trong các buổi phỏng vấn lẫn trong thực tế. Một đoạn code về hashmap được trích ra như sau:
```java
HashMap<String, String> map = new HashMap<String, String>();
map.put("one", "uno");
map.put("two", "dos");
System.out.printIn(map.get("one"));
```
Trước buổi phỏng vấn, bạn nên đảm bảo bạn hoàn toàn hiểu được các cú pháp trên đây, bởi vì bạn sẽ cần đến nó.

---
**Các câu hỏi phỏng vấn**
---
---


Hãy ghi lại chúng vì hầu như mọi bài giải trong quyển sách này đều sử dụng Java, chúng tôi chỉ chọn ra một số ít câu hỏi dành cho chương này. Hơn nữa, các câu hỏi này hầu như đều mang tính chất “đánh đố” của các ngôn ngữ, bởi vì phần sau của quyển sách gần như toàn là các câu hỏi về lập trình Java

14.1 Trong kế thừa, ý nghĩa của việc khai báo constuctor là private là gì ?

14.2 Trong Java, khối lệnh trong finally có được thực thi nếu chúng ta thêm câu lệnh return trong khối lệnh try trong cấu trúc try-catch-finally hay không ?

14.3 Phân biệt các từ khóa final, finally, finalize ?

14.4 So sánh sự khác biệt giữa templates trong C++ và generics trong Java ?

14.5 Object reflection trong Java là gì và tại sao nó lại hữu ích ?

14.6 Cài đặt lớp CircularArray hỗ trợ cấu trúc dữ liệu giống mảng mà có thể xoay một cách hữu hiệu. Class này nên là kiểu generic, và hỗ trợ con trỏ duyệt bằng cú pháp `for (Obj o : circularArray)` ?

Các câu hỏi thêm: Mảng và chuỗi (#1.4), thiết kế hướng đối tượng (#8.10), đa luồng và khóa (Threads and Locks) (#16.3)
