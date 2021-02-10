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





