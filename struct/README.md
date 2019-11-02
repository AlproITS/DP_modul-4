# Struct

## Daftar Isi

- [Halaman Awal](https://github.com/AlproITS/DP_modul-4)
- [Pengenalan Struct](#pengenalan-struct)
- [Deklarasi Struct](#deklarasi-struct)
- [Variabel Struct](#variabel-struct)
- [Akses Member Struct](#akses-member-struct)
- [Array of Struct](#array-of-struct)

## Pengenalan Struct

Dalam bahasa C, struct adalah salah satu tipe data turunan atau bisa disebut juga _User Defined Data Type_ yang dapat mengelompokkan beberapa variabel dibawah satu nama. Tidak seperti array yang hanya dapat menyimpan elemen dengan tipe data sama, struct dapat mengelompokkan elemen dengan tipe data yang berbeda-beda.

Contoh:

![](../img/mhs_entity.png)

Perhatikan gambar di atas. **Mahasiswa** merupakan suatu entitas yang didalamnya terdapat atribut-atribut berupa :
- Nama
- NRP
- Umur
- IPK
- Semester
- Status

Atribut-atribut inilah yang nantinya berperan sebagai **member** dari struct **Mahasiswa**.

## Deklarasi Struct

Struct harus dideklarasikan terlebih dahulu sebelum bisa digunakan. Pendeklarasian struct menggunakan sintaks sebagai berikut.
```
struct <nama_struct> {
    <tipe_data_member> <nama_member>;
    <tipe_data_member> <nama_member>;
    <tipe_data_member> <nama_member>;
    .
    .
    .
};
```

Berikut adalah contoh deklarasi struct berdasarkan kasus Mahasiswa di atas.

```c
struct Mahasiswa {
    char nama[100];
    char nrp[20];
    int umur;
    double ipk;
    int semester;
    int status;
};
```

## Variabel Struct

Setelah dideklarasikan, sebuah struct akan menjadi tipe data baru. Maka dalam kasus ini, struct **Mahasiswa** disini menjadi **tipe data baru** dengan member-member berupa **`nama`**, **`nrp`**, **`umur`**, **`ipk`**, **`semester`**, dan **`status`**. Untuk membuat variabel dengan tipe data struct, dilakukan dengan sintaks berikut.

```
struct <nama_struct> <nama_variabel>;
```

Contoh :

```c
struct Mahasiswa mhs1;
struct Mahasiswa mhs2;
```

Contoh di atas menunjukkan terdapat dua variabel **`mhs1`** dan **`mhs2`** bertipe struct Mahasiswa.

## Akses Member Struct

Lalu bagaimana cara untuk mengakses member dari variabel struct yang telah dibuat? Untuk mengakses member-member dari struct, digunakan **operator dot (`.`)** setelah nama variabelnya.

```
<nama_variabel>.<member_struct>
```
Contoh :
```c
mhs1.umur = 19;
mhs1.semester = 3;

mhs2.umur = 20;
mhs2.semester = 5;
```

**Contoh program untuk mendemonstrasikan Struct** :

```c
#include <stdio.h>
#include <string.h>

struct Mahasiswa {
    char nama[100];
    char nrp[20];
    int umur;
    double ipk;
    int semester;
    int status;
};

int main(void)
{
    struct Mahasiswa mhs1;

    strcpy(mhs1.nama, "Ahmad");
    strcpy(mhs1.nrp, "05111940000012");
    mhs1.umur = 18;
    mhs1.ipk = 3.94;
    mhs1.semester = 3;
    mhs1.status = 1;

    printf("Nama\t: %s\n", mhs1.nama);
    printf("NRP\t: %s\n", mhs1.nrp);
    printf("Umur\t: %d\n", mhs1.umur);
    printf("IPK\t: %.2lf\n", mhs1.ipk);
    printf("Sem\t: %d\n", mhs1.semester);
    printf("Status\t: %s\n", (mhs1.status == 1 ? "Aktif" : "Tidak Aktif"));
    
    return 0;
}
```

## Array of Struct

Kita juga dapat membuat array dengan tipe data struct. Caranya sama persis dengan deklarasi array pada umumnya.

```c
#include <stdio.h>
struct Point {
    int x, y;
};

int main()
{
    struct Point arr[3];
    arr[0].x = 2, arr[0].y = 3;
    arr[1].x = 5, arr[1].y = 3;
    arr[2].x = 2, arr[2].y = 8;

    printf("%d %d\n", arr[0].x, arr[0].y);
    printf("%d %d\n", arr[1].x, arr[1].y);
    printf("%d %d\n", arr[2].x, arr[2].y);
    
    return 0;
}
```

[Lanjut ke Pointer >](https://github.com/AlproITS/DP_modul-4/tree/master/pointer)

[Halaman Awal >](https://github.com/AlproITS/DP_modul-4)