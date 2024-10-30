# Laravel Php Mailer Helper

Laravel-Php-Mailer-Helper is a mail class with php-mailer.
## Installation

First you need to install php-mailer package to your app.

```bash
composer require phpmailer/phpmailer
```

## Usage
```env

#Fill env fields with your smtp data

MAIL_MAILER=smtp
MAIL_HOST=mailpit
MAIL_PORT=1025
MAIL_USERNAME=null
MAIL_PASSWORD=null
MAIL_ENCRYPTION=null
MAIL_FROM_ADDRESS="hello@example.com"
MAIL_FROM_NAME="${APP_NAME}"

# folder
Create 'Helpers' named folder in 'app' folder of your laravel app

# download
Download this file and move to 'Helpers' folder that you created or create new file inside folder then copy contents of this code.

# open 'config/app.php' update alieses add 'MailHelper' class.

 'aliases' => Facade::defaultAliases()->merge([
        // 'Example' => App\Facades\Example::class,
        'MailHelper' => App\Helpers\MailHelper::class,
    ])->toArray(),



# usage
First import file 

use App\Helpers\MailHelper;

then use it like;
 $mailcontent = '<h1>Hello</h1>';
 $mailcontent .= '<p style="padding-top:10px">Lorem ipsum dolor sit amet</p>';
 $mailcontent .= '<p style="padding-top:10px">
            Email: ' . $request->email . '<br>
            Message: ' .$request->message . '</p>';
        
  MailHelper::sendMail('foo@bar.com', 'Hello!', $mailcontent);

```
