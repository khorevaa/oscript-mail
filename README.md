# Работа с почтой в Односкрипте

Отправка посредством SMTP.

## Установка через OPM

```
opm install InternetMail
```

## Пример работы (отправка HTML письма с вложениями)

```bsl

Профиль = Новый ИнтернетПочтовыйПрофиль;

Профиль.АдресСервераSMTP    = "smtp.mail.ru";
Профиль.ПользовательSMTP    = "someuser@mail.ru";
Профиль.ПарольSMTP          = "somepass123";
Профиль.ИспользоватьSSLSMTP = Истина;


Профиль.АдресСервераPOP3    = "pop.mail.ru";
Профиль.ИспользоватьSSLPOP3 = Истина;
Профиль.Пользователь        = "someuser@mail.ru";
Профиль.Пароль              = "somepass123";

Сообщение = Новый ИнтернетПочтовоеСообщение;
Сообщение.Получатели.Добавить("receiver@mail.ru");
Сообщение.ОбратныйАдрес.Добавить("someuser@mail.ru");
Сообщение.Отправитель = "someuser@mail.ru";
Сообщение.Тема        = "Server is down";
Текст =  "
	|<h3>Server is down !</h3>
	|Надо что-то делать.<br/>";

Сообщение.Тексты.Добавить(Текст, ТипТекстаПочтовогоСообщения.HTML);
Сообщение.Вложения.Добавить("C:/Пример вложения 1.docx");
Сообщение.Вложения.Добавить(
        Новый ДвоичныеДанные("C:/Пример вложения 2.docx"),
        "Пример вложения 2.docx"
);

Почта = Новый ИнтернетПочта;
Почта.Подключиться(Профиль, ПротоколИнтернетПочты.POP3);
Почта.Послать(Сообщение, , ПротоколИнтернетПочты.SMTP);
```