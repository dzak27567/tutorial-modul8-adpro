# Reflection Modul 8

## 1. What are the key differences between unary, server streaming, and bi-directional streaming RPC (Remote Procedure Call) methods, and in what scenarios would each be most suitable?

Perbedaan utama antara unary, server streaming, dan bidirectional streaming RPC terletak pada arah dan jumlah komunikasi antara klien dan server. Unary RPC digunakan untuk komunikasi satu-kali (request-response), cocok untuk operasi sederhana seperti autentikasi. Server streaming mengirim banyak data sebagai respons tunggal, misalnya histori transaksi. Bidirectional streaming memungkinkan komunikasi dua arah secara simultan, sangat cocok untuk aplikasi real-time seperti chat.

## 2. What are the potential security considerations involved in implementing a gRPC service in Rust, particularly regarding authentication, authorization, and data encryption?

Pertimbangan keamanan meliputi autentikasi (misalnya dengan JWT atau OAuth2), otorisasi berbasis peran, serta penggunaan TLS untuk mengenkripsi data selama transmisi. Validasi data juga penting untuk mencegah serangan seperti injeksi atau spoofing. Rust membantu dengan tipe yang kuat, tetapi tetap perlu perlindungan dari sisi protokol dan data.

## 3. What are the potential challenges or issues that may arise when handling bidirectional streaming in Rust gRPC, especially in scenarios like chat applications?

Beberapa tantangan antara lain sinkronisasi kanal antara pengirim dan penerima, menangani klien yang tiba-tiba terputus, dan mencegah backlog jika salah satu pihak terlalu lambat. Debugging streaming dua arah juga lebih kompleks karena sifatnya yang paralel dan asynchronous.

## 4. What are the advantages and disadvantages of using the `tokio_stream::wrappers::ReceiverStream` for streaming responses in Rust gRPC services?

Kelebihan `ReceiverStream` adalah kemudahan integrasi dengan kanal `mpsc`, mendukung asynchronous stream secara natural, dan cocok untuk sebagian besar pola gRPC streaming. Namun, kekurangannya adalah tidak mendukung banyak konsumen (hanya satu receiver), serta bisa terjadi blocking jika buffer penuh dan konsumen lambat.

## 5. In what ways could the Rust gRPC code be structured to facilitate code reuse and modularity, promoting maintainability and extensibility over time?

Kode dapat disusun modular dengan memisahkan setiap layanan ke dalam file/module sendiri, menggunakan trait dan implementasi terpisah, serta membuat utilitas bersama untuk validasi, logging, atau autentikasi. Dengan pendekatan ini, kode lebih mudah diuji, diubah, dan diperluas seiring bertambahnya fitur.

## 6. In the MyPaymentService implementation, what additional steps might be necessary to handle more complex payment processing logic?

Untuk menangani logika pembayaran kompleks, perlu validasi lanjutan, dukungan retry jika transaksi gagal, integrasi dengan sistem pembayaran eksternal, pencatatan transaksi ke database, dan pengelolaan status transaksi yang lebih detail. Penggunaan UUID atau hash untuk idempotensi juga penting untuk mencegah duplikasi.

## 7. What impact does the adoption of gRPC as a communication protocol have on the overall architecture and design of distributed systems, particularly in terms of interoperability with other technologies and platforms?

Adopsi gRPC mendorong arsitektur berbasis kontrak (schema-first) dan sangat meningkatkan interoperabilitas lintas bahasa berkat penggunaan Protocol Buffers. Namun, integrasi dengan sistem berbasis REST memerlukan penyesuaian atau penggunaan gRPC gateway. Secara umum, gRPC menyederhanakan komunikasi antar layanan dengan performa tinggi.

## 8. What are the advantages and disadvantages of using HTTP/2, the underlying protocol for gRPC, compared to HTTP/1.1 or HTTP/1.1 with WebSocket for REST APIs?

HTTP/2 mendukung multiplexing, streaming dua arah, dan overhead lebih rendah dibanding HTTP/1.1. Ini sangat menguntungkan untuk aplikasi real-time. Sebaliknya, HTTP/1.1 membutuhkan WebSocket untuk komunikasi dua arah, namun WebSocket lebih kompleks dalam pengelolaan koneksi dan tidak memiliki fitur seperti flow control dan header compression bawaan.

## 9. How does the request-response model of REST APIs contrast with the bidirectional streaming capabilities of gRPC in terms of real-time communication and responsiveness?

REST bersifat sinkron dan satu arah (request-response), sedangkan gRPC streaming memungkinkan komunikasi dua arah yang aktif secara bersamaan. Ini membuat gRPC jauh lebih responsif dalam aplikasi real-time karena tidak perlu polling atau membuka koneksi baru secara berulang seperti pada REST.

## 10. What are the implications of the schema-based approach of gRPC, using Protocol Buffers, compared to the more flexible, schema-less nature of JSON in REST API payloads?

Pendekatan berbasis skema seperti Protocol Buffers menjamin kejelasan kontrak antar sistem dan parsing yang efisien. Ini cocok untuk sistem besar yang stabil. Sebaliknya, JSON memberikan fleksibilitas yang lebih besar namun rentan terhadap ketidakkonsistenan data. Dengan protobuf, komunikasi menjadi lebih cepat dan lebih aman, meski kurang human-readable.
