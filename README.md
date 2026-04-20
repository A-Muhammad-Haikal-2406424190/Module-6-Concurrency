# Commit 1 Reflection Notes

Pada milestone ini saya mempelajari bagaimana server Rust single-threaded menerima koneksi dari browser menggunakan `TcpListener` lalu memproses setiap koneksi melalui `handle_connection` dengan `TcpStream` dan `BufReader`, sehingga request HTTP dapat dibaca per baris menggunakan `.lines()`, dikumpulkan sampai baris kosong sebagai penanda akhir header, dan ditampilkan ke terminal untuk verifikasi; dari proses ini saya memahami bahwa meskipun server belum mengirim body response, server sudah dapat menangkap struktur request nyata dari browser (seperti method, path, host, dan header lain), serta menyadari bahwa log koneksi bisa muncul lebih dari sekali karena perilaku retry dari browser, sehingga langkah ini menjadi fondasi penting sebelum melanjutkan implementasi response HTTP yang lengkap.

# Commit 2 Reflection Notes

![Commit 2 Screenshot](assets/commit2.png)
![Commit 2 screenshot](assets/commit2-2.png)

# Commit 3 Reflection Notes

Pada milestone ini saya memvalidasi request agar server tidak selalu mengembalikan halaman yang sama, yaitu dengan mengambil `request_line` pertama lalu melakukan pemisahan respons menggunakan tuple `(status_line, filename)` sehingga jika request adalah `GET / HTTP/1.1` server mengirim `200 OK` dengan `hello.html`, sedangkan request lain seperti `/bad` akan mendapat `404 NOT FOUND` dengan `404.html`; refactoring ini penting karena logika pemilihan status dan file dipusatkan di satu tempat, mengurangi duplikasi saat membangun response (`Content-Length` dan body tetap diproses sekali), membuat alur kode lebih jelas untuk dikembangkan ke routing yang lebih banyak, dan memastikan perilaku server lebih realistis sesuai prinsip dasar HTTP.

![Commit 3 Screenshot](assets/commit3.png)
![Commit 3 Screenshot](assets/commit3-2.png)
