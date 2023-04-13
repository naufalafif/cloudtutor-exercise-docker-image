#### Docker Push

Docker push adalah perintah dalam Docker yang digunakan untuk mengirimkan (meng-upload) image Docker dari host lokal ke Docker registry.

Docker registry adalah layanan tempat penyimpanan image Docker yang dapat diakses dari mana saja. Docker Hub adalah salah satu contoh Docker registry yang populer. Dengan menggunakan perintah "docker push", kita dapat mempublikasikan image Docker yang telah kita buat ke registry yang sudah terdaftar di Docker.

Sebelumnya kita sudah menggunakan `docker pull` dimana pull digunakan untuk mengunduh sedangkan `docker push` bekerja sebaliknya yaitu mengirim / meng-upload image.

### Meng-upload Image

Untuk meng-upload image docker, diperlukan akses pada registry yang dituju. pada kasus ini kita akan menggunakan registry default docker yaitu dockerhub

Akses dockerhub bisa didapatkan dengan mendaftarkan akun pada website https://hub.docker.com/signup

Pada saat pertama kali melakukan push image, docker akan meminta kita untuk melakukan login menggunakan akun dockerhub. Gunakan akun yang sudah dibuat untuk login pada docker dengan perintah `docker login`

```{.bash}
$ docker login
Login in with your Docker ID to push and pull images from Docker Hub. If you do not have a Docker ID, head over to https://hub.docker.com to create one.
Username: yourusername
Password:
WARNING! Your password will be stored unencrypted in /Users/yourusername/.docker/config.json
Configure a credential helper to remove this warning. See
https://docs.docker.com/engine/reference/commandline/login/credential-store

Login Succeeded
```

Untuk meng-upload image, nama image perlu disesuaikan dengan akun dockerhub, jika sebelumnya kita sudah membuat image dengan nama `fastapi-app`, maka sekarang image tersebut perlu ditambahkan username menjadi `username_anda/fastapi-app`

Gunakan perintah dibawah untuk membuat image dengan nama yang baru dari image yang sudah dibuat

```{.bash .copy}
docker tag fastapi-app username_anda/fastapi-app
```

Cek image dengan nama yang baru menggunakan `docker images`

```{.bash}
REPOSITORY                                             TAG                IMAGE ID       CREATED         SIZE
fastapi-app                                            latest             a6856deec95a   2 minutes ago     990MB
cloudtutor-io/fastapi-app                                            latest             a6856deec80c   1 minutes ago     990MB
```

Selanjutnya gunakan docker push untuk mengupload image

```{.bash .copy}
docker push username_anda/fastapi-app
```

Ketika selesai maka image yang sudah kita buat sudah berada di dockerhub dan dapat diakses di link

```{.bash .copy}
https://hub.docker.com/r/username_anda/fastapi-app
```

> Catatan: Proses di atas berlaku untuk registry Docker Hub. Terdapat registry lain, baik itu public maupun private, yang cara autentikasinya bisa berbeda. Contoh registry lain adalah Google Cloud Registry.
