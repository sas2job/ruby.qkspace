### Ruby: Почему 2 == 2.0 (сравнение Integer и Float) возвращает true?



У людей, пришедших в руби из других языков программирования вызывает шок такая картина:

```console
irb(main):006:0> 2 == 2.0
=> true
irb(main):007:0> 3 == 3.0
=> true
```

На самом деле это [нормально](https://ruby-doc.org/core/Object.html#method-i-eql-3F). В руби есть разные сравнения.

#### Оператор `==`

Сравнивается [фактические значения чисел](https://ruby-doc.org/core/Integer.html#method-i-3D-3D).

```console
>> 5 == 5.0
=> true
```

#### Метод `equal?`

Сравниваются [ссылки на объект](https://ruby-doc.org/core/BasicObject.html#method-i-equal-3F), поэтому тип и значение играют роль.

```console
>> 5.equal? 5.0
=> false
```

По сути эта запись эквивалентна такой:

```console
>> 5.object_id == 5.0.object_id
=> false
```

#### Метод `eql?`

Сравниваются два хэш-ключа. Соответственно тип и значение [играют роль](https://ruby-doc.org/core/Numeric.html#method-i-eql-3F).

```console
>> 5.eql? 5.0
=> false
```

По сути эта запись эквивалентна такой:

```console
>> 5.hash == 5.0.hash
=> false
```

Дополнительно можете [почитать статью](archive/ravenstvo-v-ruby.md) про равенство в Руби.
