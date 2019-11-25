# Kotlin Bits
Community project for Kotlin language that provides development improvements.

# 1. General ##

## 1-1 Boolean operations ##

### 1-1.1 Convert boolean expression: `true -> Unit`, `false -> null` ###

```kotlin
fun Boolean.asUnit(): Unit? = if(this) Unit else null
```

### 1-1.2 Check if nullable `Boolean` is `true` or `false` ###

```kotlin
val Boolean?.isTrue get() = this == true
val Boolean?.isFalse get() = !isTrue
```

## 1-2 Nullability ##

### 1-2.1 Multi-argument version of `let` method ###

```kotlin
inline fun <R, A> letAll(a: A?, block: (A) -> R): R? =
  if (a != null) {
      block(a)
  } else null
```
```kotlin
inline fun <R, A, B> letAll(a: A?, b: B?, block: (A, B) -> R): R? =
  if (a != null && b != null) {
      block(a, b)
  } else null
```
```kotlin
inline fun <R, A, B, C> letAll(a: A?, b: B?, c: C?, block: (A, B, C) -> R): R? =
  if (a != null && b != null && c != null) {
      block(a, b, c)
  } else null
```
```kotlin
inline fun <R, A, B, C, D> letAll(a: A?, b: B?, c: C?, d: D?, block: (A, B, C, D) -> R): R? =
  if (a != null && b != null && c != null && d != null) {
      block(a, b, c, d)
  } else null
```
etc.

## 1-3 Collections ##

### 1-3.1 Perform `filterNotNull` on `Collection` with predicate ###

```kotlin
inline fun <reified T> Collection<T>.filterNotNull(crossinline predicate: (T) -> Any?): Collection<T> =
  filter { predicate(it) != null }
```

### 1-3.2 Perform `sumBy` on `Collection` for `Long`, `Float`, `Double` (missing from standard library) ###
```kotlin
inline fun <T> Iterable<T>.sumByLong(selector: (T) -> Long): Long {
  var sum: Long = 0
  for (element in this) {
    sum += selector(element)
  }
  return sum
}
```
```kotlin
inline fun <T> Iterable<T>.sumByFloat(selector: (T) -> Float): Float {
  var sum: Float = 0f
  for (element in this) {
    sum += selector(element)
  }
  return sum
}
```
```kotlin
inline fun <T> Iterable<T>.sumByDouble(selector: (T) -> Double): Double {
  var sum: Double = 0.0
  for (element in this) {
    sum += selector(element)
  }
  return sum
}
```

### 1-3.3 Find object of specific type in a `Collection` ###
```kotlin
  inline fun <reified T> List<*>.findIsInstance(): T? =
    filterIsInstance<T>().firstOrNull()
```
## 1-4. Numeric operations ##

### 1-4.1 Perform `round` function for `N` decimal places for `Double` ###

```kotlin
fun Double.round(decimals: Int): Double {
  var multiplier = 1.0
  repeat(decimals) { multiplier *= 10 }
  return round(this * multiplier) / multiplier
}
```


