# Reflection 1: Handle-connection, Check Response
Pada milestone pertama ini, saya telah mengimplementasikan fungsi handle_connection untuk memproses koneksi TCP yang masuk ke server. 
Berikut adalah beberapa poin utama yang saya pelajari dari implementasi ini:
1. Pembacaan Request: Menggunakan BufReader untuk membaca data dari TcpStream secara efisien. Data dibaca baris demi baris menggunakan metode .lines().
2. Transformasi Data: Saya menggunakan teknik functional programming di Rust, seperti .map() untuk membuka (unwrap) hasil pembacaan dan .take_while() untuk berhenti membaca ketika menemukan baris kosong, yang menandakan akhir dari header HTTP.
3. Koleksi Hasil: Semua baris request dikumpulkan ke dalam sebuah Vec<_> menggunakan .collect() sebelum akhirnya dicetak ke konsol untuk inspeksi.
4. Struktur Request: Melalui output konsol, saya dapat melihat struktur pesan HTTP yang dikirim oleh browser, yang mencakup metode (seperti GET), path, versi protokol, serta berbagai header seperti Host, User-Agent, dan Accept.

Implementasi ini memberikan pemahaman dasar tentang bagaimana server tingkat rendah berinteraksi dengan protokol TCP sebelum kita melangkah ke pengiriman respon HTTP yang sebenarnya.

# Reflection 2
saya telah memodifikasi fungsi handle_connection agar tidak hanya mencetak request ke konsol, tetapi juga memberikan respon balik ke browser dalam bentuk file HTML. Berikut adalah beberapa poin utama yang saya pelajari:
1. Struktur Respon HTTP Agar browser dapat merender halaman dengan benar, server harus mengirimkan respon yang mengikuti format protokol HTTP. Respon tersebut terdiri dari:
 - Status Line: Berisi versi protokol dan status code (misalnya HTTP/1.1 200 OK).
 - Headers: Memberikan informasi tambahan seperti Content-Length untuk memberi tahu browser ukuran data yang dikirim.
 - Body: Isi konten yang akan ditampilkan, dalam hal ini adalah teks dari file hello.html.

2. Penggunaan Modul fs (File System)
Saya menggunakan fs::read_to_string("hello.html") untuk membaca isi file HTML dari penyimpanan lokal ke dalam variabel string di Rust. Hal ini membuat kode lebih modular karena konten visual dipisahkan dari logika program.

3. Penulisan ke Stream
Setelah format respon disusun menggunakan macro format!, data tersebut dikonversi menjadi bytes menggunakan method .as_bytes(). Kemudian, stream.write_all() digunakan untuk mengirimkan seluruh data tersebut melalui koneksi TCP kembali ke klien.

![Milestone 2](milestone_2.png)