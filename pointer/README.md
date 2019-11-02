# Pointer

## Daftar Isi

- [Halaman Awal](https://github.com/AlproITS/DP_modul-4)
- [Alamat Memori](#alamat-memori)
- [Pengenalan Pointer](#pengenalan-pointer)
- [Pointer dan Array](#pointer-dan-array)
- [Pointer dan Fungsi](#pointer-dan-fungsi)

## Alamat Memori

### Operator Address-Of (`&`)

Setiap **variabel, fungsi, struct, ataupun objek lain** yang dibuat dalam program mempunyai alokasi masing-masing pada memori. Alokasi tersebut disimpan dalam alamat memori tertentu. Misalnya :

Terdapat variabel bernama `var`. Untuk mengetahui alamat memori dari variabel, digunakan **operator address-of** (`&`) didepan nama variabelnya.

```c
int var = 5;
printf("%d\n", var);
printf("%p\n", &var);
```

Output

```
5
0x7fffdeb3ed84
```
> Output bisa berbeda-beda di tiap komputer

`0x7fffdeb3ed84` merupakan alamat memori dari variabel `var`.

## Pengenalan Pointer

Pointer merupakan hal yang **menyenangkan dan mudah** untuk dipelajari. **Pointer** adalah variabel spesial yang menampung **alamat memori**, bukannya nilai seperti variabel biasa.

### Deklarasi Variabel Pointer

Deklarasi variabel pointer menggunakan operator **`*`** diantara tipe data dan nama variabelnya.

```c
int *ptr;
```
atau
```c
int* ptr;
```
> Kedua cara deklarasi di atas merupakan sintaks yang valid.

### Inisialisasi Variabel Pointer

Variabel **`ptr`** di atas adalah variabel pointer yang bertipe `int`. Variabel pointer menampung alamat memori. Inisialisasi variabel pointer harus berupa alamat memori, bisa dari variabel lain atau alokasi secara dinamis.

```c
int var = 55;
int *ptr = &var; // Inisialisasi menggunakan alamat dari var
```

Inisialisasi yang tidak sesuai akan menghasilkan error atau _undefined behaviour_.

```c
// ERROR
int *ptr  = 5;
// UNDEFINED BEHAVIOUR
int *ptr2 = 0x7fffdeb3ed84;
```

### Assignmet Variabel Pointer

Cara melakukan _assignment_ pada variabel pointer **tidak sama** dengan inisialisasinya.

```c
int var, *ptr;
var = 55;
ptr = &var; // Assignment pada variabel pointer menggunakan alamat dari var
```
Assignment tidak perlu menggunakan simbol **`*`** didepan nama variabelnya. Berbeda pada saat deklarasi yang mana kita perlu memberitahu _compiler_ bahwa variabel tersebut adalah variabel pointer.

### Operator Dereference (`*`)

Operator dereference menggunakan simbol yang sama dengan simbol operator perkalian, yakni **`*`** (simbol arterisk). Namun, fungsinya sangat berbeda. Operator dereference digunakan untuk mengakses **nilai** yang ditunjuk (_pointed_) dari sebuah variabel pointer.

Untuk mengakses nilai dari sebuah variabel pointer, digunakan operator dereference didepan nama variabel.

```c
int var  = 55;
int *ptr = &var;

printf("%d\n", *ptr);
*ptr = 20;
printf("%d\n", *ptr);
printf("%d\n", var);
```

Output

```
55
20
20
```

```c
#include <stdio.h>

int main(void)
{
    int x, y, z;
    int *ptr1, *ptr2;
    x = 5;
    y = 6;

    ptr1 = &x;
    ptr2 = &y;

    z = *ptr1 + *ptr2;
    printf("%d\n", z);
    
    return 0;
}
```

## Double Pointer

Variabel pointer juga dapat menunjuk variabel pointer lainnya. Hal ini disebut dengan double pointer (pointer to pointer). Untuk mendeklarasikan variabel double pointer, digunakan dua simbol `*`. Kegunaan paling umum dari variabel double pointer adalah untuk membuat array dua dimensi secara dinamis.

```c
int **dbPtr;
```

Variabel `dbPtr` di atas menyimpan alamat memori dari variabel pointer lainnya.

```c
#include <stdio.h>

int main(void)
{
    int var = 23;
    int *ptr = &var;
    int **dbPtr = &ptr;

    printf("%d\n", **dbPtr);
    
    return 0;
}
```

## Pointer dan Array

![](../img/array-2.png)

Kita sudah mengetahui bahwa array adalah kumpulan data yang disusun secara sekuensial. Karena disusun secara sekuensial, alamat-alamat memori tiap elemen array juga tersusun secara berurutan.

Bagaimana jika kita ingin mengetahui alamat memori dari array?
```c
#include <stdio.h>

int main()
{
    int arr[5] = {1, 2, 3, 4, 5};
    int i;
    for (i = 0; i < 5; ++i) {
        printf("&arr[%d] => %p\n", i, &arr[i]);
    }
    printf("Address of arr => %p\n", arr);
    return 0;
}
```
Output

```
&arr[0] => 0x7fffe85f0520
&arr[1] => 0x7fffe85f0524
&arr[2] => 0x7fffe85f0528
&arr[3] => 0x7fffe85f052c
&arr[4] => 0x7fffe85f0530
Address of arr => 0x7fffe85f0520
```

Dapat diperhatikan bahwa alamat dari `&arr[0]` sama dengan alamat dari `arr`. Dari hal ini dapat diketahui bahwa **nama array** menunjuk ke **elemen pertama** dari array tersebut. Karena **`&arr[0] = arr`**, maka dapat disimpulkan bahwa **`arr[0] = *arr`**, atau nilai dari elemen pertama dapat diakses dengan `*arr` atau `*(arr + 0)`.

```
arr[0] = *(arr + 0)
arr[1] = *(arr + 1)
arr[2] = *(arr + 2)
.
.
dst
```

**Kesimpulan :** Nama array merujuk pada alamat memori dari elemen pertama pada array.

Berbekal dari hal tersebut, maka kita dapat melakukan hal demikian.

```c
#include <stdio.h>

int main()
{
    int arr[5] = {1, 2, 3, 4, 5}, i;
    int *ptr = arr;

    for (i = 0; i < 5; ++i) {
        printf("%d ", *(ptr+i));
    }
    return 0;
}
```

Output

```
1 2 3 4 5
```

## Pointer dan Fungsi

Sebelumnya kita sudah mengetahui bahwa fungsi dapat menerima parameter sebagai input dari fungsi. Penggunaan-penggunaan parameter fungsi selama ini sebenarnya menggunakan konsep **Pass by Value**. Selain menggunakan cara _Pass by Value_, terdapat cara lain untuk passing argumen pada fungsi.

![](../img/function_passing.gif)

### _Pass by Value_

Pass by Value berarti saat kita memasukkan (passing) argumen pada fungsi, nilai dari argumen tersebut akan disalin ke variabel yang berada pada parameter fungsi. Karena hanya nilainya saja yang diterima oleh fungsi, perubahan yang terjadi pada variabel parameter fungsi tidak akan berpengaruh terhadap variabel asalnya.

Contoh

```c
#include <stdio.h>

void change(int a, int b)
{
    a = a + 5;
    b = b + 5;
}

int main()
{
    int x = 10, y = 6;
    change(x, y);
    printf("%d %d\n", x, y);

    return 0;
}
```

Nilai pada variabel `x` dan `y` tidak berubah karena metode passing yang digunakan adalah **Pass by Value**.

### _Pass by Address/Reference_

Berbeda dengan sebelumnya, sesuai namanya, metode **Pass by Address** berarti argumen yang dimasukkan (passing) ke parameter fungsi adalah alamat memori variabel. Segala perubahan yang terjadi pada variabel tersebut, juga mempengaruhi langsung ke variabel asalnya. Hal ini terjadi karena argumennya adalah langsung berupa alamat memorinya.

```c
#include <stdio.h>

void change(int *a, int *b)
{
    *a = *a + 5;
    *b = *b + 5;
}

int main()
{
    int x = 10, y = 6;
    change(&x, &y);
    printf("%d %d\n", x, y);

    return 0;
}
```

Karena parameternya menerima alamat memori, maka variabel parameternya harus berupa pointer.

Passing array sebagai parameter fungsi juga dapat dilakukan dengan pointer. Segala perubahan pada array juga akan berpengaruh pada array asalnya.

```c
#include <stdio.h>

void printArr(int *arr)
{
    // ...
    // ...
}

int main()
{
    int num[5] = {1, 2, 3, 4, 5}, i;
    printArr(num);
    // ...
    // ...
    return 0;
}
```

[Lanjut ke Struct >](https://github.com/AlproITS/DP_modul-4/tree/master/struct)

[Halaman Awal >](https://github.com/AlproITS/DP_modul-4)
