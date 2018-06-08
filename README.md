### laravel 通过 migrate 修改数据库字段类型以及添加字段，注意：

```
composer require doctrine/dbal

*用于解决修改数据表字段的属性
```

```
通过 artisan 创建出来的控制器，默认会继承 App\Http\Controllers\Controller，
我们只需要删除 use App\Http\Controllers\Controller 这一行即可，这样会继承相同命名空间下的 Controller，
也就是我们上一步中添加的那个控制器。
```

### Dingo 添加自定义返回格式

`$ mkdir App\Serializer`
`$ touch CustomSerializer.php`

```
CustomSerializer.php

<?php
/**
 * Created by PhpStorm.
 * User: zs
 * Date: 18/6/6
 * Time: 16:38
 */

namespace App\Serializer;

use League\Fractal\Serializer\ArraySerializer;


class CustomSerializer extends ArraySerializer
{
    /**
     * 重新封装Dingo API返回的data，加入code和msg
     *
     * @param string $resourceKey
     * @param array $data
     * @return array
     */
    public function collection($resourceKey, array $data)
    {
        return [
            'msg' => '操作成功',
            'code' => 200,
            'data' => $data
        ];
    }

    public function item($resourceKey, array $data)
    {
        return [
            'msg' => '操作成功',
            'code' => 200,
            'data' => $data
        ];
    }
}

```

使用示例
```
return $this->response->collection($re, new IntentTransformer(), function($resource, $fractal){
            $fractal->setSerializer(new \App\Serializer\CustomSerializer());
        });
        
注意 collection 和 item 的使用，错误会导致 json key 的错误。        
```

