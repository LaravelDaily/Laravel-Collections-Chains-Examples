# Example 1: map + implode

**Task**: within many-to-many relationship between `roles` and `permissions` DB tables (`permission_role`), we want to show the permissions of one specific role, already formatted with `<br>`, one permission per line.

**Code snippet:**

```php
$role = Role::with('permissions')->first();
$permissionsListToShow = $role->permissions
    ->map(function ($permission) {
        return $permission->display_name;
    })
    ->implode("<br>");
```

**What is $role->permissions**:

```php
class Role extends Model
{
    public function permissions()
    {
        return $this->belongsToMany(Permission::class);
    }
}
```

## Steps explained

**Step 0. Initial value.**

```php
$role = Role::with('permissions')->first();

// The value of $role:
[
  "id" => 1
  "name" => "Admin"
  "created_at" => "2022-05-14T18:21:10.000000Z"
  "updated_at" => "2022-05-14T18:21:10.000000Z"
  "permissions" => array:2 [▼
    0 => array:4 [▼
      "id" => 1
      "display_name" => "manage users"
      "created_at" => "2022-05-14T18:21:29.000000Z"
      "updated_at" => "2022-05-14T18:21:29.000000Z"
    ]
    1 => array:4 [▼
      "id" => 2
      "display_name" => "manage transactions"
      "created_at" => "2022-05-14T18:21:29.000000Z"
      "updated_at" => "2022-05-14T18:21:29.000000Z"
    ]
  ]
]
```

- - - - - 

**Step 1. map()**

```php
$role->permissions
    ->map(function ($permission) {
        return $permission->display_name;
    })
    ...
```

Result value:

```
Illuminate\Support\Collection {#396 ▼
  #items: array:2 [▼
    0 => "manage users"
    1 => "manage transactions"
  ]
}
```

- - - - - 

**Step 2. implode()**

```php
$role->permissions
    ->map(function ($permission) {
        return $permission->display_name;
    })
    ->implode("<br>");
```

Result value:

```
'manage users<br>manage transactions'
```

- - - - -

[Back to All Examples](readme.md)

[Next Example: push + map + implode](2-push-map-implode.md)