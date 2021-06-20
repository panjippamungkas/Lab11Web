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

# Praktikum 12

#### Jalankan MySQL dan buat sebuah database sebagai berikut:

![1](https://user-images.githubusercontent.com/81550517/122675300-fceba000-d202-11eb-9507-0b9dadbcceb9.jpg)

### 1 - Konfigurasi Database

Membuat konfigurasi hubungan ke database server dengan menggunakan file .env

![2](https://user-images.githubusercontent.com/81550517/122675353-315f5c00-d203-11eb-85f1-00c6767d8c25.jpg)

### 2 - Membuat Model

Buat file baru pada direktori /app/Models dengan nama ArtikelModel.php dengan code di bawah ini

```
<?php
namespace App\Models;

use CodeIgniter\Model;

class ArtikelModel extends Model
{
    protected $table = 'artikel';
    protected $primaryKey = 'id';
    protected $useAutoIncrement = true;
    protected $allowedFields = ['judul', 'isi', 'status', 'slug', 'gambar'];
}
```
### 3 - Membuat Controller

Buat Controller baru dengan nama Artikel.php pada direktori /app/Controllers dengan code di bawah ini

```
<?php
namespace App\Controllers;

use App\Models\ArtikelModel;

class Artikel extends BaseController
{
    public function index()
    {
        $title = 'Daftar Artikel';
        $model = new ArtikelModel();
        $artikel = $model->findAll();
        return view('artikel/index', compact('artikel', 'title'));
    }
}
```
### 4 - Membuat View

Buat direktori baru dengan nama artikel pada direktori /app/Views, kemudian buat file baru dengan nama index.php dengan code di bawah ini

```
<?= $this->include('template/header'); ?>

<?php if($artikel): foreach($artikel as $row): ?>
<article class="entry">
    <h2><a href="<?= base_url('/artikel/' . $row['slug']);?>"><?=$row['judul']; ?></a></h2>
    <img src="<?= base_url('/gambar/' . $row['gambar']);?>" alt="<?=$row['judul']; ?>">
    <p><?= substr($row['isi'], 0, 200); ?></p>
</article>
<hr class="divider" />
<?php endforeach; else: ?>
<article class="entry">
    <h2>Belum ada data.</h2>
</article>
<?php endif; ?>

<?= $this->include('template/footer'); ?>
```

Lalu buka alamat http://localhost:8080/artikel untuk melihat hasilnya.

![3](https://user-images.githubusercontent.com/81550517/122676715-65d61680-d209-11eb-81ff-c91766692f78.jpg)

Tidak ada data yang ditampilkan karena database masih kosong.
Tambahkan data pada database untuk ditampilkan datanya pada phpmyadmin

![4](https://user-images.githubusercontent.com/81550517/122676845-f44a9800-d209-11eb-87c6-92f60408f149.jpg)

Maka akan muncul tampilan seperti ini ketika browser direfresh.

![5](https://user-images.githubusercontent.com/81550517/122676886-252acd00-d20a-11eb-871b-1ed2f691386a.jpg)

### 5 - Membuat Tampilan Detail Artikel

Tampilan pada saat judul berita di klik maka akan diarahkan ke halaman yang berbeda. Tambahkan sebuah fungsi baru pada Controller Artikel /app/Controllers/Artikel.php dengan nama view(). dengan code dibawah ini

```
public function view($slug)
    {
        $model = new ArtikelModel();
        $artikel = $model->where([
            'slug' => $slug
        ])->first();

    // Menampilkan error apabila data tidak ada.
        if (!$artikel)
        {
            throw PageNotFoundException::forPageNotFound();
        }
        $title = $artikel['judul'];
        return view('artikel/detail', compact('artikel', 'title'));
    }
```
### 6 - Membuat View Detail

Buat file baru dalam folder artikel /app/Views/artikel/ dengan nama detail.php untuk menampilkan halaman detail dengan code dibawah ini
```
<?= $this->include('template/header'); ?>

<article class="entry">
    <h2><?= $artikel['judul']; ?></h2>
    <img src="<?= base_url('/gambar/' . $artikel['gambar']);?>" alt="<?=
    $artikel['judul']; ?>">
    <p><?= $artikel['isi']; ?></p>
</article>

<?= $this->include('template/footer'); ?>
```
### 7 - Membuat Route

Buka file Routes.php dalam folder /app/Config/ dan tambahkan routing untuk ke halaman detail artikel
```
$routes->get('/artikel/(:any)', 'Artikel::view/$1');
```
Maka akan tampil halaman dari artikel yang diklik

![6](https://user-images.githubusercontent.com/81550517/122678247-2959e900-d210-11eb-8df3-234b668c6331.jpg)

### 8 - Membuat Menu Admin

Menu admin adalah untuk proses CRUD data artikel. Buat method atau fungsi baru pada Controller Artikel dengan nama admin_index() dengan code di bawah ini
```
public function admin_index()
    {
        $title = 'Daftar Artikel';
        $model = new ArtikelModel();
        $artikel = $model->findAll();
        return view('artikel/admin_index', compact('artikel', 'title'));
    }
```
Kemudian buat file admin_index.php dalam folder /app/Views/artikel/ untuk tampilan halaman admin dengan code dibawah
```
<?= $this->include('template/admin_header'); ?>

<table class="table">
    <thead>
        <tr>
            <th>ID</th>
            <th>Judul</th>
            <th>Status</th>
            <th>Aksi</th>
        </tr>
    </thead>
    <tbody>
    <?php if($artikel): foreach($artikel as $row): ?>
    <tr>
        <td><?= $row['id']; ?></td>
        <td>
            <b><?= $row['judul']; ?></b>
            <p><small><?= substr($row['isi'], 0, 50); ?></small></p>
        </td>
        <td><?= $row['status']; ?></td>
        <td>
            <a class="btn" href="<?= base_url('/admin/artikel/edit/' .$row['id']);?>">Ubah</a>
            <a class="btn-danger" onclick="return confirm('Yakin menghapus data?');" href="<?= base_url('/admin/artikel/delete/' .
            $row['id']);?>">Hapus</a>
        </td>
    </tr>
    <?php endforeach; else: ?>
    <tr>
        <td colspan="4">Belum ada data.</td>
    </tr>
    <?php endif; ?>
    </tbody>
    <tfoot>
        <tr>
            <th>ID</th>
            <th>Judul</th>
            <th>Status</th>
            <th>Aksi</th>
        </tr>
    </tfoot>
</table>

<?= $this->include('template/admin_footer'); ?>
```
Kemudian tambahkan routing untuk menu admin sebagai berikut:

![7](https://user-images.githubusercontent.com/81550517/122678503-670b4180-d211-11eb-8dc4-a1283c811755.jpg)

Menu admin dapat diakses dengan alamat http://localhost:8080/admin/artikel

![8](https://user-images.githubusercontent.com/81550517/122678582-a46fcf00-d211-11eb-826f-0364fad104d0.jpg)

### 9 - Menambah Data Artikel

Tambahkan fungsi/method baru pada Controller Artikel dengan nama add() dengan code di bawah ini

```
 public function add()
    {
        // validasi data.
        $validation = \Config\Services::validation();
        $validation->setRules(['judul' => 'required']);
        $isDataValid = $validation->withRequest($this->request)->run();
    
        if ($isDataValid)
        {
            $artikel = new ArtikelModel();
            $artikel->insert([
                'judul' => $this->request->getPost('judul'),
                'isi' => $this->request->getPost('isi'),
                'slug' => url_title($this->request->getPost('judul')),
            ]);
            return redirect('admin/artikel');
        }
        $title = "Tambah Artikel";
        return view('artikel/form_add', compact('title'));
    }
```

Kemudian buat view untuk form tambah dengan nama form_add.php dalam folder (/app/Views/artikel/) dengan code di bawah ini

```
<?= $this->include('template/admin_header'); ?>

<h2><?= $title; ?></h2>
<form class="tambah" action="" method="post">
    <p>
        <input type="text" name="judul">
    </p>
    <p>
        <textarea name="isi" cols="50" rows="10"></textarea>
    </p>
    <p><input type="submit" value="Kirim" class="btn btn-large"></p>
</form>

<?= $this->include('template/admin_footer'); ?>
```

Dan di bawah ini adalah tampilannya

![9](https://user-images.githubusercontent.com/81550517/122678855-b2721f80-d212-11eb-81d7-8af8a09e03e3.jpg)

### 10 - Mengubah Data

Tambahkan fungsi/method baru pada Controller Artikel dengan nama edit() dengan code dibawah

```
public function edit($id)
    {
        $artikel = new ArtikelModel();
        // validasi data.
        $validation = \Config\Services::validation();
        $validation->setRules(['judul' => 'required']);
        $isDataValid = $validation->withRequest($this->request)->run();
        
        if ($isDataValid)
        {
            $artikel->update($id, [
                'judul' => $this->request->getPost('judul'),
                'isi' => $this->request->getPost('isi'),
            ]);
            return redirect('admin/artikel');
        }
        
        // ambil data lama
        $data = $artikel->where('id', $id)->first();
        $title = "Edit Artikel";
        return view('artikel/form_edit', compact('title', 'data'));
    }
```

Kemudian buat view untuk form tambah dengan nama form_edit.php dalam folder /app/Views/artikel/ dengan code di bawah ini

```
<?= $this->include('template/admin_header'); ?>

<h2><?= $title; ?></h2>
<form action="" method="post">
    <p>
        <input type="text" name="judul" value="<?= $data['judul'];?>" >
    </p>
    <p>
        <textarea name="isi" cols="50" rows="10"><?=$data['isi'];?></textarea>
    </p>
    <p><input type="submit" value="Kirim" class="btn btn-large"></p>
</form>

<?= $this->include('template/admin_footer'); ?>
```

Dan di bawah ini adalah tampilannya

![10](https://user-images.githubusercontent.com/81550517/122679279-6de78380-d214-11eb-93d2-8b664fd2f721.jpg)

### 11 - Menghapus Data

Tambahkan fungsi/method baru pada Controller Artikel dengan nama delete() dengan code dibawah

```
public function delete($id)
    {
        $artikel = new ArtikelModel();
        $artikel->delete($id);
        return redirect('admin/artikel');
    }
```
## Pertanyaan dan Tugas

Selesaikan programnya sesuai Langkah-langkah yang ada. Anda boleh melakukan improvisasi.

### Jawab/Hasil

Admin_header.php

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title><?= $title; ?></title>
    <link rel="stylesheet" href="<?= base_url('/adminstyle.css');?>">
</head>
<body>
    <div id="container">
    <header>
        <h1>Halaman Admin</h1>
    </header>
    <nav>
        <a href="<?= base_url('/admin/artikel');?>" class="active">Dashboard</a>
        <a href="<?= base_url('/artikel');?>">Artikel</a>
        <a href="<?= base_url('/admin/artikel/add');?>">Tambah Artikel</a>
    </nav>
    <section id="wrapper">
```

Admin_footer.php

```
    <footer>
        <p>&copy; 2021 - Universitas Pelita Bangsa</p>
    </footer>
    </div>
</body>
</html>
```

Hasil run

* Menambahkan artikel baru

![11](https://user-images.githubusercontent.com/81550517/122679603-b8b5cb00-d215-11eb-8d51-50da8545f8f8.jpg)

![12](https://user-images.githubusercontent.com/81550517/122679639-dd11a780-d215-11eb-940b-0744936e0042.jpg)

* Menghapus artikel

![13](https://user-images.githubusercontent.com/81550517/122679688-10eccd00-d216-11eb-9adf-b0654e3b0ac3.jpg)

![14](https://user-images.githubusercontent.com/81550517/122679737-3548a980-d216-11eb-93ae-74ddb6a39eaa.jpg)

* Mengedit artikel

![15](https://user-images.githubusercontent.com/81550517/122679815-848eda00-d216-11eb-96db-d9e2e3278d7d.jpg)

![16](https://user-images.githubusercontent.com/81550517/122679816-8789ca80-d216-11eb-9a54-324f5c17abb4.jpg)
