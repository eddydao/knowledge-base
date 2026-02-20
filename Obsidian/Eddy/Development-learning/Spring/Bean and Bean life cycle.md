# Bean
Là một object được tạo ra và quản lý bởi Spring IoC container ( ApplicationContext)

# Bean life cycle
## Bean scope
- singleton: một instance sử dụng trong suốt quá trình chạy của proj
- prototype: tạo instance mới khi có yêu cầu
- request: tạo instance cho một http request
- session: tạo instance cho một http session
- application: tạo instance cho một vòng đời của ServletContext
- WebSocket: tạo instance cho một WebSocket session

## Bean life cycle
- Definition: Khởi tạo qua anno hoặc xml
- Instantiation: khởi tạo bean và đưa vào ApplicationContext
- 