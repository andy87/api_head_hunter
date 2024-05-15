# api Head Hunter

## IN PROGRESS

PHP Фасад для API Head Hunter (www.hh.ru)

#### Реализация
 - API: реализация запросов к api сервису `Head Hunter`
 - Servcie: Фасад для класса API

### Использование Api
Методы Api возвращают массив с данными.
```php
use and_y87\api_head_hunter\ApiHeadHunter;
use and_y87\api_head_hunter\dto\HeadHunterApiRequisites;
use and_y87\api_head_hunter\cache\CacheProvider;

// Add `CacheProvider`
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

// Create object `CacheProvider`
$redisCacheProvider = new RedisCacheProvider();

// Create object `Requisites`
$headHunterApiRequisites = new HeadHunterApiRequisites( $appName, $contactEmail, $client_id, $client_secret );

// Create object `Api`
$apiHeadHunter = ApiHeadHunter( $headHunterApiRequisites, $redisCacheProvider );

// Use `Api`
$me = $apiHeadHunter->me(); // return array
```
### Использование Service
Методы Service возвращают Объекты с данными.
```php
use and_y87\api_head_hunter\service\AvitoService;

//Вводная часть при использовании сервиса аналогична Api

// Create object `Service`
$headHunterService = new HeadHunterService($apiHeadHunter);

// Use `Service`
$me = $headHunterService->me(); // return and_y87\api_head_hunter\response\Me();
```

#### Схема работы API
![Схема работы API](https://static.andy87.ru/github/api/apiLogivSchema.png)

### Исходная документация API `Head Hunter`:
 - https://github.com/hhru/api
 - https://api.hh.ru/openapi/redoc
