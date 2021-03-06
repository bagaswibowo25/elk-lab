# Membuat Visualisasi Resource Kibana

Setelah melakukan pemasangan dan konfigurasi dari semua package yang diperlukan. Maka langkah selanjutnya adalah membuat index pattern untuk mengakses data elasticsearch yang akan dieksplor.

## 1. Menambahkan Index Pattern
Buka halaman kibana pada browser.
```sh
http://10.10.6.10:5601
```
![kibana-app](capture/kibana-app-url.PNG)

Setelah halaman kibana terbuka, selanjutnya buka pengaturan **Stack Management** pada menu kibana.

![stack-management](capture/stack-management-kibana.PNG)

Selanjutnya pilih menu **Index Pattern > Create Index pattern**.

![kibana-index-pattern](capture/kibana-index-pattern-menu.PNG)

![create-index-pattern](capture/create-index-pattern-menu.png)

Selanjutnya buat definisi untuk index pattern. Karena terdapat beberapa index dari elasticsearch, maka gunakan asterisk untuk memilih seluruh index terkait dengan metricbeat.

![define-index-pattern](capture/define-index-pattern.png)

![select-time-field](capture/select-time-field.PNG)

![created-index-pattern](capture/created-index-pattern-metricbeat.png)

Setelah index pattern selesai dibuat. Cek semua data dengan membuka menu **Discover** pada kibana.

![discovery-menu-kibana](capture/kibana-discover.png)

## 2. Membuat Visualisasi

Setelah berhasil membuat index pattern selanjutnya membuat visualisasi dari data-data tersebut. Untuk membuat visualisai pergi ke menu **Visualize** pada kibana.

### a. Membuat Visualisasi Up Time

Pertama-tama edit field **system.uptime.duration.ms** pada index pattern metricbeat. Tujuan diubahnya yaitu agar data tersebut dapat dibaca dengan mudah saat divisualisasikan. Pertama pergi ke **Stack Management > Index Pattern > metricbeat > Search** lalu search **system.uptime.duration** lalu edit pada field tersebut.

Ubah format pada field tersebut dari format field sebelumnya **Number** mejadi **Duration**.

![edit-system-uptime](capture/edit-system-uptime-metric.png)

Setelah mengubah field **system.uptime.duration** selanjutnya pergi ke menu **Visualize**. Lalu buat visualisasi baru.

![create-new-visualization](capture/create-new-visualization.png)

Setelah itu pilih tipe bentuk visualisasi. Untuk system uptime maka pilih bentuk **Metric** dan pilih sumber data dari **metricbeat**.

![select-metric-visualization](capture/select-metric-visualization.png)
![select-metric-visualization](capture/select-metric-source.png)

Lalu pilih opsi pada metric dengan *aggregation = max* dan pilih field *field = system.uptime.duration*.

![select-metric-visualization](capture/create-max-system-uptime-duration.png)

Setelah pengaturan selesai, simpan visualisasi tersebut.

![save-system-uptime-visualization](capture/save-system-uptime-visualization.png)

### b. Membuat Visualisasi Jumlah Core CPU

Buat visualize baru. Pilih tipe bentuk visualisasi. Untuk melihat total **CPU Cores** maka pilih bentuk **Metric** dan pilih sumber data dari **metricbeat**.

![select-metric-visualization](capture/select-metric-visualization.png)
![select-metric-visualization](capture/select-metric-source.png)

Lalu pilih opsi pada metric dengan *aggregation = max* dan pilih field *field = system.uptime.duration*.

![total-cpu-core](capture/create-max-cpu-core.png)

Setelah selesai simpan visualisasi tersebut.

![save-cpu-core](capture/save-cpu-core-visualization.png)

### c. Membuat Visualisasi Total Memory

Pertama-tama edit field **system.memory.total** pada index pattern metricbeat. Tujuan diubahnya yaitu agar data tersebut dapat dibaca dengan mudah saat divisualisasikan. Pertama pergi ke **Stack Management > Index Pattern > metricbeat > Search** lalu search **system.memory.total** lalu edit pada field tersebut.

Ubah format pada field tersebut dari format field sebelumnya **Number** mejadi **Bytes**.

![edit-system-memory-total](capture/edit-system-memory-total.png)

Setelah selesai mengedit simpan perubahan dan pindah ke halaman **Visualize** lalu buat visualize baru dan pilih tipe bentuk visualisasi. Untuk melihat total bytes **memory** maka pilih bentuk **Metric** dan pilih sumber data dari **metricbeat**.

![select-metric-visualization](capture/select-metric-visualization.png)
![select-metric-visualization](capture/select-metric-source.png)

Lalu pilih opsi pada metric dengan *aggregation = Average* dan pilih field *field = system.memory.total*.

