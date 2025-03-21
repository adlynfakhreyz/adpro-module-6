# Advance Programming - Module 6

**Andi Muhammad Adlyn Fakhreyza Khairi Putra  
2306241713**

---

### Commit 1 reflection
---
What is inside `handle_connection` method?

Metode `handle_connection` berfungsi untuk menangani koneksi yang diterima oleh server TCP. Berikut adalah penjelasan lebih detail tentang kode pada programnya:

1. **Buffering Stream:**
   ```rust
   let buf_reader = BufReader::new(&mut stream);
   ```
   Baris ini membuat objek `BufReader` yang membungkus `stream`. Tujuan dari `BufReader` adalah untuk melakukan pembacaan stream secara efisien dengan buffering, sehingga pembacaan data dapat dilakukan baris per baris.

2. **Membaca Request HTTP:**
   ```rust
   let http_request: Vec<_> = buf_reader
       .lines()
       .map(|result| result.unwrap())
       .take_while(|line| !line.is_empty())
       .collect();
   ```
   - `.lines()`: Membaca stream per baris hingga mencapai akhir input.
   - `.map(|result| result.unwrap())`: Mengambil nilai `Result<String>` dan memaksa unwrapping. Artinya, jika ada error, program akan panik (`panic!`).
   - `.take_while(|line| !line.is_empty())`: Mengambil baris-baris hingga menemukan baris kosong (`\r\n`), yang menunjukkan akhir dari header HTTP.
   - `.collect()`: Mengumpulkan baris-baris tersebut menjadi `Vec<String>` yang merepresentasikan header HTTP.

Program ini pada intinya adalah membuat server yang mendengarkan koneksi pada address `127.0.0.1:7878`. Setiap kali ada koneksi masuk (`listener.incoming()`), koneksi tersebut diteruskan ke fungsi `handle_connection`. Fungsi `handle_connection` kemudian membaca dan memproses data dari stream tersebut, lalu menampilkannya.

---