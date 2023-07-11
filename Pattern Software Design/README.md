ㅤ
# Pattern Software Design

\
__Made for:__
> _Pattern Software Design_
>
> [ LEC ] -  Final Exam
>
> 2023 Even Semester

__Composed by:__
> 2501977941 - Kevin Gunawan
>
> ChatGPT (Best Boi)

ㅤ

## Outline

Materi UAS akan diambil dari session 08 sampai 13:

#### Tactical Patterns
- [x] Entities
- [x] Value Objects
- [x] Domain Services

#### Lifecycle Patterns
- [x] Aggregate
- [x] Factory (new instance of something)
- [x] Repository (aktivitas DB)

#### Emerging Patterns
- [x] Domain Event (History dari kejadian yang terjadi -- ditandai dengan past tense -- user logged in, message was sent, etc.)
- [x] Event Sourcing (pengolahan/manipulasi domain event)

#### Visualizations
- [ ] Class Diagram (nanti disuruh buat class diagram)

ㅤ

# Pembahasan Materi

Dibawah akan dibahas secara mendetail semua yang dimention sebelumnya.

## Tactical Patterns

### 1.	Entities

Merupakan class yang attributnya dapat berganti (mutable).
Entity biasanya ditandakan dengan memiliki ID pada attribute-nya.

ㅤ

**Class diagram:**

