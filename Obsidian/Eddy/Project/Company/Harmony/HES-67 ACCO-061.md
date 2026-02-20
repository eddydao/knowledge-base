# Q&A
1. Nếu một vật liệu xuất hiện ở nhiều bảng nguồn ( mỗi màn hình trong list lấy dữ liệu ở 1 nguồn khác nhau) -> hiển thị thông tin cột: INIT_BRGEW (기초중량 ), RECV_BRGEW(기타입고중량) , LAST_BRGEW (기말중량) như thế nào
2. Bảng dữ liệu của màn acco_054 không có giá trị của plant -> nếu chọn lọc theo plant thì sẽ xử lý thế nào? - Dev đề nghị lọc plant cho dữ liệu từ source của 2 màn hình prco_451 và prco_411, lấy toàn bộ dữ liệu từ source của màn acco_054

# Notes
- update: đổi vị trí menu - cho xuống cuối ![[flow_2026-01-06_13254255.png]] 


# Sequence of cost
  Based on SAP ECC cost accounting standards and your codebase analysis:

  1. Raw Materials → 2. Finished Goods → 3. Cost of Goods Sold

  │  prco_411.html  │────>│  prco_451.html  │────>│  acco_054.html  │
  │   SEND_NETPR    │     │   SALE_NETPR    │     │     NETPR       │
  │ (Raw Material   │     │ (Finished       │     │ (COGS unit      │
  │  outgoing cost) │     │  product cost)  │     │  price)         │
        ↓                        ↓                        ↓
     MT 261/262              MT 101/102               MT 601
     Goods Issue          Goods Receipt          Goods Issue
     for Production      from Production         for Delivery

  Cost Flow Architecture

  Stage 1: Raw Material Consumption (prco_411)
  - Field: SEND_NETPR - 기타출고단가
  - Movement Type: 261 (Goods Issue for Order)
  - Accounting: CR Raw Material Inventory → DR Production Order

  Stage 2: Finished Goods Production (prco_451)
  - Field: SALE_NETPR - 당기출고단가
  - Movement Type: 101 (Goods Receipt from Production)
  - Accounting: DR Finished Goods Inventory → CR Production Settlement

  Stage 3: Cost of Goods Sold (acco_054)
  - Field: NETPR - 매출원가 단가
  - Movement Type: 601 (Goods Issue for Delivery)
  - Accounting: DR COGS Account → CR Finished Goods Inventory

  Validation from SAP ECC Standards

  Per SAP documentation, the cost accounting flow follows:
  1. Raw Materials (MAP valuation) → Consumed via MT 261
  2. WIP (Cost accumulation on production order)
  3. Finished Goods (Standard Price) → Received via MT 101
  4. COGS (Actual cost) → Posted via MT 601 on delivery

  Your three screens track this exact sequence: raw material outgoing → finished product → customer delivery COGS.

  Key Architectural Insight

  These aren't just cost fields - they represent different inventory valuation stages in the production lifecycle. Each screen monitors a different phase of the value chain transformation from raw materials to realized revenue.

⏺ I already answered you above - no report was created. Just gave you the direct answer about the production sequence:

  Yes, they follow a production line sequence:

  1. SEND_NETPR (prco_411) - Raw material outgoing cost
  2. SALE_NETPR (prco_451) - Finished goods production cost
  3. NETPR (acco_054) - Cost of goods sold

  Raw Materials → Finished Goods → COGS

  That's the SAP ECC production cost flow sequence.