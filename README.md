# OCR Plat Nomor Kendaraan dengan VLM (Gemma 3 12B)

Proyek ini bertujuan untuk membaca teks dari plat nomor kendaraan menggunakan pendekatan Visual Language Model (VLM) yang dijalankan melalui LM Studio dan diintegrasikan dengan Python.

---

## 🔍 Konsep Utama

### Apa itu VLM?

Visual Language Model (VLM) adalah jenis model kecerdasan buatan multimodal yang bisa menerima input berupa gambar dan teks, lalu menghasilkan output berbasis pemahaman keduanya. Model ini digunakan untuk tugas seperti deskripsi gambar, tanya jawab visual, hingga OCR (Optical Character Recognition).

### Mengapa VLM untuk OCR?

Berbeda dengan metode OCR tradisional yang biasanya mengandalkan model deteksi huruf secara eksplisit, VLM seperti `google/gemma-3-12b` bisa langsung memahami isi gambar dan menjawab dengan jawaban berbasis konteks visual, termasuk plat nomor.

---

## 🔄 Alur Kerja Proyek

1. **Input Gambar**
   - Gambar plat nomor dikumpulkan dalam folder `/images`
   - Dataset dikaitkan dengan file `label.csv` berisi ground truth

2. **Koneksi ke LM Studio**
   - LM Studio dijalankan secara lokal
   - Model `google/gemma-3-12b` digunakan
   - Server lokal LM Studio aktif di `http://localhost:1234`

3. **Inferensi (Prediksi Plat Nomor)**
   - Gambar dikirim melalui API LM Studio bersama prompt:
     > What is the license plate number shown in this image? Respond only with the plate number.
   - Model membalas dengan prediksi plat nomor dalam format teks

4. **Evaluasi Akurasi (CER)**
   - Prediksi dibandingkan dengan label ground truth
   - Dihitung Character Error Rate (CER) menggunakan rumus:
     ```
     CER = (S + D + I) / N
     ```
     Di mana:
     - S = Substitusi karakter
     - D = Karakter yang dihapus
     - I = Karakter yang disisipkan
     - N = Total karakter pada label asli

5. **Penyimpanan Hasil**
   - Hasil disimpan dalam `results.csv` dengan format:
     ```
     image,ground_truth,prediction,CER_score
     ```

6. **Analisis**
   - Kasus dengan hasil baik dan buruk dianalisis untuk mengevaluasi kelemahan model
   - Performa model dipengaruhi oleh kualitas gambar, cahaya, dan resolusi

---

## 💡 Catatan

- Model multimodal mampu membaca plat nomor secara langsung dari gambar tanpa perlu training ulang
- LM Studio menyediakan antarmuka lokal yang memudahkan integrasi antara Python dan model LLM/VLM
- Proyek ini menunjukkan potensi VLM sebagai alternatif ringan dan fleksibel untuk OCR tugas ringan

---

## 📚 Referensi

- LM Studio: https://lmstudio.ai
- Dokumentasi image input LM Studio: https://lmstudio.ai/docs/python/llm-prediction/image-input
- Model: [`google/gemma-3-12b`](https://huggingface.co/google/gemma-3b)
- Evaluasi CER: via `python-Levenshtein`

