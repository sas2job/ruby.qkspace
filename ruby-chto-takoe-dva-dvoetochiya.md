# Ruby: Что такое два двоеточия "::"

Часто можно увидеть два двоеточия при вызове методов или обращению к классам:

```ruby
REXML::Document.new
```

равносильно ли это такой записи ?

```ruby
REXML.Document.new
```

Вот отличная [литература на тему](https://stackoverflow.com/questions/11043450/vs-dot-vs-double-colon-for-calling-a-method).

Пример из википедии.
```ruby
module Example
Version = 1.0

class << self # We are accessing the module's singleton class
def hello(who = "world")
"Hello #{who}"
end
end
end #/Example

Example::hello # => "Hello world"
Example.hello "hacker" # => "Hello hacker"

Example::Version # => 1.0
Example.Version # NoMethodError

# This illustrates the difference between the message (.) operator and the scope
# operator in Ruby (::).
# We can use both ::hello and .hello, because hello is a part of Example's scope
# and because Example responds to the message hello.
#
# We can't do the same with ::Version and .Version, because Version is within the
# scope of Example, but Example can't respond to the message Version, since there
# is no method to respond with.
```

То есть `::` — это оператор разрешения области видимости (scope resolution), а `.` — это оператор "посылки сообщений".

Ключевое отличие в том, что в области видимости может быть, например, константа (в примере `Version`) и через `::` её можно достать, а вот через `.` уже нет, ибо нет такого метода.

Вот ещё, кстати, момент:

> When a receiver is explicitly specified in a method invocation, it may be separated from the method name using either a period (.) or two colons (::). The only difference between these two forms occurs if the method name starts with an uppercase letter. In this case, Ruby will assume that a receiver::Thing method call is actually an attempt to access a constant called Thing in the receiver unless the method invocation has a parameter list between parentheses.

Т.е. `MyClass::Version` будет воспринято как константа даже если есть метод `Version`. Что вызовет ошибку в некоторых случаях.
