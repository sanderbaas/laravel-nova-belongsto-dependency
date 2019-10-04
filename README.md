# BelongsTo field with dependency support for Nova

This package adds extra parameters to the request used by the BelongsTo fields
to fetch the options. The extra parameters are the selected values of other
fields so they can be used to filter the options based on selections in other
fields. The extra parameters are only passed when using a BelongsTo field that
is searchable.

## Installation

You can install this package on a Laravel app that uses [Nova](https://nova.laravel.com) via composer:

```bash
composer require sanderbaas/laravel-nova-belongs-to-dependency
```

## Usage

Make sure the fields of which the values should be filtered based on selections
of other fields are `->searchable()`.

```php
return [
    ...
    BelongsTo::make('Company'),
    BelongsTo::make('Employee')
    ->searchable(),
    ...
];
```

Then on the Employee resource, in this case, use the extra fields to filter the
correct employees as follows:

```php
public static function relatableQuery(NovaRequest $request, $query)
{
    $query->where('company_id', '=', $request->selectedCompany);
    return $query;
}
```

## Credits

I got the idea of adding selected values to the request from experience with Backpack for Laravel.
Also I was inspired by the package of manmohanjit:
[nova-belongsto-dependency](https://github.com/manmohanjit/nova-belongs-to-dependency)

## License

The MIT License (MIT). Please see License File for more information.