
ㅤ
# Personal Intensive Acceleration Training (PIAT)

\
__Made for:__
> _Code Reengineering_
> [ LEC ] -  Final Exam
> 2023 Even Semester

__Composed by:__
> 2501977941 - Kevin Gunawan
> ChatGPT (Best Boi)

ㅤ

## Outline

Materi UAS akan diambil dari session 16 sampai 26:

#### Abstraction Smells _______________
- [x] **Missing Abstraction**
   Keadaan dimana encoded strings digunakan sebagai alat yang dapat mengklasifikasi suatu object

- [x] **Imperative Abstraction**
   Keadaan dimana operasi didefine sebagai class

- [x] **Incomplete Abstraction**
   Method yang tidak dilengkapi dengan keberadaannya method lain

- [x] **Multifaceted Abstraction**
   Kejadian dimana suatu class memiliki banyak tanggung jawab

- [x] **Unnecessary Abstraction**
   Kejadian dimana sebuah _**class sudah dibuatkan, tapi class itu ga berfaedah (berbobot).**_

- [x] **Unutilized Abstraction**
   Kejadian dimana suatu SUBclass extends suatu SUPERclass, namun tidak OVERRIDE semua methodnya (meskipun ia BISA)

- [x] **Duplicate Abstraction**
   Kejadian dimana suatu SUBclass extends suatu SUPERclass – namun, ada dua atau lebih SUBclasses (plural) _**memiliki method yang sama**_ meskipun itu tidak ada di SUPERclass.

ㅤ

#### Encapsulation Smells ________________
- [x] **Deficient Encapsulation**
   Kejadian dimana access modifier TIDAK DIMANFAATKAN SEPENUHNYA untuk menutupi informasi

- [x] **Leaky Encapsulation**
   Kejadian dimana sebuah method yang HANYA BERGUNA untuk men-support FUNGSIONALITAS suatu class malah dibuat public.

   Smell ini juga bisa diaplikasikan kepada method yang penamaannya tidak appropriate (bisa membocorkan cara implementasi dari suatu class).

- [x] **Missing Encapsulation**
   Kejadian dimana access modifier TIDAK DIGUNAKAN SAMA SEKALI untuk menutupi informasi

- [x] **Unexploited Encapsulation**
   Jangan pakai IF-ELSE statement untuk ngecek tipe dari sebuah object. Kalo ketauan, namanya bukan enkapsulasi.

ㅤ

#### Modularization Smells ___________
- [x] **Broken Modularization**
   Data dan/atau method yang seharusnya menjadi bagian dari class A malah ditaro di class B

- [x] **Insufficient Modularization**
   Mirip long method dan large class. Tidak adanya refactor yang cukup pada suatu class/method.

- [x] **Cyclically-dependent Modularization**
   Kejadian dimana suatu SUPERclass yang memiliki banyak SUBclass sadar jika: SUBclasses (plural) miliknya bergantung satu sama lain. Dependency selevel.

- [x] **Hub-like Modularization**
   Kejadian dimana suatu class memiliki BANYAK KETERGANTUNGAN dengan class lain.

   TLDR: Class central diperlukan/memerlukan banyak class lain agar dia dapat berfungsi.

ㅤ

#### Hierarchy Smells ___________
- [x] **Missing Hierarchy**
   Kejadian dimana terdapat lebih dari 1 class yang memiliki behaviour yang sama TANPA DILAKUKANNYA INHERITANCE

- [x] **Unnecessay Hierarchy**
   Kejadian dimana inheritance tidak diperlukan (misal suatu class hanya berbeda pada attribut saja). Untuk suatu class dapat dikatakan inherit dari suatu SUPERclas, dia itu harus berubah behaviournya.

- [x] **Unfactored Hierarchy**
   Jika ada duplicate code: baik itu attribute atau method, selidiki. Bisa jadi itu hierarchy yang tidak dibuat atau tidak benar. Ini namanya

- [x] **Wide Hierarchy**
   Kejadian dimana suatu class di-inherit oleh banyak classes.

- [x] **Speculative Hierarchy**
   Kejadian dimana suatu SUBclass dibuat, namun tidak dipakai

