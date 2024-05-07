# Ruby: Зачем конвертировать аргумент puts в строку методом to_s

Метод `puts` в руби выводит в консоль именно строковые данные.

В простом случае, когда мы выводим что-то одно:

```ruby
number = 1
puts number
```

Происходит автоматическое преобразование объекта в строку (у этого объекта под капотом `puts` вызывает метод `to_s`) и программа отрабатывает без ошибки.

А вот если аргумент puts будет посложнее, например:

```ruby
number = 1
puts "У меня есть " + number + " пирожок"
```

То при запуске программа выдаст ошибку:

```ruby
to_s.rb:2:in `+': no implicit conversion of Fixnum into String (TypeError)
from to_s.rb:2:in `<main>'
```

То есть фактически, ругается на неправильный аргумент не `puts`, а оператор сложения, т.к. не может сложить числа со строками.

В этом случае можно подсказать руби, что мы хотим скалывать именно строки, написав `number.to_s`:

```ruby
number = 1
puts "У меня есть " + number.to_s + " пирожок"
```