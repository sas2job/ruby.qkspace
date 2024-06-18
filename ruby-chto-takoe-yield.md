# Ruby: Что такое yield?

`Yield` - это ключевое слово (означающее, что оно является основной частью языка), и оно используется внутри методов для вызова блока.

### Что такое блок?

Блок - это выражение внутри фигурных скобок `{}` если это одно строчный блок или выражение между `do..end` если выражение многострочное.

`yield` - (переводится как собрать) буквально означает: вместо этого слова в методе нужно поставить блок кода и выполнить метод в обычном режиме.
Пример использования `yield`

```rb
def test
  puts "You are in the method"
  yield
  puts "You are again back to the method"
  yield
end
test {puts "You are in the block"}
```

Получим:

```console
You are in the method
You are in the block
You are again back to the method
You are in the block
```

`Yield` может передавать аргументы

```rb
def test
  yield 5
  puts "You are in the method test"
  yield 100
end

test {|i| puts "You are in the block #{i}"}
```

Вывод:

```console
You are in the block 5
You are in the method test
You are in the block 100
```

Тут после `yield` описывается его параметр, а в блоке между двумя вертикальными чертами `||` - *пайпами* определяется переменная, которая принимает этот параметр. В результате — yield 5 передает значение 5 переменной `#{i}` блока `test {}`.

Можно передать два аргумента

```rb
def test
   yield 5, 10
   puts "You are in the method test"
   yield 100, 200
end

test {|a, b| puts "You are in the block #{a} #{b}"}
```

Результат

```console
You are in the block 5 10
You are in the method test
You are in the block 100 200
```