- [x] **Deep Hierarchy**
   Kejadian dimana SUPERclass hanya di-inherit oleh sedikit SUBclass lain, namun ada BANYAK SUB-SUBCLASS YANG INHERIT dari SUBclass

- [x] **Rebellious Hierarchy**
   Kalo lu inherits, artinya lu menerima SEMUA hal yang diwariskan oleh si SUPERclass. gaboleh nolak.

- [x] **Broken Hierarchy**
   Kejadian yang menggangu inheritance

- [x] **Multipath Hierarchy**
   Kejadian dimana suatu SUB-SUBclass extends/implements dari SUPERclassnya milik SUPERclass.

- [x] **Cyclic Hierarchy**
   Semua SUBclass harus bergantung pada SUPERclass – bukan sebaliknya. Jika terbalik, bawa penulis code ke RSJ.

ㅤ

## Abstraction Smells

Semua yang berurusan dengan penataan (abstraksi)

### Missing Abstraction

Kejadian dimana seseorang menggunakan encoded string untuk membedakan class satu dari yang lain.

**CONTOH**
```java
class fruit {
	public fruit () {}
}

class vegetable {
	public vegetable () {}
}

public static void main (String [] args) {

	object apple = new fruit();

	/* Salah disini */
	if ( apple.className.equals("fruit") ) {
		// ...
	}

}
```

ㅤ

### Imperative Abstraction

Kejadian dimana sebuah ***operasi yang bisa di-define sebagai method malah dibuat sebagai class.***

**CONTOH**
```java
class PrepareConsole {
	public static clearScreen () {
		System("cls")
	}
}
```

ㅤ

### Incomplete Abstraction

Kejadian dimana sebuah ***method yang secara logika seharusnya memiliki pasangan, malah tidak memiliki pasangan.*** TL:DR; Kalo ada getter, ada setter -> kecuali jika memang intended readonly.

**CONTOH**
```java
class Car {
	public OpenTrunk () {}
	/* tidak ada CloseTrunk() */
}
```

ㅤ

### Multifaceted Abstraction

Kejadian dimana sebuah ***class memiliki lebih dari satu tanggung jawab***.

**CONTOH**
```java
class WashingMachine {
	public static washLaundry () {}

	/* mesin cuci hanya cukup utk nyuci */
	public static ironLaundry () {}
}
```

ㅤ

### Unecessary Abstraction

Kejadian dimana sebuah ***class sudah dibuatkan, tapi class itu ga berfaedah (berbobot).***

**CONTOH**
Buat apa dibikin class RedButton? Mending bikin method `setColor()` pada class `Button`.
```java
class Button {
	string color;
	public Button (String color) {
		this.color = color;
		return this;
	}
}

class RedButton extends Button {
	public RedButton () { super("Red") }
}
```

ㅤ

### Unutilized Abstraction

Unused abstraction occurs when a subclass EXTENDS a SUPERclass but fails to implement all of its methods, even though it has the capability to do so.

**CONTOH**
```java
class Animal {
    public void eat() {
        System.Out.Println('Animal is sleeping');
    }

    public void sleep() {
        // Implementation for sleeping
    }
}

class Dog extends Animal {
    @Override
    public void eat() {
        System.Out.Println('Dog is sleeping');
    }
    public void bark() {
        // Implementation for barking
    }

    /* DIA GA IMPLEMENTS METHOD eat() DAN sleep(), MESKIPUN IA BISA */
    /* INI NAMANYA UNUTILIZED ABSTRACTION */
}

public static void main (String [] args) {
    Animal a = new Dog();
    a.eat(); // ini artinya dia pakai implementasinya class Dog sendiri
}
```

ㅤ

### Duplicate Abstraction

Kejadian dimana suatu SUBclass extends suatu SUPERclass -- namun, ada dua atau lebih SUBclasses (plural) ***memiliki method yang sama*** meskipun itu tidak ada di SUPERclass.

**CONTOH**
```java
class Animal {
   public eat() {}
}

class Dog extends Animal {
   @Override
   public eat() {}

   public makeSound () {}
}

class Cat extends Animal {
   @Override
   public eat() {}

   /* nama method tidak perlu sama, asalkan dia menyelesaikan hal yang sama */
   public makeSound () {}
}
```

ㅤ



