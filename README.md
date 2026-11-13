# PoC Chatbot Layanan Nasabah Berbasis LLM + RAG

Proof of concept untuk dokumen *Rancangan Arsitektur Solusi AI untuk Layanan Informasi Nasabah pada Sektor Perbankan* (tugas mata kuliah Sistem Kecerdasan Buatan). PoC membandingkan dua konfigurasi pada 30 pertanyaan uji:

- **B0**: LLM tanpa RAG.
- **R1**: RAG dengan embedding bge-m3, ChromaDB, chunk 500 token, overlap 10%, K = 5, klasifikasi intent, dan ambang skor retrieval 0,30.

Seluruh dokumen, tarif, produk, dan nama bank (PT Bank Nusantara Mandiri) bersifat **fiktif**.

## Isi repositori

| File | Fungsi |
|---|---|
| `poc_rag_bank_nusantara_mandiri.ipynb` | Notebook 1: indeks dokumen, menjalankan B0 dan R1, menghasilkan `hasil_mentah.csv` dan `lembar_penilaian.csv` |
| `poc_rag_bank_nusantara_mandiri_lanjutan.ipynb` | Notebook 2: menghitung metrik Ragas dan ringkasan hasil dari `hasil_mentah.csv` (tidak membuat jawaban baru) |
| `poc_data.zip` | Data masukan Notebook 1: 4 dokumen fiktif dan 30 pertanyaan uji |
| `poc_lanjutan.zip` | Data masukan Notebook 2: `hasil_mentah.csv`, `lembar_penilaian_terisi.csv`, dan folder `poc/` |

## Prasyarat

- Akun Google dengan akses ke [Google Colab](https://colab.research.google.com).
- API key Gemini dari [Google AI Studio](https://aistudio.google.com).
- Disarankan memakai GPU (Runtime > Change runtime type) agar embedding bge-m3 lebih cepat. CPU tetap bisa.

## Cara menjalankan

1. Di Colab, buka ikon kunci (Secrets), tambahkan secret `GOOGLE_API_KEY` berisi API key, lalu aktifkan *Notebook access*.
2. Unggah `poc_rag_bank_nusantara_mandiri.ipynb` ke Colab, lalu unggah `poc_data.zip` ke panel File (atau biarkan sel unggah memintanya).
3. Jalankan **Runtime > Run all**. Di akhir, `hasil_mentah.csv` dan `lembar_penilaian.csv` terunduh.
4. Buka `lembar_penilaian.csv` dan isi kolom `nilai_B0` dan `nilai_R1` dengan `benar`, `sebagian`, atau `salah` untuk 20 pertanyaan `dalam_cakupan`, dengan membandingkan jawaban terhadap `jawaban_referensi`.
5. Unggah `poc_rag_bank_nusantara_mandiri_lanjutan.ipynb`, jalankan sel satu per satu dari atas, dan unggah `poc_lanjutan.zip` saat diminta. Hasil Ragas dan ringkasan (`ringkasan_poc.csv`) terunduh sebagai `hasil_poc.zip`.

## Keterbatasan

- Set uji kecil (30 pertanyaan) dan seluruh data fiktif, jadi hasilnya tidak dapat digeneralisasi ke data bank sungguhan.
