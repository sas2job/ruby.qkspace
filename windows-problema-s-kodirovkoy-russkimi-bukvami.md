# Windows: Проблема с кодировкой/русскими буквами

При написании программы на ruby, которая берет ввод пользователя из консоли, иногда возникают проблемы. Даже если файл сохранен в кодировке UTF-8, русские символы программа не выводит.

```ruby
puts "Привет! Как тебя зовут?"

name = gets.encode("UTF-8").chomp

puts "Привет, " + name + ", как дела?"
```

Результат в консоли
```ruby
D:\RUBYTUT\lesson5>ruby gets.rb
Привет! Как тебя зовут?
Карина
Привет, ��ਭ�, как дела?
```

Можно ли это как-то исправить?

Ультимативное решение -- вставить в начале файла код:
```ruby
# XXX/ Этот код необходим только при использовании русских букв на Windows
if (Gem.win_platform?)
Encoding.default_external = Encoding.find(Encoding.locale_charmap)
Encoding.default_internal = __ENCODING__

[STDIN, STDOUT].each do |io|
io.set_encoding(Encoding.default_external, Encoding.default_internal)
end
end
# /XXX
```

После этого использовать `encode` уже не нужно:

```ruby
name = gets.chomp
```
