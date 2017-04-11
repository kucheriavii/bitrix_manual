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
- прикрутимо стилі
Було:
  ```
  <link rel="stylesheet" type="text/css" href="css/common-styles.css" />
  ```
Стало:
  ```
  <?$APPLICATION->SetAdditionalCSS(SITE_TEMPLATE_PATH."/css/common-styles.css")?>
  ```
- В випадку, якщо ми інтегруємо стилі в умовні кментарі IE, то юхзаэмо таку фішку:
  ```
  <?=CUtil::GetAdditionalFileURL(SITE_TEMPLATE_PATH)?>/js/...
  ```  
- добавимо панель Бітрикса
  ```
  <?$APPLICATION->ShowPanel();?>
  ```
- добавимо в хеді тайтл
```
  <title><?$APPLICATION->ShowTitle(false);?></title>
```
- приліпимо скріпти. Зразок:
```
 $APPLICATION->AddHeadScript(SITE_TEMPLATE_PATH.'/js/vendor/jquery.min.js');
 ```

- Визначимо головна чи не головна в нас сторінка
```
$bIsMainPage = $APPLICATION->GetCurPage(false) == SITE_DIR;
```
Це потрібно щоб включати чи виключати певний контент на сторінці, ось приклад:
```
<?if($bIsMainPage):?>\\якщо сторінка головна то:
  <ol class="breadcrumb">
      <li><a href="#">Главная</a></li>
      <li><a href="#">Раздел</a></li>
      <li class="active">Детальная страница</li>
  </ol>
<?else: ?>\\якщо сторінка не головна то:
  <p>"404" - тут нікуя немає</p>
<?endif;?> \\ кінець умови
```
