# Laravel Repo Creator
Laravel Model and Repo creator for laravel framework

This library is ment to help create Repositories and Model classes when working on laravel repository pattern.

# Pre-requirement

## Models
You must have a Models folder under /app. All the database models are created under this folder.

## Repositories
You must have the following folder structure under laravel /app folder.
```php
->app
|    -> Modules
|        ->Framework
|            -> Request.php (extends use Illuminate\Foundation\Http\FormRequest)
|            -> RepositoryImplementation.php (abstract class)
|            -> Repository.php (interface) 
```

### Request.php

```php
namespace App\Modules\Framework;

use Illuminate\Foundation\Http\FormRequest;

class Request extends FormRequest
{
    /**
     * Determine if the user is authorized to make this request.
     *
     * @return bool
     */
    public function authorize()
    {
        return true;
    }

    /**
     * Get the validation rules that apply to the request.
     *
     * @return array
     */
    public function rules()
    {
        return [
            //
        ];
    }
}
```
### Repository.php
```php
namespace App\Modules\Framework;

interface Repository
{
    /**
     * Gets model for operation.
     *
     * @return mixed
     */
    public function getModel();
    
}    
```

### RepositoryImplementation.php

```php
abstract class RepositoryImplementation
{

    /**
     * Gets model for operation.
     *
     * @return mixed
     */
    public abstract function getModel();
    
}
```
# Useage
Simple instructions to see this repo in action.

## create models from database tables
```bash
$ php model tbl_users Auth Users

Created File : app/Models/Auth/Users.php
```
