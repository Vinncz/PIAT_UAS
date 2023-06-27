
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

#### Abstraction Smells
- [x] Missing Abstraction
- [x] Imperative Abstraction
- [x] Incomplete Abstraction
- [x] Multifaceted Abstraction
- [x] Unnecessary Abstraction
- [x] Unutilized Abstraction
- [x] Duplicate Abstraction

#### Encapsulation Smells
- [x] Deficient Encapsulation
- [x] Leaky Encapsulation
- [x] Missing Encapsulation
- [x] Unexploited Encapsulation

#### Modularization Smells
- [ ] Broken Modularization
- [ ] Insufficient Modularization
- [ ] Cyclically-dependent Modularization
- [ ] Hub-like Modularization

#### Hierarchy Smells
- [ ] Missing Hierarchy
- [ ] Unnecessay Hierarchy
- [ ] Unfactored Hierarchy
- [ ] Wide Hierarchy
- [ ] Speculative Hierarchy
- [ ] Deep Hierarchy
- [ ] Rebellious Hierarchy
- [ ] Broken Hierarchy
- [ ] Multipath Hierarchy
- [ ] Cyclic Hierarchy

ㅤ

# Pembahasan Materi

## Abstraction Smells

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

Kejadian dimana sebuah ***class atau interface sudah dibuatkan, tapi gapernah dipakai.***

**CONTOH**
```java
interface Animal {
	public makeSound () {}
}

class Dog {
	public bark () {
		System.Output.Println("ANJING LU");
	}
}
```

ㅤ

### Duplicate Abstraction

Kejadian dimana ***ada method/implementasi yang sama, di dua atau lebih class.***

**CONTOH**
```java

```

ㅤ



## Encapsulation Smells

### Deficient Encapsulation

Kejadian dimana ***access modifier mengizinkan pihak tidak berkepentingan, untuk dapat mengakses infromasi.***

**CONTOH**
```java
class Foo {
	/* Jika memang tidak perlu, ubah ke private */
	public bar () {}
}
```

ㅤ

### Leaky Encapsulation


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

### Missing Encapsulation

Kejadian dimana sebuah ***method yang secara logika seharusnya memiliki pasangan, malah tidak memiliki pasangan.*** TL:DR; Kalo ada getter, ada setter -> kecuali jika memang intended readonly.

**CONTOH**
```java
class Car {
	public OpenTrunk () {}
	/* tidak ada CloseTrunk() */
}
```

ㅤ

### Unexploited Encapsulation

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

