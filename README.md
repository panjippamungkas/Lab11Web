# Lab11Web
```
Nama        : Panji Putra Pamungkas
Nim         : 311910587
Kelas       : TI. 19. B1
Mata Kuliah : Pemograman Web - Praktikum 8
```
Sebelum memulai menggunakan Framework Codeigniter, perlu dilakukan konfigurasi pada webserver. Beberapa ekstensi PHP perlu diaktifkan untuk kebutuhan pengembangan Codeigniter 4. Dengan cara di bawah ini :
![1](https://user-images.githubusercontent.com/81550517/121945615-28433a80-cd7e-11eb-80da-e7d3ceab583d.png)

Hapus tanda ; (titik koma) pada bagian extension yang akan diaktifkan.
![2](https://user-images.githubusercontent.com/81550517/121945620-2b3e2b00-cd7e-11eb-9c75-aa0390a82341.png)

### Instalasi CodeIgniter 4
* Codeigniter dapat didownload dari website https://codeigniter.com/download
* Extrak file zip Codeigniter ke direktori htdocs/lab11_php_ci
* Ubah nama direktory framework-4.x.xx menjadi ci4
* Buka browser dengan alamat http://localhost/lab11_php_ci/ci4/public/

![3](https://user-images.githubusercontent.com/81550517/121946050-b61f2580-cd7e-11eb-95a8-83b5cc43c193.png)

Codeigniter menyediakan CLI, untuk mengaksesnya buka terminal lalu arahkan ke direktori project yang akan dibuat. Kemudian jalankan perintah php spark untuk memanggil CLI codeigniter.

![4](https://user-images.githubusercontent.com/81550517/121946101-c505d800-cd7e-11eb-9a76-484ea2e2bce7.png)

Codeigniter juga menyediakan mode debugging/development yang dapat menampilkan error/kesalahan dalam kode program. Cara mengaktifkannya dengan mengubah nama file env menjadi .env kemudian buka filenya dan ubah nilai CI_ENVIRONMENT menjadi development.

![7](https://user-images.githubusercontent.com/81550517/121946345-09917380-cd7f-11eb-92c1-b5b62959d146.png)

Maka pesan kesalahan akan ditampilkan.

![10](https://user-images.githubusercontent.com/81550517/121947304-19f61e00-cd80-11eb-83a6-6ee87b8b240a.jpg)

### Langkah 1 - Membuat Route
* Router terletak pada file app/config/Routes.php
* Untuk mengetahui route yg ada atau telah berjalan dapat menggunakan perintah php spark routes

![9](https://user-images.githubusercontent.com/81550517/121946769-799ff980-cd7f-11eb-976a-a2e0143e5ec0.png)

* Selanjutnya mencoba akses route yang telah dibuat dengan mengakses http://localhost:8080/contact
* Terjadi error file not found dikarenakan tidak ada file/page untuk halaman contact.

![404](https://user-images.githubusercontent.com/81550517/121947500-5164ca80-cd80-11eb-85f7-f7f80eea461c.jpg)

### Langkah 2 - Membuat Controller
* Membuat file <b>page.php</b> di dalam direktori Controller (/app/Controllers)

```
<?php
namespace App\Controllers;
class Page extends BaseController
{
    public function about()
    {
        return view('about', [
        'title' => 'Halaman About',
        'content' => 'Ini adalah halaman about yang menjelaskan tentang isi
        halaman ini.'
        ]);
       
    }

    public function contact()
    {
        return view('contact', [
            'title' => 'Halaman Contact'
        ]);
    }

    public function faqs()
    {
        echo "Ini halaman FAQ";
    }

    public function tos()
    {
        echo "ini halaman Term of Services";
    }

    public function artikel()
    {
        return view('artikel', [
            'title' => 'Halaman Artikel',
            'content' => 'Ini adalah halaman artikel yang menjelaskan tentang isi
            halaman ini.'
            ]);
    }

}
```

* Kemudian refresh browser maka halaman sudah dapat diakses dan menampilkan hasilnya.

![pagehasil](https://user-images.githubusercontent.com/81550517/121948350-58d8a380-cd81-11eb-9dc2-ab4dd22ed64c.jpg)

* Menambahkan method baru pada controller page.
* Method ini dapat diakses dengan menggunakan alamat: http://localhost:8080/page/tos

```
    public function tos()
    {
        echo "ini halaman Term of Services";
    }
```
### Langkah 3 - Membuat View
* Membuat file <b>about.php</b> di dalam direktori View (/app/view/about.php)

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title><?= $title; ?></title>
</head>
<body>
    <?= $this->include('template/header'); ?>
    <section id="introduce">
        <div class="row">
            <img src="VV.jpg" title="Rofi Ismail" alt="Rofi Ismail" class="image-circle" width="230"
            style="float: left; border: 2px solid black;">
            <h1>Hello!</h1>
            <p>Nama saya Rofi Ismail. Saya adalah seorang mahasiswa dari <i>Universitas Pelita Bangsa</i> yang saat ini sedang
                mempelajari materi PHP Framework (Codeigniter) dalam mata kuliah <i>Pemrograman Web</i>.</p>
        </div>
    </section>
    <?= $this->include('template/footer'); ?>
</body>
</html>
```
* Mengubah method about dalam controller page.
```
    public function about()
    {
        return view('about', [
        'title' => 'Halaman About',
        'content' => 'Ini adalah halaman about yang menjelaskan tentang isi
        halaman ini.'
        ]);
       
    }
```
* Maka akan tampil seperti ini

![121922195-ed340d80-cd63-11eb-9f54-9e41e41b2f5b](https://user-images.githubusercontent.com/81550517/121949511-b8837e80-cd82-11eb-9743-73e73580dc55.jpg)

### Langkah 4 - Membuat Layout Web dengan CSS
* Buat file css pada direktori public dengan nama style.css (copy file dari praktikum lab4_layout).
* Kemudian buat folder template pada direktori view, lalu buat file header.php dan footer.php.

header.php

![header](https://user-images.githubusercontent.com/81550517/121949922-3f385b80-cd83-11eb-9e92-a32a6a263ae3.jpg)

footer.php

![footer](https://user-images.githubusercontent.com/81550517/121949943-452e3c80-cd83-11eb-939e-cfa942f3f9dc.jpg)

* Kemudian ubah file about.php (/app/view/about.php) seperti berikut.
```
<?= $this->include('template/header'); ?>
<h1><?= $title; ?></h1>
<hr>
<p><?= $content; ?></p>
<?= $this->include('template/footer'); ?>
```

* refresh browser atau akses alamat http://localhost:8080/about

![about](https://user-images.githubusercontent.com/81550517/121950207-8888ab00-cd83-11eb-827c-38435ae5dced.jpg)

## Pertanyaan dan Tugas
Lengkapi kode program untuk menu lainnya yang ada pada Controller Page, sehingga semua link pada navigasi header dapat menampilkan tampilan dengan layout yang sama.

### Hasil tugas
* Tampilan page about

![about](https://user-images.githubusercontent.com/81550517/121950326-ace48780-cd83-11eb-8859-652d0e118ace.jpg)

* Tampilan page artikel

![artikel](https://user-images.githubusercontent.com/81550517/121950578-0351c600-cd84-11eb-955a-45e71c9a77d9.jpg)

* Tampilan page kontak

![kontak](https://user-images.githubusercontent.com/81550517/121950587-064cb680-cd84-11eb-961c-4a4a58e2d94d.jpg)