![create-total-memory](capture/create-total-memory.png)

Jika sudah selesai simpan visualisasi tersebut/

![simpan-total-memory](capture/save-total-memory-metric.png)

### d. Membuat Visualisasi Disk Space

Pertama-tama edit field **system.filesystem.total** pada index pattern metricbeat. Tujuan diubahnya yaitu agar data tersebut dapat dibaca dengan mudah saat divisualisasikan. Pertama pergi ke **Stack Management > Index Pattern > metricbeat > Search** lalu search **system.filesystem.total** lalu edit pada field tersebut.

Ubah format pada field tersebut dari format field sebelumnya **Number** mejadi **Bytes**.

![edit-system-filesystem-total](capture/edit-system-filesystem-total.png)

Setelah selesai mengedit simpan perubahan dan pindah ke halaman **Visualize** lalu buat visualize baru dan pilih tipe bentuk visualisasi. Untuk melihat total bytes dari **Disk** maka pilih bentuk **Metric** dan pilih sumber data dari **metricbeat**.

![select-metric-visualization](capture/select-metric-visualization.png)
![select-metric-visualization](capture/select-metric-source.png)

Lalu pilih opsi pada metric dengan *aggregation = Max* dan pilih field *field = system.filesystem.total*.

![create-total-memory](capture/create-system-filesystem-total.png)

Jika sudah selesai simpan visualisasi tersebut.

![simpan-total-memory](capture/save-system-filesystem-total-visualization.png)

### e. Membuat Visualisasi Outbound Traffic Network

Pertama-tama pergi ke halaman **Visualize** lalu bentuk yang dipilih adalah **TSVB** karena untuk melihat jumlah **bytes/s** dari metric **system.network.out.bytes**

![select-tsvc-visual](capture/select-tsvb-visualization.png)

Atur semua pengaturan data seperti pada gambar dibawah ini. Untuk menampilkan metric secara realtime

![create-outbound-traffic](capture/create-traffic-outbound.png)

Pada bagian *metric options* ubah format data default menjadi bytes.

![edit-metric-optios-outbound-traffic](capture/create-traffic-outbound-options.png)

Untuk menampilkan total bytes yang telah dikeluarkan tambahkan metric baru lagi dalam data tersebut.

![total-outbound-traffic](capture/create-traffic-outbound-total-transfered.png)

Setelah selesai membuatnya, simpan visualisasi tersebut.

### f. Membuat Visualisasi Inbound Traffic Network

Pertama-tama pergi ke halaman **Visualize** lalu bentuk yang dipilih adalah **TSVB** karena untuk melihat jumlah **bytes/s** dari metric **system.network.in.bytes**

![select-tsvc-visual](capture/select-tsvb-visualization.png)

Atur semua pengaturan data seperti pada gambar dibawah ini. Untuk menampilkan metric secara realtime

![create-outbound-traffic](capture/create-traffic-inbound.png)

Pada bagian *metric options* ubah format data default menjadi bytes.

![edit-metric-optios-outbound-traffic](capture/create-traffic-inbound-options.png)

Untuk menampilkan total bytes yang telah dikeluarkan tambahkan metric baru lagi dalam data tersebut.

![total-outbound-traffic](capture/create-traffic-inbound-total-transfered.png)

Setelah selesai membuatnya, simpan visualisasi tersebut.

### g. Membuat Visualisasi CPU Usage

Pertama-tama pergi ke halaman **Visualize** lalu bentuk yang dipilih adalah **TSVB** karena untuk melihat jumlah penggunaan resource cpu dalam tamapilan gauge dengan persentase.

![select-tsvc-visual](capture/select-tsvb-visualization.png)

Atur semua pengaturan data seperti pada gambar dibawah ini. Untuk menampilkan persentasi metric penggunaan cpu secara realtime.

![create-outbound-traffic](capture/create-cpu-usage.png)

Pada bagian *metric options* ubah format data default menjadi persen untuk menampilkan persentase dari metric.

![edit-cpu-usage-option](capture/create-cpu-usage-options.png)

Setelah selesai membuatnya, simpan visualisasi tersebut.

### h. Membuat Visualisasi Memory Usage

Pertama-tama pergi ke halaman **Visualize** lalu bentuk yang dipilih adalah **TSVB** karena untuk melihat gauge dari penggunaan memory.

![select-tsvc-visual](capture/select-tsvb-visualization.png)

Atur semua pengaturan data seperti pada gambar dibawah ini. Untuk menampilkan metric penggunaan memory secara realtime.

![create-memory-usage-gauge](capture/create-memory-usage-gauge.png)

Pada bagian **Panel Options** ubah style yang diinginkan untuk menampilkan visualisasi **Memory Usage**.

![](capture/memory-usage-gauge-style.png)

