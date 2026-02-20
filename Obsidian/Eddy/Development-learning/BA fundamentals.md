1. 1. Vẽ userflow e2e (tool draw.io, dùng UML vẽ, xịn thì tool machination),
2. Từ userflow chia module tính năng (theo user nha, đừng theo tech aspect),
3. Từ module chia thành các userstory, cố gắng chia nhỏ thành từng màn hình hoặc nhóm màn hình dưới 8pt,
4. Hoàn thiện từng userstory:,
    
    a. UI overview: vẽ nhanh wireframe (tool Baslamiq) b. Element explaination c. Acceptance Criteria (viết bằng BDD cucumber) d. Tech note nếu có 
    Keyword nào chưa biết thì search nhanh rồi học qua là dk
    Phần 4 nếu dự án siêuuu đơn giản thì cắt luôn b, c, d cũng dk. Mỗi cái US theo format 
    As a 
    I want to 
    So that 
    Với cái wireframe là ok rồi, độ linh hoạt cao, chi tiết dev tự quyết định cũng dk. Chú ý trong code mng làm sao cho thống nhất giữa các dev là dk (edited)


Machination -> tìm hiểu Framework


1. Về self-test thì nên tham khảo kĩ thuật tính case của manual tester, keyword: EP, BVA, Decision table và Transition State
    
    Tính cho đủ case code cover đủ thì mai mốt đỡ phải fix bug