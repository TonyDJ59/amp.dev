---
"$title": Валидация AMP-писем
"$order": '1'
author: CrystalOnScript
formats:
- email
---

AMP-письмам требуется JS-библиотека AMP, чтобы обеспечить насыщенное интерактивное взаимодействие и динамические возможности при чтении. Именно поэтому поставщики электронной почты требуют валидации писем. Соблюдение требований к разметке AMP гарантирует безопасность писем и максимальный уровень комфорта при их просмотре.

# Как проверить, корректно ли сформировано мое AMP-письмо?

Есть несколько способов убедиться в том, что AMP-письмо сформировано корректно. Все эти способы одинаково эффективны, так что выбирайте тот, который лучше всего вписывается в ваш процесс разработки.

## Веб-валидатор

[Веб-валидатор AMP](https://validator.ampproject.org/#htmlFormat=AMP4EMAIL) поддерживает платформу «AMP для писем». Для того чтобы воспользоваться веб-валидатором, вставьте в него текст AMP-письма. Все ошибки валидации будут помечены прямо в коде.

{{ image('/static/img/docs/guides/emailvalidate.jpg', 500, 382, alt='Image of web-based email validator' ) }}

## Валидатор для командной строки

Для валидации файлов AMP-писем можно использовать [инструмент валидации AMP HTML для командной строки](https://www.npmjs.com/package/amphtml-validator).

### Установка

1. Убедитесь, что в вашей системе установлен [Node.js с менеджером пакетов npm](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm).
2. Установите инструмент валидации AMP HTML для командной строки при помощи следующей команды: `npm install -g amphtml-validator`.

### Использование

После установки инструмента командной строки запустите следующую команду, заменив `<amphtml file>` названием файла с содержимым AMP-письма.

```
amphtml-validator --html_format AMP4EMAIL <amphtml file>
```

Если письмо пройдет валидацию, инструмент командной строки вернет результат `PASS`. В противном случае он выведет обнаруженные ошибки.

## Песочница AMP

Для валидации AMP-писем можно также использовать [песочницу AMP](https://playground.amp.dev/?runtime=amp4email). Порядок действий тот же, что и при использовании веб-валидатора: вставьте в песочницу AMP-письмо, и она пометит все ошибки валидации прямо в коде.

### Валидация доставленных писем

Иногда код уже доставленных AMP-писем оказывается некорректным, даже если на момент создания письма его разметка успешно проходила проверку инструментами, перечисленными на этой странице. Причина обычно заключается в том, что используемый [поставщик электронной почты (ESP)](https://amp.dev/support/faq/email-support/), получив письма для доставки, модифицирует их разметку и тем самым нарушает ее корректность. Например, если вы используете ESP SparkPost и не настроили в нем отслеживающие пиксели на основе HTTPS, SparkPost будет добавлять в каждое письмо небезопасный отслеживающий пиксель на основе HTTP. Такие AMP-письма не будут проходить проверку на правильность кода, так как в AMP-письмах разрешены только HTTPS-изображения.

Для того чтобы проверить правильность кода AMP-письма, доставленного на вашу почту:

1. [Скачайте AMP-письмо в виде файла `.eml`](https://www.codetwo.com/kb/export-email-to-file), используя почтовый клиент.
2. Откройте [песочницу AMP](https://playground.amp.dev/?runtime=amp4email).
3. Нажмите «IMPORT EMAIL» и выберите файл `.eml`, который вы только что скачали.

Песочница импортирует AMP-письмо, которое вы скачали, во встроенный редактор и пометит ошибки валидации.

# Что произойдет, если письмо не пройдет валидацию?

AMP-валидатор существует не просто для удобства разработчиков: поставщики электронной почты, поддерживающие AMP-письма, будут автоматически переключаться на версию письма с другим MIME-типом (HTML или чистый текст), если AMP-версия не проходит проверку. Отправляйте AMP-письма только в том случае, если они прошли проверку валидатором.
