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
- [ ] Entities
- [ ] Value Objects
- [ ] Domain Services

#### Lifecycle Patterns
- [ ] Aggregate
- [ ] Factory (new instance of something)
- [ ] Repository (aktivitas DB)

#### Emerging Patterns
- [ ] Domain Event (History dari kejadian yang terjadi -- ditandai dengan past tense -- user logged in, message was sent, etc.)
- [ ] Event Sourcing (pengolahan/manipulasi domain event)

#### Visualizations
- [ ] Class Diagram (nanti disuruh buat class diagram)

ㅤ

# Pembahasan Materi

Dibawah akan dibahas secara mendetail semua yang dimention sebelumnya.

ㅤ


## Tactical Patterns

### 1.	Entities

Merupakan class yang memiliki identitas dan valuenya dapat berganti (mutable).

Entity biasanya ditandakan dengan memiliki ID pada attribute-nya.

**Contoh:**
[class diagram here]

ㅤ

### 2.	Value Objects

Merupakan class yang ada untuk ***menandakan sebuah value*** (seperti String, Integer, Double, etc.) yang tidak memiliki identitas.

Value Objects tidak dapat diganti value-nya (immutable). Jadi, jikalau sudah memiliki value, dan kita ingin agar value-nya berubah, kita harus `create new` si Value Objects.

**Contoh:**
[class diagram here]

ㅤ

### 3.	Domain Services

Merupakan class yang hanya menyimpan method dan tidak menyimpan data. Class ini biasanya ada untuk ***memenuhi logic dari sebuah business***.

**Contoh:**
[class diagram here]

ㅤ

## Lifecycle Patterns

### 1.	Aggregates

Merupakan ***gabungan dari satu atau banyak class***.

Diantara class-class yang digabungin itu, ambil salah satu menjadi ***root***.

Tujuan dari ***root*** adalah sebagai gatekeeper, yang menentukan semua asosiasi dari dan keluar aggregate.

Kalau digambarkan pada `class diagram`, aggregates dapat terlihat sebagai garis yang ngelilingi sekumpulan class.

**Contoh:**
[class diagram here]

ㅤ

### 2.	Factories

Merupakan class yang tujuannya adalah ***membuatkan object***.

Lu bisa ngertiin factories sebagai *glorified* class yang ngurusin `new Something()`.

Ada dua tipe factory:
a.)	**Factory Method Pattern**, dan
b.)	**Abstract Factory Pattern**.

ㅤ

#### A.) Factory Method Pattern
---
Merupakan pattern yang dipakai untuk menyediakan ***constructor khusus*** untuk ***suatu varian*** dari ***suatu class***.

Disini, dianggap semua class yang di-factory-kan ***PASTI memiliki varian lebih dari satu***.

Jika class yang mau kita factory-kan hanya memiliki satu varian, maka lebih baik provide ***constructor method*** saja.

ㅤ

**Contoh:**

Terdapat tiga pilihan jalur saat mahasiswa registrasi masuk perkuliahan:

(1) Jalur Regular
(2) Jalur International
(3) Jalur Double Degree

Karena ketiga varian ini semuanya bergantung dengan class `Mahasiswa`, dan class `Mahasiswa` BUKAN MILIK DARI AGGREGAT TERTENTU, bisa pakai Factory Method Pattern.
ㅤ
[class dari Mahasiswa]
[implementasi factory method pattern]

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
`Paket Hemat A` dan `Paket Hemat B` disini adalah factory, yang membuatkan suatu "paket" dari class `McDonkey`.

![abstract factory](https://i.ibb.co/gmsgpQQ/image.png)

ㅤ

### 3.	Repositories

Merupakan class yang mengurus presistence (penyimpanan data permanen di SSD, HDD, etc.). Artinya, data dari suatu object class akan disimpan kedalam database sebagai row-row data.

Repositories tidak mengurus validasi. Misalnya dipaksa-pun, repo hanya akan mengurus "apakah data yang di-passing argumen layak untuk dimasukkan ke database atau tidak".

Repo tidak menampung data. Kalau adapun, itu biasanya related dengan functional repo:
- connection string
- object connection
- database settings
- etc.

**Contoh:**
[class diagram here]

ㅤ

## Emerging Patterns

### 1.	Domain Event

Event adalah perubahan data di aplikasi.

Setiap perubahan perlu dikomunikasikan dari si-pengubah, ke semua pihak yang perlu tahu.

Cara komunikasinya:
1. Manipulator class (class yang membuat perubahan pada data) akan membuat `new object Event`. Object Event ini merupakan instance dari suatu class biasa.
3. Class Event biasanya berisi attribut: "apa yang berubah", "siapa yang membuat perubahan", dan "value baru nya apa" -- sambil tidak memiliki method apa-apa.
4. Setelah object event dibuat, dia dikirim ke mereka yang perlu tahu tentang perubahan data. Ada beberapa cara utk ngirim object event ini:
	- panggil method dari class yang perlu tahu secara langsung
	- pakai messaging
	- lewat service
	- lewat databases (bikin tabel yang nampung event)
	- dll.

**Contoh:**
[class diagram here]

ㅤ

### 2.	Event Sourcing

Merupakan konsep (pattern) untuk mengolah event-event tadi.

Pada class diagram, Event Sourcing dapat dilihat saat suatu class mengolah data yang ada pada List of Events.

**Contoh:**
[class diagram here]

ㅤ

## Case Study

What the fuck.
