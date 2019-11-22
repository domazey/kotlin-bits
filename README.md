# Kotlin Bits
Community project for Kotlin language that provides many development improvements.

## 1. Boolean operations ##

### 1.1 Convert boolean expression: `true -> Unit`, `false -> null` ###

```kotlin
fun Boolean.asUnit(): Unit? = if(this) Unit else null
```

