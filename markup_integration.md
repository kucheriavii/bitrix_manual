## 2. Інтегрування вєрстки
- створимо папки "local/templates" в корні домена
- скопіюємо з папки "bitrix/templates/empty" в папку "local/templates/empty"
- повидаляємо файли стилей
- скопіюємо файли нашого шаблону в папку "local/templates/empty"
- перенесемо в файли header.php і footer.php контен для хедера і фуера
- видалимо теги, що відповідають за кодування і метатеги, а замість них вставимо  <?$APPLICATION->ShowHead();?>
- шлях до .css, .js файлів зберігається в змінній, тому рядки типу:
  ```
  <link rel="icon" href="ico/favicon_bx.png">
  ```
  стануть такими
  ```
  <link rel="icon" href="<?=SITE_TEMPLATE_PATH?>/ico/favicon_bx.png">
  ``` 
