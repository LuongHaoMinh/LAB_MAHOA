# LAB 1: MÃ HÓA ĐỐI XỨNG CỔ ĐIỂN

Dự án thực hành môn **An toàn và Bảo mật thông tin**. Chương trình được xây dựng bằng ngôn ngữ Java (Maven), giao diện đồ họa Java Swing và kết nối cơ sở dữ liệu Microsoft SQL Server để lưu trữ lịch sử thao tác.

---

## 📌 MỤC LỤC
1. [Yêu Cầu Hệ Thống](#-yêu-cầu-hệ-thống)
2. [Cấu Trúc Dự Án](#-cấu-trúc-dự-án)
3. [Danh Sách Thuật Toán & Tính Năng](#-danh-sách-thuật-toán--tính-năng)
4. [Bộ Dữ Liệu Kiểm Thử (Test Cases)](#-bộ-dữ-liệu-kiểm-thử-test-cases)
5. [Hướng Dẫn Cài Đặt & Cấu Hình](#-hướng-dẫn-cài-đặt--cấu-hình)
    * [1. Cấu hình Microsoft SQL Server](#1-cấu-hình-microsoft-sql-server)
    * [2. Biên dịch và Chạy ứng dụng](#2-biên-dịch-và-chạy-ứng-dụng)
6. [Tác Giả](#-tác-giả)

---

## 🛠 YÊU CẦU HỆ THỐNG

* **Java Development Kit (JDK):** Version 17 hoặc 21.
* **Build Tool:** Apache Maven 3.x.
* **IDE Khuyên Dùng:** Apache NetBeans (Phiên bản 20 trở lên) hoặc IntelliJ IDEA / VS Code.
* **Database:** Microsoft SQL Server Express 2019/2022 + SQL Server Management Studio (SSMS).

---

## 📂 CẤU TRÚC DỰ ÁN

```text
LAB1_MaHoaCoDien/
├── pom.xml                     # Tệp cấu hình Maven & Dependencies (mssql-jdbc)
├── README.md                   # Tài liệu hướng dẫn dự án
└── src/
    └── main/
        └── java/
            └── week_01/
                ├── FileTextIO.java          # Tiện ích mở/lưu tệp văn bản .txt (UTF-8)
                ├── CaesarCipher.java        # Xử lý thuật toán Caesar
                ├── VigenereCipher.java      # Xử lý thuật toán Vigenère
                ├── RailFenceCipher.java     # Xử lý thuật toán Rail Fence (Zíc zắc)
                ├── PlayfairCipher.java      # Xử lý thuật toán Playfair (Ma trận 5x5)
                ├── TranspositionCipher.java # Xử lý thuật toán Hoán vị cột
                ├── AutokeyCipher.java       # Xử lý thuật toán Autokey
                ├── CipherTongHop.java       # Bộ điều phối 6 thuật toán cổ điển
                ├── DbConfig.java            # Cấu hình kết nối JDBC SQL Server
                ├── HistoryDao.java          # Đọc/ghi bảngdbo.history trong SQL Server
                ├── AttackDemos.java         # Module thám mã (Brute force, Frequency, Known Plaintext)
                ├── frm_Caesar.java          # Form giao diện mã Caesar
                ├── frm_Vigenere.java        # Form giao diện mã Vigenère
                ├── frm_RailFence.java       # Form giao diện mã Rail Fence
                ├── frm_Playfair.java        # Form giao diện mã Playfair
                ├── frm_Transposition.java   # Form giao diện mã Hoán vị cột
                ├── frm_Autokey.java        # Form giao diện mã Autokey
                ├── frm_TongHop.java        # Form chương trình tổng hợp 6 thuật toán
                ├── frm_KetNoiSQL.java       # Form cấu hình & kiểm thử kết nối SQL Server
                ├── frm_LichSu.java          # Form xem lịch sử thao tác lưu từ CSDL
                ├── frm_TanCong.java         # Form phân tích & tấn công mật mã
                └── frm_Menu.java            # Menu chính chạy toàn bộ ứng dụng
```

---

## 🚀 DANH SÁCH THUẬT TOÁN & TÍNH NĂNG

### 1. Sáu Thuật Toán Cơ Bản
* **Caesar Cipher:** Dịch chuyển $k$ vị trí trong bảng chữ cái ($C = (P + k) \bmod 26$).
* **Vigenère Cipher:** Mã hóa đa bảng dựa trên từ khóa ($C_i = (P_i + K_i) \bmod 26$).
* **Rail Fence Cipher:** Ghi bản rõ theo đường zíc zắc trên $k$ hàng và đọc theo từng hàng.
* **Playfair Cipher:** Mã hóa thay thế theo cặp ký tự trên ma trận $5 \times 5$ (gộp I/J).
* **Transposition Cipher:** Hoán vị các cột theo thứ tự khóa số (ví dụ: `2,3,1`).
* **Autokey Cipher:** Dòng khóa kết hợp từ khóa mồi và nối tiếp bởi chính bản rõ.

### 2. Bài Nâng Cao 01 – Chương Trình Tổng Hợp & Lưu Lịch Sử
* Chọn nhanh 6 thuật toán qua `JComboBox`.
* Tự động lưu nhật ký mã hóa/giải mã vào bảng `dbo.history` trong Microsoft SQL Server.
* Quản lý kết nối SQL động và xem lại 50 lịch sử mới nhất trên bảng `JTable`.

### 3. Bài Nâng Cao 02 – Phân Tích (Tấn Công) Mật Mã Cổ Điển
* **Vét cạn (Brute Force):** Thử toàn bộ 26 khóa Caesar và tự động chấm điểm tiếng Anh (`englishScore`).
* **Phân tích tần suất (Frequency Analysis):** Thống kê tỷ lệ phần trăm xuất hiện các chữ cái trong bản mã.
* **Biết trước bản rõ (Known Plaintext):** Suy ngược từ khóa Vigenère khi biết trước cặp bản rõ/bản mã.

---

## 🧪 BỘ DỮ LIỆU KIỂM THỬ (TEST CASES)

Tất cả các thuật toán phải vượt qua bộ kiểm thử chuẩn dưới đây:

| Thuật toán | Plaintext | Key | Ciphertext đúng |
|---|---|---|---|
| **1.1 Caesar** | `HELLO` | `3` | `KHOOR` |
| **1.2 Vigenère** | `HELLO` | `KEY` | `RIJVS` |
| **1.3 Rail Fence** | `HELLO WORLD` | `3` | `HOREL OLLWD` |
| **1.4 Playfair** | `HELLOWORLD` | `KEYWORD` | `GYIZSCOKCFBU` |
| **1.5 Transposition** | `BAOMAT` | `2,3,1` | `AAOTBM` |
| **1.6 Autokey** | `HELLO` | `KEY` | `RIJSS` |

---

## 🔧 HƯỚNG DẪN CÀI ĐẶT & CẤU HÌNH

### 1. Cấu hình Microsoft SQL Server
1. **Mở SQL Server Configuration Manager:**
   * Chọn `Protocols for SQLEXPRESS` $\rightarrow$ Chuyển `TCP/IP` sang **Enabled**.
   * Nhấp đúp `TCP/IP` $\rightarrow$ Tab **IP Addresses** $\rightarrow$ Mục `IPAll`: Xóa ô `TCP Dynamic Ports`, nhập **`14333`** vào ô `TCP Port`.
   * Restart lại dịch vụ `SQL Server (SQLEXPRESS)`.
2. **Cấu hình Mixed Mode trên SSMS:**
   * Kết nối Server bằng `Windows Authentication`.
   * Click phải Server $\rightarrow$ `Properties` $\rightarrow$ `Security` $\rightarrow$ Chọn **SQL Server and Windows Authentication mode**. Restart Server.
3. **Chạy Script khởi tạo CSDL:**
   * Mở SSMS, chạy các lệnh SQL tạo Database `LAB1_MaHoaCoDien` và bảng `dbo.history`.
   * Tạo tài khoản đăng nhập `lab1_user` với mật khẩu **`LabUser@2026`** và cấp quyền `SELECT, INSERT, DELETE` trên bảng `dbo.history`.

### 2. Biên dịch và Chạy ứng dụng

#### Bằng Apache NetBeans:
1. Mở NetBeans $\rightarrow$ **File** $\rightarrow$ **Open Project...** $\rightarrow$ Trỏ tới thư mục `LAB1_MaHoaCoDien`.
2. Nhấp phải project $\rightarrow$ chọn **Clean and Build** (`Shift + F11`) để tải dependency `mssql-jdbc` từ Maven.
3. Nhấn **F6** (hoặc nhấp phải `frm_Menu.java` chọn **Run File**) để khởi chạy ứng dụng chính.

#### Bằng Dòng Lệnh (Terminal/CMD):
```bash
# Di chuyển vào thư mục dự án
cd C:\BaoMat\LAB1_MaHoaCoDien

# Biên dịch dự án
mvn clean install

# Chạy ứng dụng qua Maven
mvn exec:java
```

---

## 👤 TÁC GIẢ

* **Bài thực hành:** LAB 1 - Mã hóa đối xứng cổ điển
* **Môn học:** An toàn và Bảo mật thông tin