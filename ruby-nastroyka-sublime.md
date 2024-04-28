### Ruby: Настройка Sublime



В руби [принято](https://github.com/arbox/ruby-style-guide/blob/master/README-ruRU.md#spaces-indentation) делать отступ двумя пробелами:

```ruby
if a == 2
  puts "А у нас равно 2"
end
```

По умолчанию в Саблайме табуляция добавляет отступ символом табуляции. Вот, как можно настроить Саблайм на правильную работу.

1. Открыть руби файл (с расширением `.rb`)
2. Перейти `Preferences -> Settings -> More -> Syntax Specific -> User`
Ввести (или заменить):

```
{
  "tab_size": 2,
  "translate_tabs_to_spaces": true,
  "trim_trailing_white_space_on_save": true,
  "ensure_newline_at_eof_on_save": true,
  "trim_only_modified_white_space": false
}
```

Заодно это избавит вас от лишних пробелов в конце строк и автоматически добавит ровно одну пустую строку в конце файла.
