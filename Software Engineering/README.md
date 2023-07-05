
ㅤ
# [PIAT] Personal Intensive Acceleration Training

\
__Made for:__
> _Software Engineering_
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

### I. Multiple Choices (20%)
- [X] Software Configuration Management
- [X] Version Control and Branch Management
- [X] CI/CD
- [X] Software Architecture
- [X] Deployment
- [ ] Maintenance and Reengineering

### II. Essay (30%)
- [X] Emerging Trends in Software Engineering
- [X] Security Engineering

### III. Case (50%)
- [ ] Software Architecture
- [X] Risk Management

ㅤ

# Pembahasan Materi

## Multiple Choices (20%)

### Software Configuration Management

Merupakan hal yang lu lakuin untuk menata dan mengontrol konfigurasi dari sebuah software.

SCM mencakup:
- Version Control

  Helps in maintaining a history of changes, facilitates collaboration among team members, and enables reverting to previous versions if necessary.

- Change Management

  Provides mechanisms to track, review, approve, and implement changes in a controlled manner. This includes the ability to create change requests, assign them to appropriate individuals, and track their status throughout the change lifecycle.

- Release Management

  Ensures that the correct versions of software artifacts are utilized during the build and release processes.

Software Configuration Management memiliki beberapa elemen:
- Component elements:
- Process elements:
- Construction elements:
- Human elements:

Software Configuration Management memiliki proses sbg berikut:
1. User sadar kalo perlu ada perubahan/perkembangan
2. User kirim request ke developer untuk perubahan
3. Developer evaluasi, dan membuat report ttg apa yang terjadi
4. Change Control Authority membuat keputusan
5. Jika tidak diterima, kasih tau pengirim request kalau ia ditolak
6. Jika diterima, masukan request ke antrian "TODO"
7. Untuk setiap request yang ada di antrian, pilih seseorang yang akan menyelesaikannya
8. Check-out <configuration objects> yang appropriate sesuai dengan Request. (kalo lu pake versionning, object-object yang layak pakai akan ada versionnya sendiri dan disimpan di database. Check-out ini artinya lu ngambil object yang dipakai oleh aplikasi sekarang, untuk dimodifikasi)
9. Buatlah perubahan yang appropriate sehingga Request terpenuhi
10. Review (audit) perubahan yang telah lu buat.
11. Check-in config object yang udah dimodifikasi, dan tes itu sesuai dengan ***baseline*** yang ada.
12. Perform quality assurance dan tes lainnya
13. Usulkan agar object yang udah lulus tes ikut pada rilis selanjutnya.
14. Rebuild aplikasinya, dan masukkan object yang berubah kedalamnya
15. Distribute aplikasi versi baru.

ㅤ


### Version Control and Branch Management

Version control adalah gabungan dari sesuatu yang lu lakuin, dengan alat yang membantu lu dalem menjaga riwayat dari sebuah file.

Aplikasi version control yang terkenal adalah Git untuk lokal, dan GitHub yang di-host pada cloud.

Pada aplikasi version control, ada yang namanya **Change Set**. Yang disimpan pada sebuah **Change Set** adalah semua perubahan pada file yang di-*track*.

Ketika suatu perubahan ingin kita simpan supaya dapat dilihat kembali, aplikasi umumnya akan memberikan kemudahan untuk kita dengan menamai commit kita.

\
Version control system terdapat 2 tipe:
1. **Centralized Version Control System**

   semua perubahan perlu dikomunikasikan dengan suatu entity central yang mendata semua perubahan.

   Ini kaku, developer akan susah bekerja sama dengan leluasa.


2. **Decentralized Version Control System**

   Ini kaya GitHub, lu clone repository ke device lu, dan lu bisa modify semua file dan commit ke repository punya lu sendiri.

   Ketika lu memang mau publish sebuah perubahan, lu bisa open a pull request dengan central repository.

ㅤ

#### Branch Management

Konsep yang digunakan untuk me-refer kepada kegiatan mengurus branch.

Branch management biasanya dilakukan di decentralized version control system, untuk meng-resolve conflict yang ada ketika terdapat perbedaan yang berbeda pada branch.

ㅤ

### Continuous Integration, Continuous Development (CI/CD)

Continuous integration dalah sebuah konsep yang memasukkan code-yang-baru-ditulis kedalam repo, dan menguji kode itu secara cepat.

Continuous deployment adalah konsep yang dilakukan SETELAH cont. integration, yang meng-compile dan me-rilis software versi baru, setelah code-nya lulus uji.

Manfaatnya ada beberapa:
- Feedback dateng lebih cepat (karena lu rilisnya cepet)
- Bug lebih sedikit, dan terdeteksi lebih cepat (karena setiap rilis bedanya tidak banyak)
- Mempercepat proses rilis

ㅤ


### Software Architecture

Software architecture adalah blueprint dari sebuah software. Ia menentukan ***component*** mana yang interaksi dengan siapa, dan mengatur organisasinya.

