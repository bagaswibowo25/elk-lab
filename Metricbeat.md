# Membuat Visualisasi Metric Resource Kibana

Setelah melakukan pemasangan dan konfigurasi dari semua package yang diperlukan. Maka langkah selanjutnya adalah membuat index pattern untuk mengakses data elasticsearch yang akan dieksplor.

## 1. Menambahkan Index Pattern
Buka halaman kibana pada browser di http://pod06-elk:5601.

```sh
http://10.10.6.10:5601
```
![kibana-app](/capture/kibana-app-url.PNG)

Setelah halaman kibana terbuka, selanjutnya buka pengaturan **Stack Management** pada menu kibana.

![stack-management](/capture/stack-management-kibana.PNG)

Selanjutnya pilih menu **Index Pattern > Create Index pattern**.

![kibana-index-pattern](/capture/kibana-index-pattern-menu.PNG)

![create-index-pattern](/capture/create-index-pattern-menu.png)

Selanjutnya buat definisi untuk index pattern. Karena terdapat beberapa index dari elasticsearch, maka gunakan asterisk untuk memilih seluruh index terkait dengan metricbeat.

![define-index-pattern](/capture/define-index-pattern.png)


