# Harmony PICs



# App installed location

## Warp
C:\Users\Eddie\AppData\Local\Programs\Warp

## Vim
C:\Program Files\Vim

## Notepad ++
C:\Program Files\Notepad++

## Intellij
C:\Program Files\JetBrains\IntelliJ IDEA 2025.2

## VsCode
C:\Users\Eddie\AppData\Local\Programs\Microsoft VS Code

## Java JDK
C:\Users\Eddie\.jdks\azul-1.8.0_462

## HeidiSQL
C:\Users\Eddie\AppData\Local\Programs\HeidiSQL

# Account

## VPN
marusys09/hvn032025@!   mail otp pass: Changeme00@!    br0ac2it

marusys01 / Humax2024@! (Save Jacob)
marusys02 / 
@Lovebum91
marusys08/!Nguyenhoang19 (Huang)
marusys09/hvn032025@! (Peanut)
marusys12/ Menu00d1@ (Zed)   - GMS

marusys07 / Hoanguyen12#

## Mail OTP VPN 
https://email.humaxdigital.com/owa
tqtrung@humaxdigital.com/hvn062025@!  / n0tPubl1c@

## AI tool

### ChatGPT:
co_mvn_license@marusysvina.com
Marusys@!#2025

### Copilot
nhquang@humaxdigital.com
@Lovebum91

## Windows Server Remote (AI Portal)
Public IP: 183.91.13.5
IP: 192.168.100.164
ID: Joey
PW: Marusys@2025

## GMS dev Server
IP: 192.168.100.180
ID: mvn
MK: 123456

dbc-url: jdbc:log4jdbc:mariadb://192.168.100.180:33061/gmsdev
username: histarchdev
password: histarchdev00!

# GMS public server
Public IP: 
183.91.13.5 
IP: 
192.168.100.173
ID: 
Joey 
PW: 
Marusys@2025


This is the VPN Account Information for external access

-          ID: dkthanh

-          PW: 0m72pz


## Harmony test site
http://erpdev.hansolpapermall.com/

## Old canvas system
172.16.0.68
Admin
Marusys@


## Sonic VPN
pvdung /  Dungpham2026.

# DAM test Server
IP: 192.168.100.180
ID: mvn
MK: 123456


# Overview

## **Project Overview**
**Hansol Harmony ERP** is a comprehensive enterprise resource planning system developed for Hansol Group, a major Korean conglomerate. This is a Spring Boot-based web application that serves as an integrated business management platform.

## **Technical Architecture**

### **Core Technology Stack**
- **Framework**: Spring Boot 2.3.10.RELEASE
- **Java Version**: JDK 1.8
- **Database**: Oracle Database (HARMONY schema)
- **Template Engine**: Thymeleaf 3.0.11
- **Build Tool**: Gradle 5.2.1
- **IDE**: Spring Tool Suite 4
- **Caching**: Redis
- **Session Management**: Redis-based session storage

### **Key Dependencies**
- MyBatis for database operations
- Apache CXF for web services
- Log4j2 for logging
- Spring Security for authentication
- ModelMapper for object mapping
- Apache Commons libraries
- JSON processing libraries

## **Business Modules Structure**

The system is organized into distinct business modules, each handling specific functional areas:

### **1. HPLB2B - B2B Mall Management**
- **Purpose**: B2B e-commerce platform management
- **Sub-modules**:
  - `csmg`: Customer management
  - `hsmg`: Dashboard and analytics
  - `mbmg`: Member management  
  - `ormg`: Order management
  - `prmg`: Product management
  - `stmg`: Statistics management

### **2. HPLSD - Sales & Distribution**
- **Purpose**: Sales order processing and distribution management
- **Sub-modules**:
  - `ords`: Order management
  - `sale`: Sales processing
  - `ship`: Shipping management
  - `cust`: Customer management
  - `pric`: Pricing management
  - `rept`: Reporting

### **3. HPLMM - Materials Management**
- **Purpose**: Procurement and materials management
- **Sub-modules**:
  - `pumg`: Purchase order management
  - `immg`: Inventory management
  - `ivmg`: Invoice management
  - `mtmg`: Material management
  - `stmg`: Stock management

### **4. HPLFI - Financial Management**
- **Purpose**: Financial accounting and reporting
- **Sub-modules**:
  - `figl`: General ledger
  - `fiaa`: Asset accounting
  - `fiab`: Asset management
  - `ficl`: Credit management
  - `fifs`: Financial statements
  - `fitr`: Treasury management
  - `fitx`: Tax management

### **5. HPLCO - Controlling**
- **Purpose**: Cost accounting and controlling
- **Sub-modules**:
  - `prco`: Product costing
  - `pran`: Profitability analysis
  - `buco`: Budget control
  - `bupl`: Budget planning

### **6. HPLCM - Common Management**
- **Purpose**: System administration and common functions
- **Sub-modules**:
  - `auth`: Authorization management
  - `user`: User management
  - `menu`: Menu management
  - `code`: Code management
  - `syst`: System management

