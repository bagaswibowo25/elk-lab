# Eksekusi pada POD06-ELK

## 1. Instalasi Elasticsearch
Impor elasticsearch public GPG key kedalam APT.

```sh
$ curl -fsSL https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -
```
Tambahkan repositori elasticsearch kedalam /etc/apt/source.list.d/elasticsearch-7.x.list untuk dapat menginstall elasticsearch versi 7.
```sh
$ echo "deb https://artifacts.elastic.co/packages/7.x/apt stable main" | sudo tee -a /etc/apt/sources.list.d/elastic-7.x.list
```
Selanjutnya lakukan update pada apt agar dapat memasang elasticsearch.
```sh
$ sudo apt-get update
```
Setelah repositori berhasil ditambahkan dilanjutkan dengan melakukan pemasangan dari elasticsearch.
```sh
$ sudo apt-get install elasticsearch
```
Setelah elasitcsearch berhasil terpasang, selanjutnya lakukan konfigurasi pada elasticsearch dengan melakukan modifikasi pada file /etc/elasticsearch/elasticsearch.yml.

```sh
$ sudo nano /etc/elasticsearch/elasticsearch.yml
```
Selanjutnya edit beberapa konfigurasi dibawah ini:
- **network.host** - Atur listen address ke ip address node pod06-elk agar elasticsearch dapat diakses oleh node lain dalam satu jaringan LAN.
  ```sh
  network.host: 10.10.6.10
  ```
- **cluster.name** - Atur nama cluster untuk elasticsearch. Jika terdapat node lain maka harus dalam cluster yang sama. Karena saat ini hanya menggunakan single node maka tidak berpengaruh.
  ```sh
  cluster.name: elasticsearch
  ```
- **node.name** - Atur nama untuk node dari elasticseaerch untuk menjadi identitas node dalam cluster.
  ```sh
  node.name: pod06-elk
- **discovery.type** - Karena hanya menggunakan single node maka pengaturan discovery yang digunakan adalah single node.
   ```sh
   discovery.type: single-node
   ```

Setelah semua selesai dikonfigurasi. Simpan konfigurasi tersebut dan jalankan service dari elasticsearch.
```sh
$ sudo systemctl enable elasticsearch
$ sudo systemctl start elasticsearch
```
Verifikasi service elasticsearch bahwa telah berjalan
```sh
$ sudo systemctl status -l elasticsearch
```
![Verifikasi](/capture/verifikasi-status-elasticsearch.png)

Setelah elasticsearch running, verifikasi bahwa konfigurasi yang telah dilakukan telah sesuai dengan perintah berikut.

```sh
$ curl -X GET 'http://10.10.6.10:9200/?pretty'
```
![Verifikasi](/capture/verifikasi-instalasi-elasticsearch.png)

## 2. Instalasi Logstash

Setelah selesai memasang elasticsearch maka langkah selanjutnya adalah memasang logstash. Logstash digunakan untuk melakukan parsing data dari sumber dan diproses lalu dikirim ke elasticsearch.

Pertama tama jalankan perintah berikut untuk memasang logstash

```sh
$ sudo apt-get install logstash
```
Setelah memasang logstash jalankan perintah berikut untuk mengaktifkan service logstash dan menjalankannya.

```sh
$ sudo systemctl enable logstash
$ sudo systemctl start logstash
```
Verifikasi instalasi service logstash
```sh
$ sudo systemctl status logstash
```
![Verifikasi](/capture/verifikasi-status-logstash.png)

## 3. Instalasi Kibana

Setelah selesai memasang logstash selanjutnya pasang kibana untuk melakukan visualisasi data.

Pertama-tama jalankan perintah berikut untuk memasang kibana.
```sh
$ sudo apt-get install kibana
```
Setelah kibana terpasang, selanjutnya edit beberapa konfigurasi dibawah ini:
- **server.host** - Atur listen address ke ip address node pod06-elk agar kibana dapat diakses oleh node lain dalam satu jaringan LAN.
  ```sh
  server.host: 10.10.6.10
  ```
- **server.name** - Atur display name dari kibana.
  ```sh
  server.name: "pod06-elk"
  ```
- **elasticsearch.hosts** - Atur alamat dari elasticsearch yang telah terpasang.
  ```sh
  elasticsearch.hosts: ["http://10.10.6.10:9200"]
  ```

Selanjutnya aktifkan dan jalankan service kibana.
```sh
$ sudo systemctl enable kibana
$ sudo systemctl start kibana
```
Setelah kibana berjalan, lakukan verifikasi bahwa service kibana sudah aktif
```sh
$ sudo systemctl status -l kibana
```
![Verifikasi](/capture/verifikasi-status-kibana.png)

# Eksekusi pada POD06-client
 
## 1. Instalasi Metricbeat
Pada pod06-client akan dijadikan sebagai node klien yang akan dilakukan monitoring terhadap resource yang dimilikinya. Seperti CPU, Memory, Disk, Network.

Untuk memasang Metricbeat perlu menambahkan repositori dari elasticsearch.

Impor elasticsearch public GPG key kedalam APT.
```sh
$ curl -fsSL https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -
```
Tambahkan repositori elasticsearch kedalam /etc/apt/source.list.d/elasticsearch-7.x.list untuk dapat menginstall elasticsearch versi 7.
```sh
$ echo "deb https://artifacts.elastic.co/packages/7.x/apt stable main" | sudo tee -a /etc/apt/sources.list.d/elastic-7.x.list
```
Setelah repositori berhasil ditambahkan lakukan update dan dilanjutkan dengan pemasangan metricbeat.

```sh
$ sudo apt-get update && apt-get install metricbeat
```

Setelah metricbeat berhasil terpasang edit pengaturan pada metricbeat.

```sh
$ sudo nano /etc/metricbeat/metricbeat.yml
```
Selanjutnya edit konfigurasi metricbeat dibawah ini:
- **output.elasticsearch** - Atur output metricbeat ke elasticsearch dengan memanambahkan ip address pod06-elk.
  ```sh
  host: ["10.10.6.10:9200"]
  ```
Setelah selesai memasang metricbeat, aktifkan dan jalankan service metricbeat pada pod06-client.

```sh
$ sudo systemctl enable metricbeat
$ sudo systemctl start metricbeat
```
Setelah service diaktifkan dan dijalankan lakukan verifikasi bahwa service telah berjalan dengan benar.

```sh
$ sudo systemctl status -l metricbeat
```
![Verifikasi](/capture/verifikasi-status-metricbeat.png)