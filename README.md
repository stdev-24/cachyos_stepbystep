Untuk mulai instalasi CachyOS sesuai rancangan kita — **CachyOS + Hyprland + Quickshell custom + Foot + Zsh + Btrfs + Limine** — sebaiknya kita kerjakan bertahap. Yang paling penting: pastikan installer hanya menyentuh SSD baru 256 GB, bukan SSD Fedora lama.

## **Tahap 1 — Persiapan sebelum instalasi**

1. **Pastikan SSD baru kompatibel.** Laptop Acer Aspire A315-35 memiliki beberapa variasi konfigurasi. Kita belum memastikan apakah slot M.2 pada unitmu menerima SSD SATA atau hanya NVMe. Jangan lanjut sebelum tipe SSD dan kompatibilitasnya jelas.
2. **Backup data penting** dari Fedora, termasuk file proyek Next.js, konfigurasi, SSH key, dan dokumen.
3. Siapkan:
   - Flashdisk minimal 8 GB.
   - Koneksi internet.
   - Charger laptop terpasang.
   - SSD baru 256 GB sudah terpasang.
4. Unduh ISO CachyOS dari situs resminya: [CachyOS Download](https://cachyos.org/download/?utm_source=chatgpt.com).

## **Tahap 2 — Buat USB installer**

1. Unduh ISO CachyOS.
2. Tulis ISO ke flashdisk menggunakan Fedora Media Writer, Ventoy, atau balenaEtcher.
3. Setelah selesai, restart laptop.
4. Masuk Boot Menu BIOS/UEFI Acer (umumnya tombol **F12**; mungkin perlu mengaktifkan F12 Boot Menu di BIOS).
5. Pilih USB installer dalam mode UEFI.

## **Tahap 3 — Konfigurasi BIOS**

Sebelum instalasi, periksa:

- Boot mode: **UEFI**.
- Secure Boot: **Disabled**, jika diwajibkan oleh installer.
- CSM/Legacy: **Disabled**.
- Jangan mengubah atau menghapus entri boot Fedora lama.

## **Tahap 4 — Instal CachyOS ke SSD baru**

Bagian paling berisiko

Pilih instalasi manual, bukan *Install alongside* atau *Replace partition*. Panduan resmi CachyOS juga menyarankan partisi manual karena pilihan otomatis tersebut tidak selalu sesuai untuk semua konfigurasi.&#x20;

[image](https://www.google.com/s2/favicons?domain=https://wiki.cachyos.org\&sz=32)

CachyOS



Rencana partisi SSD baru:

| Partisi | Ukuran         | Format / mount |
| ------- | -------------- | -------------- |
| Boot    | 4192 MiB       | FAT32, `/boot` |
| Root    | Sisa kapasitas | Btrfs, `/`     |

Untuk konfigurasi Limine, partisi `/boot` FAT32 perlu disediakan dengan ukuran sekitar 4 GiB atau mengikuti rekomendasi installer.&#x20;

[image](https://www.google.com/s2/favicons?domain=https://wiki.cachyos.org\&sz=32)

CachyOS+1



**Perhatian:** jangan format, hapus, atau jadikan EFI Fedora lama sebagai target instalasi. Pastikan setiap partisi yang dibuat berada di SSD 256 GB yang baru.

Lalu pilih:

- Bootloader: **Limine**
- Filesystem: **Btrfs**
- Desktop environment: **No Desktop / minimal**, jika opsi tersebut tersedia
- Buat user dan password
- Jalankan instalasi

## **Tahap 5 — Setelah berhasil masuk CachyOS**

Urutan konfigurasi yang akan kita lakukan:

1. Update sistem.
2. Aktifkan NetworkManager dan PipeWire.
3. Pasang Hyprland dan komponen Wayland yang dibutuhkan.
4. Pasang Foot dan Zsh.
5. Konfigurasi login TTY tanpa Display Manager, jika tetap ingin model tersebut.
6. Pasang Quickshell dan mulai buat shell sendiri dengan QML.
7. Konfigurasi Snapper dan integrasi snapshot dengan Limine.
8. Pasang VS Code, Node.js, dan pnpm untuk pengembangan Next.js.
