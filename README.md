<<<<<<< HEAD
# LabMobile5_Sesa-Ajeng-Maesara_ShiftB
=======
# Screenshot Website tokokita **Sesa Ajeng**

Registrasi
![Halaman Registrasi](registrasi_berhasil.png)

Login
![Halaman Login](login_gagal.png)

Produk
![Halaman List_Produk](list_produk.png)

Tambah Produk
![Halaman Tambah_Produk](tambah_produk_sebelum.png)
![Halaman Tambah_Produk](tambah_produk_setelah.png)

Edit Produk
![Halaman Edit_Produk](ubah_produk_sebelum.png)
![Halaman Edit_Produk](ubah_produk_setelah.png)

Hapus Produk
![Halaman Hapus_Produk](hapus_sebelum.png)
![Halaman Hapus_Produk](hapus_sesudah.png)

# Alur Website Website tokokita **Sesa Ajeng**
1. **Proses Registrasi**
   a. Input Data untuk Registrasi
   Penjelasan:
   Pada proses ini, pengguna akan mengisi nama, email, password, dan konfirmasi password pada form registrasi. Data ini kemudian dikirim ke server untuk disimpan di database. Kode berikut menangani pengiriman data ke API:

   RegistrasiBloc.registrasi(
   nama: \_namaTextboxController.text,
   email: \_emailTextboxController.text,
   password: \_passwordTextboxController.text
   )

   b. Pop-up Berhasil Registrasi
   Penjelasan:
   Setelah berhasil mendaftar, pengguna akan melihat pop-up notifikasi bahwa registrasi berhasil, seperti yang ditampilkan oleh kode berikut:

   showDialog(
   context: context,
   barrierDismissible: false,
   builder: (BuildContext context) => SuccessDialog(
   description: "Registrasi berhasil, silahkan login",
   okClick: () { Navigator.pop(context); }
   )
   );

3. **Proses Login**
   a. Input Data untuk Login
   Penjelasan:
   Pengguna mengisi email dan password di halaman login. Data tersebut dikirim ke API untuk proses autentikasi:

   LoginBloc.login(
   email: \_emailTextboxController.text,
   password: \_passwordTextboxController.text
   )

   b. Pop-up Gagal Login
   Penjelasan:
   Jika autentikasi gagal (misalnya, email atau password salah), sistem akan menampilkan pesan pop-up gagal login:

   showDialog(
   context: context,
   barrierDismissible: false,
   builder: (BuildContext context) => WarningDialog(
   description: "Login gagal, silahkan coba lagi",
   )
   );

   c. Berhasil Login
   Penjelasan:
   Jika login berhasil, pengguna akan diarahkan ke halaman daftar produk:

   Navigator.pushReplacement(
   context,
   MaterialPageRoute(builder: (context) => const ProdukPage())
   );

4. **Proses Tambah Data Produk**
   a. Input Data Produk Baru
   Penjelasan:
   Pengguna mengisi kode produk, nama produk, dan harga produk di form tambah produk. Data ini dikirim ke server untuk ditambahkan ke database:

   ProdukBloc.addProduk(
   produk: Produk(
   kodeProduk: \_kodeProdukController.text,
   namaProduk: \_namaProdukController.text,
   hargaProduk: int.parse(\_hargaProdukController.text)
   )
   )

5. **Proses Detail Produk**
   a. Melihat Detail Produk
   Penjelasan:
   Saat pengguna memilih produk dari daftar, detail produk akan ditampilkan menggunakan halaman detail:

   Navigator.push(
   context,
   MaterialPageRoute(
   builder: (context) => ProdukDetail(produk: produk)
   )
   );

6. **Proses Ubah Produk**
   a. Input Data untuk Ubah Produk
   Penjelasan:
   Pengguna dapat mengubah kode produk, nama produk, atau harga produk di halaman ubah produk. Perubahan ini kemudian disimpan di database:

   ProdukBloc.updateProduk(
   produk: Produk(
   id: produk.id,
   kodeProduk: \_kodeProdukController.text,
   namaProduk: \_namaProdukController.text,
   hargaProduk: int.parse(\_hargaProdukController.text)
   )
   )

   b. Berhasil Ubah Data Produk
   Penjelasan:
   Berhasil mengubah nama produk.

7. **Proses Hapus Produk**
   a. Konfirmasi Hapus Produk
   Penjelasan:
   Saat pengguna mengklik tombol hapus, sebuah dialog konfirmasi akan muncul untuk memastikan apakah pengguna ingin menghapus produk:

   showDialog(
   context: context,
   builder: (BuildContext context) => AlertDialog(
   content: const Text("Yakin ingin menghapus produk ini?"),
   actions: [
   OutlinedButton(
   child: const Text("Ya"),
   onPressed: () {
   ProdukBloc.deleteProduk(id: produk.id)
   Navigator.pop(context);
   }
   ),
   OutlinedButton(
   child: const Text("Batal"),
   onPressed: () => Navigator.pop(context),
   )
   ]
   )
   );

   b. Berhasil Hapus Data Produk
   Penjelasan:
   Berhasil hapus data produk.

8. **Proses Logout**
   a. Tombol Logout
   Penjelasan:
   Pengguna dapat logout dari sistem dengan menekan tombol logout. Ini akan menghapus sesi pengguna dan mengarahkan kembali ke halaman login:

   ListTile(
   title: const Text('Logout'),
   onTap: () async {
   await LogoutBloc.logout();
   Navigator.pushAndRemoveUntil(
   context,
   MaterialPageRoute(builder: (context) => LoginPage()),
   (route) => false
   );
   }
   )

