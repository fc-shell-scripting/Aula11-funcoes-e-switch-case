- [Funções](#funções)
    - [Funções com parâmetros](#funções-com-parâmetros)
- [Switch case](#switch-case)
- [Exercícios](#exercícios)

# Funções

---


Para exemplificar o uso de funções, considere o seguinte problema:

> Você precisa desenvolver um programa para uma loja de eletrônicos que mostre na tela todos os monitores disponíveis na loja, seguido de um relatório de todos os mouses existentes, etc..

Você pode repetir todo o layout múltiplas vezes, e isso pode funcionar para poucos itens. Mas e se novos relatórios forem adicionados? E se precisarmos fazer alterações no layout dos dados? Para esses casos usamos funções.

Funções são trechos de código que são declarados no fonte, e podem ser chamados em qualquer lugar dentro do script. As funcções precisam ser declaradas antes de serem utilizadas, e por este motivo é uma boa prática deixarmos todas as funções juntas antes da rotina do script.

A sintaxe de uma função é bem simples:

```shell
#!/bin/bash

# Declarando a função:
_olaMundo(){
    echo "ola mundo"
}
```

A declaração da função acima, mostra que quando chamarmos a função *_olaMundo*, será executado o comando echo "ola mundo".

Mas atenção: Se você colocar o código acima em um script e fazer a execução do script, nada será mostrado na tela. Isso porque nós apenas declaramos a função, mas não a executamos. Para executar, precisamos adicionar a linha da chamada da função:

```shell
#!/bin/bash

# Declarando a função:
_olaMundo(){
    echo "ola mundo"
}

# Chamada da função
_olaMundo
```

O código acima irá mostrar na tela a frase "minha funcao", que foi colocada dentro da função.

Para declarar uma funcação, geralmente usamos um _underscore_ no ínicio, para não confundir com a declaração de variáveis,seguido do nome da função e de um par de parênteses, e uma abertura de chaves. Esta abertura de chaves indica o início do conteúdo da função (ou, escopo da função). 

Dentro da função, você pode colocar todos os comandos que serão executados e, no final você deve colocar o fechamento da chave para indicar que o escopo terminou.

## Funções com parâmetros

Muitas vezes vamos precisar passar parâmetros para que as funções possam ser executadas. Para passar um parâmetro para a função, nõs colocamos o parâmetro ao lado da chamada da função.

```shell
#!/bin/bash

# Declarando a função:
_olaMundo(){
    echo "ola mundo"
}

# Chamada da função
_olaMundo "fernando"
```

O comando acima ainda irá mostrar "_ola mundo_" como resposta. Isso acontece porque não específicamos na função o que fazer com o parâmetro passado. Para testar, vamos alterar a função para escrever "ola ", seguido do nome passado como parâmetro:

```shell
#!/bin/bash

# Declarando a função:
_olaMundo(){
    echo "ola $1"
}

# Chamada da função
_olaMundo "fernando"
```

Veja que ao usarmos _$1_, o comando irá mostrar _olá fernando_. Mas vamos entender com calma o que está acontecendo:
Quando chamamos um programa passando os arqumentos (_bash programa "argumento1"), o interpretador entende a variável _$1_ como o primeiro argumento. Entretanto, quando o script chama uma função passando um parâmetro (_minhaFuncao "parametro"), o interpretador cria uma nova área de armazenamento de variáveis, onde será aramazenado o valor de "parametro" como _$1_. Você precisa ter cuidado para não tentar acessar o dado da variável errada.

Considere o seguinte script:

```shell
#!/bin/bash

_funcaoTeste(){
    echo $1
}

echo $1
_funcaoTeste "abc"
_funcaoTeste "def"
```

Em seguida vamos chamar este programa por linha de comando para ver o que será mostrado:

```shell
$> bash ./teste.sh "123"
123
abc
def
$>
```

Ou seja, o valor de _$1_ dentro da função é válido apenas para aquela instância da função, sem ter acesso às variáveis de passagem de parâmetros:

|                  |$1 (script)     | $1  (abc)      | $1 (def)       |
|------------------|:--------------:|:--------------:|:--------------:|
|bash ./teste.sh   | "123"          | não disponível | não disponível |
|_funcaoteste "abc"| não disponível | "abc"          | não disponível |
|_funcaoteste "def"| não disponível | não disponível | "def"          |

Por este motivo, é sempre uma boa prática colocar as variáveis recebidas em uma variável nova, com um nome mais significativo.

# Switch case

---

Em aulas passadas, vimos o comando o laço _select_ que monta uma lista para que o usuário possa escolher uma opção. Se fizermos um bloco de _if_ para cada opção, vamos manter um código extenso e demora, porque cada opção será validada, mesmo que apenas uma seja verdadeira. Com o _switch case_, o interpretador carrega as opçõe sna memória e consegue executar o bloco de código correto, sem precisar ir _if_ a _if_:

```shell
#!/bin/bash

echo "digite uma letra:"
read letra

case $letra in
    "a")
        echo "você digitou a"
        ;;
    "b")
        echo "você digitou b"
        ;;
    "c")
        echo "você digitou c"
        ;;
    *)
        echo "Você digitou uma letra que não está no switch case"
        ;;
esac
```

A sintaxe fica mais clara que uma série de _ifs_. Além disso, você ainda tem o _*)_ que permite uma resposta default para qualquer caso que não esteja dentro do case.

# Exercícios

1. Monte um programa que leia dois números e uma operação (+ - / * ), e retorne o resultado no seguinte formato:

Utilize Funções e switch case para resolver o problema

```shell
+------------------------------+
|         3 + 2 = 5            |
+------------------------------+
```