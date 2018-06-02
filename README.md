### laravel 通过 migrate 修改数据库字段类型以及添加字段，注意：

```
composer require doctrine/dbal

*用于解决修改数据表字段的属性
```

```
通过 artisan 创建出来的控制器，默认会继承 App\Http\Controllers\Controller，我们只需要删除 use App\Http\Controllers\Controller 这一行即可，这样会继承相同命名空间下的 Controller，也就是我们上一步中添加的那个控制器。
```
