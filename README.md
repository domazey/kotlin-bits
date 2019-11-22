# Kotlin Bits
Community project for Kotlin language that provides development improvements.

## 1. Boolean operations ##

### 1.1 Convert boolean expression: `true -> Unit`, `false -> null` ###

```kotlin
fun Boolean.asUnit(): Unit? = if(this) Unit else null
```

### 1.2 Check if nullable `Boolean` is `true` or `false` ###

```kotlin
val Boolean?.isTrue get() = this == true
val Boolean?.isFalse get() = !isTrue
```

## 2. Nullability ##

### 2.1 Multi-argument version of `let` method ###

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
