#### Clone Aplikasi

Pertama, kita akan men-clone aplikasi yang ada di github pada direktori `/home/admin`

```{.bash .copy}
cd /home/admin && git clone https://github.com/cloudtutor-io/fastapi-app.git
```

Perintah di atas akan meng-clone repository fastapi-app ke local.

> Update `editor` disebelah kanan dengan meng-klik icon refresh untuk memunculkan direktori aplikasi

#### Menyiapkan Dockerfile

Pastikan posisi direktori sama dengan aplikasi yang sudah di clone.

```{.bash .copy}
cd fastapi-app
```

Kedua, buat file Dockerfile didalam direktori aplikasi.
gunakan perintah dibawah atau gunakan editor yang berada diatas terminal

```{.bash .copy}
touch Dockerfile
```

Selanjutnya edit file `Dockerfile` dan mulai dengan menambahkan base image `python`.

```{.bash .copy}
FROM python:3.10-alpine
```

Atur direktori tempat aplikasi akan ditempatkan dan copy file ke dalam docker image.

```{.bash .copy}
# set a directory for the app
WORKDIR /app

# copy all the files to the container
COPY . .
```

Selanjutnya adalah melakukan instalasi dependensi, tambahkan perintah berikut

```{.bash .copy}
# install dependencies
RUN pip install --no-cache-dir -r requirements.txt
```

Selanjutnya expose port yang digunakan oleh aplikasi agar bisa diakses dari luar container & berikan script yang digunakan untuk menjalankan aplikasi

```{.bash .copy}
# define the port number the container should expose
EXPOSE 8080

# run the command
CMD ["python", "./main.py"]
```

Dockerfile berhasil dibuat. berikut hasil akhirnya

```{.bash .copy}
FROM python:3.10-alpine

# set a directory for the app
WORKDIR /app

# copy all the files to the container
COPY . .

# install dependencies
RUN pip install --no-cache-dir -r requirements.txt

# define the port number the container should expose
EXPOSE 8080

# run the command
CMD ["python", "./main.py"]
```

### Mem-build Image

Dockerfile sudah siap, sekarang kita bisa mem-build imagenya. gunakan perintah `docker build` diikuti dengan tag untuk memberikan nama pada image.

```{.bash .copy}
docker build -t fastapi-app .
```

keterangan:

1. -t digunakan untuk memberikan tag atau nama pada image
2. . pada akhir perintah digunakan untuk menentukan path atau root direktori. jika diubah maka perintah copy didalam Dockerfile akan menyesuikan root atau path

docker akan mem-build image dan mengeksekusi perintah - perintah yang ada dalam Dockerfile seperti pada output dibawah

```{.bash}
$ docker build -t fastapi-app .
[+] Building 13.3s (10/10) FINISHED
 => [internal] load build definition from Dockerfile              0.0s
 => => transferring dockerfile: 38B                               0.0s
 => [internal] load .dockerignore                                 0.0s
 => => transferring context: 2B                                   0.0s
 => [internal] load metadata for docker.io/library/python:latest  0.0s
 => [1/5] FROM docker.io/library/python                           0.0s
 => [internal] load build context                                 0.0s
 => => transferring context: 3.36kB                               0.0s
 => CACHED [2/5] WORKDIR /app                                     0.0s
 => [3/5] COPY requirements.txt .                                 0.0s
 => [4/5] RUN pip install -r requirements.txt                    12.6s
 => [5/5] COPY . .                                                0.1s
 => exporting to image                                            0.4s
 => => exporting layers                                           0.4s
 => => writing image sha256:a6856deec95a2b62eb45156bc3c1b45ce7ab  0.0s
 => => naming to docker.io/library/fastapi-app                    0.0s
```

berhasil, kita sudah men-dockerize aplikasi. Image dapat dicek menggunakan perintah `docker images`.

```{.bash}
REPOSITORY                                             TAG                IMAGE ID       CREATED         SIZE
fastapi-app                                            latest             a6856deec95a   2 minutes ago     990MB
```

#### Menjalankan Container

selanjutnya jalankan aplikasi menggunakan `docker run` dan expose pada port 80

```{.bash .copy}
docker run -p 80:8080 fastapi-app
```

aplikasi akan berjalan dan dapat ditemukan pada url berikut

```{.bash .copy}
https://#ID#.host.cloudtutor.io
```

gunakan browser disebelah kanan atau buka tab baru pada browser untuk mengecek aplikasi
