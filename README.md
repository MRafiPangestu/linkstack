# Aplikasi Web "LinkStack"

## Sekilas Tentang
**LinkStack** adalah aplikasi web open-source untuk membuat halaman profil berisi kumpulan tautan (link bio), mirip seperti **Linktree**.  
Aplikasi ini memudahkan pengguna menampilkan semua tautan sosial medianya dalam satu halaman yang menarik, dapat di-hosting secara mandiri (*self-hosted*), dan dapat dikustomisasi penuh.

Aplikasi ini diinstal menggunakan **Docker** dan dideploy di server **AWS EC2** dengan konfigurasi **Cloudflare SSL (Flexible HTTPS)** agar bisa diakses publik dengan aman.

## Instalasi
### Prasyarat
  1. Akun **AWS** aktif (Free Tier).
  2. Membuat **Instance EC2** dengan spesifikasi:
     - OS: Ubuntu Server 22.04 LTS  
     - Instance type: `t3.micro`
     - Storage: 8 GB (default)
     - Security Group:
       - Port 22 (SSH)
       - Port 80 (HTTP)
       - Port 443 (HTTPS)
  3. Akses SSH key pair (`.pem`) dari AWS.

### ⚙️ Langkah Instalasi di AWS EC2
  1. **Masuk ke server via SSH**
     ```bash
     ssh -i "linkstack-key.pem" ubuntu@<PUBLIC_IP_EC2>
  2. **Update & install Docker**
      sudo apt update
      sudo apt install docker.io -y
      sudo systemctl start docker
      sudo systemctl enable docker
  
  3. **Buat Docker volume dan jalankan LinkStack**
      sudo docker volume create linkstack
      sudo docker run --detach \
          --name linkstack \
          --publish 80:80 \
          --publish 443:443 \
          --restart unless-stopped \
          --mount source=linkstack,target=/htdocs \
          linkstackorg/linkstack
  
  4. **Cek container berjalan**
      sudo docker ps
     
      <img width="2845" height="227" alt="image" src="https://github.com/user-attachments/assets/61610334-19f3-411a-ba41-da712967cdf7" />
  
  6. **Akses aplikasi**
      Buka browser → http://3.25.186.21/
      Akan muncul halaman setup admin LinkStack.

## Cara Pemakaian
✨ Tampilan Aplikasi
Setelah setup selesai, pengguna dapat login ke dashboard:
http://3.25.186.21/

Fungsi utama:
  1. Membuat profil dan tautan seperti Instagram, YouTube, GitHub, dll.
  2. Mengganti tema tampilan halaman.
  3. Mengatur urutan dan ikon link.
  4. Mendukung kustomisasi warna, teks, dan gambar.

📸 Tampilan

  A. Sebagai Admin
  
    1. Halaman admin LinkStack
  <img width="2880" height="1800" alt="image" src="https://github.com/user-attachments/assets/3ec03cc3-3923-4e2a-803d-396dece011d9" />

    2.Untuk menambahkan blok tautan baru ke halaman utama LinkStack
  <img width="2827" height="1507" alt="image" src="https://github.com/user-attachments/assets/31eb22c8-815e-4618-9ac7-5967507ee189" />

    3. tempat admin bisa mengatur perilaku sistem, keamanan, hingga backup.
  <img width="2824" height="1542" alt="image" src="https://github.com/user-attachments/assets/cd629778-c3e3-4634-ac5c-ddc6b6d67f8e" />

    4. Membantu user untuk memperbaiki akun atau profile tanpa password
<img width="2838" height="1447" alt="image" src="https://github.com/user-attachments/assets/572d8830-52c0-42fe-b747-ea8b79eae922" />

    5. Menambah kredibilitas dan informasi tambahan di halaman publik LinkStack.
<img width="2829" height="1589" alt="image" src="https://github.com/user-attachments/assets/0ef8a44d-0286-4ab7-9038-50c7468f21c1" />

    6. Menyesuaikan tampilan umum aplikasi
<img width="2823" height="1557" alt="image" src="https://github.com/user-attachments/assets/4bb5a3ac-e617-4d2f-9631-b6ae510a2a07" />

    7. Melihat dan mengatur semua link yang sudah dibuat sebelumnya (bisa edit , hapus atau ubah urutan link)
<img width="2820" height="1616" alt="image" src="https://github.com/user-attachments/assets/9ea73cde-67f9-4600-927b-60faf904e4f8" />

    8. Mengatur konten profil user
<img width="2842" height="1625" alt="image" src="https://github.com/user-attachments/assets/97bf53ac-3a49-4c5e-a0c7-a63b05fafd5a" />

    9. Mengubah tema tampilan halaman publik
<img width="2841" height="1590" alt="image" src="https://github.com/user-attachments/assets/f7b8a03b-775c-4d1a-88e0-cb2d2b0bc962" />



  B. Sebagai User
  
    1. Halaman publik link bio dengan beberapa tautan aktif
  <img width="2880" height="1800" alt="image" src="https://github.com/user-attachments/assets/e65e454e-4d14-41c5-9bfa-090642c073bb" />
  
    2. Halaman untuk menambahkan link
  <img width="2880" height="1800" alt="image" src="https://github.com/user-attachments/assets/5094aa55-ebb9-4976-af3f-cf4cf6e02383" />
  
    3. Halaman untuk memanage link yang sudah ditambahakan
  <img width="2880" height="1800" alt="image" src="https://github.com/user-attachments/assets/a84f2edc-92a1-49bc-9495-93646297eda9" />
  
    4. Mengatur isi dan informasi pribadi yang muncul di halaman publik user (halaman link bio).
  <img width="2880" height="1800" alt="image" src="https://github.com/user-attachments/assets/b001adb6-9de0-4ad2-9f4b-0c7e1820f445" />

    5. Mengubah gaya tampilan dan nuansa visual halaman publik user (tema warna, latar, tata letak).
  <img width="2880" height="1800" alt="image" src="https://github.com/user-attachments/assets/733d968a-a801-4c8f-8400-6d33dbbe3f42" />
  
  
  


Pembahasan
💬 Kelebihan
  1. Instalasi mudah dengan Docker.
  2. Bisa di-host sendiri (kontrol penuh atas data).
  3. Desain modern dan ringan.
  4. Gratis & open source.
  5. Dapat diintegrasikan dengan domain custom.

⚠️ Kekurangan
  1. Tidak ada analitik bawaan (perlu plugin tambahan).
  2. Fitur drag-drop link belum seintuitif Linktree.

Perbandingan dengan Linktree
LinkStack merupakan aplikasi web open-source yang dapat di-host secara mandiri (self-hosted), sedangkan Linktree adalah layanan komersial yang di-host oleh penyedia resminya. Dari segi biaya, LinkStack sepenuhnya gratis, sementara Linktree menggunakan model freemium, di mana fitur dasar tersedia gratis dan fitur tambahan memerlukan biaya langganan. LinkStack menawarkan fleksibilitas penuh dalam kustomisasi, termasuk pengaturan tema, CSS, dan logo, sedangkan Linktree memiliki batasan dalam hal kustomisasi tampilan. Untuk keamanan, LinkStack dapat menggunakan SSL gratis melalui Cloudflare, sementara Linktree secara otomatis menyediakan SSL bagi penggunanya.

Referensi
  1. LinkStack Docker Official Repository
  2. LinkStack Documentation
  3. AWS EC2 Documentation
  4. Cloudflare SSL Guide
  5. Docker Hub - linkstackorg/linkstack
