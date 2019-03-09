---
date: 2019-03-09 20:44:21 +0000

---
# Criar um diretório caso não exista com apenas uma linha de código!


```php
<?php

$directory = '/var/www/site/public/img';

is_dir($directory) || mkdir($directory)

```