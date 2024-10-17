> **Linguagens e Paradigmas de Programação - Prof. Cassio Leonardo**
> 
> **Nome**: Gustavo Neves Piedade Louzada
> 
> **Matrícula**: 202107016
> 
> **Linguagem escolhida**: Rust 🦀

---

#variáveis #tipos 

**Tipos primitivos:**

 - **Escalares:** abrigam um único valor
	 - Numéricos: Inteiros e ponto-flutuantes
	 - Não-numéricos: booleanos e caracteres
 - **Compostos:** abrigam múltiplos valores em uma única variávels
	 - Arrays e tuplas


**Inteiros**

Os inteiros podem ser dos tipos `signed` e `unsigned` e seus tamanhos são definidos em seus nomes:

- `i8`: inteiro signed de 8 bits;
- `u8`: inteiro unsigned de 8 bits;
- `i16`: inteiro signed de 16 bits;
- `u16`: inteiro unsigned de 16 bits;
- `i32`: inteiro signed de 32 bits;
- `u32`: inteiro unsigned de 32 bits;
- `i64`: inteiro signed de 64 bits;
- `u64`: inteiro unsigned de 64 bits.


**Flutuantes**

Seguem um padrão parecido com os inteiros, podendo ser `f32`, para 32 bits, e `f64` para 64 bits.


**Caracteres e strings**

Caracteres devem ser definidos utilizando-se aspas simples, enquanto strings devem estar entre aspas duplas:

```rust
fn main(){
	let char_1 = 'a'; // definição implícita
	let str_1:&str = "Rust"; // definição explícita
}
```

Entretanto, existem dois tipos de strings em Rust: `&str` e `String`.

`&str` é um tipo primitivo, imutável, com tamanho fixo e armazenada em algum lugar da memória, e seu valor é conhecido em tempo de compilação.

Já `String` é um objeto com as seguintes propriedades:

- Codificada em UTF-8;
- Estrutura de dados armazenada no Heap da memória;
- Tamanho modificável;
- Não terminada em *null*;
- Aceita valores determinados em tempo de execução.

```rust
fn main(){
  // create a String literal
  let course2 = "Rust Programming";
  // convert String literal to string object using .to_string
  let s_course2 = course2.to_string();
  // print the String object
  println!("This is a string literal : {}.", s_course2);
  // print the length of a String object
  println!("This is a length of my string literal {}.", s_course2.len());

  // define a String object using from method
  let course3 = String::from("Rust Language");
  // print the String object
  println!("This is a string object : {}.", course3);
  // print the length of an string object
  println!("This is the length of my string object {}.", course3.len());
}
```


**Arrays**

A inicialização de arrays deve seguir o seguinte padrão:

![[Pasted image 20240923221850.png]]

Por convenção, todo array possui um tamanho fixo.

Exemplo:

```rust
fn main() {
   // definição e inicialização de um array com 4 itens 
   let arr:[i32;4] = [1, 2, 3, 4];
   // inicialização de um array de 4 itens com o valor 0
   let arr1 = [0 ; 4];
   // acesso a elemento 
   println!("The first value of array is {}", arr[0]);
}

```





