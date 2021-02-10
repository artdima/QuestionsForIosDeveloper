## The algorithms

### Бинарный поиск
Бинарный поиск производится в упорядоченном массиве. При бинарном поиске искомый ключ сравнивается с ключом среднего элемента в массиве. Если они равны, то поиск успешен. В противном случае поиск осуществляется аналогично в левой или правой частях массива.
```swift
func binarySearch<T: Comparable>(_ a: [T], key: T, range: Range<Int>) -> Int? {
    if range.lowerBound >= range.upperBound {
        return nil
    } else {
        let midIndex = range.lowerBound + (range.upperBound - range.lowerBound) / 2
        if a[midIndex] > key {
            return binarySearch(a, key: key, range: range.lowerBound ..< midIndex)

        } else if a[midIndex] < key {
            return binarySearch(a, key: key, range: midIndex + 1 ..< range.upperBound)

        } else {
            return midIndex
        }
    }
}
```

### Стэк
Стек (от англ. stack — стопка) — структура данных, представляющая из себя упорядоченный набор элементов, в которой добавление новых элементов и удаление существующих производится с одного конца, называемого вершиной стека. Притом первым из стека удаляется элемент, который был помещен туда последним, то есть в стеке реализуется стратегия «последним вошел — первым вышел» (last-in, first-out — LIFO). 

```swift
public struct Stack<T> {
  fileprivate var array = [T]()

  public var isEmpty: Bool {
    return array.isEmpty
  }

  public var count: Int {
    return array.count
  }
  
  /// Добовляем элемент
  public mutating func push(_ element: T) {
    array.append(element)
  }
  
  /// Возвращает последний элемент и сразу удаляет его
  public mutating func pop() -> T? {
    return array.popLast()
  }
}
```

### Палиндромы
Палиндром - это слово или фраза, которые пишутся одинаково при чтении вперед или назад. 

```swift
func isPalindrome(_ str: String) -> Bool {
  let strippedString = str.replacingOccurrences(of: "\\W", with: "", options: .regularExpression, range: nil)
  let length = strippedString.characters.count

  if length > 1 {
    return palindrome(strippedString.lowercased(), left: 0, right: length - 1)
  }

  return false
}

private func palindrome(_ str: String, left: Int, right: Int) -> Bool {
  if left >= right {
    return true
  }

  let lhs = str[str.index(str.startIndex, offsetBy: left)]
  let rhs = str[str.index(str.startIndex, offsetBy: right)]

  if lhs != rhs {
    return false
  }

  return palindrome(str, left: left + 1, right: right - 1)
}
```

И простой вариант 
```swift
// Функция reversed: O(1)
if str == String(str.reversed()) {
    print("Палиндром")
} else {
    print("Нет")
}
```

