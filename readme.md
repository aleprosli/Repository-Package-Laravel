# Repository Package

Automatic generate repo pattern with single command

## Installation
```
composer require aleprosli/repository-pattern
```

## Configuration
Publish the configuration file

```
php artisan vendor:publish --provider="Aleprosli\RepositoryPattern\RepositoryServiceProvider"
```

## Usage

The command

```
php artisan make:repo Model
```
## Example

```
php artisan make:repo User
```

### Go To 
```Providers/RepositoryServiceProvider.php```
 and bind interface and class you just created

```php
<?php

namespace App\Repositories;

use Illuminate\Support\ServiceProvider;

class RepositoryServiceProvider extends ServiceProvider
{

    public function register()
    {
        $this->app->bind('App\Repositories\UserRepositoryInterface','App\Repositories\UserRepository');
    }
}

```
##### And now go to your ```app/Http/Controllers/Usercontroller```

```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;
use App\Repositories\UserRepositoryInterface;

class UserController extends Controller
{
    protected $user;

    public function __construct(UserRepositoryInterface $user)
    {
        $this->user = $user;
    }

    /**
     * Display a listing of the resource.
     *
     * @return \Illuminate\Http\Response
     */
    public function index()
    {
        return $this->user->all();
    }
}
```
