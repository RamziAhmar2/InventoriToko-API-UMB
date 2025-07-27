# 📦 API Inventaris Toko

Backend API untuk aplikasi inventaris toko, dibangun menggunakan **Node.js**, **Express**, dan **MySQL**. API ini menyediakan endpoint untuk:

- Autentikasi pengguna (Login & Register)
- Manajemen produk
- Keranjang belanja
- Riwayat pembelian
- Manajemen pengguna (admin)

---

## 👤 Informasi Pengembang

- **Nama Lengkap**: Ahmar Ramzi Sanjaya  
- **NIM**: [Masukkan NIM Anda]

---

## 📚 Dokumentasi API

### 🔐 Autentikasi

#### ✅ Registrasi Pengguna

`POST /api/auth/register`  
Mendaftarkan pengguna baru (default role: customer)

**Request Body:**
```json
{
  "username": "nama_pengguna",
  "password": "kata_sandi"
}
```

**Response (201 Created):**
```json
{ "message": "User registered successfully" }
```

**Response (400 Bad Request):**

```json
{ "message": "Username already exists" }
```

**🔓 Login Pengguna**

```json
POST /api/auth/login
```

Mengautentikasi pengguna dan mengembalikan token JWT.

Request Body:

```json
{
  "username": "nama_pengguna",
  "password": "kata_sandi"
}
```
**Response (200 OK):**

```json

{
  "message": "Login successful",
  "token": "eyJhbGciOiJIUzI1Ni...",
  "role": "customer",
  "userId": 1
}
```
**Response (401 Unauthorized):**

```json

{ "message": "Invalid credentials" }
```

**🛒 Endpoint Customer**

**📦 Mendapatkan Daftar Produk**

```json GET /api/customer/products ```

Authorization: Bearer Token JWT

Response (200 OK):

```json

[
  {
    "id": 1,
    "name": "Laptop Gaming",
    "description": "Laptop canggih untuk gaming.",
    "price": 15000000.00,
    "stock": 10,
    "image_url": "http://example.com/laptop.jpg",
    "created_at": "2025-07-27T10:00:00.000Z"
  }
]
🛒 Mendapatkan Item Keranjang
GET /api/customer/cart
Authorization: Bearer Token JWT

Response (200 OK):

```json

[
  {
    "cart_id": 101,
    "product_id": 1,
    "product_name": "Laptop Gaming",
    "price": 15000000.00,
    "quantity": 1,
    "subtotal": 15000000.00
  }
]
➕ Menambahkan ke Keranjang
POST /api/customer/cart
Authorization: Bearer Token JWT

Request Body:

```json

{
  "productId": 1,
  "quantity": 1
}
Response (200 OK):

```json

{ "message": "Product added to cart" }
❌ Menghapus Item Keranjang
DELETE /api/customer/cart/{cartItemId}
Authorization: Bearer Token JWT

Response (200 OK):

```json

{ "message": "Cart item deleted successfully" }
🛍️ Melakukan Pembelian
POST /api/customer/purchase
Authorization: Bearer Token JWT

Response (200 OK):

```json

{ "message": "Purchase completed successfully" }
📜 Riwayat Pembelian
🧾 Mendapatkan Riwayat Pembelian Customer
GET /api/customer/purchases
Authorization: Bearer Token JWT

Response (200 OK):

```json

[
  {
    "purchase_id": 201,
    "product_name": "Laptop Gaming",
    "image_url": "http://example.com/laptop.jpg",
    "quantity": 1,
    "total_price": 15000000.00,
    "purchase_date": "2025-07-27T11:00:00.000Z"
  }
]
🛠️ Endpoint Admin
📦 Mendapatkan Semua Produk
GET /api/admin/products
Authorization: Admin Token JWT

Response: Sama dengan endpoint customer, namun dapat menyertakan lebih banyak detail produk.

➕ Menambahkan Produk
POST /api/admin/products
Authorization: Admin Token JWT

Request Body:

```json

{
  "name": "Monitor UltraWide",
  "description": "Monitor 34 inci, 144Hz.",
  "price": 5000000.00,
  "stock": 5,
  "image_url": "http://example.com/monitor.jpg"
}
Response (201 Created):

```json

{ "message": "Product added successfully" }
✏️ Memperbarui Produk
PUT /api/admin/products/{id}
Authorization: Admin Token JWT

Request Body:

```json

{
  "name": "Monitor UltraWide Pro",
  "description": "Monitor 34 inci, 165Hz, HDR.",
  "price": 5500000.00,
  "stock": 4,
  "image_url": "http://example.com/monitor_pro.jpg"
}
Response (200 OK):

```json

{ "message": "Product updated successfully" }
🗑️ Menghapus Produk
DELETE /api/admin/products/{id}
Authorization: Admin Token JWT

Response (200 OK):

```json

{ "message": "Product deleted successfully" }
📊 Mendapatkan Semua Riwayat Pembelian
GET /api/admin/purchases
Authorization: Admin Token JWT

Response (200 OK):

```json

[
  {
    "purchase_id": 201,
    "username": "user_customer_1",
    "product_name": "Laptop Gaming",
    "image_url": "http://example.com/laptop.jpg",
    "quantity": 1,
    "total_price": 15000000.00,
    "purchase_date": "2025-07-27T11:00:00.000Z"
  },
  {
    "purchase_id": 202,
    "username": "user_customer_2",
    "product_name": "Keyboard Mekanik",
    "image_url": "http://example.com/keyboard.jpg",
    "quantity": 2,
    "total_price": 2000000.00,
    "purchase_date": "2025-07-27T12:00:00.000Z"
  }
]
👥 Mendapatkan Semua Pengguna
GET /api/admin/users
Authorization: Admin Token JWT

Response (200 OK):

```json

[
  {
    "id": 1,
    "username": "admin_user",
    "role": "admin"
  },
  {
    "id": 2,
    "username": "customer_user_1",
    "role": "customer"
  }
]
❌ Menghapus Pengguna
DELETE /api/admin/users/{id}
Authorization: Admin Token JWT

Response (200 OK):

```json

{ "message": "User deleted successfully" }
🚀 Cara Menjalankan Proyek
Install dependensi

bash

npm install
Jalankan server

bash

npm start
URL dasar API
Ganti http://10.0.2.2:3000/ dengan URL backend Anda jika menggunakan hosting atau IP lokal lainnya.

✅ Catatan Tambahan
Pastikan semua endpoint yang memerlukan autentikasi memiliki header:

makefile

Authorization: Bearer <token>
Implementasikan validasi input dan penanganan error untuk keamanan dan keandalan.

Gunakan file .env untuk menyimpan konfigurasi sensitif seperti:

DB_HOST

DB_USER

DB_PASSWORD

JWT_SECRET

PORT

