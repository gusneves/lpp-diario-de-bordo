> **Linguagens e Paradigmas de Programação - Prof. Cassio Leonardo**
> 
> **Nome**: Gustavo Neves Piedade Louzada
> **Matrícula**: 202107016
> **Linguagem escolhida**: Rust 🦀

---

### Operadores

**Unários (em ordem de precedência):**
- Negação: `!`;
- Desreferência: `*`;
- *Borrow*: `&`, `&mut`.


**Binários (em ordem de precedência):**
- *Typecast*: `as`;
- Aritméticos: `*`, `/`, `%`, `+`, `-`;
- Deslocamento de bits: `<<`, `>>`;
- *Bitwise*: `&`, `^`, `|`;
- Lógicos:  `==`, `!=`, `<`, `>`, `<=`, `>=`, `&&`, `||`;
- Intervalo: `start .. stop`;
- Atribuição: `=`;
- Atribuição composta: `-=`, `+=`, `/=`, `%=`, `*=`;

**Tabela de precedência e associatividade de operadores em Rust:**

| Operator/Expression                                           | Associativity       |
| ------------------------------------------------------------- | ------------------- |
| Paths                                                         |                     |
| Method calls                                                  |                     |
| Field expressions                                             | left to right       |
| Function calls, array indexing                                |                     |
| `?`                                                           |                     |
| Unary `-` `*` `!` `&` `&mut`                                  |                     |
| `as`                                                          | left to right       |
| `*` `/` `%`                                                   | left to right       |
| `+` `-`                                                       | left to right       |
| `<<` `>>`                                                     | left to right       |
| `&`                                                           | left to right       |
| `^`                                                           | left to right       |
| `\|`                                                          | left to right       |
| `==` `!=` `<` `>` `<=` `>=`                                   | Require parentheses |
| `&&`                                                          | left to right       |
| `\|`                                                          | left to right       |
| `..` `..=`                                                    | Require parentheses |
| `=` `+=` `-=` `*=` `/=` `%=`  <br>`&=` `\|=` `^=` `<<=` `>>=` | right to left       |
| `return` `break` closures                                     |                     |
[Referência](https://doc.rust-lang.org/reference/expressions.html)


### Estruturas de controle

**`if...else if...else`:**

```rust
fn main() {
      let learn_language="Rust";
      if learn_language == "Rust" {
         println!("You are learning Rust language!");
      }
      else if learn_language == "Java" {
         println!("You are learning Java language!");
      }
      else {
         println!("You are learning some other language!");
      }
}
```
**`match`:**

Para alcançar um comportamento semelhante ao `switch` de C, utiliza-se a palavra-chave `match`.

```rust
fn main() {
    let number = 13;

    println!("Tell me about {}", number);
    match number {
        // Match a single value
        1 => println!("One!"),
        // Match several values
        2 | 3 | 5 | 7 | 11 => println!("This is a prime"),
        // Match an inclusive range
        13..=19 => println!("A teen"),
        // Handle the rest of cases
        _ => println!("Ain't special"),
        // TODO ^ Try commenting out this catch-all arm
    }
}
```

### Sentenças iterativas

As sentenças iterativas de Rust são separadas em dois grupos: definidas e indefinidas. As sentenças definidas são executadas por um número de iterações já conhecidas a tempo de compilação, enquanto o número de iterações das indefinidas não é.

**Loops definidos: `for`**

```rust
fn main() {
    //define a for loop
    for i in 0..5 {
      println!("{}", i);
    }
}
```


**Loops indefinidos: `while`**

```rust
fn main() {
	let mut var = 1; //define an integer variable
	let mut found = false; // define a boolean variable
  // define a while loop
	while !found {
	    var=var+1;
	    //print the variable
	    println!("{}", var);
	    // if the modulus of variable is 1 then found is equal to true
	    if var % 3 == 1 {
		    found = true;
	    }
	    println!("Loop runs");
  }
}
```

**Loops indefinidos: `loop`**

```rust
fn main() {
	//define an integer variable
	let mut var = 1;
	// define a loop that continue infinite times
	loop {
		var = var + 1;
	    println!("{}", var);
	}
}
```
**Controle definidos por usuário:** Para controle de iterações utiliza-se a palavra-chave `break`.

**Controle lógico:** Para controle lógico de iterações utiliza-se a palavra-chave `continue`.

- ***Loop labels:*** Rust permite, também, atribuir *labels* a sentenças iterativas aninhadas, de modo que comportamentos como o seguinte sejam possíveis:

```rust
fn main() {
	'outer:for i in 1..5 { //outer loop
		println!("Muliplication Table : {}", i);
		'inner:for j in 1..5 { // inner loop
			if i == 3 { continue 'outer; } // Continues the loop over `i`.
			if j == 2 { continue 'inner; } // Continues the loop over `j`.
			println!("{} * {} = {}", i, j, i * j);
		}
	}
}
```
- Saída:

```none
Muliplication Table : 1
1 * 1 = 1
1 * 3 = 3
1 * 4 = 4
Muliplication Table : 2
2 * 1 = 2
2 * 3 = 6
2 * 4 = 8
Muliplication Table : 3
Muliplication Table : 4
4 * 1 = 4
4 * 3 = 12
4 * 4 = 16
```
