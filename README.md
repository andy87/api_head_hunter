# providerHeadHunter

PHP Фасад для API Head Hunter (www.hh.ru)

---

> [!NOTE]
> ![IN PROGRESS](http://www.bc-energy.it/wp-content/uploads/2013/08/work-in-progress.png)

---

#### Реализация
 - API: реализация запросов к api сервису `Head Hunter`
 - Servcie: Фасад для класса API

### Использование Api
Методы Api возвращают массив с данными.
```php
use and_y87\api_head_hunter\ApiHeadHunter;
use and_y87\api_head_hunter\dto\HeadHunterApiRequisites;
use and_y87\api_head_hunter\cache\CacheProvider;

// Создание класса `CacheProvider`
class RedisCacheProvider extends CacheProvider
{
    public function getValue( string $key ): string
    {
        return (string) Yii::$app->redis->get( $key );
    }

    public function setValue( string $key, mixed $value ): bool
    {
        return Yii::$app->redis->set( $key, $value );
    }
}

// Создание экземпляра класса `CacheProvider`
$redisCacheProvider = new RedisCacheProvider();

// Создание экземпляра класса `Requisites`
$headHunterApiRequisites = new HeadHunterApiRequisites( $appName, $contactEmail, $client_id, $client_secret );

// Создание экземпляра класса `Api`
$apiHeadHunter = ApiHeadHunter( $headHunterApiRequisites, $redisCacheProvider );

// Использование `Api`
$me = $apiHeadHunter->me(); // return array

echo $me['name']; // получение значения массива по ключу (hardcode)
```
### Использование Service
Методы Service возвращают объекты(экзмпляры классов) содержащие актуальные для endpoint свойства, согласно документации сервиса.
```php
use and_y87\api_head_hunter\service\AvitoService;

//Вводная часть при использовании сервиса аналогична Api

// Создание экземпляра класса `Service`
$headHunterService = new HeadHunterService($apiHeadHunter);

// Использование `Service`
$me = $headHunterService->myInfo(); // return and_y87\api_head_hunter\response\Me();

echo $me->name; // Получение значение из объекта через обращение к свойству
```

#### Схема работы API
![Схема работы API](https://static.andy87.ru/github/api/apiLogivSchema.png?v=3)

### Исходная документация API `Head Hunter`:
 - https://github.com/hhru/api
 - https://api.hh.ru/openapi/redoc
