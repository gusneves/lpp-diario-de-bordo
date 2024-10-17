> **Linguagens e Paradigmas de Programação - Prof. Cassio Leonardo**
> 
> **Nome**: Gustavo Neves Piedade Louzada
> 
> **Matrícula**: 202107016
> 
> **Linguagem escolhida**: Rust 🦀

---

### Tratamento de exceções

Rust não possui exceções, mas divide seus erros em dois grupos: erros *recuperáveis* e erros *irrecuperáveis*.

Para a primeira categoria, Rust dispõe do tipo `Result<T, E>`, e para o segundo grupo, possui o macro `panic!` que para a execução do programa caso um erro irrecuperável ocorra.

#### Erros irrecuperáveis com `panic!`

Há duas maneiras de causar pânico na prática: tomando uma ação que cause pânico no código (como acessar um índice inexistente de um array) ou chamando explicitamente o macro `panic!`.

Vamos visualizar estes casos:

```rust
fn main() {
	panic!("crash and burn");
}
```

A execução deste programa gera a seguinte saída:

```console
$ cargo run
   Compiling panic v0.1.0 (file:///projects/panic)
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.25s
     Running `target/debug/panic`
thread 'main' panicked at src/main.rs:2:5:
crash and burn
note: run with `RUST_BACKTRACE=1` environment variable to display a backtrace
```

E se tentarmos acessar um índice acima do limite de tamanho de um array:

```rust
fn main() {
	let v = vec![1, 2, 3];
	
	v[99];
}
```

Como tentamos acessar um endereço que não foi alocado pelo vetor, ao executarmos o programa, teremos o mesmo comportamento de pânico do exemplo anterior:

```console
$ cargo run
   Compiling panic v0.1.0 (file:///projects/panic)
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.27s
     Running `target/debug/panic`
thread 'main' panicked at src/main.rs:4:6:
index out of bounds: the len is 3 but the index is 99
note: run with `RUST_BACKTRACE=1` environment variable to display a backtrace
```


#### Erros recuperáveis com `Result<T, E>`


O tipo `Result<T, E>` é um enum definido da seguinte maneira:

```rust
enum Result<T, E> {
    Ok(T),
    Err(E),
}
```

`T` e `E` são parâmetros genéricos de tipo, onde `T` representa o tipo de valor que será retornado no caso de sucesso da variante `Ok`, e `E` representa o tipo de erro que será retornado no caso de falha da variante `Err`.

Para identificar se o retorno de determinada função foi um `Ok` ou um `Err`, utiliza-se a estrutura de controle `match`. Vejamos um exemplo para a abertura de um arquivo:

```rust
use std::fs::File;
use std::io::ErrorKind;

fn main() {
    let greeting_file_result = File::open("hello.txt");

    let greeting_file = match greeting_file_result {
        Ok(file) => file,
        Err(error) => match error.kind() {
            ErrorKind::NotFound => match File::create("hello.txt") {
                Ok(fc) => fc,
                Err(e) => panic!("Problem creating the file: {e:?}"),
            },
            other_error => {
                panic!("Problem opening the file: {other_error:?}");
            }
        },
    };
}
```

##### Métodos `unwrap` e `expect`

Usar o `match` para verificar e tratar o erro funciona bem o suficiente, no entanto, pode acabar se tornando um atividade repetitiva e verbosa, dificultando a leitura do código. Para evitar isso, o tipo `Result<T, E>` disponibiliza uma série de métodos auxiliares.

Entre eles, o método `unwrap` serve como atalho para, em caso de sucesso, retornar o valor esperado, e, em caso de erro, chamar o macro `panic!`:

```rust
use std::fs::File;

fn main() {
	let greeting_file = File::open("hello.txt").unwrap();
}
```

Executando este código, em caso de erro, teremos a seguinte saída:

```console
thread 'main' panicked at src/main.rs:4:49:
called `Result::unwrap()` on an `Err` value: Os { code: 2, kind: NotFound, message: "No such file or directory" }
```

Similarmente, o método `expect` apresenta o mesmo comportamento, mas nos permite definir a mensagem de erro do `panic!`, o que facilita a compreensão do que causou o comportamento fatal.

```rust
use std::fs::File;

fn main() {
    let greeting_file = File::open("hello.txt")
        .expect("hello.txt should be included in this project");
}
```

Saída:

```console
thread 'main' panicked at src/main.rs:5:10:
hello.txt should be included in this project: Os { code: 2, kind: NotFound, message: "No such file or directory" }
```