Tujuan dari style adalah mengatur warna dari gauge ketika sudah mencapai titik tertentu.

Pada bagian *metric options* ubah format data default menjadi persen untuk menampilkan persentase dari metric.

Setelah selesai membuatnya, simpan visualisasi tersebut.

### i. Membuat Visualisasi System Load

Pertama-tama pergi ke halaman **Visualize** lalu bentuk yang dipilih adalah **TSVB** karena untuk melihat gauge dari penggunaan memory.

![select-tsvc-visual](capture/select-tsvb-visualization.png)

Atur semua pengaturan data seperti pada gambar dibawah ini. Untuk menampilkan metric system load selama 5 menit. Pilih metric yang akan digunakan, yaitu **system.load.5** untuk menampilkan jumlah load dalam 5 menit.

![create-system-load](capture/create-system-load-5min.png)

Pada bagian *metric options* ubah format data default menjadi persen untuk menampilkan persentase dari metric.

Setelah selesai membuatnya, simpan visualisasi tersebut.

### j. Membuat Visualisasi Disk Used

Pertama-tama pergi ke halaman **Visualize** lalu bentuk yang dipilih adalah **TSVB** karena untuk melihat gauge dari penggunaan disk.

![select-tsvc-visual](capture/select-tsvb-visualization.png)

Atur semua pengaturan data seperti pada gambar dibawah ini. Untuk menampilkan metric system load selama 5 menit. Untuk menampilkan penggunaan ini maka perlu ada tambahan expression pada metric yaitu dengan membagi metric **system.fsstat.total_size.used** dengan **system.fsstat.total_size.total** untuk mendapatkan hasil persentase disk yang telah digunakan.

![create-disk-used](capture/create-disk-used.png)

Pilih tab **Gauge** untuk memilih bentuk tampilan *Gauge*. Pada bagian *metric options* ubah format data default menjadi persen untuk menampilkan persentase dari metric.

Lalu pada bagian **Panel Options** ubah style yang diinginkan untuk menampilkan visualisasi **Disk Used**.

![option-disk-used](capture/create-disk-used-option.png)

Setelah selesai membuatnya, simpan visualisasi tersebut.

### k. Membuat Visualisasi Disk Usage

Pertama-tama pergi ke halaman **Visualize** lalu bentuk yang dipilih adalah **TSVB** karena untuk melihat chart dari penggunaan Disk. Pada pilihan tab **TSVB** pilih bentuk **Top N** untuk menampilkan bentuk chart bar  dari persentase disk yang digunakan.

![create-disk-usage](capture/create-disk-usage.png)

Untuk melakukan filter pada disk yang akan ditampilkan pindah ke bagian tab **Panel Options** lalu pada bagian **Panel Filters** isikan mount point yang tidak akan ditampilkan.

![disk-usage-panel-option](capture/disk-usage-panel-option.png)

Setelah itu simpan visualisasi yang telah dibuat.

### l. Membuat Visualisasi CPU Usage - Time Series

Pertama-tama pergi ke halaman **Visualize** lalu bentuk yang dipilih adalah **TSVB** karena untuk melihat chart dari penggunaan CPU dalam bentuk Time Series. Pada pilihan tab **TSVB** pilih bentuk **Time Series** untuk menampilkan bentuk grafik chart dari persentase cpu yang digunakan. Ubah format data default menjadi **Percentage**.

![create-cpu-usage-time-series](capture/create-cpu-usage-time-series.png)

Isikan metric untuk melihat penggunaan CPU berdasarkan process yang sedang berjalan, seperti **system.cpu.user.pct**,  **system.cpu.system.pct**, **system.cpu.nice.pct**, **system.cpu.irq.pct**, **syst.cpu.softirq.pct**, **system.cpu.iowait.pct**.

Setelah selesai simpan konfigurasi visualisasi yang telah dibuat.


### m. Membuat Visualisasi Memory Usage - Time Series

Pertama-tama pergi ke halaman **Visualize** lalu bentuk yang dipilih adalah **TSVB** karena untuk melihat chart dari penggunaan memory dalam bentuk Time Series. Pada pilihan tab **TSVB** pilih bentuk **Time Series** untuk menampilkan bentuk grafik chart dari banyaknya byte yang digunakan oleh memory. Ubah format pada field tersebut dari format field sebelumnya **Number** mejadi **Bytes**.

![create-memory-usage-time-series](capture/create-memory-usage-time-series.PNG)

Jika semua metric sudah disesuaikan simpan konfigurasi visualisasi tersebut.</br></br>


[< Langkah Sebelumya](https://github.com/bagaswibowo25/elk-lab/blob/master/Install.md) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; [Langkah Selanjutnya >](https://github.com/bagaswibowo25/elk-lab/blob/master/RawData.md)