> Component bisa dimengerti sebagai *module*, *library*, *service* atau apapun yang digunakan untuk meng-accomplish sesuatu.

Anggaplah mau buat rumah. Sebelum dibuat, rumah harus sudah di-plan dulu sebelum pesen material dan eksekusi pembangunan.

Setelah selesai pembangunan pun, blueprint bisa berguna untuk membantu memahami struktur dari rumah.

Arsitektur ada banyak gaya:

- Data-centered Style

  Bayangin ada 5 toko yang saweran buat sewa suatu gudang. Gudang itu diakses terus-terusan sama kelima toko ini.

  Jadi di style ini, data storage itu adalah inti dibalik arsitekturnya. Data storage akan sering diakses, dan akan melakukan banyak data modifying activity.

- Call-and-return Style

  Lu panggil sebuah modul dari software, ia mengembalikan data yang lu minta (API)

- Layered Style

  Bayangin ada beberapa level di suatu game. Semakin bertambahnya level, lu semakin deket dengan boss.

  Sama dengan ini: disini, program memiliki beberapa layer: semakin dalem, semakin deket dengan data.

  Ini itu MVC (Model View Controller) (inget PSD LAB). Paling atas adalah layer View (yang nampung UI .aspx). Layer tengah adalah controller (yang validasi dan mengatur logika). Layer bawah adalah database dan model (data).

ㅤ


### Deployment

Deployment adalah aktivitas yang memungkinkan software utk dapat berjalan pada sebuah sistem (device-nya pengguna).

Deployment biasanya di-bundle dengan aktivitas:
1. penyediaan env
2. installing
3. testing

Ketika software di-deploy, ia itu sebaiknya dimonitor untuk beberapa saat (jaga-jaga kalau ada masalah)

ㅤ

#### Deployment Strategies

* Basic Deployment

  Deploy keseluruhan update diatas versi yang sekarang

* Rolling Deployment

  Deploy sebagian saja dari keseluruhan update

* Multiservice Deployment

  Pada microservices architecture, dia itu update banyak service sekaligus

* Blue/Green Deployment

  Jadinya terdapat 2 versi (satu old, satu new) yang working secara sekaligus

* Canary Deployment

  Deploy sedikit-sedikit (incremental) (BUKAN SUBSET DARI UPDATE)

* Shadow Deployment

  Keadaan dimana incoming request milik aplikasi lama diarahkan ke versi yang terbaru. Ini seakan-akan aplikasinya belum update, meskipun sebenarnya sudah.

ㅤ

#### Deployment Best Practices

1. Buat cluster berbeda untuk production dan non-production
2. Apply resource limits (kalo something gone wrong, karena resourcenya terbatas, dampaknya juga minimal)
3. Collect deployment metrics (angka-angka analytics)
4. Otomate database updates

ㅤ


### Maintenance and Reengineering

Maintenance and reengineering are **two different areas in software engineering**. Maintenance is for running the system till the age of the system where as the reengineering make the system new to work for another life span. Scope of reengineering is vast and challenging as compared to maintenance.

ㅤ

ㅤ
ㅤ
ㅤ
## Essay (30%)

### Emerging Trends in Software Engineering

Tiga pertanyaan pada emerging trends:
1. Seberapa cepat teknologi bisa berkembang?
2. Seberapa signifikan efeknya feedback?
3. Seberapa berasa dampaknya?

#### Soft Trends yang Telah Diamati

1. Connectivity and Collaboration

   Ini telah membuat proses kolaborasi saat perancangan software bisa dilakukan dari jarak jauh.

2. Globalization

   Anggota tim bisa berasal darimana saja, dengan ekspertise yang berbeda-beda. Untuk software dapat berhasil, si developer sebagai tim harus dapat berhasil dalam meng-harness potensial penuh dari tim-nya.

#### Open-World Software

Merupakan software yang didesign untuk terus beradaptasi dengan environment yang terus berganti.

#### Open Source Software

Merupakan software yang source-code nya tersedia secara public.

Open Source merupakan methodology yang mengizinkan **siapa saja** untuk berkontribusi, sehingga dapat menghasilkan product yang berkualitas dan reliable (akibat expertise orang-orang)

#### Technology Direction

Software engineering is about people dan kebisaan mereka untuk saling mengkomunikasikan kebutuhan mereka, dan berinovasi sehingga kebutuhan mereka itu bisa terpenuhi.

Setiap kali ada unsur orang, maka sudah pasti akan ada perubahan.

Software engineering pada umumnya ingin perubahan untuk datang secara jarang-jarang namun periodik. Hanyalah ketika sebuah tipping point tercapai, baru mereka mau berubah.

ㅤ


### Security Engineering

Kunci penting dari keamanan sebuah aplikasi adalah: **menjaga mereka yang tidak memiliki kepentingan dari mengakses sebuah informasi**.

Mengantisipasi pihak luar dari mendapatkan akses atas data dinamakan ***threat analysis***.

Dengan menjaga software untuk terus secure, anda telah menjaga **integrity, avaibility, reliability, dan safety dari software**.