## Encapsulation Smells

ㅤ

### Deficient Encapsulation

Kejadian dimana ***access modifier mengizinkan pihak tidak berkepentingan, untuk dapat mengakses infromasi.***

**CONTOH**
```java
public class BankAccount {
    public double balance;
    /* ada pengecekan balance di method withdraw */
    /* tapi masih bisa diakses directly, jadi sama aja useless */
    public void withdraw(double amount) {
        if (amount > 0 && amount <= balance) {
            balance -= amount;
            System.out.println("Withdrawal successful!");
        } else {
            System.out.println("Insufficient funds!");
        }
    }
}

public class Main {
    public static void main(String[] args) {
        BankAccount account = new BankAccount();

        account.balance = 500; // DISINI DIA AKSES DIRECTLY
        account.balance -= 200; // DISINI DIA AKSES DIRECTLY

        System.out.println("Current balance: " + account.balance);
    }
}
```

ㅤ

### Leaky Encapsulation

Kejadian dimana sebuah method yang HANYA BERGUNA untuk men-support FUNGSIONALITAS suatu class malah dibuat public.

**CONTOH**
```java
class SoccerPlayer {
	public kickBall () {
		locateBall();
		executeKickingManeuver();
	}

	/* karena locateBall adalah function yang support class SoccerPlayer, dia seharusnya dibuat sebagai private  */
	public locateBall () {}
	public executeKickingManeuver () {}
}
```
\
Smell ini juga bisa diaplikasikan kepada method yang penamaannya tidak appropriate (bisa membocorkan cara implementasi dari suatu class).

**CONTOH**
```java
class CardMatch {
    /* penamaan ini sama aja boong.. meskipun di private juga implementasinya ketahuan */
	private bubbleSortCard () {}
}
```

ㅤ

### Missing Encapsulation

Kejadian dimana ***access modifier mengizinkan pihak tidak berkepentingan, untuk dapat mengakses infromasi.***

Bedanya dengan `DEFICIENT ENCAPSULATION` adalah disini, TIDAK ADA EFFORT yang dialokasikan untuk menegakkan enkapsulasi -- dimana pada `DEFICIENT ENCAPSULATION` itu ada, tapi TIDAK CUKUP.
\
**CONTOH**
```java
class Car {
	public OpenTrunk () {}
	/* tidak ada CloseTrunk() */
}
```

ㅤ

### Unexploited Encapsulation

Jangan pakai IF-ELSE statement untuk ngecek tipe dari sebuah object. Kalo ketauan, namanya bukan enkapsulasi.

**CONTOH**
```java
class Vehicle {}

class Car extends Vehicle {}

public static void main () {
   Vehicle a = new Car()

   if (a.class.equalsIgnoreCase("Car")) {
      ...
   } else {
      ...
   }
}
```

ㅤ

## Modularization Smell

Semua yang berhubungan dengan pembagian kode manjadi bagian-bagian kecil. Prinsipnya itu mudah:

- Related data dan methods harusnya berkumpulan (localized)
- Abstraksi jangan terlalu ribet sampe susah baca sendiri
- JANGAN ADA CYCLIC dependencies
- Dependencies secukupnya aja. Kalo ga bagus, jangan dipaksain

ㅤ


### Broken Modularization

Data dan methods yang bagian dari suatu class dipisah-pisah ke tempat lain.

```java
lu tau lah
```

ㅤ


### Insufficient Modularization

Class/method terlalu besar, kurang dimodularisasi. (Long method/large class)

**CONTOH**
```java
lu tau lah
```

ㅤ


### Cyclically-dependent Modularization

Class yang bergantung dengan class selevel dengannya.

Anggap ada class **Bapak** yang extends dari class **Kakek**.

Jika ada juga class **Paman** yang juga extends dari class **Kakek**, dan si class **Bapak** mengandung class **Paman** didalamnya (sebagai ATTRIBUT maupun PARAMETER), itu namanya Cyclically-dependent Modularization.

**CONTOH**
```java
lu tau lah
```
ㅤ

### Hub-like Dependencies

Kejadian dimana suatu class memiliki BANYAK KETERGANTUNGAN dengan class lain.

TLDR: Class central diperlukan/memerlukan banyak class lain agar dia dapat berfungsi.

