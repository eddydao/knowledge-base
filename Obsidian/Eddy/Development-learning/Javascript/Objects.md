#javascript 

# Object creation

Cách dùng thường gặp nhất là dùng object literal:
```javascript
const myObject = {
	property: ‘Value!’,
	otherProperty: 77,
	“string property”: function() {
		// some code do stuffs
	}
}
```

Có 2 cách để lấy dữ liệu từ một obj:
- dot notation: `myObject.property;`
- bracket notation: `myObject[”string property”];`

Dot notation thường được dùng hơn, tuy nhiên trong một số trường hợp như property có dấu cách ở giữa thì sẽ cần dùng bracket notation

## Tạo object thông qua hàm taoj

```javascript
function Player(name, marker){
	this.name = name;
	this.market = market;
}
```

Sử dụng bằng cách dùng từ khoá `new`
```javascript
const player = new Player(‘steve’, ‘X’);
```

Code đầy đủ:
```javascript
function Player(name, marker){
	if(!new.target){
		throw Error(“Must use ‘new’ keyword to call the operator”);
	}
	this.name = name;
	this.marker = marker;
	this.function = function() {
		// code block
	}
}
```

## The prototype
Mọi object đều có một prototype => mọi obj đều thừa kế từ một obj nào đó => các obj có thể access vào các phương thức hoặc thuộc tính của `prototype`

```javascript
Player.prototype.sayHello = function() {
	console.log(“Hello, I’m a player”);
}

player1.sayHello();
player2.sayHello();
```

=> Do phương thức `sayHello` được định nghĩa trong prototype của Player => player1 và player 2 có thể sử dụng phương thức này

**Access an object’s prototype**
```javascript
Object.getPrototypeOf(player1) === Player.prototype;
```
Phương thức `getPrototypeOf()` lấy ra property `.prototype` của Object Constructor

**Object.getPrototypeOf() vs .___proto___ vs [[Prototype]] **


**Mục đích sử dụng của prototype**
1. Định nghĩa thuộc tính và phương thức common trong mọi obj với `prototype` để tiết kiệm bộ nhớ (memory)
2. Thực hiện kế thừa nguyên mẫu: cho phép đối tượng khác nhau sử dụng các phương thức chung

```javascript
Object.getPrototypeOf(Player.prototype) === Object.prototype; //(1)

player1.valueOf(); // (2)
```

=> (1): `Player.prototype` có giá trị của `Object.prototype`
=> (2): `valueOf` function được định nghĩa ở `Object.prototype` dẫn đến việc nó cũng xuất hiẹn ở `Player.prototype`

Cách kiểm tra phương thức có nằm trong `prototype` hay không:
`player1.hasOwnProperty(’valueOf);`

