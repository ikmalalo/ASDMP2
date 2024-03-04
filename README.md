# ASDMP2
Ikmal Ali Azhari, Sistem Informasi B, 2309116087
from prettytable import PrettyTable

class CircularNode:
    def __init__(self, robux):
        self.robux = robux
        self.next = None

class CircularLinkedList:
    def __init__(self):
        self.head = None

    def tambahcircularlinkedlist(self, robux):
        new_node = CircularNode(robux)
        if not self.head:
            self.head = new_node
            new_node.next = self.head
        else:
            temp = self.head
            while temp.next != self.head:
                temp = temp.next
            temp.next = new_node
            new_node.next = self.head

    def display(self):
        if not self.head:
            print("Circular Linked Listnya kosong")
        else:
            temp = self.head
            while True:
                print(f"Kode Robux: {temp.robux.kode}, Paket Robux: {temp.robux.paket_robux}, "
                    f"Paket Subscription: {temp.robux.paket_subscription}, Harga: {temp.robux.harga}, "
                    f"Diskon: {temp.robux.diskon}%")
                temp = temp.next
                if temp == self.head:
                    break
class akun:
    def __init__(self, nama, emoney):
        self.nama = nama
        self.emoney = emoney

class Robux:
    def __init__(self, kode, paket_robux, paket_subscription, harga, diskon):
        self.kode = kode
        self.paket_robux = paket_robux
        self.paket_subscription = paket_subscription
        self.harga = harga
        self.diskon = diskon

class CRUD:
    def __init__(self):
        self.daftar_robux = {
            "HGH67": Robux("HGH67", 400, 200, 50000, 12)
        }
        self.table = PrettyTable()

    def lihat_robux(self):
        if not self.daftar_robux:
            print("List Robux tidak ada")
        else:
            table = PrettyTable()
            table.field_names = ["No", "Kode Robux", "Paket Robux", "Paket Subscription", "Harga", "Diskon"]

            for idx, (kode_robux, robux) in enumerate(self.daftar_robux.items(), start=1):
                rupiah = f"Rp.{robux.harga}"
                persen = f"{robux.diskon}%"
                table.add_row([idx, kode_robux, robux.paket_robux, robux.paket_subscription, rupiah, persen])
            print(table)

    def tambah_robux(self):
        kode_robux = input("Masukkan Kode robux: ")
        paket_robux = input("Masukkan Paket robux: ")
        paket_subscription = input("Masukkan Paket Subscription Robux: ")
        harga = input("Masukkan Harga Robux: ")
        diskon = input("Apakah anda ingin menambahkan diskon? (y/n): ")

        if diskon == "y":
            tambah_diskon = int(input("Masukkan Diskon untuk paket ini: "))
        else:
            tambah_diskon = 0

        self.daftar_robux[kode_robux] = Robux(kode_robux, paket_robux, paket_subscription, harga, tambah_diskon)
        print("Data Robux Sudah ditambahkan di table")

    def edit_robux(self):
        kode_robux = input("Masukkan Kode Robux yang ingin di edit: ")

        while kode_robux in self.daftar_robux:
            robux = self.daftar_robux[kode_robux]
            print(f"Data Robux untuk Kode {kode_robux}:")
            print(f"1. Paket Robux: {robux.paket_robux}")
            print(f"2. Paket Subscription: {robux.paket_subscription}")
            print(f"3. Harga Robux: {robux.harga}")
            print(f"4. Diskon: {robux.diskon}%")

            pilih = input("Pilih data yang ingin diubah (1-4), atau 0 untuk keluar: ")

            if pilih == "0":
                break

            if pilih in ["1", "2", "3", "4"]:
                if pilih == "1":
                    robux.paket_robux = input("Masukkan Paket Robux baru: ")
                elif pilih == "2":
                    robux.paket_subscription = input("Masukkan Paket Subscription baru: ")
                elif pilih == "3":
                    robux.harga = input("Masukkan Harga Robux baru: ")
                elif pilih == "4":
                    robux.diskon = input("Masukkan Diskon baru: ")
                else:
                    print("Pilihan tidak valid.")
            else:
                print("Pilihan tidak valid. Silakan masukkan angka 1-4 atau 0 untuk kembali.")
        else:
            print(f"Kode {kode_robux} Robux Yang Anda Masukkan Salah!")

    def hapus_robux(self):
        kode_robux = input("Masukkan Kode Robux yang ingin di hapus dari tabel: ")

        if kode_robux in self.daftar_robux:
            del self.daftar_robux[kode_robux]
            print("Data Robux yang anda hapus sudah tidak ada di tabel lagi")
        else:
            print(f"Kode {kode_robux} Robux Yang Anda Masukkan Salah!")

    def menu_admin(self):
        while True:
            print("\n==== Selamat Datang Admin ====")
            print("1. Lihat Robux di tabel")
            print("2. Tambah Data Robux")
            print("3. Ubah Data Robux")
            print("4. Hapus Data Robux")
            print("5. Keluar")

            pilih = input("Pilih menu (1-5): ")

            if pilih == "1":
                self.lihat_robux()
            elif pilih == "2":
                self.tambah_robux()
            elif pilih == "3":
                self.edit_robux()
            elif pilih == "4":
                self.hapus_robux()
            elif pilih == "5":
                break

