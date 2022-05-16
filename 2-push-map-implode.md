# Example 2: push + map + implode

**Task**: array of Twitter usernames comes from the Artisan command option. We need to add some hardcoded items to that array, filter out the '@' symbol, and display all usernames as comma-separated string.

**Code snippet:**

```php
class TwitterGiveawayCommand extends Command
{
    protected $signature = 'twitter:giveaway {--exclude=*}';

    public function handle()
    {
        $excluded = collect($this->option('exclude'))
            ->push('povilaskorop', '@dailylaravel')
            ->map(fn (string $name): string => str_replace('@', '', $name))
            ->implode(', ');

        $this->info(sprintf('Users excluded: %s', $excluded));

        return 0;
    }
}
```

How to call this Artisan command:

```bash
php artisan twitter:giveaway --exclude=someuser --exclude-@otheruser
```

Expected result:

```bash
Users excluded: someuser, otheruser, povilaskorop, dailylaravel
```

- - - - - 

## Steps explained

**Step 0. Initial value.**

```php
collect($this->option('exclude'));

// The value:
array:2 [
  0 => "someuser"
  1 => "@otheruser"
]
```

- - - - - 

**Step 1. push()**

```php
collect($this->option('exclude'))
    ->push('povilaskorop', '@dailylaravel')
    // ...
```

Result value:

```
array:4 [
  0 => "someuser"
  1 => "@otheruser"
  2 => "povilaskorop"
  3 => "@dailylaravel"
]
```

- - - - - 

**Step 2. map()**

```php
collect($this->option('exclude'))
    ->push('povilaskorop', '@dailylaravel')
    ->map(fn (string $name): string => str_replace('@', '', $name))
    // ...
```

Result value:

```
array:4 [
  0 => "someuser"
  1 => "otheruser"
  2 => "povilaskorop"
  3 => "dailylaravel"
]
```

- - - - - 

**Step 3. implode()**

```php
collect($this->option('exclude'))
    ->push('povilaskorop', '@dailylaravel')
    ->map(fn (string $name): string => str_replace('@', '', $name))
    ->implode(', ');
```

Result value:

```
'someuser, otheruser, povilaskorop, dailylaravel'
```

- - - - -

[Back to All Examples](readme.md)

[Previous Example: map + implode](1-map-implode.md)