**CONTOH**
```java
lu tau lah
```


ㅤ




## Hierarchy

Semuanya yang berhubungan dengan inheritance di OOP. Hafalkan poin-poin berikut untuk lebih mudah mengidentifikasi smell hierarchy:

1. Semua elemen yang mirip harus digabungkan. Jika tidak digabungkan, mungkin dia memiliki smell **Missing Hierarchy**.
   ```java
   class Bus {}
   class Car {}
   class Bike {}

   /* semua yang sama pada class-class diatas bisa di-extract ke interface/abstract class */
   abstract class Vehicle {}
   ```
2. Jika ada duplicate code: baik itu attribute atau method, selidiki. Bisa jadi itu hierarchy yang tidak dibuat atau tidak benar. Ini namanya **Unfactored Hierarchy**
   ```java
   class Car {
      protected int Speed;
   }

   class RedCar extends Car {
      String color = 'red'; /* attribut yang sama di kedua SUBclass namun gaada di parent, sehinnga perlu ditambahin sendiri di SUBclass */
      void accelerate () {
         this.Speed++; /* method melakukan hal yang sama */
      }
   }
   class BlueCar extends Car {
      String color = 'blue'; /* attribut yang sama di kedua SUBclass namun gaada di parent, sehinnga perlu ditambahin sendiri di SUBclass */
      void accelerate () {
	     this.Speed++; /* method melakukan hal yang sama */
      }
   }
   ```
3. Pastikan bahwa inheritance itu berguna (setiap inheritance harus memiliki perbedaan dalam sifat, bukan hanya attribut saja). Ini namanya smell **Unnecessary Hierarchy**.
   ```java
   abstract class Car {
      static final int maxSpeed;
      void move () {};
   }

   class RedCar extends Car {
      static final String color = "red"; /* TDK VALID KALO HANYA NAMBAHIN ATTRIBUT */
      @Override
      void move () {};
   }

   class BlueCar extends Car {
      static final String color = "blue"; /* TDK VALID KALO HANYA NAMBAHIN ATTRIBUT */
      @Override
      void move () {};
   }
   ```
4. Pastikan bahwa setiap SUBclass dari SUPERclass inherit semua sifat-sifatnya. Tidak boleh menolak satu-pun sifat yang diwariskan. Ini itu smell **Rebellious Hierarchy** atau `Refused Bequest`
   ```java
   abstract class Person {
      void Live () {}
   }
   class Binusian extends Person {
      @Override
      void Live () {
         throw new Eexception ('DEAD INSIDE');
      }
   }
   ```
6. Semua inheritance harus dilakukan dari class yang paling BAWAH. Kalo ga begitu, namanya **Multipath Hierarchy**
   ```java
   class Person {
      void Live () {}
   }
   class Employee extends Person { }

   /* TIDAK BOLEH MAIN EXTENDS KE PERSON, KARENA MANAGER SEHARUSNYA ADALAH TURUNAN EMPLOYEE */
   class Manager extends Person { }
   ```
7. Semua SUBclass harus bergantung pada SUPERclass -- bukan sebaliknya. Jika terbalik, bawa penulis code ke RSJ. Ini namanya **Cyclic Hierarchy**.


ㅤ

## CONTRIBUTED BY KELVIN GIOVANNO

ㅤ

### Missing Hierarchy
Smell ini terjadi ketika terdapat lebih dari 1 subclass yang memiliki method dan behaviour class yang sama.

<br />

**Contoh Smell :**

```java
public Insets getBorderInsets(Component c, Insets insets){
  Insets margin = null;

  if (c instanceof AbstractButton)
  {
    margin = ((AbstractButton)c).getMargin();
  }
  else if (c instanceof JToolBar)
  {
    margin = ((JToolBar)c).getMargin();
  }
  else if (c instanceof JTextComponent)
  {
    margin = ((JTextComponent)c).getMargin();
  }

}
```
<br />

Dalam code ini, terdapat tiga objek (`AbstractButton`, `JToolBar`, `JTextComponent`) yang memiliki method yang sama yaitu `getMargin()`. Daripada memiliki method yang sama di setiap objek untuk
memeriksa apakah objek tersebut memiliki margin, kita dapat menggunakan  object inheritance dengan
menggunakan superclass atau interface untuk menempatkan method dan behavior yang sama.

