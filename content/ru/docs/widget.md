---
view::extends: _includes.ru.docs_post_base
view::yields: post_body
pageTitle: Widget
pageDescription: Laravel Widget
---
@verbatim
# Виджет
----------

Виджет (widget) — это экземпляр класса Widget или унаследованного от него. Это компонент, применяемый, в основном, с целью оформления. Виджеты обычно встраиваются в представления для формирования некоторой сложной, но в то же время самостоятельной части пользовательского интерфейса.


К примеру, виджет календаря может быть использован для рендеринга сложного интерфейса календаря. Виджеты позволяют повторно использовать код пользовательского интерфейса.

### Создание:
	
Чтобы создать новый виджет, необходимо выполнить
```php
php artisan make:widget MySuperWidget
```

В папке `app/Http/Widgets` создаться класс шаблон виджета Как и у контроллера, у виджета может быть собственное представление. 
Рекомендуется распологать файлы виджета в поддиректории views.

```php
namespace App\Http\Widgets;

use Orchid\Dashboard\Services\Widget\Widget;

class MySuperWidget extends Widget {

    /**
     * Class constructor.
     */
    public function __construct(){

    }

    /**
     * @return mixed
     */
     public function run(){
         return view('',[
         ]);
     }

}
```


Для регистрации Вашего нового виджета необходимо занести его в `config/widget.php`

```php
'widgets' => [
    'NameForMySuperWidget' => App\Widgets\MySuperWidget::class
 ],
```
	


### Использование :


При вызове виджета поумолчанию исполняется метод `"run"`.
Для подключения виджета необходимо выполнить в коде используя синтаксис Blade:
```php
@widget('NameForMySuperWidget')
```


@endverbatim
