# UAS

KODE PYTHON:

    # === Modul Data ===
    class KasirData:
    def _init_(self):
        self.keranjang = []

    def tambah_barang(self, nama, harga, jumlah):
        self.keranjang.append({"nama": nama, "harga": harga, "jumlah": jumlah, "total": harga * jumlah})

    def total_harga(self):
        return sum(item["total"] for item in self.keranjang)

    def kosongkan_keranjang(self):
        self.keranjang.clear()


    # === Modul View ===
    class KasirView:
    @staticmethod
    def tampilkan_menu():
        print("\n=== Program Kasir ===")
        print("1. Tambah Barang\n2. Lihat Keranjang\n3. Checkout\n4. Keluar")
        return input("Pilih menu: ")

    @staticmethod
    def input_barang():
        try:
            nama = input("Nama Barang: ")
            harga = float(input("Harga Barang: "))
            jumlah = int(input("Jumlah Barang: "))
            return nama, harga, jumlah
        except ValueError:
            print("Input tidak valid! Masukkan angka untuk harga dan jumlah.")
            return None, None, None

    @staticmethod
    def tampilkan_keranjang(keranjang):
        if keranjang:
            print("\n=== Keranjang Belanja ===")
            for i, item in enumerate(keranjang, 1):
                print(f"{i}. {item['nama']} - Rp{item['harga']} x {item['jumlah']} = Rp{item['total']}")
        else:
            print("\nKeranjang kosong.")

    @staticmethod
    def tampilkan_total(total):
        print(f"Total Harga: Rp{total}")

    @staticmethod
    def input_pembayaran():
        try:
            return float(input("Bayar: "))
        except ValueError:
            print("Input tidak valid! Masukkan angka.")
            return 0

    @staticmethod
    def tampilkan_kembalian(kembalian):
        print(f"Kembalian: Rp{kembalian}")

    @staticmethod
    def tampilkan_error_bayar():
        print("Uang tidak cukup!")


    # === Modul Process ===
    class KasirProcess:
    def _init_(self):
        self.data = KasirData()
        self.view = KasirView()

    def tambah_barang(self):
        nama, harga, jumlah = self.view.input_barang()
        if nama and harga and jumlah:
            self.data.tambah_barang(nama, harga, jumlah)

    def lihat_keranjang(self):
        self.view.tampilkan_keranjang(self.data.keranjang)

    def checkout(self):
        total = self.data.total_harga()
        self.view.tampilkan_total(total)
        bayar = self.view.input_pembayaran()
        if bayar >= total:
            self.view.tampilkan_kembalian(bayar - total)
            self.data.kosongkan_keranjang()
        else:
            self.view.tampilkan_error_bayar()

    def jalankan(self):
        while True:
            pilihan = self.view.tampilkan_menu()
            if pilihan == "1":
                self.tambah_barang()
            elif pilihan == "2":
                self.lihat_keranjang()
            elif pilihan == "3":
                self.checkout()
            elif pilihan == "4":
                print("Terima kasih telah menggunakan program kasir!")
                break
            else:
                print("Pilihan tidak valid!")
                

    # === Main Program ===
    if _name_ == "_main_":
    KasirProcess().jalankan()

PENJELASAN:

1. Modul Data (KasirData)

a. __init__
Tujuan: Menginisialisasi objek dengan atribut keranjang, yang berupa list kosong untuk menyimpan barang.
Penjelasan: Semua data barang akan disimpan dalam self.keranjang.
python

       def __init__(self):
       self.keranjang = []
b. tambah_barang
Tujuan: Menambahkan barang ke dalam keranjang belanja.
Penjelasan:
Input berupa nama, harga, dan jumlah barang.
Barang disimpan dalam bentuk dictionary: {nama, harga, jumlah, total}.
Kemudian, dictionary ditambahkan ke self.keranjang.
python

        def tambah_barang(self, nama, harga, jumlah):
        self.keranjang.append({"nama": nama, "harga": harga, "jumlah": jumlah, "total": harga * jumlah})
c. total_harga
Tujuan: Menghitung total harga semua barang dalam keranjang.
Penjelasan:
Menggunakan fungsi sum untuk menjumlahkan nilai total dari setiap barang dalam keranjang.
python

        def total_harga(self):
       return sum(item["total"] for item in self.keranjang)
d. kosongkan_keranjang
Tujuan: Menghapus semua barang di keranjang.
Penjelasan: Metode ini memanggil fungsi clear() pada list self.keranjang.
python

        def kosongkan_keranjang(self):
        self.keranjang.clear()
2. Modul View (KasirView)
   
a. tampilkan_menu
Tujuan: Menampilkan menu utama program dan meminta input pilihan dari pengguna.
Penjelasan: Mengembalikan input berupa string pilihan menu.
python

          def tampilkan_menu():
        print("\n=== Program Kasir ===")
        print("1. Tambah Barang\n2. Lihat Keranjang\n3. Checkout\n4. Keluar")
        return input("Pilih menu: ")
