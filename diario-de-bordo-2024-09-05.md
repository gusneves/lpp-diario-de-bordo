> **Linguagens e Paradigmas de Programação - Prof. Cassio Leonardo**
> 
> **Nome**: Gustavo Neves Piedade Louzada
> **Matrícula**: 202107016
> **Linguagem escolhida**: Rust 🦀

---
#variáveis 

### Nome

De modo geral, a nomenclatura em Rust tende a utilizar `UpperCamelCase` para constructos de nível de tipo (como tipos, *enums* e *traits*) e `snake_case` para constructos de nível de valor (como variáveis locais, métodos e funções). Mais detalhes podem ser vistos na [RFC 430](https://github.com/rust-lang/rfcs/blob/master/text/0430-finalizing-naming-conventions.md).

### Tipos

#### Amarração

As variáveis em Rust possuem amarração estática de tipo, podendo der explicitamente ou implicitamente definido, por exemplo:

```rust
fn main(){
	// definição implícita
	let x = 2.0; // tipo: f64
	
	// definição explícita
	let y: f32 = 3.55; // tipo: f32
}
```
#### Inteiros

Os tipos inteiros em Rust são separados entre inteiros *signed* (`i`) e *unsigned* (`u`)

| Length  | Signed  | Unsigned |
| ------- | ------- | -------- |
| 8-bit   | `i8`    | `u8`     |
| 16-bit  | `i16`   | `u16`    |
| 32-bit  | `i32`   | `u32`    |
| 64-bit  | `i64`   | `u64`    |
| 128-bit | `i128`  | `u128`   |
| arch    | `isize` | `usize`  |

#### Exemplos de declaração

```rust
fn main() {
	// tupla
    let tup: (i32, f64, u8) = (500, 6.4, 1);
	
	// vetor
	let a: [i32; 5] = [1, 2, 3, 4, 5];
	
	// inteiro
	let i = 5;
	
	// booleano
	let t = true;
}
```

### Mutabilidade

Por padrão, variáveis em Rust são imutáveis, o que garante maior segurança e facilidade de concorrência em programas com a linguagem e permite que todos os seus valores sejam alocados na *stack* da memória. No entanto, ainda é possível criar uma variável mutável explicitamente adicionando a palavra-chave `mut` em sua declaração: 

```rust
fn main() {
    let mut x = 5;
    println!("The value of x is: {x}");
    x = 6;
    println!("The value of x is: {x}");
}
```

Com a execução deste programa, teremos a seguinte saída:

```console
$ cargo run
   Compiling variables v0.1.0 (file:///projects/variables)
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.30s
     Running `target/debug/variables`
The value of x is: 5
The value of x is: 6
```


#### Constantes

Diferentemente das variáveis, que podem ser imutáveis, as constantes são *sempre* imutáveis. Portanto, não é possível adicionar `mut` à declaração de uma constante. Outro detalhe é que o tipo de uma constante deve ser obrigatoriamente definido de maneira explícita:

```rust
const YEAR: u16 = 2024; 
```


### Escopo

Rust segue a definição de escopo estático, de modo que a execução do programa:

```rust
fn main() {
    let x = 5;

    let x = x + 1;

    {
        let x = x * 2;
        println!("The value of x in the inner scope is: {x}");
    }

    println!("The value of x is: {x}");
}
```

Terá a saída:

```console
$ cargo run
   Compiling variables v0.1.0 (file:///projects/variables)
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.31s
     Running `target/debug/variables`
The value of x in the inner scope is: 12
The value of x is: 6

```

Nesse exemplo também é possível observar que é permitido declarar uma variável com um nome já utilizado anteriormente no mesmo escopo, no entanto, a última declaração daquela variável substituirá a anterior.

