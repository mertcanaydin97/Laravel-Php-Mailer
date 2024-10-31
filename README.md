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


# open 'routes/web.php' add the code below.
Route::post('/contact-form', [MainController::class, 'contactForm'])->name('contactForm');


# usage
First import file 

use App\Helpers\MailHelper;

then use it like;
Controller;
 public function contactForm(Request $request){

        $find = array('name','email','subject','phone','message');
        $replace = array('Ad Soyad','E-Posta','Konu','Telefon','Mesaj');

        $mailcontent = '<h1>Merhaba</h1>';
        $mailcontent .= '<p style="padding-top:10px">Yeni web sitesi iletişim formu gönderildi</p>';
        $mailcontent .= '<p style="padding-top:10px">';

        foreach ($request->all() as $key => $value) {
             $mailcontent .= str_replace($find,$replace,$key).': '.$value.'<br>';
        }

        $mailcontent .= '</p>';

        MailHelper::sendMail('web@mertcanaydin.com.tr', 'Web Sitesi Yeni İletişim Formu!', $mailcontent);

        return response()->json(['message' => 'Tebrikler! Mesajınız başarıyla gönderildi. En kısa süre içerisinde size geri dönüş yapacağız.']);

    }

Blade;
response div,
                        <div class="alert alert-success" id="response" style="display: none"></div>
xhr request,

 <script>
        const form = document.querySelector('form');
        let resposenseDiv = document.getElementById('response');
        form.addEventListener('submit', function(e) {
            e.preventDefault();

            let formElement = document.getElementsByTagName("form")[0],
                inputElements = formElement.getElementsByTagName("input"),
                textArea = formElement.getElementsByTagName("textarea"),
                jsonObject = {};
            for (let i = 0; i < inputElements.length; i++) {
                let inputElement = inputElements[i];
                jsonObject[inputElement.name] = inputElement.value;

            }
            for (let i = 0; i < textArea.length; i++) {
                let tElement = textArea[i];
                jsonObject[tElement.name] = tElement.value;

            }

            let post = JSON.stringify(jsonObject)
            const url = "{{ route('contactForm') }}"
            let xhr = new XMLHttpRequest()
            xhr.open('POST', url, true)
            xhr.setRequestHeader('Content-type', 'application/json; charset=UTF-8')
            xhr.setRequestHeader('X-CSRF-TOKEN', '{{ csrf_token() }}');

            xhr.send(post);
            xhr.onload = function() {
                if (xhr.status === 200) {
                    form.reset();
                    resposenseDiv.innerHTML = JSON.parse(xhr.response).message;
                    resposenseDiv.style.display = 'block';
                    let rHeight = resposenseDiv.offsetHeight,
                    rPadding = window.getComputedStyle(resposenseDiv, null).getPropertyValue('padding').replace('px',''),
                    fixHeight = rHeight,
                    fixPadding = rPadding;
                    console.log(rPadding)
                    setTimeout(() => {
                        var fadeEffect = setInterval(function() {
                            if (!resposenseDiv.style.opacity) {
                                resposenseDiv.style.opacity = 1;
                            }
                            if (resposenseDiv.style.opacity > 0) {
                                rHeight -= (fixHeight/9);
                                rPadding -= (fixPadding/9);
                                console.log(rPadding)
                                resposenseDiv.style.height = + rHeight + 'px'
                                resposenseDiv.style.padding =  + rPadding +'px 1rem '

                                resposenseDiv.style.opacity -= 0.1;
                            } else {
                                clearInterval(fadeEffect);
                                resposenseDiv.style.display = 'none';
                            }
                        }, 100);
                    }, 5000);
                }
            }
        });
    </script>



```