<br />

**Setelah Refactor :**
```java
public Insets getBorderInsets(Component c, Insets insets){
  Insets margin = null;

  if (c instanceof MarginSupported)
  {
    margin = c.getMargin();
  }
}
```
<br />

### Unnecessary Hierarchy
Smell ini terjadi dikarenakan pembagian Object/Class dengan data yang berbeda beda instead of behaviour.

<br />

**Contoh Smell :**
```
[Flower]
  | (generalizes)
  +--[RedFlower]
  +--[GreenFlower]
  +--[YellowFlower]
```
<br />

Superclass `Flower` tidak di butukan . alasanya subclass pada superclass flower di bagikan atas perbedaan attribute warna . menurut Bertrand Meyer class Hierarchy dapat di terapkan jika class tersebut functionality baru atau feature baru.

<br />

### Unfactored Hierarchy
Smell ini bisa kembung jika terdapat code class yang sama atau duplikasi code. duplikasi code itu biasanya terdapat 5 tempat yaitu
- Duplication in siblings Type : duplikasi ini terdapat pada class yang berbeda namum superclassnya sama
- Duplication in Super and Subtype : duplikasi ini terjadi pada antar superclass atau subclass dari Superclass yang berbeda
- Unfactored Interface : terjadi ketika terdapat satu atau lebih interface yang memiliki method dengan kemiripan pada signature (parameter/return type)
- Unfactored implementation: terjadi ketika terdapat dua atau lebih kelas yang memiliki method dengan implementasi/behavior yang serupa.
- Unfactored interface and implementation: terjadi ketika terdapat method yang memiliki kemiripan baik pada signature (parameter/return type) maupun implementasi/behavior yang seharusnya dapat ditempatkan pada sebuah superclass.

<br/>

**Contoh Smell :**
```java
class Player implement Hittable {

    void hit(int dmg){
        this.hp = this.hp - dmg;
    }

    // rest of the code elided ...
}

class Monster implement Hittable {
    void hit(int dmg){
        this.hp = this.hp - dmg;
    }

    // rest of the code elided ...
}
```
<br/>

**Setelah Refactor :**
```java
class GameUnit implement Hittalble{
    void hit(int dmg){
        this.hp = this.hp - dmg;
    }

    // rest of the code elided ...
}

class Player extends GameUnit {

    // rest of the code elided ...

}

class Monster extends GameUnit {

    // rest of the code elided ...

}
```
<br/>

### Wide Hierarchy
Smell ini terjadi pada superclass yang terdapat banyak subclass

<br/>

**Penyebab smell ini terjadi :**
- Minimnya ***generalization***
- Malas Refactor (asal extends)

**Penyelesaian :**
- Terapin  ***introduce intermediate class***

**Contoh Smell :**

- Contoh 1

![Alt text](image-1.png)

- Contoh 2

Sebelum Refactor
![Alt text](image-2.png)

<br/>

Setelah Refactor
![Alt text](image-3.png)

<br/>

### Speculative Hierarchy
Smell ini terjadi di karenakan class yang dibuat tidak digunakan dan dibuat hanya untuk keperluan pada waktu tertentu (Gabakal di pakai juga)

**Penyelesaian :** langsung di hapus aja atau bahasa kerennya ***Collapse Hierarchy***

![Alt text](image.png)

<br/>

###  Deep Hierarchy
Smell ini terjadi pada Hierarchy yang memiliki ***generalisasi*** yang berlebihan.

<br />

**Penyelesaian :**
- Collapse Hierarchy

**Contoh Smell :**
![Alt text](image-5.png)

<br/>

### Rebellious Hierarchy
Smell ini terjadi pada Hubunagn Hierarchy yaitu yang tidak masuk akal. Smell ini mirip dengan smell Refused Bequest kalo lu pernah dengar. tetapi lebih merujuk pada pelanggaran ***interface***

**Contoh Smell :**

<br/>

