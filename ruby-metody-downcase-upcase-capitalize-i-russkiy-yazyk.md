# Ruby: Методы downcase, upcase, capitalize и русский язык

В руби есть удобные методы `downcase`, `upcase` или `capitalize` для изменения регистра букв в строках:

```ruby
'i am a string'.upcase
=> "I AM A STRING"

'I AM A STRING'.downcase
=> "i am a string"

'i am a string'.capitalize
=> "I am a string"
```

Но иногда эти методы не работают с кириллическими строками (на русском типа). Что делать?

```ruby
> 'я строка'.upcase
=> "Я СТРОКА"
```

У руби с UTF вообще сложная история взаимоотношений. Руби научился работать с русскими буквами нормально с версии 2.4 научилась. Так что проверьте версию руби и поставьте последний, если надо:
```console
$ ruby -v
ruby 2.6.5
```

Если же вы не можете поменять версию руби (в проекте, например, она зафиксирована), то можно установить gem, который называется **unicode**. Для этого в консоли наберите
```console
gem install unicode
```

Затем, чтобы добавить этот gem в вашу программу в начале файла с вашей программой добавьте строчку
```ruby
require 'unicode'
```

Теперь вам доступны следующие методы:
```ruby
require 'unicode'

test_str = "Я тЕсТОвая строКА"

puts Unicode::downcase(test_str)
# > я тестовая строка

puts Unicode::upcase(test_str)
# > Я ТЕСТОВАЯ СТРОКА

puts Unicode::capitalize(test_str)
# > Я тестовая строка
```
