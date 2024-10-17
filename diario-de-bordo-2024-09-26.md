> **Linguagens e Paradigmas de Programação - Prof. Cassio Leonardo**
> 
> **Nome**: Gustavo Neves Piedade Louzada
> 
> **Matrícula**: 202107016
> 
> **Linguagem escolhida**: Rust 🦀

---

### Subprogramas

#### Definição

A definição de um subprograma em Rust se dá da seguinte maneira:

```rust
fn function_name(param1: datatype, param2: datatype, ....paramN: datatype) -> returntype{
	statement 1;
	statement 2;
	statement N;
}
```

- `fn`: palavra-chave para a definição de funções;
- `function_name`: nome da função;
- `param1....paramN`: parâmetros da função;
- `datatype`: tipos dos parâmetros;
- `returntype`: tipo do retorno.


#### Passagem de parâmetros por valor

A passagem de parâmetros por valor não se difere muito do que já é tido como "convencional" nas linguagens imperativas:

```rust
fn square(mut n:i32){
	n = n * n;
	println!("The value of n inside function : {}", n);
}

fn main() {
	let n = 4;
	println!("The value of n before function call : {}", n);
	println!("Invoke Function");
	square(n);
	println!("\nThe value of n after function call : {}", n);
}
```

Executando o código acima, temos a seguinte saída:

```console
The value of n before function call : 4
Invoke Function
The value of n inside function : 16

The value of n after function call : 4
```

É possível observar como, apesar de ter sido alterado dentro da função, o valor permanece o mesmo no escopo em que o subprograma foi invocado.


#### Passagem de parâmetros por referência

Utilizando o exemplo anterior, apenas com uma pequena modificação, podemos observar a passagem de parâmetros por referência:

```rust
fn square(n:&mut i32){
	*n = *n * *n;
	println!("The value of n inside function : {}", n);
}

fn main() {
	let  mut n = 4;
	println!("The value of n before function call : {}", n);
	println!("Invoke Function");
	square(&mut n);
	println!("The value of n after function call : {}", n);
}
```

Observemos o uso do caractere `&` junto da palavra-chave `mut`, que indica a passagem por referência, bem como a utilização de `*` para acessar o valor do argumento recebido.

Executando o código, obtemos como saída:

```console
The value of n before function call : 4
Invoke Function
The value of n inside function : 16
The value of n after function call : 16
```

Aqui, diferentemente da passagem por valor, podemos observar que o valor atribuído à variável `n` dentro da função, se mantém fora de seu escopo.


#### Passagem por resultado

O retorno de valores de funções, como já explicitado anteriormente, deve ter seu tipo explicitado e declarado juntamente ao cabeçalho da função:

```rust
fn square(n:i32)->i32{
	println!("The value of n inside function : {}", n);
	return n * n;
}
```

No exemplo acima, podemos ver como o tipo do retorno (`i32`) é explicitado após o `->`.


#### Genéricos

É possível definir parâmetros de tipos genéricos da seguinte maneira em Rust:

```rust
fn foo<T>(arg: T) { ... }
```

Onde `T` define um tipo genérico que deve ser o mesmo tipo do parâmetro `arg`.


#### Subprogramas como parâmetros

A passagem de subprogramas como parâmetros em Rust é possível da seguinte maneira:

```rust
fn add_one(x: i32) -> i32 {
    x + 1
}

fn do_twice(f: fn(i32) -> i32, arg: i32) -> i32 {
    f(arg) + f(arg)
}

fn main() {
    let answer = do_twice(add_one, 5);
    println!("The answer is: {answer}");
}
```

Tendo como saída:

```bash
The answer is: 12
```