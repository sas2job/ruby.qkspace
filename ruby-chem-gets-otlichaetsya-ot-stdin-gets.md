# Ruby: Чем gets отличается от STDIN.gets?

Если написать в руби просто `gets`, то будет вызван метод `Kernel#gets`, а этот [метод](https://ruby-doc.org/core/Kernel.html#method-i-gets) в руби устроен довольно интересно. Если при запуске программы был передан аргумент (который позже можно получить в программе из массива `ARGV`), то он воспримет его как путь к файлу и попытается этот файл прочитать, а у пользователя в консоли ничего не просит.
```ruby
input = gets.chomp

puts input
```

Запуск:
```ruby

$ ruby main.rb
Привет!
Привет!

$ ruby main.rb Привет
Traceback (most recent call last):
2: from main.rb:1:in `<main>'
1: from main.rb:1:in `gets'
main.rb:1:in `gets': No such file or directory @ rb_sysopen - Привет (Errno::ENOENT)
```

Чтобы этого избежать, можно обратиться к методу `gets` объекта `STDIN`.

`STDIN` — сокращение от `STandarD INput` — в данном случае консоль. Если вызвать метод `STDIN.gets`, то руби вызовет этот метод у объекта стандартного ввода и будет совершенно точно читать именно из консоли, не отвлекаясь на `ARGV`.

```ruby
input = STDIN.gets.chomp

puts input
```

Запуск:

```ruby
$ ruby main.rb Привет
Досвидули!
Досвидули!
```

**Правило буравчика**: если ваша программа использует `ARGV`, вместо `gets` необходимо использовать `STDIN.gets`, если не использует — можно оставить `gets`, но если везде замените на `STDIN.gets` хуже не будет.
