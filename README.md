# UAS-OCR 
# Optical Character Recognition (OCR) with VLM using Gemma 3 12B

Proyek ini bertujuan untuk mengekstrak teks dari plat nomor kendaraan menggunakan pendekatan Visual Language Model (VLM). Model yang digunakan adalah `google/gemma-3-12b`, dijalankan melalui LM Studio dan diintegrasikan dengan Python. Selain melakukan prediksi, proyek ini juga mengevaluasi akurasi menggunakan Character Error Rate (CER).

## 📁 Struktur Proyek


## 🚀 Cara Menjalankan

### 1. Persiapan Awal
- Unduh dan install [LM Studio](https://lmstudio.ai)
- Aktifkan opsi **Enable local server** di LM Studio
- Pastikan model `google/gemma-3-12b` telah tersedia dan berjalan di LM Studio

### 2. Instalasi Dependensi Python

```bash
pip install openai pillow python-Levenshtein pandas
What is the license plate number shown in this image? Respond only with the plate number.
import requests
import base64

def ask_vlm(image_path):
    with open(image_path, "rb") as img_file:
        base64_img = base64.b64encode(img_file.read()).decode("utf-8")

    payload = {
        "model": "google/gemma-3-12b",
        "messages": [
            {"role": "user", "content": [
                {"type": "text", "text": "What is the license plate number shown in this image? Respond only with the plate number."},
                {"type": "image_url", "image_url": {"url": f"data:image/jpeg;base64,{base64_img}"}}
            ]}
        ]
    }

    response = requests.post("http://localhost:1234/v1/chat/completions", json=payload)
    return response.json()["choices"][0]["message"]["content"]
CER = (S + D + I) / N
image,ground_truth,prediction,CER_score
img001.jpg,B1234XYZ,B1234XY,0.14
