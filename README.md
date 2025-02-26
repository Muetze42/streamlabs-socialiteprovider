# Streamlabs API V2

Refactor for Streamlabs API V2.

Add to `composer.json`:

```json
{
    "repositories": [
        {
            "type": "vcs",
            "url": "https://github.com/Muetze42/streamlabs-socialiteprovider"
        }
    ]
}
```

```bash
composer require socialiteproviders/streamlabs:"dev-main"
```

## Installation & Basic Usage

Please see the [Base Installation Guide](https://socialiteproviders.com/usage/), then follow the provider specific instructions below.

### Add configuration to `config/services.php`

```php
'streamlabs' => [
  'client_id' => env('STREAMLABS_CLIENT_ID'),  
  'client_secret' => env('STREAMLABS_CLIENT_SECRET'),  
  'redirect' => env('STREAMLABS_REDIRECT_URI') 
],
```

### Add provider event listener

Configure the package's listener to listen for `SocialiteWasCalled` events.

Add the event to your `listen[]` array in `app/Providers/EventServiceProvider`. See
the [Base Installation Guide](https://socialiteproviders.com/usage/) for detailed instructions.

```php
protected $listen = [
    \SocialiteProviders\Manager\SocialiteWasCalled::class => [
        // ... other providers
        \SocialiteProviders\Streamlabs\StreamlabsExtendSocialite::class.'@handle',
    ],
];
```

### Usage

You should now be able to use the provider like you would regularly use Socialite (assuming you have the facade installed):

```php
return Socialite::with('streamlabs')->redirect();
```

### Returned User fields

- `id`
- `name`
- `accounts`

> Note: `accounts` is an array of providers that the user has signed-in with Streamlabs; included values are Twitch (`twitch`),
> YouTube (`youtube`), and Facebook (`facebook`).

### Reference

- [Streamlabs API Reference](https://dev.streamlabs.com/)
