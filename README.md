# Laravel Repo Creator
Laravel Model and Repo creator for laravel framework

This library is ment to help create Repositories and Model classes when working on laravel repository pattern and assumes that you have experience with *Laravel Repository Pattern*.

# Pre-requirement

## Models
You must have a Models folder under /app. All the database models are created under this folder.

## Repositories
You must have the following folder structure under laravel /app folder.
```
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

## create model class from database tables

$ php model [table_name] [path_to_the_model] [class_name]

The path_to_the_model should have front slashes and follow from Models folder.

```bash
$ php model tbl_users Auth Users

Created File : app/Models/Auth/Users.php
```

## create repository classes

The repository classes include the create and update request classes and the model repository classes.

$ php repo [module_path/] [module_name] [optional:model_class_name]

module_path -> should have front slashes and follow from Modules folder.

module_name -> the class name prefix that you require

model_class_name(optional) -> if the repository should be associated with a model class then the name of the model class

```bash
$ php repo Auth User Users

Creating directory app/Modules/Auth/User
Creating directory app/Modules/Auth/User/Requests
Created File : app/Modules/Auth/User/Requests/CreateUserRequest.php
Created File : app/Modules/Auth/User/Requests/UpdateUserRequest.php
Creating directory app/Modules/Auth/User/Repositories
Created File : app/Modules/Auth/User/Repositories/UserRepository.php
Created File : app/Modules/Auth/User/Repositories/UserRepositoryImplementation.php
Created Module : Auth/User
```
This will also add specific lines in app/Providers/DependencyInjectionServiceProvider.php to inject the repositories into the controllers.
