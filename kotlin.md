# Kotlin Notları

### comment line
```kotlin
// This a a comment.

```

### print
```kotlin
println("Happy Birthday, Rover!")
println("You are already ${age}!")

```

### variables
```kotlin
val age = 5   // set once
var age = 5   // can change later

```
> val: A variable declared as val can only be set once and not changeable.
> var: You can declare a changeable variable with the var keyword.

### function
```kotlin
fun main() {}

fun printBorder() {
    repeat(23) {
        print("=")
    }
    println()
}

fun printBorder(border: String, timesToRepeat: Int) {
    repeat(timesToRepeat) {
        print(border)
    }
    println()
}
```

> A repeat() inside another repeat(), creating what's called a "nested loop".

```kotlin
fun printCakeBottom(age: Int, layers: Int) {
    repeat(layers) {
        repeat(age + 2) {
            print("@")
        }
        println()
    }    
}
```


```
The Layout Editor helps you create the UI for your Android app.
Almost everything you see on the screen of your app is a View.
A TextView is a UI element for displaying text in your app.
A ConstraintLayout is a container for other UI elements.
Views need to be constrained horizontally and vertically within a ConstraintLayout.
One way to position a View is with a margin.
A margin says how far a View is from an edge of the container it's in.
You can set attributes on a TextView like the font, text size, and color.
```
