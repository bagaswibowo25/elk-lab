# Membuat Visualisasi Resource Kibana

Setelah melakukan pemasangan dan konfigurasi dari semua package yang diperlukan. Maka langkah selanjutnya adalah membuat index pattern untuk mengakses data elasticsearch yang akan dieksplor.

## 1. Menambahkan Index Pattern
Buka halaman kibana pada browser.
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

### b. Membuat Visualisasi Jumlah Core CPU

Buat visualize baru. Pilih tipe bentuk visualisasi. Untuk melihat total **CPU Cores** maka pilih bentuk **Metric** dan pilih sumber data dari **metricbeat**.

![select-metric-visualization](/capture/select-metric-visualization.png)
![select-metric-visualization](/capture/select-metric-source.png)

Lalu pilih opsi pada metric dengan *aggregation = max* dan pilih field *field = system.uptime.duration*.

![total-cpu-core](capture/create-max-cpu-core.png)

Setelah selesai simpan visualisasi tersebut.

![save-cpu-core](capture/save-cpu-core-visualization.png)

### c. Membuat Visualisasi Total Memory

Pertama-tama edit field **system.memory.total** pada index pattern metricbeat. Tujuan diubahnya yaitu agar data tersebut dapat dibaca dengan mudah saat divisualisasikan. Pertama pergi ke **Stack Management > Index Pattern > metricbeat > Search** lalu search **system.memory.total** lalu edit pada field tersebut.

Ubah format pada field tersebut dari format field sebelumnya **Number** mejadi **Bytes**.

![edit-system-memory-total](/capture/edit-system-memory-total.png)

Setelah selesai mengedit simpan perubahan dan pindah ke halaman **Visualize** lalu buat visualize baru dan pilih tipe bentuk visualisasi. Untuk melihat total bytes **memory** maka pilih bentuk **Metric** dan pilih sumber data dari **metricbeat**.

![select-metric-visualization](/capture/select-metric-visualization.png)
![select-metric-visualization](/capture/select-metric-source.png)

Lalu pilih opsi pada metric dengan *aggregation = Average* dan pilih field *field = system.memory.total*.

![create-total-memory](/capture/create-total-memory.png)

Jika sudah selesai simpan visualisasi tersebut/

![simpan-total-memory](capture/save-total-memory-metric.png)

### d. Membuat Visualisasi Disk Space

Pertama-tama edit field **system.filesystem.total** pada index pattern metricbeat. Tujuan diubahnya yaitu agar data tersebut dapat dibaca dengan mudah saat divisualisasikan. Pertama pergi ke **Stack Management > Index Pattern > metricbeat > Search** lalu search **system.filesystem.total** lalu edit pada field tersebut.

Ubah format pada field tersebut dari format field sebelumnya **Number** mejadi **Bytes**.

![edit-system-filesystem-total](/capture/edit-system-filesystem-total.png)

Setelah selesai mengedit simpan perubahan dan pindah ke halaman **Visualize** lalu buat visualize baru dan pilih tipe bentuk visualisasi. Untuk melihat total bytes dari **Disk** maka pilih bentuk **Metric** dan pilih sumber data dari **metricbeat**.

![select-metric-visualization](/capture/select-metric-visualization.png)
![select-metric-visualization](/capture/select-metric-source.png)

Lalu pilih opsi pada metric dengan *aggregation = Max* dan pilih field *field = system.filesystem.total*.

![create-total-memory](/capture/create-system-filesystem-total.png)

Jika sudah selesai simpan visualisasi tersebut.

![simpan-total-memory](capture/save-system-filesystem-total-visualization.png)

### Membuat Visualisasi Outbound Traffic Network

Pertama-tama pergi ke halaman **Visualize** lalu bentuk yang dipilih adalah **TSVB** karena untuk melihat jumlah **bytes/s** dari metric **system.network.out.bytes**

![select-tsvc-visual](capture/select-tsvb-visualization.png)

Atur semua pengaturan data seperti pada gambar dibawah ini. Untuk menampilkan metric secara realtime

![create-outbound-traffic](capture/create-traffic-outbound.png)