![Entity example](https://i.ibb.co/0tWv8Ws/image.png)

Meskipun **namanya diganti**, *lokasinya pindah*, dan **karyawan yang bekerja disitu telah diganti semua dengan orang baru**, hotel tersebut tetaplah hotel yang sama -> ***KARENA ID-nya SAMA***.

ㅤ

### 2.	Value Objects

Merupakan class yang ada untuk ***menandakan sebuah value*** (seperti String, Integer, Double, etc.) yang tidak memiliki identitas.

Value-nya tidak dapat diubah, sebab itu ***dianggap sebagai identitasnya.***

---


###### Statement:
Anggep terdapat dua buah object warna. Yang satu dipanggil ungu, dan yang satu dipanggil hijau.

###### Question:
Ketika gw ubah attribut `Hex` dari si ungu menjadi **#47D3FF**, apakah ia layak masih dipanggil ungu?

![value objects](https://i.ibb.co/wd3m5vx/image.png)

###### Answer
Jawabannya adalah tidak. Karena attribut **HEX** yang adalah **#9747FF** menentukan siapa object si ungu itu.

---

**Class diagram:**

![value object example](https://i.ibb.co/ch1vLBP/image.png)

ㅤ

### 3.	Domain Services

Merupakan class yang ***hanya menyimpan method*** dan bukan merupakan bagian dari suatu kesatuan.

Class ini biasanya ada untuk ***memenuhi logic dari sebuah business***.

ㅤ

**Class diagram:**

![Domain Service Example](https://i.ibb.co/YTKKtqm/image.png)

ㅤ

## Lifecycle Patterns

### 1.	Aggregates

Merupakan ***gabungan dari satu atau banyak class***.

Diantara class-class yang digabungin itu, ambil salah satu menjadi ***root***.

Tujuan dari ***root*** adalah sebagai gatekeeper, yang menentukan semua asosiasi dari dan keluar aggregate.

Kalau digambarkan pada `class diagram`, aggregates dapat terlihat sebagai garis yang ngelilingi sekumpulan class.

**Contoh:**

![Aggregate Example](https://i.ibb.co/8K7F8rC/image.png)

ㅤ

### 2.	Factories

Merupakan class yang tujuannya adalah ***membuatkan object. (***   `new Something( )`   ***)***

Tidak ada standar/peraturan yang mengatur ***KAPAN DARI SEBUAH FACTORY HARUS DIPAKAI.***

\
Ada dua tipe factory:

a.)	**Factory Method Pattern**

b.)	**Abstract Factory Pattern**

ㅤ

#### A.) Factory Method Pattern

Merupakan pattern yang dipakai untuk menyediakan ***constructor khusus*** untuk ***suatu varian*** dari ***suatu class***.

Disini, dianggap semua class yang di-factory-kan ***PASTI memiliki varian lebih dari satu***.

Jika class yang mau kita factory-kan hanya memiliki satu varian, maka lebih baik provide ***constructor method*** saja.

ㅤ

**Contoh:**

Terdapat 4 tipe dari ranjang yang ada di hotel:

(1) Single yang cukup untuk satu orang dengan satu buah ranjang

(2) Double yang cukup untuk dua orang dengan satu buah ranjang besar

(3) Twin yang cukup untuk dua orang dengan dua buah ranjang terpisah

(4) Quad yang cukup untuk empat orang dengan empat ranjang terpisah


![Contoh Factory Method Pattern](https://i.ibb.co/dbsnMX8/image.png)

ㅤ

#### B.) Abstract Factory Pattern
---
Merupakan pattern yang dipakai untuk menyiapkan suatu varian dari sebuah class; dimana pada variannya, komponen yang dimiliki suatu varian, berbeda dari komponen yang dimiliki varian yang lain.

***TL:DR*** -- Bukan varian class-nya yang menjadi fokus dari abstract factory :: melainkan komponen yang dimiliki varian tersebut yang menjadi fokus.

Sama seperti **Factory Method Pattern**,  semua class yang di-factory-kan disini akan dianggap ***PASTI memiliki varian LEBIH dari satu***.

Jika class yang mau kita factory-kan hanya memiliki satu varian, maka lebih baik provide ***constructor method*** saja.

ㅤ


**Contoh:**

Sebuah restoran menjual 2 macam makanan paketan:

(1) **Paket Hemat A** terdiri dari `Burger` dan `Coca Cola`

(2) **Paket Hemat B** terdiri dari `Pizza` dan `Pepsi`
\
\
`Paket Hemat A` dan `Paket Hemat B` disini adalah factory, yang gunanya adalah untuk menyediakan instance dari class `Baverage` dan `Food`, bagi class factory `McDonkey`.

![abstract factory](https://i.ibb.co/gmsgpQQ/image.png)

ㅤ

### 3.	Repositories

Merupakan class yang mengurus presistence (penyimpanan data permanen di SSD, HDD, etc.). Artinya, data dari suatu object class akan disimpan kedalam database sebagai row-row data.

Repositories tidak mengurus validasi. Meski dipaksa-pun, repo hanya akan mengurus "apakah data yang di-passing argumen layak untuk dimasukkan ke database atau tidak".

Repo ***tidak menampung data***. Kalau adapun, itu biasanya ***related dengan functional repo***:
- connection string
- object connection
- database settings
- etc.

**Contoh:**

![Repository Example](https://i.ibb.co/9njY0hg/image.png)

ㅤ

## Emerging Patterns

### 1.	Domain Event

Event adalah **perubahan data di aplikasi**.

Setiap perubahan perlu dikomunikasikan **dari** si-pengubah, **ke** semua pihak yang perlu tahu.

Cara komunikasinya:
1. **Manipulator class** (class yang membuat perubahan pada data) akan **membuat** `new Event()`.

   Event yang dibuat biasanya memegang attribut: **"apa yang berubah"**, **"siapa yang membuat perubahan"**, dan **"value baru nya apa"**. Ia tidak memiliki method apa-apa.

2. Setelah object Event dibuat, **kirim Event ke mereka yang perlu tahu tentang perubahan data**.

   Ada beberapa cara utk ngirim object event ini:
	- panggil method dari class yang perlu tahu secara langsung
	- pakai messaging
	- lewat service
	- lewat databases (bikin tabel yang nampung event)
	- dll.

**Contoh:**

![Domain Event Example](https://i.ibb.co/169kBKs/image.png)

nantinya setelah membuat Event, method `PublishBookingMadeEvent` akan memanggil method si class yang perlu tahu, dan mengirim Event itu sebagai parameternya.

Ini dilanjut di #Event Sourcing.

ㅤ

### 2.	Event Sourcing

Merupakan konsep (pattern) untuk mengolah event-event tadi.

Pada class diagram, Event Sourcing dapat dilihat saat suatu class mengolah data yang ada pada List of Events.

**Contoh:**

Method `PublishBookingMadeEvent` pada class domain service `RoomBookingApplication` memanggil method `AdjustAvailability()` milik class `Room`, untuk mengirim Event yang ia buat.

Method `AdjustAvailability()` akan menerima Event yang dikirim, lalu menambahkannya pada attribut `UsageHistory`. Sambil ia menambahkan, ia juga mengatur attribut `IsAvailable` miliknya.

![Event Sourcing Example](https://i.ibb.co/mS4sCFH/image.png)

ㅤ

## Case Study

Next update gw tambahin.