class TopUp:
    def __init__(self, daftar_robux):
        self.daftar_robux = daftar_robux

    def lihat_robux(self):
        if not self.daftar_robux:
            print("Daftar Robux tidak ada")
        else:
            table = PrettyTable()
            table.field_names = ["No", "Kode Robux", "Paket Robux", "Paket Subscription", "Harga", "Diskon"]

            for idx, (kode_robux, robux) in enumerate(self.daftar_robux.items(), start=1):
                rupiah = f"Rp.{robux.harga}"
                persen = f"{robux.diskon}%"
                table.add_row([idx, kode_robux, robux.paket_robux, robux.paket_subscription, rupiah, persen])
            print(table)

    def beli_robux(self, player, kode_robux, jumlah_robux):
        if kode_robux in self.daftar_robux:
            robux = self.daftar_robux[kode_robux]
            harga_per_robux = float(robux.harga)
            total_harga = harga_per_robux * jumlah_robux

            if robux.diskon > 0:
                diskon_amount = (robux.diskon / 100) * total_harga
                total_harga -= diskon_amount

            print(f"\n===== Struk Pembelian Atas Nama {player.nama} =====")
            print(f"Robux yang anda beli: {jumlah_robux} Robux")
            print(f"Paket Robux Yang Anda Beli Ada Diskon {robux.diskon}%")
            print(f"Jadi Total Harga Anda Menjadi: Rp.{int(total_harga)} dari Rp.{int(robux.harga)} menjadi Rp.{int((robux.diskon / 100) * harga_per_robux * jumlah_robux)}")

            if total_harga <= player.emoney:
                player.emoney -= total_harga
                print(f"Berhasil Dibeli Sekarang Sisa E-Money Anda: Rp.{int(player.emoney)}")
            else:
                print("Maaf E-Money Anda tidak Cukup")
        else:
            print(f"Kode {kode_robux} Robux Yang Anda Masukkan Salah!")

    def menu_player(self, player):
        while True:
            print(f"\n==== Selamat Datang {player.nama} ====")
            print("1. Lihat List harga paketan robux")
            print("2. Beli Robux")
            print("3. Keluar")

            pilih = input("Pilih menu(1-3): ")

            if pilih == "1":
                self.lihat_robux()
            elif pilih == "2":
                kode_robux = input("Masukkan kode Robux yang ingin dibeli: ")
                jumlah_robux = int(input("Masukkan Jumlah Paket Robux yang ingin dibeli: "))
                self.beli_robux(player, kode_robux, jumlah_robux)
            elif pilih == "3":
                break

def menu_login():
    admin_crud = CRUD()
    while True:
        print("\n==== Selamat Datang di Toko Robux Kami ====")
        print("1. Login sebagai Admin")
        print("2. Login sebagai Player")
        print("3. Keluar")

        pilih = input("Pilih menu (1-3): ")

        if pilih == "1":
            admin_crud.menu_admin()

        elif pilih == "2":
            xakun = akun("ikmalgans", 1000000) 
            player_topup = TopUp(admin_crud.daftar_robux)
            player_topup.menu_player(xakun)

        elif pilih == "3":
            print("Terima kasih. Sudah Mampir Di Toko Kami!")
            break  # Keluar dari loop setelah opsi keluar dipilih

        else:
            print("Pilihan Gak Ada Coba masukkan angka 1-3.")
            break 
        
if __name__ == "__main__":
    menu_login()
        
crud = CRUD()
crud.menu_admin()
topup = TopUp(crud.daftar_robux)
topup.menu_player(akun) 
