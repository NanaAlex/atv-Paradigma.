# Capítulo 8 – Atividades para Casa (Resolvido)

## Índice
- [Atividade 1 – Reescrevendo código sem `goto`](#atividade-1--reescrevendo-código-sem-goto)
- [Atividade 2 – Seleção múltipla em diferentes linguagens](#atividade-2--seleção-múltipla-em-diferentes-linguagens)
- [Atividade 3 – Explorando alternativas ao `goto`](#atividade-3--explorando-alternativas-ao-goto)

---

## Atividade 1 – Reescrevendo código sem `goto`

### Pseudocódigo original:
```text
i := 1
goto check

loop:
    print(i)
    i := i + 1

check:
    if (i <= 10) then
        goto loop
```

### Versão em Python usando `while`
```python
i = 1
while i <= 10:
    print(i)
    i += 1
```

### Versão em C usando `for`
```c
#include <stdio.h>

int main() {
    for (int i = 1; i <= 10; i++) {
        printf("%d\n", i);
    }
    return 0;
}
```

**Discussão:**  
- O código com `goto` é funcional, mas pouco legível e sujeito a erros.  
- As versões com `while` e `for` são mais claras, concisas e refletem melhor a intenção do programador.  
- Entre elas, o `for` é o mais adequado, já que o número de repetições é conhecido.

---

## Atividade 2 – Seleção múltipla em diferentes linguagens

### Versão em C usando `switch/case`
```c
#include <stdio.h>

int main() {
    int opcao, num;
    do {
        printf("Menu:\n");
        printf("1. Quadrado de um número\n");
        printf("2. Fatorial de um número\n");
        printf("3. Sair\n");
        printf("Escolha uma opção: ");
        scanf("%d", &opcao);

        switch(opcao) {
            case 1:
                printf("Digite um número: ");
                scanf("%d", &num);
                printf("Quadrado: %d\n", num * num);
                break;
            case 2:
                printf("Digite um número: ");
                scanf("%d", &num);
                int fat = 1;
                for(int i = 1; i <= num; i++) {
                    fat *= i;
                }
                printf("Fatorial: %d\n", fat);
                break;
            case 3:
                printf("Saindo...\n");
                break;
            default:
                printf("Opção inválida!\n");
        }
    } while(opcao != 3);

    return 0;
}
```

---

### Versão em Python usando `if/elif/else`
```python
def fatorial(n):
    fat = 1
    for i in range(1, n + 1):
        fat *= i
    return fat

while True:
    print("Menu:")
    print("1. Quadrado de um número")
    print("2. Fatorial de um número")
    print("3. Sair")
    opcao = int(input("Escolha uma opção: "))

    if opcao == 1:
        num = int(input("Digite um número: "))
        print("Quadrado:", num ** 2)
    elif opcao == 2:
        num = int(input("Digite um número: "))
        print("Fatorial:", fatorial(num))
    elif opcao == 3:
        print("Saindo...")
        break
    else:
        print("Opção inválida!")
```

**Comentário final:**  
- Em **C**, o `switch/case` deixa o menu estruturado, mas precisa de mais código (entrada, variáveis, laço manual).  
- Em **Python**, a implementação é mais enxuta e simples devido à sintaxe.  
- A clareza foi maior em Python.

---

## Atividade 3 – Explorando alternativas ao `goto`

### Versão em Python com `break`, `continue` e `return`
```python
def processar(lista):
    for num in lista:
        if num == 0:
            break
        if num < 0:
            continue
        if num % 2 == 0:
            return num * 2
    return None

print(processar([1, -3, 5, 8, 7]))  # retorna 16
print(processar([1, 3, 5, 0, 8]))   # para no 0, retorna None
```

---

### Versão em C com `break`, `continue` e `return`
```c
#include <stdio.h>

int processar(int arr[], int tamanho) {
    for(int i = 0; i < tamanho; i++) {
        if(arr[i] == 0)
            break;
        if(arr[i] < 0)
            continue;
        if(arr[i] % 2 == 0)
            return arr[i] * 2;
    }
    return -1; // nenhum número par encontrado antes do zero
}

int main() {
    int lista1[] = {1, -3, 5, 8, 7};
    int lista2[] = {1, 3, 5, 0, 8};

    printf("%d\n", processar(lista1, 5)); // 16
    printf("%d\n", processar(lista2, 5)); // -1
    return 0;
}
```

---

**Discussão:**  
- Usar `goto` obrigaria criar rótulos e saltos manuais, deixando o código confuso e mais difícil de manter.  
- Com `break`, `continue` e `return`, o código fica mais **legível, modular e seguro**.  
- Essa é a principal razão pela qual linguagens modernas desencorajam ou eliminam o uso de `goto`.  
