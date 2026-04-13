# Copilot Instructions - Excel Advanced Practice Files

## Tujuan
Dokumen ini menjadi dasar instruksi untuk AI saat membuat, merevisi, atau menambah file latihan di project ini.
Gunakan instruksi yang sama untuk file yang sudah ada (week1 sampai week7) dan file latihan berikutnya.

## Ruang Lingkup
- Semua file latihan HTML di root project.
- Fokus pada materi latihan Excel: data mentah, simulasi tabel, instruksi praktik, dan tombol salin data.

## Standar Umum Pembuatan File
- Gunakan HTML tunggal per file dengan Tailwind CDN, seperti pola file latihan yang sudah ada.
- Pertahankan gaya penulisan bahasa Indonesia untuk judul, instruksi, dan alert.
- Jangan ubah logika data/latihan yang sudah ada kecuali diminta eksplisit.
- Jika menambah fitur, lakukan perubahan minimal dan konsisten dengan pola file lain.

## Standar Konsistensi Script Copy ke Excel (WAJIB)
Semua fitur salin data harus konsisten di setiap file.

### Aturan inti
- Salin hanya plain text (TSV), bukan HTML style.
- Gunakan pemisah tab (\t) antar kolom dan newline (\n) antar baris.
- Data angka yang disalin harus angka murni tanpa pemisah ribuan.
- Data tanggal yang disalin harus format yyyy-mm-dd.
- Tetap sediakan fallback copy via textarea + document.execCommand('copy') jika Clipboard API tidak tersedia atau gagal.

### Helper yang harus digunakan
Setiap file latihan yang punya tombol salin wajib menggunakan 3 helper berikut (nama fungsi dipertahankan):
- normalizeExcelCell(cell)
- normalizeExcelText(text)
- copyPlainTextForExcel(text)

Perilaku helper:
- normalizeExcelCell:
  - Jika cell berisi tanggal ISO yyyy-mm-dd, biarkan.
  - Jika cell berisi tanggal dd/mm/yyyy, dd-mm-yyyy, atau dd.mm.yyyy, konversi ke yyyy-mm-dd.
  - Jika cell berisi nominal dengan format ribuan (contoh 1.500.000 atau 1,500,000, termasuk prefiks Rp), ubah ke digit-only tanpa separator.
- normalizeExcelText:
  - Proses setiap cell per baris TSV dengan normalizeExcelCell.
- copyPlainTextForExcel:
  - Coba navigator.clipboard.writeText terlebih dahulu.
  - Jika gagal, fallback ke textarea + execCommand.

## Aturan Data Latihan
- Untuk tampilan di web, angka boleh diformat ramah baca (misal toLocaleString) jika dibutuhkan.
- Untuk data yang disalin, tetap gunakan angka mentah.
- Untuk tampilan di web, tanggal boleh ditampilkan sama dengan sumber data; untuk data salin tetap wajib yyyy-mm-dd.
- Jangan menyisipkan formula Excel otomatis ke data salin kecuali memang bagian dari instruksi latihan.

## Aturan UI dan Konten
- Pertahankan struktur komponen latihan: header, instruksi, tabel referensi, area latihan, dan tombol salin.
- Jaga kompatibilitas desktop dan mobile seperti file yang sudah ada.
- Hindari perubahan visual besar jika tidak diminta.

## Aturan Saat Menambah File Latihan Baru
Untuk file week berikutnya:
- Ikuti pola struktur halaman dari file minggu sebelumnya.
- Sediakan minimal satu tombol salin data latihan.
- Terapkan helper normalisasi copy yang sama persis agar konsisten lintas minggu.
- Pastikan dataset salin bisa langsung di-paste ke Excel mulai dari sel A1.

## Checklist Sebelum Menyelesaikan Perubahan
- Tombol salin menyalin plain text, bukan HTML style.
- Angka hasil salin tanpa separator ribuan.
- Tanggal hasil salin format yyyy-mm-dd.
- Fallback copy tersedia jika Clipboard API gagal.
- Tidak ada perubahan logika latihan yang tidak diminta.