- Sebelum refactor :
```java
public interface Shape {
  public int luas();
  public int keliling();
  public int volume();
}

public class Rectangle implements Shape {
  int w, h;

  @Override
  public int luas() {
    return w * h;
  }

  @Override
  public int keliling() {
    return 2 * (w + h);
  }

  @Override
  public int volume() {
    throw new UnsupportedMethodException("Not implemented yet!");
  }
}

public class Cube extends Shape {
  int l, w, h;

  @Override
  public int luas() {
    return 2 * (l * w + l * h + w * h);
  }

  @Override
  public int keliling() {
    return 4 * (l + w + h);
  }

  @Override
  public int volume() {
    return l * w * h;
  }
}
```

<br />

- Setelah Refactor :
```java
public interface Shape {
  public int luas();
  public int keliling();
  public int volume();
}

public class Rectangle implements Shape {
  int w, h;

  @Override
  public int luas() {
    return w * h;
  }

  @Override
  public int keliling() {
    return 2 * (w + h);
  }

  @Override
  public int volume() {
    throw new UnsupportedMethodException("Not implemented yet!");
  }
}

public class Cube extends Shape {
  int l, w, h;

  @Override
  public int luas() {
    return 2 * (l * w + l * h + w * h);
  }

  @Override
  public int keliling() {
    return 4 * (l + w + h);
  }

  @Override
  public int volume() {
    return l * w * h;
  }
}
```

<br/>

### Broken Hierarchy
Smell ini terjadi karna superclass dan subclass hubunganya tidak bersifat `is-a` .

**Ada 3 jenis Broken Hierarchy :**
- Hubungan superclass dan subclass yang seharusnya is-a (yang dapat diturunkan dengan keyword extends atau implements) malah diubah relasinya sebagai has-a sehingga relasi antar kedua class terputus.
- Hubungan base class dengan implementer yang seharusnya has-a (hubungan delegatif/aggregates) malah dipaksakan untuk berelasi sebagai is-a (inhertied superclass-subclass).
- Hubungan base class dan subclass yang terbalik, sehingga terdapat hierarki yang seharusnya tidak mendapatkan peran yang seharusnya malah harus menerimanya.

<br/>

**Contoh Smell :**

![Alt text](image-6.png)

Vector memiliki Method Push dan Pop sedangnkan Stack memiliki method Push , Pop dan Peek. Secara Konseptual hubungan antara vector dan stack itu seharusnya `has-a` namum malah digunakan sebagai hubungan `is-a`. hal ini menyebabkan sebagian method dari Object/Class Vector tidak dapat di gunakan di Object/Class Stack

Dalam class Stack, terdapat fungsi standar sebuah stack LIFO yaitu pop, push, dan peek.
```java
public void push(E data) {
  this.add(data);
}

public void pop() {
  this.removeElementAt(this.size()-1);
}

public E peek() {
  return this.elementAt(this.size()-1);
}
```

Namun dalam class Vector, beberapa method yang seharusnya diaplikasikan dari Vector sebagai berikut:
```java
@Override
public synchronized void add(int index, E element) {
  return super.add(index, element);
}

@Override
public synchronized E remove(int index) {
  return super.remove(index);
}
```
Malah ditolak oleh Stack dengan throw exception/return null karena tidak boleh return sembarang value.
```java
/*
* you cannot add or remove by index, use push/pop instead
*/
@Override
public synchronized void add(int index, E element) {
  throw new Exception("You can't add element at random index!");
}

@Override
public synchronized E remove(int index) {
  return null;
}
```

**Penyelesaian :**

![Alt text](image-7.png)

Mengubah Hubungan kedua Object menjadi `has-a` sehingga Stack dapat memanfaatkan Vector sebagai media penampungan dan mendelegasikan setiap kebutuhan dari Stack kepada Vector, namun tidak terakses oleh class lain.

```java
public class Stack<E> {
  private Vector<E> stack = new Vector<>();

  public void push(E data) {
    stack.add(data);
  }

  public void pop() {
    stack.removeElementAt(stack.size()-1);
  }

  public E peek() {
    return stack.elementAt(stack.size()-1);
  }
}
```
Pada class Vector hasil perubahan relationship, fungsi-fungsi Stack LIFO yaitu pop, push, dan peek didelegasikan ke Vector untuk add/remove/get object sesuai kebutuhan Stack itu sendiri.
