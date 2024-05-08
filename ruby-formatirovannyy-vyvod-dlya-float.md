# Ruby: Форматированный вывод для Float

Как прописать количество разрядов после запятой в выводе числа с плавающей точкой без округления? Как обозначить минимальное количество знакомест под вывод значения?

[https://stackoverflow.com/questions/12389567/how-to-format-a-string-with-floats-in-ruby-using-variable](https://stackoverflow.com/questions/12389567/how-to-format-a-string-with-floats-in-ruby-using-variable)

Лично мне больше нравится подход с округлением прямо во время интерполяции — оно при этом не меняет само исходное число:

```ruby
num = 1.23456
puts "Num is: #{num.round(2)}"  # Num is 1.23
puts "Num is #{num}" # Num is 1.23456
```

Ещё есть возможность использовать следующий синтаксис:

```ruby
num = 1.23456
puts "Num is: #{'%.2f' % num}" # Num is 1.23
puts "Num is: #{'%.3f' % num}" # Num is 1.235
```
