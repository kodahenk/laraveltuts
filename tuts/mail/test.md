# Mail Test

Laravel uygulamasında mail gönderme işlemini test etmek için Laravel'in sağladığı bir özellik olan "Mail Fake" kullanılabilir. Bu, gerçek mail gönderimini engelleyerek, gönderilen maili loglamak veya belirli bir test e-posta adresine yönlendirmek için kullanılır.

Aşağıda, yukarıda verdiğimiz mail kodu için bir PHPUnit test örneği bulunmaktadır:

```php
// tests/Feature/MailTest.php

namespace Tests\Feature;

use Illuminate\Foundation\Testing\RefreshDatabase;
use Illuminate\Foundation\Testing\WithFaker;
use Illuminate\Support\Facades\Mail;
use Tests\TestCase;
use App\Mail\SampleMail;

class MailTest extends TestCase
{
    /** @test */
    public function it_sends_email()
    {
        // Fake mail gönderimini kullanarak test et
        Mail::fake();

        // Mail gönderimini tetikle
        $response = $this->get('/send-mail');

        // Mailin gönderilip gönderilmediğini assert et
        Mail::assertSent(SampleMail::class, function ($mail) {
            return $mail->hasTo('example@email.com');
        });

        // Başarılı response kontrolü
        $response->assertStatus(200)
                 ->assertSeeText('Mail gönderildi!');
    }
}
```

Bu test sınıfında `Mail::fake()` kullanılarak mail gönderimleri sahte (fake) bir şekilde yakalanır. Ardından `Mail::assertSent()` metodu ile gönderilen mailin belirli bir mail sınıfına ait olduğu ve doğru alıcıya gittiği kontrol edilir.

Bu testi çalıştırmak için terminalde şu komutu kullanabilirsiniz:

```bash
php artisan test
```

Bu, Laravel'in yerleşik PHPUnit testlerini çalıştırmak için kullanılan komuttur. Bu testin başarılı olması durumunda, mail gönderimi işleminiz doğru bir şekilde çalışıyor demektir.