> Developer tidak mungkin untuk membuat sistem yang 100% secure, makanya buatlah backup copy dari data penting, dan siapkan system komponen yang redundant (berlebihan).

Urutan flownya **secara UMUM** adalah sebagai berikut:
1. Cari vulnerabilitas (celah) dimana pihak luar dapat mengakses informasi yang tidak-tidak
2. Analisis caranya agar celah tersebut bisa ditambel (plan cara memperbaikinya)
3. Eksekusikan plan yang dibuat.
4. Jika sudah terlanjur jebol, cari cara untuk memitigasi future breach.

Security Engineering memiliki 6 tahap:
1. Identify asset" yang dimiliki software, supaya lu bisa analisa nantinya
2. Buatlah architecture overview supaya ngerti hubungan dari software dengan asset"nya
3. Decompose the application agar lu punya clue "dimana Risk mungkin sembunyi"
4. Mulailah cari threat-threat yang ada.
5. Dokumentasikan threat yang lu temuin
6. Klasifikasi threat-nya. Yang klasifikasinya berat, lu harus selesaiin secepetnya.
ㅤ

ㅤ
ㅤ
ㅤ
## Case (50%)

### Software Architecture

What the fu-

ㅤ


### Risk Management

![risk management paradigm](https://i.ibb.co/GJmBYQ7/Screenshot-2023-06-26-194331.jpg)

Didalam sebuah risk management, semua dimulai dari:
1. **Mengidentifikasi Risk yang ada**,

diikuti dengan

2. **Menganalisa Risk yang tadi ditemukan akan nature yang dibawanya**,

yang begitu kita dapat buat

3. **Rencana untuk memitigasinya**.

Lalu seiring berjalannya waktu, kita

4. **Pantau apakah Risk itu makin benar-benar terjadi atau bisa dibiarkan.**

Ketika Risk itu benar-benar terjadi, kita

5. **Kontrol dia sesuai dengan rencana yang dibuat pada tahap 3.**

---

Ada dua strategi dalam Risk Management:

**I. Reactive Management**

- Dilakuin setelah sebuah risk muncul.
- Resources baru akan dialokasi SETELAH perkara terjadi

**II. Proactive Management**

- Dilakuin sebelum sebuah risk muncul, dan menghindari dari terjadinya sebuah risk.
- Secara periodic akan melakukan sebuah analisa akan Risk yang dapat muncul
- Membuat plan contigency yang dapat memitigasi seberapa dampak buruk yang dapat diakibatkan sebuah Risk

---

Terdapat 3 kata kunci yang berkaitan dengan ***Risk*** pada software engineering:

1. **Mitigation**

   Gimana caranya menghindar dari risk?

2. **Monitoring**

   Faktor apa yang bisa kita amati untuk bisa tau bahwa si Risk nya ini makin likely atau sebaliknya?

3. **Management**

   Apa yang kita lakuin kalo Risknya kebeneran terjadi?

---

Untuk prinsip, terdapat 7 prinsip disekitar Software Risk:
1. Maintain a global perspective

   Lu kalo mau analisa sebuah Risk, liat itu dari konteks-nya sebuah sistem dan sisi bisnis

2. Take a forward-looking view

   Pikirin juga tentang Risk yang mungkin muncul di waktu kedepan -- supaya lu siap-siap.

3. Encourage open communication

   Kalo seseorang menaikkan topik potensi Risk, lu perhatiin

4. Integrate

   Software process harus mencerminkan konsiderasi yang lu ambil dalam memitigasi sebuah Risk

5. Emphasize a continuous process

   Sembari lu develop software, lu juga harus sembari pantau Risk-Risk yang udah lu indentifikasiin. Naikan treat level-nya sesuai dengan informasi yang muncul.

6. Develop a shared product vision

   Kalo semua stakeholders memiliki visi yang sama untuk suatu software, maka bisa jadi Risk Identificationnya akan berjalan lebih baik.

7. Encourage teamwork

   Gunakan semua available efforts agar terhindar dari perkara.

---

Risk umumnya muncul disekitar:
1. Product size

   Risk yang muncul akan terasosiasi dengan seberapa besar (ribet) software yang ingin dibuat.

2. Business impact

   Risk yang muncul akan terasosiasi dengan constraint dari management ataupun keadaan pasar.

3. Customer characteristics

   Risk yang muncul akan terasosiasi dengan customer yang menggunakan aplikasinya.

4. Process definition

   Risk yang muncul akan terasosiasi dengan seberapa derajat lu ngikutin pre-defined guidance, pas lu buat proses dari suatu software.

5. Devlopment environment

   Risk yang muncul akan terasosiasi dengan ketersediaan dan kualitas dari alat yang dipake dalam membuat software.

6. Technology to be built

   Risk yang muncul akan terasosiasi dengan keterbaruan (generasi) dari teknologi yang dipakai oleh software.

7. Staff size & experience

   Risk yang muncul akan terasosiasi dengan expertise dan jumlah orang yang dapat berkontribusi pada proses pembangunan software.
