OOP gồm có 4 nguyên lí cơ bản:
+ Abstraction ( trừu tượng)
+ Inheritance ( thừa kế)
+ Polymorphism ( đa hình)
+ Encapsulation ( bao đóng)
4 nguyên lý này liên hệ mật thiết với nhau, lấy tính trừu tượng hoá làm gốc

# Abstraction ( trừu tượng hoá)
Được hiểu là các hành vi của một đối tượng A, cách thực hiện hành vi đó bên trong đối tượng không được để lộ ra ngoài cho các đối tượng khác thấy, thay vào đó các đối tượng khác chỉ có thể thấy được để thực hiện hành vi đó, đối tượng A sẽ cần đầu vào là gì và cho ra kết quả là gì

Tính trừu tượng được thể hiện trong Java thông qua Interface và Abstraction class
Tính trừu tượng liên quan đến hành vi của đối tượng ( methods trong class Java)

## Interface
Định nghĩa một nhóm method ( hành vi) chung, các class thể hiện interface đó cần implement các method này
Không chứa thân phương thức
```java
public interface MyInterface {
	public int getPersonAgeById(int personId);
	public String getPersonNameById`(int personId);
}
```

Trong Java 8, default method cho interface được giới thiệu, cho phép viết code cho một phương thức xuất hiện trong interface của java
```java
public interface MyInterface{
	default int getPersonAgeById(int personId){
		// code to get person age by id
		return personAge;
	}
}
```

So sánh Interface default method với Abstraction class [[Interface default method vs Abtract class]]

# Encapsulation ( Bao đóng)
Được hiểu là các đối tượng khác không thể truy cập và thay đổi giá trị thuộc tính của một đối tượng mà cần thông qua các phương thức của đối tượng đó.
Tính bao đóng liên quan đến thuộc tính của đối tượng, thể hiện qua access modifier

# Tính thừa kế
Một đối tượng B có thể sử dụng lại các thuộc tính và phương thức của đối tượng A, tăng tính tái sử dụng code.

Thể hiện bằng cách sử dụng từ khoá `extends`
```java
public class B extends A {
// code
}
```

> Lưu ý: sử dụng tính kế thừa đối với các đối tượng có quan hệ is-a, tức là đối tượng B là một loại A
> Các đối tượng có quan hệ has-a ( ví dụ như một văn phòng có nhiều nhân viên) thì cần sử dụng [[Project/Blog/Inheritance vs Composition]]
# Tính đa hình
Thể hiện ở việc một phương thức có thể có các hành vi khác nhau dựa vào ngữ cảnh sử dụng

Trong java, có 2 kiểu
- Đa hình trong biên dịch ( Overload): trong một class, có nhiều phương thức cùng tên nhưng khác kiểu dữ liệu của tham số hoặc khác số lượng tham số
- Đa hình trong runtime ( Override): phương thức ở class con ghi đè lên phương thức ở class cha để thực hiện hành vi riêng của phương thức tại class con
