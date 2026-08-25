
# Kotlin Regex — Interview Quick Notes

## 1. What is Regex?

**Regex (Regular Expression)** is a pattern used to search, validate, extract, split, or replace text.
```kotlin
val regex = Regex("""\d+""")
```

Prefer Kotlin's `""" """` raw strings for Regex because you don't need extra escaping.

---

## 2. Basic Patterns

|Pattern|Meaning|
|---|---|
|`.`|Any character|
|`\d`|Digit `0-9`|
|`\D`|Not a digit|
|`\w`|Letter, digit or `_`|
|`\W`|Not a word character|
|`\s`|Whitespace|
|`\S`|Not whitespace|
|`[abc]`|a, b or c|
|`[a-z]`|Lowercase letter|
|`[A-Z]`|Uppercase letter|
|`[0-9]`|Digit|
|`[^0-9]`|Anything except digit|

---

fun main() {

    // 1. Check only digits
    val number = "12345"
    println(
        Regex("""^\d+$""").matches(number)
    )
    // true


    // 2. Extract all numbers
    val text = "Product 12 costs 500 and quantity is 3"

    val numbers = Regex("""\d+""")
        .findAll(text)
        .map { it.value }
        .toList()

    println(numbers)
    // [12, 500, 3]


    // 3. Remove special characters
    val input = "Hello@#123!"

    val cleaned = input.replace(
        Regex("""[^a-zA-Z0-9]"""),
        ""
    )

    println(cleaned)
    // Hello123


    // 4. Replace multiple spaces with one
    val sentence = "Hello    Kotlin   World"

    val normalized = sentence.replace(
        Regex("""\s+"""),
        " "
    )

    println(normalized)
    // Hello Kotlin World


    // 5. Validate exactly 6 digits
    val otp = "123456"

    println(
        Regex("""^\d{6}$""").matches(otp)
    )
    // true


    // 6. Validate username
    // Starts with letter
    // Only letters/numbers
    // Total length: 5-12

    val username = "yogendra123"

    val validUsername = Regex(
        """^[a-zA-Z][a-zA-Z0-9]{4,11}$"""
    ).matches(username)

    println(validUsername)
    // true


    // 7. Split by comma OR semicolon
    val languages = "Java,Kotlin;Python,Swift"

    val result = languages.split(
        Regex("""[,;]""")
    )

    println(result)
    // [Java, Kotlin, Python, Swift]


    // 8. Extract groups
    val date = "2026-08-14"

    val dateRegex = Regex(
        """(\d{4})-(\d{2})-(\d{2})"""
    )

    val match = dateRegex.find(date)

    println(match?.groupValues?.get(1)) // 2026
    println(match?.groupValues?.get(2)) // 08
    println(match?.groupValues?.get(3)) // 14
}