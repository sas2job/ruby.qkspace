# Ruby: Почему puts «съедает» один перенос строки?



В описании говорится что в `puts` по умолчанию встроен переход на следующую строку, (в отличии от `print`), но если добавить `\n` в конце — новая строка не появится, она появится только если добавить два `\n\n`.

```ruby
puts "Привет, дорогой друг.\n\n"
```

Вопрос: «Почему?»

Ответ: «Так задумано…»

[https://ruby-doc.org/core-2.2.2/IO.html#method-i-puts](https://ruby-doc.org/core-2.2.2/IO.html#method-i-puts)

> Writes the given objects to ios as with IO#print. Writes a record separator (typically a newline) after any **that do not already end with a newline sequence**. If called with an array argument, writes each element on a new line. If called without arguments, outputs a single record separator.

Если интересно, можно посмотреть [исходный код puts](https://github.com/ruby/ruby/blob/0db6b623a63003aad342739e66d81f957deff60c/io.c#L7223) в руби.
