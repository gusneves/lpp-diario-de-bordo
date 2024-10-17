> **Linguagens e Paradigmas de Programação - Prof. Cassio Leonardo**
> 
> **Nome**: Gustavo Neves Piedade Louzada
> **Matrícula**: 202107016
> **Linguagem escolhida**: Rust 🦀

---

#categorias #métodos-de-implementação


Rust é uma **linguagem imperativa** de propósito geral com ênfase em performance, *type safety* e, principalmente, *memory safety*. Além disso, Rust é uma linguagem compilada e possui um compilador consideravelmente rigoroso, que convence (e, muitas vezes, obriga) o desenvolvedor a lidar com potenciais problemas de memória e tipagem.

Mesmo não usando um *garbage collector*, a segurança de memória do Rust é atingida através de seus mecanismos de "propriedade" (***ownership***) que assegura que cada recurso possua apenas um proprietário, o que evita que estes sejam liberados da memória mais de uma vez, e "empréstimo" (***borrowing***), que permite o acesso a um recurso sem assumir a responsabilidade sobre ele. Através de uma "checagem de empréstimo" (***borrow checking***), o compilador estaticamente garante que referências *sempre* apontem para objetos válidos. Isto é, enquanto uma referência para um objeto existir, ele não pode ser destruído.

Com os conceitos listados acima, Rust também consegue lidar com problemas  de condição de corridas entre *threads*, já que não é possível duas *threads* possuírem propriedade simultânea sobre um recurso. Ou seja, é possível a concorrência, mas sem disputa de dados.
