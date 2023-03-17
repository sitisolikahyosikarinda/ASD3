import os

class Siswa: # class Siswa
    # constructor dengan parameter nama, nis, tgl_lahir, kelas, status
    def __init__(self, nama, nis, tgl_lahir, kelas, status):
        self.nama = nama
        self.nis = nis
        self.tgl_lahir = tgl_lahir
        self.kelas = kelas
        self.status = status
        self.next = None

class LinkedList: # class LinkedList
    # constructor dengan parameter head
    def __init__(self):
        self.head = None
        self.history_masuk = []
        self.history_hapus = []

    # method untuk menambahkan siswa
    def tambah_siswa(self, siswa):
        if not self.head: # jika head kosong
            self.head = siswa # siswa akan menjadi head
        else: # jika head tidak kosong
            current = self.head # current akan menjadi head
            while current.next: # jika current.next tidak kosong
                current = current.next # current akan menjadi current.next
            current.next = siswa # siswa akan menjadi current.next
        self.history_masuk.append(siswa.nis) # siswa.nis akan ditambahkan ke history_masuk  

    # method untuk menghapus siswa
    def hapus_siswa(self, nis): # parameter nis
        if not self.head:
            print("Tidak ada siswa.")
            return
        if self.head.nis == nis:
            self.history_hapus.append(self.head.nis)
            self.head = self.head.next
            return
        current = self.head
        while current.next:
            if current.next.nis == nis:
                self.history_hapus.append(current.next.nis)
                current.next = current.next.next
                return
            current = current.next
        print("Siswa dengan NIS tersebut tidak ditemukan.")

    # method untuk menampilkan siswa berdasarkan halaman
    # default halaman = 1 dan per_halaman = 5
    # dengan menampilkan 5 siswa per halaman
    def tampil_siswa(self, halaman = 1, per_halaman = 5):
        start = (halaman - 1) * per_halaman # start = (halaman - 1) * per_halaman
        end = start + per_halaman # end = start + per_halaman
        current = self.head # current akan menjadi head
        siswa_list = [] # siswa_list akan menjadi list kosong
        while current: # jika current tidak kosong
            siswa_list.append(current) # current akan ditambahkan ke siswa_list
            current = current.next # current akan menjadi current.next
        if start >= len(siswa_list): # jika start lebih besar atau sama dengan panjang siswa_list
            return None # mengembalikan nilai None
        else: # jika start tidak lebih besar atau sama dengan panjang siswa_list
            return siswa_list[start:end] # mengembalikan nilai siswa_list[start:end]

    def tampil_history_masuk(self):
        if not self.history_masuk:
            print("Belum ada data masuk.")
        else:
            print("Daftar NIS siswa yang masuk:")
            print("---------------------------")
            for nis in self.history_masuk:
                print(nis)

    def tampil_history_hapus(self):
        if not self.history_hapus:
            print("Belum ada data dihapus.")
        else:
            print("Daftar NIS siswa yang dihapus:")
            print("------------------------------")
            for nis in self.history_hapus:
                print(nis)

linked_list = LinkedList()

def tambah_siswa():
    nama = input("Masukkan nama siswa: ")
    nis = input("Masukkan NIS siswa: ")
    tgl_lahir = input("Masukkan tanggal lahir siswa: ")
    kelas = input("Masukkan kelas siswa: ")
    status = input("Masukkan status siswa [terdaftar/pindahan/keluar]: ")
    siswa = Siswa(nama, nis, tgl_lahir, kelas, status)
    
    linked_list.tambah_siswa(siswa)
    print("Siswa berhasil ditambahkan!")

def hapus_siswa():
    nis = input("Masukkan NIS siswa yang ingin dihapus: ")
    if linked_list.hapus_siswa(nis):
        print("Siswa dengan NIS", nis, "berhasil dihapus!")
    else:
        print("Siswa dengan NIS", nis, "tidak ditemukan.")

def tampil_siswa():
    halaman = 1
    while True:
        siswa_list = linked_list.tampil_siswa(halaman=halaman)
        if siswa_list:
            # print("No  Nama                NIS            Tanggal Lahir  Kelas       Status")
            # print("--  ------------------ -------------- -------------- ----------- ----------------")
            # for i, siswa in enumerate(siswa_list):
            #     print(f"{i+1:2}. {siswa.nama.ljust(19)} {siswa.nis.ljust(14)} {siswa.tgl_lahir.ljust(14)} {siswa.kelas.ljust(11)} {siswa.status.ljust(9)}")
            #     print("-- ------------------ -------------- -------------- ----------- ----------------")

            for siswa in siswa_list:
                print(f"NIS: {siswa.nis}")
                print(f"Nama: {siswa.nama}")
                print(f"Tanggal lahir: {siswa.tgl_lahir}")
                print(f"Kelas: {siswa.kelas}")
                print(f"Status: {siswa.status}")
                print("\n====================================\n")

            print(f"Halaman {halaman}")
        else:
            print("Tidak ada siswa.")
            break

        aksi = input("[n] Next [p] Previous [q] Quit\nAksi: ")
        if aksi.lower() == "n":
            halaman += 1
        elif aksi.lower() == "p" and halaman > 1:
            halaman -= 1
        else:
            break

def login(username, password):
    users = {
        "admin" : "admin123",
        "admin1" : "admin321",
        "admin2" : "admin111"
    }

    if username in users and users[username] == password :
        return True
    
    else:
        return False

if __name__ == '__main__':
    print("Login Terlebih Dahulu: \n\n")
    username = input("Masukkan Username: ")
    password = input("Masukkan Password: ")

    if(login(username, password)):
        os.system('cls')
        while True:
            print("=== Aplikasi Sekolah ===")
            print("1. Tambah siswa")
            print("2. Hapus siswa")
            print("3. Tampilkan daftar siswa")
            print("4. Tampilkan history siswa masuk")
            print("5. Tampilkan history siswa dihapus")
            print("6. Keluar")
            pilihan = input("Masukkan pilihan: ")
            if pilihan == "1":
                os.system("cls")
                print("\n=== Tambah Siswa ===\n")

                tambah_siswa()

            elif pilihan == "2":
                os.system("cls")
                print("\n=== Hapus Siswa ===\n")

                hapus_siswa()

            elif pilihan == "3":
                print("\n=== List Siswa ===\n")

                tampil_siswa()
            
            elif pilihan == "4":
                print("\n=== History Siswa Masuk ===\n")

                linked_list.tampil_history_masuk()

            elif pilihan == "5":
                print("\n=== History Siswa Dihapus ===\n")

                linked_list.tampil_history_hapus()

            elif pilihan == "6":
                break
            else:
                print("Pilihan tidak valid.")

    else:
        print("Otentikasi Gagal. Silakan coba kembali")
