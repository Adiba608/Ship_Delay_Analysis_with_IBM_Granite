# Analisis Keterlambatan Kapal dengan IBM Granite

## Project Overview
Proyek ini bertujuan untuk menganalisis penyebab keterlambatan kapal menggunakan model AI **IBM Granite-3.0-8b-instruct**. Fokus utama meliputi:
- Klasifikasi penyebab keterlambatan (Cuaca, Teknis, Logistik, Bea Cukai, atau Lainnya).
- Pembuatan ringkasan otomatis dari laporan keterlambatan.
- Visualisasi data untuk identifikasi pola dominan.

Dataset berisi catatan historis keterlambatan kapal, termasuk deskripsi kejadian dan durasi. Proyek ini cocok untuk manajemen logistik, pelabuhan, atau operator kapal.

---

## Raw Dataset
Dataset sederhana yang digunakan dalam proyek ini dapat diakses melalui struktur berikut (format dictionary Python):
```python
data = {
    "tanggal": ["2023-01-10", "2023-02-15", "2023-03-20", "2023-04-05"],
    "deskripsi": [
        "Kapal delay karena badai di Laut Jawa",
        "Kerusakan mesin menyebabkan keterlambatan 12 jam",
        "Pemeriksaan bea cukai memakan waktu 24 jam",
        "Keterlambatan bongkar muat di pelabuhan"
    ],
    "durasi_jam": [24, 12, 24, 8]
}

## Insight & findings
HASIL RINGKASAN:
1. Keterlambatan disebabkan oleh faktor cuaca (badai) dan teknis (kerusakan mesin).
2. Proses bea cukai dan bongkar muat berkontribusi pada delay hingga 24 jam.
3. Diperlukan mitigasi untuk faktor cuaca dan optimasi proses logistik.

## AI Support Explanation
1. Klasifikasi Penyebab
def klasifikasi_penyebab(teks):
    prompt = f"Klasifikasikan penyebab keterlambatan kapal berikut ke dalam salah satu kategori: [Cuaca, Teknis, Logistik, Bea Cukai, Lainnya]..."
    response = replicate.run("ibm-granite/granite-3.0-8b-instruct", input={"prompt": prompt, "max_tokens": 10})
    return response

2. Summarization
def buat_ringkasan(daftar_teks):
    prompt = f"Buatlah ringkasan laporan keterlambatan kapal dalam 3 poin penting: - {gabungan_teks}..."
    response = replicate.run("ibm-granite/granite-3.0-8b-instruct", input={"prompt": prompt, "max_tokens": 150})

3. Fallback Rule-Based
kategori_manual = {
    "badai": "Cuaca",
    "mesin": "Teknis",
    "bea cukai": "Bea Cukai",
    "bongkar muat": "Logistik"
}

4. Visualisasi
plt.bar(df["tanggal"], df["durasi_jam"], color='skyblue')
plt.title("Durasi Keterlambatan per Kejadian")
plt.xlabel("Tanggal")
plt.ylabel("Durasi (Jam)")