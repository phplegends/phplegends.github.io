---
date: 2019-03-09 20:44:21 +0000

---
# Code Golf - Criar um diretório caso não exista e outras operações com arquivos

## introdução
No PHP, uma vez ou outra, principalmente quando precisamos fazer um upload, sempre precisamos criar uma pasta condicionalmente, caso a mesma não exista. 

Geralmente, fazemos um `if` para saber se o diretório já existe e, em seguida, executamos a função `mkdir`.

Assim:

```php

$directory = '/var/www/public/img';

if (! is_dir($directory)) {
    mkdir($directory);
}

```

## o truque
Eu, particularmente, não gosto de usar `if` para casos assim. Isso porque tanto no PHP quanto no Javascript, é possível executar funções condicionalmente, sem precisar de `if`.

Veja:

```php

$directory = '/var/www/site/public/img';

is_dir($directory) || mkdir($directory);
```


O código acima faz o seguinte processamento *se `is_directory($directory)` for `true`, não faça nada. Se for `false`, execute `mkdir($directory)`.

Isso acontece porque o PHP vai avaliando cada expressão, começando da esquerda para direita. O operador `||` vai executar cada expressão enquanto nenhuma delas for avaliada como verdadeira!

Há um truque para fazer isso com o operador `&&`, porém, se fôssemos aplicar ao caso da verificação se o diretório existe para então criá-lo, seria necessário mudar a expressão, colocando uma negação no início.

```php
!is_dir($directory) && mkdir($directory)
```

# exemplos mais avançados

Há muitos casos que já vi em códigos PHP onde o programador se preocupou em separar nome do arquivo e nome do diretório separadamente, justamente para criar o diretório caso não exista.

Houve casos onde eu tinha o nome do arquivo de destino para um upload "montado" e não havia separação entre "diretório" e "nome do arquivo".

Nesses casos, se for necessário saber se a pasta existe antes de mover o arquivo para aquele destino, basta apenas usar uma função do php que extrai o nome da pasta baseada no caminho completo do arquivo: `dirname`.

Assim:

```php

$directory =  dirname($midia->file_path);

is_dir($directory) || mkdir($directory, 0775, true);

move_uploaded_file($_FILES['file'], $midia->file_path);

```

Com o código acima, não há necessidade de separar concatenar os valores para depois montar o nome do arquivo.