### **7. HPLVN - Vietnam Operations**
- **Purpose**: Vietnam-specific business operations
- **Sub-modules**:
  - `hkuk`: Integration with Hankuk Paper (한국제지)

### **8. HPLMOBILE - Mobile Interface**
- **Purpose**: Mobile application support and APIs

## **External System Integrations**

### **SAP Integration**
- **SAP RFC Connection**: Direct integration with SAP ERP systems
- **Connection Details**: Multiple SAP environments (QA, Production)
- **SAP JCo Libraries**: Uses SAP Java Connector for RFC calls
- **Data Synchronization**: Real-time data exchange with SAP modules

### **Third-Party Systems**
1. **Hankuk Paper (한국제지) API**: REST API integration for paper industry operations
2. **HanTalk Messaging**: Internal communication system
3. **BPEL Workflow Engine**: Business process automation
4. **Report Server**: Dedicated reporting services
5. **Scan Services**: Document scanning integration
6. **Tax Bill System (SmartBill)**: Electronic tax invoice processing
7. **Mobile Platform (Grooup)**: Mobile application backend

### **Web Services (WSDL)**
- Multiple SOAP web services for:
  - Purchase order processing
  - Sales order management
  - Delivery information
  - Customer order integration

## **Key Features & Functionality**

### **Order Management**
- Sales order processing with SAP integration
- Purchase order automation
- Order status tracking and history
- Multi-company order handling

### **Customer & Vendor Management**
- Customer master data management
- Vendor registration and approval workflows
- Change history tracking for audit trails
- Credit management and payment terms

### **Financial Operations**
- General ledger posting
- Asset management
- Budget planning and control
- Financial reporting and analytics
- Approval workflows for financial documents

### **Inventory & Materials**
- Stock management
- Material master data
- Inventory valuation
- Purchase requisition processing

### **B2B E-commerce**
- Product catalog management
- Online ordering system
- Customer portal
- Order tracking and status updates

## **Development Standards & Practices**

### **Code Organization**
- Package structure: `com.hansol.{module}.{submodule}.{layer}`
- Layered architecture: Controller → Service → Mapper → Database
- MyBatis for database operations
- Thymeleaf templates for UI

### **Development Guidelines**
- UTF-8 encoding throughout
- 4-space indentation
- JavaScript: single quotes, HTML: double quotes
- Thymeleaf comments for security
- Comprehensive logging with custom functions

### **Git Workflow**
- Branch naming: `dev/{developer-name}`
- No direct commits to master
- Merge requests for all changes
- Regular pulls from master to avoid conflicts

## **Recent Development Activities**

Based on commit history, recent major developments include:

1. **Customer Change History Tracking**: Implementation of audit trails for customer data modifications
2. **Authorization Process Improvements**: Enhanced approval workflows with notifications and documentation
3. **Sales Process Automation**: Automated discount calculations and sales categorization
4. **Vendor Management Enhancements**: Improved vendor registration and change tracking
5. **Email Reporting Updates**: Team name changes and report modifications
6. **Korean Paper Integration**: Enhanced integration with Hankuk Paper systems
7. **Mobile API Enhancements**: Improved mobile platform connectivity

## **Infrastructure & Deployment**

### **Environment Profiles**
- **Development**: Local development with specific database and Redis configurations
- **Test**: QA environment with test data
- **Production**: Live environment with production SAP connections

### **Security Features**
- Session management with Redis
- HTTPS enforcement in production
- File upload restrictions
- SQL injection protection
- Cross-site scripting prevention



## Popup behavior in common
- Put partial name -> open the pop up -> auto search the name
- Put exactly name -> auto search -> auto close the modal and fill the search box 
if there is only one result
- Put exact code -> auto search -> close and auto fill the search box
if there is only one result

# Screen notice
- fifs_03n: uncomment this line `//|| params.USER_ID == 'marusys'` to get data returned when search
- ords_030: sample data `100001` and `11001`


local IP: 192.168.102.64




---
Add new screen to Menu
Below are concrete DB checks and SQL statements you can run to grant an Administrator auth group access to the new program when you cannot use the UI. I include queries to find the correct auth-group and to verify state, plus the INSERT/UPDATE statements you will likely need. Back up data or test on a dev DB before running in production.

1) Find the auth-group you should use (Administrator for SD)
- Look for auth groups for `SD` and scan names for "admin" / "관리자" / "Administrator":
```/dev/null/find_auth_group.sql#L1-6
SELECT AUTH_GRP_ID, AUTH_GRP_NM, SYSCD, USE_YN
FROM HPLCM.TB_AUTH_010
WHERE SYSCD = 'SD'
ORDER BY SORT_ORD;
```

- If you want a broader search (any syscd):
```/dev/null/find_auth_group_by_name.sql#L1-4
SELECT AUTH_GRP_ID, AUTH_GRP_NM, SYSCD, USE_YN
FROM HPLCM.TB_AUTH_010
WHERE LOWER(AUTH_GRP_NM) LIKE '%admin%' OR AUTH_GRP_NM LIKE '%관리자%';
```

