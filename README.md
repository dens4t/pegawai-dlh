# Go Pegawai (TUI)

Aplikasi desktop ringan berbasis Go (Terminal UI) untuk pengecekan data kepegawaian.

## Fitur Utama

- TUI cepat dan ringan (cocok untuk spesifikasi rendah)
- Pencarian realtime (Nama, Jabatan, Unit Kerja, NIP, Email)
- Detail data pegawai lengkap
- Dukungan file data eksternal `pegawai.csv`
- Dukungan delimiter data: `;`, `,`, atau tab
- Instalasi awal Windows untuk akses `Win + R`

## Struktur Penting

- `pegawai.exe` / `pegawai` : binary aplikasi
- `pegawai.csv` : sumber data utama (wajib)
- `pegawai.csv.template` : template header data
- `config.json` : konfigurasi lebar kolom

## Menjalankan Aplikasi

### Windows

1. Jalankan `pegawai.exe` pertama kali.
2. Ikuti proses instalasi awal (opsi `y/n`).
3. Setelah terpasang, jalankan lewat `Win + R` lalu ketik:

```text
pegawai
```

### Linux

```bash
./pegawai
```

## Sumber Data CSV

Aplikasi hanya membaca file eksternal `pegawai.csv` di folder executable.

Jika file belum ada, aplikasi akan menampilkan pesan lokasi folder tujuan dan menunggu Enter sebelum menutup (di Windows).

> Gunakan `pegawai.csv.template` sebagai acuan header.

## Format CSV yang Didukung

- Separator titik koma (`;`) — umum dari Excel regional Indonesia
- Separator koma (`,`) 
- Separator tab (`\t`)

Nama file tetap: `pegawai.csv`.

## Konfigurasi Kolom

File `config.json` dibuat otomatis saat pertama kali aplikasi berjalan (jika belum ada).

Contoh:

```json
{
  "columns": {
    "nama": 30,
    "jabatan": 34,
    "unit_kerja": 34,
    "gol": 10,
    "status": 14
  }
}
```

## Kontrol Keyboard TUI

- `/` : fokus ke kolom pencarian
- `Esc` : lepas fokus pencarian / kembali dari detail
- `↑` / `↓` : navigasi baris
- `Enter` : buka detail pegawai
- `q` : keluar aplikasi

## Build dari Source

```bash
go test ./...
go build -ldflags="-s -w" -o pegawai .
GOOS=windows GOARCH=amd64 go build -ldflags="-s -w" -o pegawai.exe .
```

## Catatan Installer Windows

- Jika sudah ada instalasi sebelumnya, aplikasi akan menanyakan konfirmasi `y/n` untuk overwrite.
- Lokasi instalasi default:

```text
%LOCALAPPDATA%\GoPegawai\bin
```

Folder tersebut ditambahkan ke User PATH agar bisa dipanggil dari `Win + R`.
