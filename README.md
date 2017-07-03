# Codeigniter2-HMVC-Modular
Codeigniter 2 HMVC Modular Knugraha.id

# Cara installation

Codeigniter-HMVC
================

Diambil dari https://bitbucket.org/Knugraha.id/codeigniter-modular-extensions-hmvc

Modular Extensions membuat CodeIgniter PHP framework modular. Modul adalah kelompok komponen independen, biasanya model, controller dan view, yang disusun dalam sub-modul modul aplikasi, yang dapat dimasukkan ke aplikasi CodeIgniter lainnya.

HMVC adalah singkatan dari Hierarchical Model View Controller.

Modul Controllers dapat digunakan sebagai Controllers biasa atau Controller HMVC dan dapat digunakan untuk membantu Anda membangun view parsial.

##Fitur:

Semua pengendali dapat berisi variabel kelas autoload $, yang menampung serangkaian item yang akan dimuat sebelum menjalankan konstruktor. Ini bisa digunakan bersamaan dengan `module / config / autoload.php`, namun menggunakan variabel` $ autoload` hanya bekerja untuk pengontrol tertentu.

Array `Modules :: $ locations` dapat diatur dalam file` application / config.php`. yaitu:

$ Config ['modules_locations'] = array (
APPPATH.'modules / '=>' ../modules/ ',
);

`Modul :: run ()` output disangga, jadi setiap data yang dikembalikan atau output langsung dari controller ditangkap dan dikembalikan ke pemanggil. Secara khusus, `$ this-> load-> view ()` dapat digunakan seperti yang Anda lakukan pada pengendali normal, tanpa perlu kembali.

Controller dapat dimuat sebagai variabel kelas dari pengendali lain dengan menggunakan modul `$ this-> load-> modul ('module / controller');` atau hanya `$ this-> load-> module ('module');` if the controller Nama cocok dengan nama modul

Setiap pengontrol modul yang dimuat kemudian dapat digunakan seperti perpustakaan, yaitu: `$ this-> controller-> method ()`, namun memiliki akses ke model dan perpustakaannya sendiri secara independen dari pemanggil.

Semua pengendali modul dapat diakses dari URL melalui `module / controller / method` atau hanya` module / method` jika nama modul dan controller cocok.

Jika Anda menambahkan metode `_remap ()` ke pengendali Anda, Anda dapat mencegah akses yang tidak diinginkan ke URL dan mengarahkan ulang kesalahan yang Anda inginkan.

#### Catatan:

Untuk menggunakan fungsi HMVC, seperti `Modules :: run ()`, pengendali harus memperpanjang kelas `MX_Controller`.

Untuk menggunakan Pemisahan Modular saja, tanpa HMVC, pengendali akan memperpanjang kelas Controller CodeIgniter.

Anda harus menggunakan konstruktor gaya PHP5 di controller Anda. yaitu:

<? Php
Kelas Xyz memperluas MX_Controller
{
    Fungsi __construct ()
    {
        Induk :: __ construct ();
    }
}

Konstruktor tidak diperlukan kecuali jika Anda perlu memuat atau memproses sesuatu saat pengendali pertama kali dibuat.

Semua perpustakaan ekstensi MY_ harus menyertakan (memerlukan) file perpustakaan MX yang setara dan memperpanjang kelas MX_ yang setara

Setiap modul mungkin berisi file `config / routes.php` dimana routing dan pengendali default dapat didefinisikan untuk modul yang menggunakan:

$ Route ['module_name'] = 'controller_name';

Controller dapat dimuat dari sub direktori `application / controllers`.

Controller juga dapat diambil dari sub-direktori `module / controllers`.

Sumber daya mungkin disilangkan antara modul. Yaitu: `$ this-> load-> model ('module / model');`

`Modules :: run ()` dirancang untuk mengembalikan partial view, dan akan mengembalikan output buffer (view) dari controller. Sintaks untuk menggunakan modul :: run adalah string tersegmentasi gaya URI dan variabel tak terbatas.

/ ** nama modul dan controller berbeda, Anda harus menyertakan nama metode juga, termasuk 'index' ** /
Modules :: run ('module / controller / method', $ params, $ ...);

/ ** nama modul dan controller sama tapi metodenya bukan 'index' ** /
Modules :: run ('module / method', $ params, $ ...);

/ ** nama modul dan controller sama dan metodenya adalah 'index' ** /
Modules :: run ('module', $ params, $ ...);

/ ** Parameter bersifat opsional, Anda bisa melewati sejumlah parameter. ** /

