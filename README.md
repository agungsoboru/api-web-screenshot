# api-web-screenshot
Docker image apline linux dan google chrome driver dengan fast api python. bagi yang  memerlukan chrome driver untuk web scraping screenshot web. image ini berfungsi untuk screenshot web mengunakan http request hasil gambar.png di simpan di directory container

![image](https://github.com/agungsoboru/api-web-screenshot/blob/main/gambar/Screenshot%20(848).png)

![image](https://github.com/agungsoboru/api-web-screenshot/blob/main/gambar/Capturess.JPG)

# Docker image yang sudah jadi 

`docker run -it --cap-add=SYS_ADMIN -p 12002:8000 -u agungsurya agungsurya/api-web-screenshot:v2`

untuk menjalankan api pertama perlu masuk kedalam kontainer api-srver pertama nya. command untuk masuk kontainer

`docker exec -u agungsurya -it <mana kontainer ketika sudah di run / pull> /bin/ash`

ketika sudah masuk kedalam kontainer maka akan berada pada directory ini `/usr/src/app $`

lalu ketik command cd agar kembali ke home directory yaitu /home/agungsurya

lalu di sana ada direcotry screnshoot masuk ke dalam dir tersebut

ada file python bernama `api-screenshoot.py` jalankan file tersebut dengan tmux atau screen dengan command seperti di bawah ini

di bagian bawah kode `api-screenshoot.py` harus di isi telegram token dan chat id untuk mengirimkan hasil foto agar bisa di lihat secara langsung 

`python3 -m uvicorn api-screenshoot:app --host=0.0.0.0`

ketika sudah berjalan bisa di cek port external di host yaitu 12000 (ketika membuat kontainer)

lalu coba akses

http://alamat-ip:12002/screenshot/google.com/ atau http://alamat-ip:12002/api

# Docker compose

```
version: '3'
services:
  api-web-screenshot:
    image: agungsurya/api-web-screenshot:v2
    volumes:
      - /home/agungsurya/screenshoot:/home/agungsurya/screenshoot
    ports:
      - "12002:8000"
    command: python3 -m uvicorn api-screenshoot:app --host=0.0.0.0
```
Setelah melakukan perubahan pada docker-compose.yml, jalankan perintah docker-compose up pada direktori yang sama dengan docker-compose.yml file untuk menjalankan container Docker.

# image alpine dari

https://github.com/Zenika/alpine-chrome

