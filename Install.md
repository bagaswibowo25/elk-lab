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
![Verifikasi](/images/verifikasi-instalasi-elasticsearch.png)
Format: ![Alt Text](url)