Untuk memanggil pengontrol modul dari dalam controller Anda dapat menggunakan modul modul `$ this-> load-> module ()` or `Modules :: load ()` dan metode PHP5 chaining yang tersedia untuk objek yang dimuat oleh MX. Yaitu: `$ this-> load-> library ('validation') -> run ()`.

Untuk memuat bahasa untuk modul disarankan menggunakan metode Loader yang akan memasukkan nama modul aktif ke instance Lang; Yaitu: `$ this-> load-> language ('language_file')`;

Fitur spl_autoload PHP5 memungkinkan Anda untuk secara bebas memperluas kelas kontrol, model dan perpustakaan Anda dari kelas inti aplikasi / inti` atau `aplikasi / perpustakaan` tanpa perlu menyertakan atau memerlukannya secara khusus.

Pemuat perpustakaan juga telah diperbarui untuk mengakomodasi beberapa fitur CI 1.7: yaitu alias Perpustakaan diterima dengan cara yang sama seperti model alias, dan memuat file konfigurasi dari direktori konfigurasi modul sebagai parameter perpustakaan (re: form_validation.php) telah ditambahkan.

Mengembalikan array konfigurasi yang terisi ke variabel Anda: `$ config = $ this-> load-> config ('config_file')`

Model dan perpustakaan juga dapat dimuat dari sub-direktori di direktori aplikasi masing-masing.

Saat menggunakan validasi bentuk dengan MX, Anda perlu memperpanjang kelas `CI_Form_validation` seperti yang ditunjukkan di bawah ini, sebelum menetapkan pengontrol saat ini sebagai variabel` $ CI` ke perpustakaan form_validation. Ini akan memungkinkan metode panggilan balik Anda berfungsi dengan baik. (Ini telah dibahas di forum CI juga). yaitu:

<? Php
/ ** aplikasi / libraries / MY_Form_validation ** /
Kelas MY_Form_validation memperluas CI_Form_validation
{
    Publik $ CI;
}

Dan:

<? Php
Kelas Xyz memperluas MX_Controller
{
Fungsi __construct ()
{
Induk :: __ construct ();
        
$ This-> load-> library ('form_validation');
$ This-> form_validation-> CI = & $ this;
}
}

## Lihat Partial

Menggunakan Modul sebagai tampilan parsial dari dalam suatu tampilan semudah menulis:

<? Php echo Modules :: run ('module / controller / method', $ param, $ ...); ?>

Parameter bersifat opsional, Anda bisa melewati sejumlah parameter.

Instalasi Modular Extensions

1) Mulailah dengan pemasangan CI yang bersih

2) Set `$ config ['base_url' ]` dengan benar untuk instalasi Anda

3) Akses URL `/ index.php / welcome` => tampilkan Selamat Datang di CodeIgniter

4) Tambahkan file library Extensions Modular Extensions ke direktori CI 2.0 `application / libraries`

5) Drop Modular Extensions file inti ke dalam `application / core`, file` MY_Controller.php` tidak diperlukan kecuali Anda ingin membuat ekstensi Controller Anda sendiri.

6) Akses URL `/ index.php / welcome` => show Selamat Datang di CodeIgniter

7) Buat struktur direktori modul `application / modules / welcome / controllers`

8) Pindahkan controller `application / controllers / welcome.php` ke` application / modules / welcome / controllers / welcome.php`

9) Akses URL `/ index.php / welcome` => show Selamat Datang di CodeIgniter

10) Buat direktori `application / modules / welcome / views`

11) Pindahkan tampilan `application / views / welcome_message.php` ke` application / modules / welcome / views / welcome_message.php`

12) Akses URL `/ index.php / welcome` => show Selamat Datang di CodeIgniter

Anda sekarang harus memiliki instalasi Modular Extensions yang sedang berjalan.

Petunjuk Pemasangan Petunjuk:

-Langkah 1-3 memberitahu Anda bagaimana cara menginstal CI standar - jika Anda menginstal CI yang bersih / teruji, lompat ke langkah 4.

-Langkah 4-5 menunjukkan bahwa CI normal masih bekerja setelah menginstal MX - seharusnya tidak mengganggu pengaturan CI normal.

-Steps 6-8 menunjukkan MX bekerja bersama CI - controller pindah ke modul "selamat datang", file tampilan tetap berada di direktori CI `application / views` - ​​MX dapat menemukan sumber daya modul di beberapa tempat, termasuk direktori aplikasi.

-Steps 9-11 menunjukkan MX bekerja dengan kedua pengontrol dan melihat modul "selamat datang" - seharusnya tidak ada file di direktori `application / controllers` or` application / views`.
