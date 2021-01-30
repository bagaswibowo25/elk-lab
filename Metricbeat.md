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

![select-time-field](/capture/select-time-field.PNG)

![created-index-pattern](/capture/created-index-pattern-metricbeat.png)

Setelah index pattern selesai dibuat. Cek semua data dengan membuka menu **Discover** pada kibana.

![discovery-menu-kibana](/capture/kibana-discover.png)

## 2. Membuat visualisasi

Setelah berhasil membuat index pattern selanjutnya membuat visualisasi dari data-data tersebut. Untuk membuat visualisai pergi ke menu **Visualize** pada kibana.

### a. Membuat visualisasi Up Time

Pertama-tama edit field **system.uptime.duration.ms** pada index pattern metricbeat. Tujuan diubahnya yaitu agar data tersebut dapat dibaca dengan mudah saat divisualisasikan. Pertama pergi ke **Stack Management > Index Pattern > metricbeat > Search** lalu search **system.uptime.duration** lalu edit pada field tersebut.

Ubah format pada field tersebut dari format field sebelumnya **Number** mejadi **Duration**.

![edit-system-uptime](/capture/edit-system-uptime-metric.png)

Setelah mengubah field **system.uptime.duration** selanjutnya pergi ke menu **Visualize**. Lalu buat visualisasi baru.

![create-new-visualization](/capture/create-new-visualization.png)

Setelah itu pilih tipe bentuk visualisasi. Untuk system uptime maka pilih bentuk **Metric** dan pilih sumber data dari **metricbeat**.

![select-metric-visualization](/capture/select-metric-visualization.png)
![select-metric-visualization](/capture/select-metric-source.png)

Lalu pilih opsi pada metric dengan *aggregation = max* dan pilih field *field = system.uptime.duration*.

![select-metric-visualization](/capture/create-max-system-uptime-duration.png)

Setelah pengaturan selesai, simpan visualisasi tersebut.

![save-system-uptime-visualization](/capture/save-system-uptime-visualization.png)