# Reflection 1: Handle-connection, Check Response
Pada milestone pertama ini, saya telah mengimplementasikan fungsi handle_connection untuk memproses koneksi TCP yang masuk ke server. 
Berikut adalah beberapa poin utama yang saya pelajari dari implementasi ini:
1. Pembacaan Request: Menggunakan BufReader untuk membaca data dari TcpStream secara efisien. Data dibaca baris demi baris menggunakan metode .lines().
2. Transformasi Data: Saya menggunakan teknik functional programming di Rust, seperti .map() untuk membuka (unwrap) hasil pembacaan dan .take_while() untuk berhenti membaca ketika menemukan baris kosong, yang menandakan akhir dari header HTTP.
3. Koleksi Hasil: Semua baris request dikumpulkan ke dalam sebuah Vec<_> menggunakan .collect() sebelum akhirnya dicetak ke konsol untuk inspeksi.
4. Struktur Request: Melalui output konsol, saya dapat melihat struktur pesan HTTP yang dikirim oleh browser, yang mencakup metode (seperti GET), path, versi protokol, serta berbagai header seperti Host, User-Agent, dan Accept.

Implementasi ini memberikan pemahaman dasar tentang bagaimana server tingkat rendah berinteraksi dengan protokol TCP sebelum kita melangkah ke pengiriman respon HTTP yang sebenarnya.



