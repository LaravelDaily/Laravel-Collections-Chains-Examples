# Example 3: filter + map + implode

**Task**: you have a User model with links to social network profiles: Twitter, Facebook, Instagram. Some of them may be empty. Your goal is to show non-empty links, separated by | symbol.

**Code snippet:**

```php
$socialLinks = collect([
    'Twitter' => $user->link_twitter,
    'Facebook' => $user->link_facebook,
    'Instagram' => $user->link_instagram,
])
->filter()
->map(fn ($link, $network) => '<a href="' . $link . '">' . $network . '</a>')
->implode(' | ');
```

- - - - - 

## Steps explained

**Step 0. Initial value.**

```php
$profile = collect([
    'Twitter' => 'https://twitter.com/povilaskorop',
    'Facebook' => '',
    'Instagram' => 'https://instagram.com/povilaskorop',
]);

// The value:
array:3 [
  "Twitter" => "https://twitter.com/povilaskorop"
  "Facebook" => ""
  "Instagram" => "https://instagram.com/povilaskorop"
]
```

- - - - - 

**Step 1. filter()**

```php
$profile->filter()
// ...
```

Result value:

```
array:2 [
  "Twitter" => "https://twitter.com/povilaskorop"
  "Instagram" => "https://instagram.com/povilaskorop"
]
```

- - - - - 

**Step 2. map()**

```php
$profile
    ->filter()
    ->map(fn ($link, $network) => '<a href="' . $link . '">' . $network . '</a>')
// ...
```

Result value:

```
array:2 [
  "Twitter" => "<a href="https://twitter.com/povilaskorop">Twitter</a>"
  "Instagram" => "<a href="https://instagram.com/povilaskorop">Instagram</a>"
]
```

- - - - - 

**Step 3. implode()**

```php
$profile
    ->filter()
    ->map(fn ($link, $network) => '<a href="' . $link . '">' . $network . '</a>')
    ->implode(' | ');
```

Result value:

```
'<a href="https://twitter.com/povilaskorop">Twitter</a> | <a href="https://instagram.com/povilaskorop">Instagram</a>'
```

- - - - -

[Back to All Examples](readme.md)

[Previous Example: push + map + implode](2-push-map-implode.md)