If you find (for example) `AUTH_GRP_ID = 'SD999'` and that is the Administrator group, use that in the next steps. If no admin group exists, you can create one (example below).

2) Verify the program row exists and has the flags required by the screen select
select_auth_screen2 requires `USE_YN = 'Y'`, `POPUP_YN = 'N'`, and `ERP_USE_YN = 'Y'` on TB_MENU_110. Check your new program:
```/dev/null/check_prog.sql#L1-6
SELECT PROG_ID, PROG_NM, MENU_ID, USE_YN, POPUP_YN, MIS_USE_YN, ERP_USE_YN
FROM HPLCM.TB_MENU_110
WHERE PROG_ID = 'SD.COVT.YOUR_PROG_ID'; -- replace with your PROG_ID
```

If `ERP_USE_YN` or `USE_YN` is not `'Y'`, update it:
```/dev/null/update_menu_110.sql#L1-6
UPDATE HPLCM.TB_MENU_110
SET USE_YN = 'Y', ERP_USE_YN = 'Y', POPUP_YN = 'N', AENAM = 'your_user', AEDAT = SYSDATE
WHERE PROG_ID = 'SD.COVT.YOUR_PROG_ID';
```

3) Grant the program to the auth-group (insert into TB_AUTH_020)
- After selecting the correct `AUTH_GRP_ID` (e.g. `SD999`), insert mapping(s):
```/dev/null/insert_auth_020.sql#L1-8
INSERT INTO HPLCM.TB_AUTH_020 (SYSCD, AUTH_GRP_ID, PROG_ID, ERNAM, ERDAT)
VALUES ('SD', 'SD999', 'SD.COVT.YOUR_PROG_ID', 'your_user', SYSDATE);
```

- You can also insert multiple program mappings in one run if necessary.

4) Ensure the target user (Administrator) is assigned to that auth group for the company (TB_AUTH_110)
- Check current user-group assignment:
```/dev/null/check_auth_110.sql#L1-6
SELECT MANDT, BUKRS, USER_ID, SYSCD, AUTH_GRP_ID, USE_YN
FROM HPLCM.TB_AUTH_110
WHERE BUKRS = 'M200' AND USER_ID = 'marusys' AND SYSCD = 'SD';
```

- If missing, insert (adjust MANDT if required; many installs use '100' or another client code):
```/dev/null/insert_auth_110.sql#L1-8
INSERT INTO HPLCM.TB_AUTH_110
  (MANDT, BUKRS, USER_ID, SYSCD, AUTH_GRP_ID, ERNAM, ERDAT)
VALUES
  ('100', 'M200', 'marusys', 'SD', 'SD999', 'your_user', SYSDATE);
```
- If a row exists but `AUTH_GRP_ID` should be changed, you can UPDATE instead:
```/dev/null/update_auth_110.sql#L1-6
UPDATE HPLCM.TB_AUTH_110
SET AUTH_GRP_ID = 'SD999', AENAM = 'your_user', AEDAT = SYSDATE
WHERE BUKRS = 'M200' AND USER_ID = 'marusys' AND SYSCD = 'SD';
```

5) Optional: create an auth-group if none exists
```/dev/null/insert_auth_010.sql#L1-8
INSERT INTO HPLCM.TB_AUTH_010
  (SYSCD, AUTH_GRP_ID, AUTH_GRP_NM, REMARK, USE_YN, ERNAM, ERDAT)
VALUES
  ('SD', 'SD999', 'SD Administrator', 'Created for new screen access', 'Y', 'your_user', SYSDATE);
```

6) Verify everything
- Check TB_AUTH_020 row(s):
```/dev/null/verify_auth_020.sql#L1-6
SELECT SYSCD, AUTH_GRP_ID, PROG_ID, ERNAM, ERDAT
FROM HPLCM.TB_AUTH_020
WHERE PROG_ID = 'SD.COVT.YOUR_PROG_ID';
```

- Check TB_AUTH_110 for the user:
```/dev/null/verify_auth_110.sql#L1-6
SELECT MANDT, BUKRS, USER_ID, SYSCD, AUTH_GRP_ID
FROM HPLCM.TB_AUTH_110
WHERE USER_ID = 'marusys' AND BUKRS = 'M200' AND SYSCD = 'SD';
```

- Re-run the screen-list query (select_auth_screen2) or log in as the user to confirm visibility. If you previously filtered by pattern like `prog_id like 'SD.COVT%'`, ensure the PROG_ID matches.

Important notes & cautions
- MANDT value: some environments require a particular `MANDT` (client). Use the same MANDT as existing TB_AUTH_110 rows (check existing rows for your user).
- Make sure to set `ERNAM` to a traceable username and consider `AENAM`/`AEDAT` values where appropriate.
- If other authorization filters apply (e.g., TB_AUTH_210, TB_CODE_030 system visibility), verify those are correct; you can query `TB_AUTH_210` for BUKRS = 'M200' and SYSCD 'SD'.
- These are direct DB changes. Prefer the UI when possible because the UI may apply additional business logic / triggers. If you must run SQL directly, run in a transaction and test.