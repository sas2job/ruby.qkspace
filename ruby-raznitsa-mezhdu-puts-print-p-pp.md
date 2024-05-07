# Ruby: Разница между puts, print, p, pp

Написано по мотивам [этой статьи](https://dev.to/lofiandcode/ruby-puts-vs-print-vs-p-vs-pp-vs-awesome-5akl) (вольный перевод и адаптация).

В Ruby для вывода данных в консоли доступно 4 метода: `puts`, `print`, `p`, `pp`. Рассмотрим подробнее:

## puts

```ruby
> puts "Hello World!"
Hello World!
=> nil
```

`puts` печатает всё, что передаётся методу, а в конце печатается символ перевода строки.

При помощи `puts` можно вывести построчно все элементы массива.

```ruby
> puts [1, 2, 3]
1
2
3
=> nil
```

Всё, что передается методу `puts` благодаря методу `.to_s` превращается в строку. То есть если у вас в массиве есть `nil`-элементы, то при использовании `puts` они будут напечатаны в виде пустой строки.

```ruby
> puts [1, nil,nil, 4]
1

4
=> nil
```

## print

Этот метод похож на `puts`, но он не добавляет в конце символ новой строки:

```ruby
> print "Hello World!"
Hello World!=> nil
```

Если передать методу массив то он полностью выведет его включая скобки.
```ruby
> print [1, 2, 3][1, 2, 3]=> nil
```

После каждого использования `puts` (или `print`) вы видите «nil» — это происходит потому, что любой метод в ruby возвращает какое то значение, и `puts`/`print` возвращают ничего, специальный объект — `nil`.

## p

Метод `p` для вывода использует метод `.inspect`, который есть у любого объекта в руби. Получается вывод объекта в наиболее «говорящем» для разработчика виде:
```ruby
irb(main):006:0> p "Hello World!"
"Hello World!"
=> "Hello World!"

irb(main):007:0> p [1, 2, 3]
[1, 2, 3]
=> [1, 2, 3]
```

Важно, что метод `p` возвращает уже не `nil`, а сам объект, который ему передали.

Как видно в примере `p` выводит на печать то что ему передали в качестве аргумента и возвращает тот же объект.

## pp

Метод `pp` (от англ. pretty print) — это специальная версия `p`, которая выводит аргумент в более читаемом виде.

Пример с хэшем выглядит так:
```ruby
> h = {some: 1, "the" => {subone: "true", subtwo: [1,2,"3333", {subsub: "one", nonenone: {twotwo: [{keyone: 1, keytwo: ["222","sdsd"]},1,2], some: "free"}}]}, ne: "xt"}
> pp h

{:some=>1,
"the"=>
{:subone=>"true",
:subtwo=>
[1,
2,
"3333",
{:subsub=>"one",
:nonenone=>
{:twotwo=>[{:keyone=>1, :keytwo=>["222", "sdsd"]}, 1, 2],
:some=>"free"}}]},
:ne=>"xt"}

=> {:some=>1, "the"=>{:subone=>"true", :subtwo=>[1, 2, "3333", {:subsub=>"one", :nonenone=>{:twotwo=>[{:keyone=>1, :keytwo=>["222", "sdsd"]}, 1, 2], :some=>"free"}}]}, :ne=>"xt"}
```
Возвращает, как и `p` переданный объект.

## ap

Есть ещё более «крутой» способ вывести что-то — гем **awesome_print**. Установить его можно командой:

```console
gem install awesome_print
```

Далее в irb необходимо включить гем
```console
> require "awesome_print"
=> true
```

Этот метод `ap` выводит данные не только в удобочитаемом виде, но ещё и с нужными отступами, а также печатает значение индекса рядом с каждым элементом массива.

Вот наш пример с хэшем:
```ruby
> h = {some: 1, "the" => {subone: "true", subtwo: [1,2,"3333", {subsub: "one", nonenone: {twotwo: [{keyone: 1, keytwo: ["222","sdsd"]},1,2], some: "free"}}]}, ne: "xt"}
> ap
{
:some => 1,
"the" => {
:subone => "true",
:subtwo => [
[0] 1,
[1] 2,
[2] "3333",
[3] {
:subsub => "one",
:nonenone => {
:twotwo => [
[0] {
:keyone => 1,
:keytwo => [
[0] "222",
[1] "sdsd"
]
},
[1] 1,
[2] 2
],
:some => "free"
}
}
]
},
:ne => "xt"
}
=> nil
```