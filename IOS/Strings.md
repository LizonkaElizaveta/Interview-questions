# Swift

## ___Strings and Characters___

*Multiline String Literals*

Для облегчения чтения кода, без реального разрыва строки используется косая черта.
```swift
let softWrappedQuotation = """
    The White Rabbit put on his spectacles.  "Where shall I begin, \  
    please your Majesty?" he asked.

    "Begin at the beginning," the King said gravely, "and go on \
    till you come to the end; then stop."
"""
```
Пробел перед первыми кавычками сообщает Swift, какие пробелы игнорировать перед всеми другими строками: 

<img src="https://docs.swift.org/swift-book/_images/multilineStringWhitespace_2x.png" width="600">


*Swift’s String type is a value type.*

Значение строки не будет изменено (напр. при передаче строки функции), пока Вы сами его не измените. 

Разница между строками и подстроками заключается в том, что для оптимизации производительности подстрока может повторно использовать часть памяти, которая использовалась для хранения исходной строки. Когда строка создается из подстроки, у нее есть собственное хранилище.

<img src="https://docs.swift.org/swift-book/_images/stringSubstring_2x.png" width="400">











