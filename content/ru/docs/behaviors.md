---
view::extends: _includes.ru.docs_post_base
view::yields: post_body
pageTitle: - Behaviors
pageDescription: Laravel Behaviors
---
@verbatim
# Поведения 
----------

Поведение является основной частью ORCHID, вместо того, чтобы генерировать CRUD для каждой модели
Вы можете выбрать любой объект в отдельном типе и легко управлять им


Собственное поведение должно быть зарегистрировано в `config/content.php` в разделе типов


```php
//
'pages' => [
    //App\Core\Behaviors\Single\DemoPage::class,
],


//
'types' => [
    //App\Core\Behaviors\Many\DemoPost::class,
],
```


Тип выглядит следующим образом:

```php
namespace DummyNamespace;

use Orchid\Behaviors\Many;

class DummyClass extends Many
{

    /**
     * @var string
     */
    public $name = '';

    /**
     * @var string
     */
    public $slug = '';

    /**
     * @var string
     */
    public $icon = '';

    /**
     * Slug url /news/{name}.
     * @var string
     */
    public $slugFields = '';

    /**
     * Rules Validation.
     * @return array
     */
    public function rules()
    {
        return [];
    }

    /**
     * @return array
     */
    public function fields()
    {
        return [];
    }

    /**
     * Grid View for post type.
     */
    public function grid()
    {
        return [];
    }

    /**
     * @return array
     */
    public function modules()
    {
        return [];
    }
}

```

Вы можете расширить тип данных всеми доступными методами, чтобы добавить к нему новую функциональность, которая соответствует вашему приложению

 
#### Модификация сетки
 

Данные, которые вы хотите отобразить в сетке, можно изменить, передав массив с именем и функцией вместо значения ключа, где переданный параметр является исходным срезом данных.

 ```php
 /**
  * Grid View for post type.
  */
 public function grid()
 {
     return [
         'name'       => 'Name',
         'publish_at' => 'Date of publication',
         'created_at' => 'Date of creation',
         'full_name'  =>  => [
             'name' => 'Full name',
             'action' => function($post){
                 return  $post->getContent('fist_name') 
                  .' '.
                  $post->getContent('last_name');
             }
         ],
     ];
 }

```


Вы можете создать поведения с помощью команд:
```php
//Создат поведения для многих записей
php artisan make:manyBehavior
  
//Создат поведения для одной записи  
php artisan make:singleBehavior      
```
 

 
@endverbatim
