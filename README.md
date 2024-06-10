#include <iostream>
#include <vector>
#include <string>
#include <cstring>
using namespace std;

// Struktur Buku
struct Buku {
    char judul[100];
    char penulis[100];
    int tahun;

    Buku(const char* j, const char* p, int t) : tahun(t) {
        strncpy(judul, j, 99);
        judul[99] = '\0';
        strncpy(penulis, p, 99);
        penulis[99] = '\0';
    }
};

// Kelas Perpustakaan
class Perpustakaan {
    vector<Buku*> koleksiBuku;

public:
    ~Perpustakaan() {
        for (auto& buku : koleksiBuku) {
            delete buku;
        }
    }

    void tambahBuku(const Buku& buku) {
        Buku* bukuBaru = new Buku(buku);
        koleksiBuku.push_back(bukuBaru);
    }

    void tampilkanBuku() const {
        for (const auto& buku : koleksiBuku) {
            cout << "Judul: " << buku->judul << ", Penulis: " << buku->penulis << ", Tahun: " << buku->tahun <<endl;
        }
    }

    bool cariBuku(const char* judul) const {
        for (const auto& buku : koleksiBuku) {
            if (strcmp(buku->judul, judul) == 0) {
                return true;
            }
        }
        return false;
    }
};

// Fungsi untuk menambahkan buku
void tambahBukuKePerpustakaan(Perpustakaan& perpustakaan) {
    char judul[100];
    char penulis[100];
    int tahun;

    cout << "Masukkan judul buku: ";
    cin.ignore();
    cin.getline(judul, 100);

    cout << "Masukkan penulis buku: ";
    cin.getline(penulis, 100);

    cout << "Masukkan tahun terbit: ";
    cin >> tahun;

    Buku buku(judul, penulis, tahun);
    perpustakaan.tambahBuku(buku);
    cout << "Buku berhasil ditambahkan!\n";
}

// Fungsi untuk mencari buku
void cariBukuDiPerpustakaan(const Perpustakaan& perpustakaan) {
    char judul[100];
    cout << "Masukkan judul buku yang ingin dicari: ";
    cin.ignore();
    cin.getline(judul, 100);

    if (perpustakaan.cariBuku(judul)) {
        cout << "Buku \"" << judul << "\" tersedia di perpustakaan.\n";
    } else {
        cout << "Buku \"" << judul << "\" tidak tersedia di perpustakaan.\n";
    }
}

// Fungsi untuk menampilkan semua buku
void tampilkanSemuaBuku(const Perpustakaan& perpustakaan) {
    cout << "Buku-buku di perpustakaan:\n";
    perpustakaan.tampilkanBuku();
}

// Fungsi utama
int main() {
    Perpustakaan perpustakaan;
    int pilihan;

    do {
        cout << "\nMenu Perpustakaan:\n";
        cout << "1. Tambah Buku\n";
        cout << "2. Cari Buku\n";
        cout << "3. Tampilkan Semua Buku\n";
        cout << "4. Keluar\n";
        cout << "Masukkan pilihan: ";
        cin >> pilihan;

        switch (pilihan) {
            case 1:
                tambahBukuKePerpustakaan(perpustakaan);
                break;
            case 2:
                cariBukuDiPerpustakaan(perpustakaan);
                break;
            case 3:
                tampilkanSemuaBuku(perpustakaan);
                break;
            case 4:
                cout << "Keluar dari program.\n";
                break;
            default:
                cout << "Pilihan tidak valid. Silakan coba lagi.\n";
        }
    } while (pilihan != 4);

    return 0;
}

//Link screenshot hasil program (output)
[https://drive.google.com/file/d/1y5DXjFyk0fTz5eTTmY-OQ9vpoxOQM0ry/view?usp=drivesdk]

//Llink vidio persentasi
[https://drive.google.com/file/d/1y-X_y1gFpUFlIX_tXkBaGIhERQbvrRUP/view?usp=drivesdk]
