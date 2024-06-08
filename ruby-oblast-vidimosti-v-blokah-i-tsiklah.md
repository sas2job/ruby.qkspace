# Ruby: Область видимости в блоках (и циклах)

### Вопрос

Почему в руби переменные, объявленные внутри блока `do-end` (например, циклов), иногда не видны вне этого блока, а иногда видны? Вроде бы, два одинаковых кода, но почему-то такой код отработает:

```ruby
name = 'Вадик'

count = 0
while count < 1 do
string = 'Какая-то строка'
puts name
count += 1
end

puts string
```

А такой код уже упадет с ошибкой:

```ruby
name = 'Вадик'

1.times do
string = 'Какая-то строка'
puts name
end

puts string
```

т.к. не увидит переменную `string` в основной программе:

```ruby
NameError (undefined local variable or method `string' for main:Object)
```

Почему один блок требует объявить переменную заранее, а другой нет?

### Ответ

Обратите внимание на разницу в этих двух местах кода. Во втором случае `times` это метод, вызванный у целого числа 1, которому мы передаем, что делать 1 раз, а `until` — это встроенная в руби конструкция для создание циклов. Это отличие очень важное.

Строго говоря, первое — это просто тело цикла, а второе — это блок.

И области видимости они создают разные, так авторы Ruby решили сделать и их можно понять. Блок это как будто анонимный метод, логично что внутри метода свои локальные переменные (но отличие блока от метода в том, что блок еще сохраняет ссылку на внешний scope где он был объявлен).

Короче, если вкратце:

- Блок (то есть, грубо говоря, код между `do... end` и `{ ... }`) «захватывает» в себя переменные, которые были 
  объявлены до его начала. Позволяя получать их значение и изменять.
- Циклы (`while`, `until`, `for`) не влияют на область видимости переменных. В Ruby есть возможность писать циклы с `do`, но 
  делать этого ни при каких условиях не следует, чтобы не путать себя и других.
- Методы (`def something... end`) позволяют использовать (кроме своих явных аргументов/параметров) и менять только 
  instance-переменные (`@variable`) того же объекта, чей метод вызывается.