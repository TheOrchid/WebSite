---
view::extends: _includes.ru.docs_post_base
view::yields: post_body
pageTitle: Filters Laravel
---
@verbatim
# Фильтры
----------

Для выборки значений на основе параметров Http запроса можно с помощью комманды создать фильтры:

```php
php artisan make:filter QueryFilter
```

Это создаст класс фильтр в папке `app/Http/Filters`


Пример фильтра:
```php
namespace App\Http\Filters;

use Orchid\Filters\Filter;
use Illuminate\Database\Eloquent\Builder;

class QueryFilter extends Filter
{

    /**
     * @var array
     */
    public $parameters = ['query'];

    /**
     * @var bool
     */
    public $display = true;

    /**
     * @var bool
     */
    public $dashboard = false;

    /**
     * @param Builder $builder
     *
     * @return Builder
     */
    public function run(Builder $builder): Builder
    {
        return $builder->where('demo', $this->request->get('query'));
    }

    /**
     * @return \Illuminate\Contracts\View\Factory|\Illuminate\View\View
     */
    public function display()
    {
        return view('simpleFilter',[]);
    }
}
```

Фильтр сработает, при условии наличии хотя бы одного параметра указанного в массиве `$parameters`, если массив будет пуст, тогда фильтр будет работать при каждом запросе

#### Использование

Для использования фильтра, необходимо указать его в классе поведения
```php
use Orchid\Behaviors\Many;

class MyBehaviorPost extends Many
{

    /**
     * HTTP data filters
     *
     * @var array
     */
    public $filters = [
        QueryFilter::class,
    ];
}
```

Фильтрацию можно запустить методом `filtersApply`:
```php
use Orchid\Core\Models\Post;

Post::type('news')->filtersApply()->simplePaginate(10);
```
 
 
 
 @endverbatim
