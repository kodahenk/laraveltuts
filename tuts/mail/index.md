# Mail

Laravel, güçlü ve kullanıcı dostu bir mail gönderme sistemi sunar. Bu rehberde, Laravel uygulamanızda nasıl mail göndereceğinizi adım adım öğreneceksiniz.

## Adım 1: Laravel Projenizi Oluşturun

Öncelikle, Laravel projesi oluşturun. Aşağıdaki terminal komutunu kullanarak yeni bir Laravel projesi başlatın.

```bash
composer create-project --prefer-dist laravel/laravel MailGondermeProjesi
```

## Adım 2: Mail Ayarlarını Yapın

Laravel'de mail gönderimi için `.env` dosyasında mail ayarlarını yapmanız gerekmektedir. Örnek bir `.env` dosyası aşağıdaki gibi olabilir:

```env
MAIL_MAILER=smtp
MAIL_HOST=mailtrap.io
MAIL_PORT=2525
MAIL_USERNAME=your_username
MAIL_PASSWORD=your_password
MAIL_ENCRYPTION=null
```

`MAIL_MAILER`, `MAIL_HOST`, `MAIL_PORT`, `MAIL_USERNAME`, ve `MAIL_PASSWORD` gibi değerleri kendi mail sağlayıcınıza göre güncelleyin.

## Adım 3: Mail Gönderme Fonksiyonunu Oluşturun

Laravel, mail gönderimi için `Mail` facade'ini kullanır. Aşağıdaki gibi bir örnek mail gönderme fonksiyonu oluşturun.

```php
// app/Http/Controllers/MailController.php

namespace App\Http\Controllers;

use Illuminate\Support\Facades\Mail;
use App\Mail\SampleMail;

class MailController extends Controller
{
    public function sendMail()
    {
        $to = 'example@email.com';
        $subject = 'Konu Başlığı';
        $data = ['message' => 'Mail içeriği burada.'];

        Mail::to($to)->send(new SampleMail($data, $subject));

        return 'Mail gönderildi!';
    }
}
```

## Adım 4: Mail Şablonunu Oluşturun

Mail şablonlarını `resources/views/mail` klasörü altında oluşturabilirsiniz. Örneğin, `SampleMail.blade.php` adında bir dosya oluşturun.

```blade
<!-- resources/views/mail/SampleMail.blade.php -->

<p>{{ $data['message'] }}</p>
```

## Adım 5: Mail Gönderimi Rota ve Controller'ı Tanımlayın

```php
// routes/web.php

use App\Http\Controllers\MailController;

Route::get('/send-mail', [MailController::class, 'sendMail']);
```

## Adım 6: Uygulamanızı Çalıştırın ve Test Edin

Uygulamanızı ayağa kaldırın ve tarayıcınızda `http://localhost:8000/send-mail` adresine giderek mail gönderimini test edin.