b. input_barang
Tujuan: Meminta input data barang dari pengguna (nama, harga, dan jumlah).
Penjelasan:
Meminta input satu per satu untuk nama, harga, dan jumlah barang.
Melakukan validasi sederhana untuk memastikan harga dan jumlah berupa angka.
Mengembalikan tuple (nama, harga, jumlah).
python

        def input_barang():
        try:
        nama = input("Nama Barang: ")
        harga = float(input("Harga Barang: "))
        jumlah = int(input("Jumlah Barang: "))
        return nama, harga, jumlah
        except ValueError:
        print("Input tidak valid! Masukkan angka untuk harga dan jumlah.")
        return None, None, None
c. tampilkan_keranjang
Tujuan: Menampilkan isi keranjang belanja.
Penjelasan:
Jika keranjang kosong, mencetak pesan "Keranjang kosong".
Jika ada barang, mencetak daftar barang dengan format: No. Nama Barang - Harga x Jumlah = Total.
python

        def tampilkan_keranjang(keranjang):
        if keranjang:
        print("\n=== Keranjang Belanja ===")
        for i, item in enumerate(keranjang, 1):
            print(f"{i}. {item['nama']} - Rp{item['harga']} x {item['jumlah']} = Rp{item['total']}")
        else:
        print("\nKeranjang kosong.")
d. tampilkan_total
Tujuan: Menampilkan total harga barang dalam keranjang.
Penjelasan: Mencetak total harga yang dihitung sebelumnya.
python

        def tampilkan_total(total):
        print(f"Total Harga: Rp{total}")
e. input_pembayaran
Tujuan: Meminta input pembayaran dari pengguna.
Penjelasan:
Memastikan input berupa angka.
Jika input tidak valid, mengembalikan 0.
python

        def input_pembayaran():
        try:
        return float(input("Bayar: "))
        except ValueError:
        print("Input tidak valid! Masukkan angka.")
        return 0
f. tampilkan_kembalian
Tujuan: Menampilkan kembalian pembayaran.
Penjelasan: Mencetak jumlah kembalian berdasarkan selisih antara pembayaran dan total harga.
python

        def tampilkan_kembalian(kembalian):
        print(f"Kembalian: Rp{kembalian}")
g. tampilkan_error_bayar
Tujuan: Menampilkan pesan jika pembayaran kurang dari total harga.
Penjelasan: Mencetak pesan "Uang tidak cukup!".
python

        def tampilkan_error_bayar():
        print("Uang tidak cukup!")
3. Modul Process (KasirProcess)
   
a. __init__
Tujuan: Menghubungkan modul data (KasirData) dan view (KasirView).
Penjelasan: Membuat instance self.data dan self.view.
python

        def __init__(self):
        self.data = KasirData()
        self.view = KasirView()
b. tambah_barang
Tujuan: Mengelola proses penambahan barang ke keranjang.
Penjelasan:
Memanggil input_barang untuk mendapatkan data barang.
Menambahkan data ke keranjang menggunakan metode tambah_barang.
python

        def tambah_barang(self):
       nama, harga, jumlah = self.view.input_barang()
        if nama and harga and jumlah:
        self.data.tambah_barang(nama, harga, jumlah)
c. lihat_keranjang
Tujuan: Menampilkan isi keranjang belanja.
Penjelasan: Memanggil tampilkan_keranjang dengan data dari self.data.keranjang.
python

        def lihat_keranjang(self):
        self.view.tampilkan_keranjang(self.data.keranjang)
d. checkout
Tujuan: Mengelola proses pembayaran.
Penjelasan:
Menghitung total harga menggunakan total_harga.
Meminta pembayaran pengguna.
Jika pembayaran mencukupi, menghitung kembalian dan mengosongkan keranjang.
Jika tidak cukup, menampilkan pesan error.
python

        def checkout(self):
        total = self.data.total_harga()
        self.view.tampilkan_total(total)
        bayar = self.view.input_pembayaran()
        if bayar >= total:
        self.view.tampilkan_kembalian(bayar - total)
        self.data.kosongkan_keranjang()
        else:
        self.view.tampilkan_error_bayar()
e. jalankan
Tujuan: Menjalankan alur utama program.
Penjelasan:
Menampilkan menu utama dan menavigasikan pengguna berdasarkan input.
pythoN

       def jalankan(self):
        while True:
        pilihan = self.view.tampilkan_menu()
        if pilihan == "1":
            self.tambah_barang()
        elif pilihan == "2":
            self.lihat_keranjang()
        elif pilihan == "3":
            self.checkout()
        elif pilihan == "4":
            print("Terima kasih telah menggunakan program kasir!")
            break
        else:
            print("Pilihan tidak valid!")

LINK YOUTUBE:
https://youtu.be/hx37smJxz3A?si=ktczUKfrFB2_Xuvq
