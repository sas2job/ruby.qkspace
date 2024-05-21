# Ruby: Зачем пустая строка в конце файла?

Коротко: она нужна там по code-style https://github.com/rubocop-hq/ruby-style-guide#newline-eof

Подробно: существует стандарт, который называется POSIX и в этом стандарте [прописано определение](https://pubs.opengroup.org/onlinepubs/9699919799/basedefs/V1_chap03.html#tag_03_206) того, что такое 
строка:

> **3.206 Line**

> `A sequence of zero or more non- <newline> characters plus a terminating <newline> character.`

Строка — это последовательность из 0 и более символов, оканчивающаяся символом конца строки (символом перевода строки, `<newline> character`, тот самый `\n`)

То есть по факту пустая строка в конце файла - это не строка (согласно стандарту). Это лишь то, как текстовый редактор отображает символ перевода строки в конце файла.

https://stackoverflow.com/questions/729692/why-should-text-files-end-with-a-newline
