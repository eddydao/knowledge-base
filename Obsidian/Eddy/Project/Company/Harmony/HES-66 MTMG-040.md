# Nguồn gốc của dữ liệu tồn kho
Hệ thống sử dụng ATP model để tính toán dữ liệu kho
Công thức: ( tồn kho) ATP = Physical stock - commited order

  ATP_QTY = SUM(STOCK_QTY) - SUM(ORDS_QTY)
  ATP_WGT = SUM(STOCK_WGT) - SUM(ORDS_WGT)

Tồn kho vật lý: View VW_STOCK1 -> ( tổng hợp dữ liệu từ TB_MCHB, TB_MCSD, TB_MSLB)

Committed order: 
- TB_ORDS_010/011 - Web orders (last 30 days)
- TB_ORDS_020/021 - Cutting orders (last 30 days)
- TB_ORDS_060/061 - Production orders (last 30 days)
- TB_RESB - Transfer orders (last 10 days)
- VW_VBAK_VBAP - SAP sales orders (last 60 days)

Hệ thống không tính đến các order bị block (CSPEM) trong công thức ( đơn hàng hỏng, legal, auditing,...)

# Check luồng phê duyệt của CSN
Service ngoài, unknown.

# Status trong màn MTMG-050
Thông báo quá trình gửi sang CSN thành công hay thất bại.

# Xử lý lỗi trong mtmg-040
Khi CSN có lỗi business, hệ thống set bản ghi có status là N và result code trả về là 2 
->  không thực hiện rollback  
-> Thay đổi dữ liệu:  
Dữ liệu lỗi được tính trong tồn kho trong vòng 10 ngày. Sau 10 ngày, dữ liệu lỗi không thấy trong dữ liệu truy vấn ra ( giá trị tồn kho bị thay đổi)