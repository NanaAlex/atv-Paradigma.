# Capítulo 9 – Exercícios: Subprogramas (Resolvido)

## Índice
- [Exercício 1 – Passagem de Parâmetros por Valor e por Referência](#exercício-1--passagem-de-parâmetros-por-valor-e-por-referência)
- [Exercício 2 – Corrotinas em GoLang](#exercício-2--corrotinas-em-golang)

---

## Exercício 1 – Passagem de Parâmetros por Valor e por Referência

### Pseudocódigo
```text
procedure dobrar(x)
    x := x * 2
end
```

---

### Implementação em C (por valor)
```c
#include <stdio.h>

void dobrarValor(int x) {
    x = x * 2;
    printf("Dentro da função (valor): %d\n", x);
}

int main() {
    int num = 10;
    printf("Antes da função: %d\n", num);
    dobrarValor(num);
    printf("Depois da função: %d\n", num);
    return 0;
}
```

**Saída esperada:**
```
Antes da função: 10
Dentro da função (valor): 20
Depois da função: 10
```

---

### Implementação em C (por referência)
```c
#include <stdio.h>

void dobrarReferencia(int *x) {
    *x = *x * 2;
    printf("Dentro da função (referência): %d\n", *x);
}

int main() {
    int num = 10;
    printf("Antes da função: %d\n", num);
    dobrarReferencia(&num);
    printf("Depois da função: %d\n", num);
    return 0;
}
```

**Saída esperada:**
```
Antes da função: 10
Dentro da função (referência): 20
Depois da função: 20
```

---

### Discussão
- **Por valor**: a variável é copiada, logo mudanças afetam apenas a cópia local.  
- **Por referência**: a função acessa o endereço original da variável, alterando seu valor diretamente.  
- Isso mostra a diferença entre **estratégias de passagem de parâmetros**: cópia x referência.  
- Em linguagens de alto nível, esse comportamento influencia a performance e a forma de manipular dados complexos.

---

## Exercício 2 – Corrotinas em GoLang

### Código Go
```go
package main

import (
    "fmt"
    "time"
)

func escrever(texto string) {
    for i := 0; i < 5; i++ {
        fmt.Println(texto, i)
        time.Sleep(time.Millisecond * 500)
    }
}

func main() {
    go escrever("Corrotina")  // executa em paralelo
    escrever("Função normal") // executa no fluxo principal
}
```

---

### Execução
```bash
go run main.go
```

### Saída típica (pode variar):
```
Função normal 0
Corrotina 0
Função normal 1
Corrotina 1
Função normal 2
Corrotina 2
Função normal 3
Corrotina 3
Função normal 4
Corrotina 4
```

---

### Discussão
- A ordem das mensagens **não é fixa**: como há concorrência, os outputs se intercalam.  
- A função `escrever("Corrotina")` roda em paralelo graças à palavra-chave **`go`**, enquanto a outra roda no fluxo principal.  
- Isso ilustra o conceito de **corrotinas**: subprogramas que podem suspender e retomar sua execução de forma cooperativa ou concorrente.  
- No Go, isso é implementado de forma leve e eficiente com **goroutines**, permitindo programação concorrente de maneira simples.  
