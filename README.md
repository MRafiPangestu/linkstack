# Aplikasi Web "LinkStack"

## Sekilas Tentang
**LinkStack** adalah aplikasi web open-source untuk membuat halaman profil berisi kumpulan tautan (link bio), mirip seperti **Linktree**.  
Aplikasi ini memudahkan pengguna menampilkan semua tautan sosial medianya dalam satu halaman yang menarik, dapat di-hosting secara mandiri (*self-hosted*), dan dapat dikustomisasi penuh.

Aplikasi ini diinstal menggunakan **Docker** dan dideploy di server **AWS EC2** dengan konfigurasi **Cloudflare SSL (Flexible HTTPS)** agar bisa diakses publik dengan aman.

---

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
     
    ---

## Cara Pemakaian
✨ Tampilan Aplikasi
Setelah setup selesai, pengguna dapat login ke dashboard:
http://3.25.186.21/

Fungsi utama:
Membuat profil dan tautan seperti Instagram, YouTube, GitHub, dll.
Mengganti tema tampilan halaman.
Mengatur urutan dan ikon link.
Mendukung kustomisasi warna, teks, dan gambar.

📸 Screenshot (contoh tampilan)
Halaman admin LinkStack
Halaman publik link bio dengan beberapa tautan aktif
(sertakan screenshot hasil deploy di laporan final)

Pembahasan
💬 Kelebihan
Instalasi mudah dengan Docker.
Bisa di-host sendiri (kontrol penuh atas data).
Desain modern dan ringan.
Gratis & open source.
Dapat diintegrasikan dengan domain custom.

⚠️ Kekurangan
Tidak ada analitik bawaan (perlu plugin tambahan).
Fitur drag-drop link belum seintuitif Linktree.

Perbandingan dengan Linktree
LinkStack merupakan aplikasi web open-source yang dapat di-host secara mandiri (self-hosted), sedangkan Linktree adalah layanan komersial yang di-host oleh penyedia resminya. Dari segi biaya, LinkStack sepenuhnya gratis, sementara Linktree menggunakan model freemium, di mana fitur dasar tersedia gratis dan fitur tambahan memerlukan biaya langganan. LinkStack menawarkan fleksibilitas penuh dalam kustomisasi, termasuk pengaturan tema, CSS, dan logo, sedangkan Linktree memiliki batasan dalam hal kustomisasi tampilan. Untuk keamanan, LinkStack dapat menggunakan SSL gratis melalui Cloudflare, sementara Linktree secara otomatis menyediakan SSL bagi penggunanya.

---

Referensi
LinkStack Docker Official Repository
LinkStack Documentation
AWS EC2 Documentation
Cloudflare SSL Guide
Docker Hub - linkstackorg/linkstack
