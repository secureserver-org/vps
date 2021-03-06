# VPS
###### beta version
[![License](https://poser.pugx.org/iluminar/vps/license?format=flat-square)](https://packagist.org/packages/iluminar/vps)
[![StyleCI](https://styleci.io/repos/65676805/shield)](https://styleci.io/repos/65676805)

A laravel 5 package to easily create and maitain vps on digital ocean. Yet to complete
 Have a look at the usage
``` php
$value = ["name"=> "test.com","region"=> "blr1","size"=> "512mb","image"=> "centos-7-2-x64"];
$result = VPS::droplet()->create($value);
```
We just created a droplet in digital ocean.

``` php
$result = VPS::droplet($id)->delete();
```
We just deleted a droplet by passing the id of our droplet.

Want to shutdown a droplet
``` php
$result = VPS::droplet($id)->shutdown();
```

How about getting all droplets we created
``` php
$result = VPS::droplet()->all();
```

## Install

You can pull in the package via composer:
``` bash
$ composer require iluminar/vps
```

Or you can add this in your composer.json

``` bash
"require": {
    "iluminar/vps": "dev-develop"
}
```

and then terminal from your root directory of project run following command
``` bash
$ composer update
```

After updating composer, add a fluent service provider to the providers array in config/app.php file.

``` php
 'providers' => array(
        // ...
        Iluminar\VPS\Providers\VPSServiceProvider::class,
    )
```

then run in terminal
``` bash
$ php artisan vendor:publish
```

## Configuration

First you have to get a [personal access token](https://cloud.digitalocean.com/settings/api/tokens) and set the `DIGITAL_OCEAN_TOKEN` in the .env file.

## Usage

Import the `VPS` facade in your controller

### Account information
``` php
$result = VPS::account();
```

### Get action information
Get all actions performed on an account
``` php
$result = VPS::action()->all();
```

Get information of an action
``` php
$result = VPS::action()->find($id);
```

### Get droplet information

Get information of all droplets
``` php
$result = VPS::droplet()->all();
```

Get information of a single droplet
``` php
$result = VPS::droplet()->find($id);
```

Get all snapshots of a droplet 
``` php
$result = VPS::droplet($id)->snapshots();
```

Get all backups of a droplet 
``` php
$result = VPS::droplet($id)->backups();
```

Enable backups of a droplet 
``` php
$result = VPS::droplet($id)->enableBackups();
```

Disable backups of a droplet 
``` php
$result = VPS::droplet($id)->disableBackups();
```

Reboot a droplet 
``` php
$result = VPS::droplet($id)->reboot();
```

Power cycle a droplet 
``` php
$result = VPS::droplet($id)->powerCycle();
```

Shutdown a droplet 
``` php
$result = VPS::droplet($id)->shutdown();
```

Power off a droplet 
``` php
$result = VPS::droplet($id)->powerOff();
```

Power on a droplet 
``` php
$result = VPS::droplet($id)->powerOn();
```

Restore a droplet by providing a id of previous image
``` php
$result = VPS::droplet($id)->restore();
```

Resize a droplet, pass a size parameter (1gb, 2gb etc..). For permanent resize also passed a boolen valu of true
``` php
$result = VPS::droplet($id)->resize('1gb');
$result = VPS::droplet($id)->resize('1gb', true); // permanent resize
```

Rebuild a droplet, pass a image id or slug as a parameter
``` php
$result = VPS::droplet($id)->rebuild($id);
$result = VPS::droplet($id)->rebuild('ubuntu-14-04-x64'); // rebuild by image slug
```

Rename a droplet, pass a string as a parameter
``` php
$result = VPS::droplet($id)->rebuild('name');
```

Enable ipv6 on a droplet
``` php
$result = VPS::droplet($id)->enableIPv6();
```

Enable private networking on a droplet
``` php
$result = VPS::droplet($id)->enablePrivateNetworking();
```

Take snapshot of a droplet, pass a string as a parameter to name the snapshot
``` php
$result = VPS::droplet($id)->takeSnapshot('new nifty snapshot');
```

Get information of a action performed on this droplet
``` php
$result = VPS::droplet($id)->action($actionId);
```

### Get image information

List all images
``` php
$result = VPS::image()->all();
```

List all distribution images
``` php
$result = VPS::image()->where(['type' => 'distribution']);
```

List all application images
``` php
$result = VPS::image()->where(['type' => 'application']);
```

List all private images of user
``` php
$result = VPS::image()->where(['private' => 'true']);
```

Get information of a single image
``` php
$result = VPS::image()->find($id);
```

Get information of a single image by slug
``` php
$result = VPS::image()->find('ubuntu-14-04-x64');
```

List all actions for an images
``` php
$result = VPS::image($id)->actions();
```

Rename an image
``` php
$result = VPS::image($id)->rename('new cool name');
```

Delete an image
``` php
$result = VPS::image($id)->delete();
```

Transfer an image to a different region
``` php
$result = VPS::image($id)->transfer('nyc1');
```

Convert an image to a snapshot
``` php
$result = VPS::image($id)->convert();
```

Get information of an action performed on an image
``` php
$result = VPS::image($id)->action($actionId);
```

### SSH keys

List all keys associated with this account
``` php
$result = VPS::ssh()->all();
```

Add a new ssh key to your account
``` php
$result = VPS::ssh()->create(['name' => 'my-home-key', 'public_key' => "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAAAQQDDHr/jh2Jy"]);
```

Get information about a key by key id or fingerprint
``` php
$result = VPS::ssh()->find($id); // or $fingerprint instead of $id
```

Rename a key
``` php
$result = VPS::ssh($id)->rename('new key name');
```

Delete a key
``` php
$result = VPS::ssh($id)->delete(); // $fingerprint can also be used instead of $id
```

## Documentation

Yet to be added.

### TODO

> **documentation**

> **Error handling**

## Security Vulnerabilities

If you discover a security vulnerability in the package, please send an e-mail to Nehal Hasnayeen at searching.nehal@gmail.com. All security vulnerabilities will be promptly addressed.

## License

The **Iluminar\VPS** is open-sourced software licensed under the [MIT license](http://opensource.org/licenses/MIT).

## Change log

Please see [CHANGELOG](CHANGELOG.md) for more information what has changed recently.

## Contributor

Made by [Hasnayeen](https://github.com/hasnayeen) with love in ![Bangladesh](https://upload.wikimedia.org/wikipedia/commons/thumb/f/f9/Flag_of_Bangladesh.svg/20px-Flag_of_Bangladesh.svg.png)