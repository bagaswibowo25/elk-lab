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
Selanjutnya lakukan update pada apt agar dapat menginstall elasticsearch.
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

Setelah elasticsearch running, verifikasi bahwa konfigurasi yang telah dilakukan telah sesuai dengan perintah berikut.

```sh
$ curl -X GET 'http://10.10.6.10:9200/?pretty'
```
![Verifikasi](/capture/verifikasi-instalasi-elasticsearch.png)