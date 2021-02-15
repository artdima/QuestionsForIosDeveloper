## The algorithms

### Сортировки
- [Сортировка вставкой](#Сортировка-вставкой)
- [Сортировка выбором](#Сортировка-выбором)
- [Quicksort(Быстрая сортировка)](#Quicksort)

### Поиск
- [Бинарный поиск](#Бинарный-поиск)

### Структуры данных
- [Стэк](#Стэк)

### Алгоритмы
- [Палиндромы](#Палиндромы)

### Сортировка вставкой
swapAt(_:_:) - обменивает значения по указанным индексам коллекции.
```swift
func insertionSort(_ array: [Int]) -> [Int] {
    var a = array			 // 1
    for x in 1..<a.count {		 // 2
        var y = x
        while y > 0 && a[y] < a[y - 1] { // 3
            a.swapAt(y - 1, y)
            y -= 1
        }
    }
    return a
}
```

### Сортировка выбором
Работает медленно - O(n^2)
```swift
func selectionSort(_ array: [Int]) -> [Int] {
  guard array.count > 1 else { return array }  // 1

  var a = array                    // 2

  for x in 0 ..< a.count - 1 {     // 3

    var lowest = x
    for y in x + 1 ..< a.count {   // 4
      if a[y] < a[lowest] {
        lowest = y
      }
    }

    if x != lowest {               // 5
      swap(&a[x], &a[lowest])
    }
  }
  return a
}
```

### Quicksort(Быстрая сортировка)
Quicksort-один из самых известных алгоритмов в истории. Он был изобретен в далеком 1959 году Тони Хоаром, в то время, когда рекурсия была еще довольно туманным понятием.
```swift
func quicksort<T: Comparable>(_ a: [T]) -> [T] {
  guard a.count > 1 else { return a }

  let pivot = a[a.count/2]
  let less = a.filter { $0 < pivot }
  let equal = a.filter { $0 == pivot }
  let greater = a.filter { $0 > pivot }

  return quicksort(less) + equal + quicksort(greater)
}
```

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

