Captcha
=======

![Captchas examples](http://gregwar.com/captchas.png)
[![paypal](https://www.paypalobjects.com/en_US/i/btn/btn_donateCC_LG.gif)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=YUXRLWHQSWS6L)

Installation
============

Install composer and gd:
```
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
php -r "if (hash_file('SHA384', 'composer-setup.php') === '669656bab3166a7aff8a7506b8cb2d1c292f042046c5a994c43155c0be6190fa0355160742ab2e1c88d40d5be660b410') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
php composer-setup.php
php -r "unlink('composer-setup.php');"
```
and 
```
sudo apt-get -y install php-gd
```

Usage
=====

You can create a captcha with the `CaptchaBuilder` :

```php
<?php

use Gregwar\Captcha\CaptchaBuilder;

$builder = new CaptchaBuilder;
$builder->build();
```

You can then save it to a file :

```php
<?php

$builder->save('out.jpg');
```

Or output it directly :

```php
<?php

header('Content-type: image/jpeg');
$builder->output();
```

Or inline it directly in the HTML page:

```php
<img src="<?php echo $builder->inline(); ?>" />
```

You'll be able to get the code and compare it with a user input :

```php
<?php

// Example: storing the phrase in the session to test for the user 
// input later
$_SESSION['phrase'] = $builder->getPhrase();
```

You can compare the phrase with user input:
```php
if($builder->testPhrase($userInput)) {
    // instructions if user phrase is good
}
else {
    // user phrase is wrong
}
```
