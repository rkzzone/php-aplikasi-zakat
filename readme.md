# 💰 Zakat Fitrah Management Application

A web-based information system for managing zakat fitrah payments efficiently and systematically. This application enables recording of muzakki data, zakat calculation based on rice prices, and zakat transaction reporting.

## 📋 Project Description

The Zakat Fitrah Management Application is an information system designed to facilitate the management of zakat fitrah payments in mosques, prayer rooms, or zakat amil institutions. The system calculates the amount of zakat based on the price of rice consumed and the number of family members.

### Main Features

- **Zakat Data Management**: Complete recording of muzakki data including address, number of family members, and payment details
- **Rice Price Management**: Manage various rice prices and automatic zakat calculation per person
- **Automatic Calculation**: System automatically calculates zakat bills and change
- **Data Search**: Search feature to facilitate transaction data tracking
- **Excel Export**: Export zakat and rice data to Excel format for reporting
- **Pagination**: Data display with pagination for optimal performance
- **User Authentication**: Login system with password security (SHA1 hash)

## 🛠️ Technologies Used

| Category | Technology |
|----------|------------|
| **Backend** | PHP 8.2.4 (Native) |
| **Frontend** | HTML5, CSS3, JavaScript |
| **Framework CSS** | Bootstrap 3.x |
| **Database** | MySQL/MariaDB 10.4.28 |
| **Web Server** | Apache (XAMPP/WAMP/LAMP) |

## 📁 Project Structure

```
php-aplikasi-zakat/
├── _assets/              # Static assets (CSS, JS, Fonts)
│   ├── css/             # Bootstrap & Custom CSS
│   ├── js/              # jQuery & Bootstrap JS
│   └── fonts/           # Font files
├── _config/             # Application configuration
│   └── config.php       # Database connection & base URL
├── auth/                # Authentication module
│   ├── login.php        # Login page
│   └── logout.php       # Logout process
├── dashboard/           # Main dashboard
│   └── index.php        # Dashboard page
├── zakat/               # Zakat management module
│   ├── data.php         # Zakat transaction list
│   ├── add.php          # Add zakat form
│   ├── edit.php         # Edit zakat form
│   ├── del.php          # Delete zakat data
│   ├── proses.php       # Zakat CRUD process
│   └── export.php       # Export data to Excel
├── beras/               # Rice price management module
│   ├── data.php         # Rice price list
│   ├── add.php          # Add rice price form
│   ├── edit.php         # Edit rice price form
│   ├── del.php          # Delete rice data
│   ├── proses.php       # Rice CRUD process
│   └── export.php       # Export data to Excel
├── db/                  # Database
│   └── zakat.sql        # SQL database file
├── _header.php          # Header & sidebar template
├── _footer.php          # Footer template
├── index.php            # Application entry point
└── readme.md            # Project documentation
```

## 🚀 Installation Guide

### Prerequisites

Make sure your system has installed:
- PHP 7.4 atau lebih tinggi
- MySQL/MariaDB
- Web Server (Apache/Nginx)
- XAMPP/WAMP/LAMP (for local development)

### Installation Steps

1. **Clone or Download Project**
   ```bash
   git clone <repository-url>
   ```
   or download ZIP and extract to web server folder

2. **Move to Web Server Directory**
   ```bash
   # For XAMPP
   C:\xampp\htdocs\zakat
   
   # For WAMP
   C:\wamp64\www\zakat
   
   # For Linux
   /var/www/html/zakat
   ```

3. **Import Database**
   - Open phpMyAdmin (`http://localhost/phpmyadmin`)
   - Create a new database named `zakat`
   - Import file `db/zakat.sql` to the created database

4. **Database Configuration**
   
   Edit file [_config/config.php](_config/config.php) according to your local configuration:
   ```php
   $con = mysqli_connect('localhost', 'root', '', 'zakat');
   
   function base_url($url = null) {
       $base_url = "http://localhost/zakat";
       // Adjust according to your project path
   }
   ```

5. **Access Application**
   
   Open browser and access:
   ```
   http://localhost/zakat
   ```

## 🔐 Default Account

Use the following credentials for first login:

| Username | Password | Level |
|----------|----------|-------|
| `admin` | `admin` | Administrator |

> **⚠️ Important**: Immediately change the default password after first login for system security!

## 📊 Database Schema

### Table: `tb_user`
Stores system user data
- `id_user` (VARCHAR) - Primary Key
- `nama_user` (VARCHAR) - User full name
- `username` (VARCHAR) - Login username
- `password` (VARCHAR) - Password (SHA1 hash)
- `level` (ENUM) - Access level (1: Admin, 2: User)

### Table: `tb_beras`
Stores rice price data and zakat calculation
- `id_beras` (INT) - Primary Key
- `harga_beras` (INT) - Rice price per kg
- `harga_zakat` (INT) - Zakat price per person (3.5 kg rice)

### Table: `tb_zakat`
Stores zakat payment transactions
- `id_zakat` (INT) - Primary Key
- `nama_muzakki` (VARCHAR) - Zakat payer name
- `alamat` (VARCHAR) - Muzakki address
- `jml_jiwa` (INT) - Number of family members
- `id_beras` (INT) - Foreign Key to tb_beras
- `tagihan_zakat` (INT) - Total bill
- `jumlah_uang` (INT) - Amount paid
- `kembalian` (INT) - Change
- `tanggal_transaksi` (DATE) - Transaction date

## 📖 User Guide

### 1. Login to System
- Access application through browser
- Enter username and password
- Click Login button

### 2. Manage Rice Price Data
- Navigate to **Beras** menu
- Click **Tambah Beras** button to add new price
- System automatically calculates zakat price (rice price × 3.5 kg)
- Edit or delete data as needed

### 3. Input Zakat Transaction
- Navigate to **Zakat** menu
- Click **Tambah Data Zakat** button
- Fill out the form completely:
  - Muzakki Name
  - Address
  - Number of Family Members
  - Select Rice Price consumed
  - Enter Amount of Money paid
- System automatically calculates bill and change
- Click **Simpan** (Save)

### 4. Export Data
- On Data Zakat or Data Beras page
- Click **Export Ke Excel** link
- Excel file will automatically download

### 5. Search Data
- Use search form at the top of table
- Enter keyword
- Click **Search** button

## 🔒 Security

- Passwords stored with SHA1 encryption
- Session management for user authentication
- Prepared statements to prevent SQL Injection
- Input validation with `mysqli_real_escape_string()`

> **⚠️ Security Note**: For production, it is recommended to use more modern hashing algorithms such as `password_hash()` with bcrypt.

## 🐛 Known Issues & Limitations

- Password uses SHA1 (recommended upgrade to bcrypt/argon2)
- No complex multi-user role management feature yet
- Excel export uses simple method (can be improved with PHPExcel/PhpSpreadsheet library)
- No automatic database backup feature yet
- UI still uses Bootstrap 3 (can be upgraded to Bootstrap 5)

## 🔄 Future Development

Planned features for development:
- [ ] Multi-level user management (Admin, Operator, Viewer)
- [ ] Dashboard with statistics & charts
- [ ] Notification/reminder for zakat payment
- [ ] Generate automatic receipt (PDF)
- [ ] RESTful API for mobile app integration
- [ ] More comprehensive reporting features
- [ ] Dark mode UI
- [ ] Responsive design optimization
- [ ] Audit trail for tracking data changes
- [ ] Backup & restore database from application

## 📝 License

This project was created for educational and learning purposes. Can be used and modified as needed.

## 📞 Contact & Support

For questions, bug reports, or contributions, please contact the development team or create an issue in this repository.

---

