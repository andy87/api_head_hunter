# api Head Hunter

PHP Фасад для API Head Hunter (www.hh.ru)

#### Схема работы API
https://miro.com/app/board/uXjVKHFfUB0=/

#### Реализация
 - API: реализация запросов к api сервису `Head Hunter`
 - Servcie: Фасад для класса API

### Использование Api
```php
use and_y87/api_head_hunter/ApiHeadHunter;
use and_y87/api_head_hunter/dto/HeadHunterApiRequisites;
use and_y87/api_head_hunter/tools/CacheProvider;

// Add `CacheProvider`
class RedisCacheProvider extends CacheProvider
{
    public function getValue(string $key )
    {
        Yii::$app->redis->get( $key );
    }

    public function setValue( string $key, string $value )
    {
        Yii::$app->redis->set( $key, value );
    }
}

// Create object `CacheProvider`
$redisCacheProvider = new RedisCacheProvider();

// Create object `Requisites`
$headHunterApiRequisites = new HeadHunterApiRequisites( $appName, $contactEmail, $client_id, $client_secret );

// Create object `Api`
$apiHeadHunter = ApiHeadHunter( $headHunterApiRequisites, $redisCacheProvider );

// Use `Api`
```

### Исходная документация API `Head Hunter`:
 - https://github.com/hhru/api
 - https://api.hh.ru/openapi/redoc
