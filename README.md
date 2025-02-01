# **Project Based Internship: Big Data Analytics - Kimia Farma**

Tool : BigQuery  <br>
Visualization : Looker Data Studio  <br>
Dataset : VIX Kimia Farma

---

## Introduction

Project Based Internship Big Data Analytics Kimia Farma merupakan program virtual internship berbasis project yang difasilitasi oleh Rakamin Academy. Pada project ini saya berperan sebagai Data Analyst Intern yang diminta untuk menganalisis dan membuat laporan penjualan perusahaan menggunakan data-data yang telah disediakan. Dari project ini, saya juga banyak belajar tentang data data warehouse, datalake, dan datamart.


Objectives

- Membuat design datamart (Tabel analisa) dari dataset yang sudah disediakan
- Membuat visualisasi/dashboard **Performance Analysis** perusahaan

Dataset
Dataset yang disediakan terdiri dari tabel-tabel berikut:

- Final Transaction
- Kantor Cabang
- Inventory
- Product

---

# Design Datamart

## Tabel Analisa 

tabel analisa adalah tabel yang berisi data - data gabungan yang berasa dari ke empat tabel yang ada  dan beberapa kolom yang sudah dilakukan perubahan untuk kebutuhan dan memudahkan analisa dan mempunyai primary key <br>
yaitu transaction_id.</p>

<details>
  <summary> Klik untuk melihat Query </summary>
    <br>
 ```sql
SELECT 
ft.transaction_id, 
ft.date, 
ft.branch_id,
kc.branch_name, 
kc.kota, 
kc.provinsi, 
kc.rating AS rating_cabang, 
ft.customer_name, 
ft.product_id, 
p.product_name,
p.price AS actual_price, 
ft.discount_percentage, 
CASE WHEN p.price <= 50000 THEN 0.1
     WHEN p.price BETWEEN 50000 AND 100000 THEN 0.15
     WHEN p.price BETWEEN 100000 AND 300000 THEN 0.2
     WHEN p.price BETWEEN 300000 AND 500000 THEN 0.25
     WHEN p.price <= 500000 THEN 0.3
END AS persentase_gross_laba,
(p.price * (1-ft.discount_percentage)) AS nett_sales, 
(p.price * (CASE 
               WHEN p.price <= 50000 THEN 0.1
               WHEN p.price BETWEEN 50000 AND 100000 THEN 0.15
               WHEN p.price BETWEEN 100000 AND 300000 THEN 0.2
               WHEN p.price BETWEEN 300000 AND 500000 THEN 0.25
               ELSE 0.3
          END)) AS nett_profit,
ft.rating AS rating_transaksi
FROM kimia_farma.kf_final_transaction AS ft
JOIN kimia_farma.kf_kantor_cabang AS kc ON ft.branch_id = kc.branch_id
JOIN kimia_farma.kf_product As p ON ft.product_id = p.product_id
```
<br>
</details>
<br>

![Screenshot 2025-02-01 100336](https://github.com/user-attachments/assets/12dd3617-d00a-4b02-8ee1-41687a1fe299)

   </kbd> <br> Gambar 1 — Sampel Hasil Pembuatan Tabel Analisa  


<br>

---                                
# **Data Vizualisation**
[Klik untuk melihat hasil analisa di LookerStudio](https://lookerstudio.google.com/reporting/b4c9f280-8d2a-4510-bf21-c6ee7d5120e6)


![Screenshot 2024-03-02 at 00 18 43](https://github.com/afifhibban21/Big-Data-Analytic-Performance-Analysis-Kimia-Farma/assets/117912771/d1733720-a815-42ea-b66b-81134ad892a9)

   </kbd> <br> Gambar 2 — Performance Analysis Dashboard Kimia Farma
    


---
