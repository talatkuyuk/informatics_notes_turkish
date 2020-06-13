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

fun main() {
    val num = 3
    if (num > 4) {
        println("The variable is greater than 4")
    } else {
        println("The variable is less than 4")
    }
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

### class
```kotlin
class Dice {
    var sides = 6
    fun roll1() {
        val randomNumber = (1..6).random()
        println(randomNumber)
    }
    fun roll2(): Int {
        val randomNumber = (1..sides).random()
        return randomNumber
    }
}

fun main() {
    val myFirstDice = Dice()
    println(myFirstDice.sides)
    myFirstDice.roll1()
    myFirstDice.sides = 10;
    val diceRoll = myFirstDice.roll2()
    println("Your ${myFirstDice.sides} sided dice rolled ${diceRoll}!")
}


fun main() {
    val myFirstDice = Dice(6)
    val diceRoll = myFirstDice.roll()
    println("Your ${myFirstDice.numSides} sided dice rolled ${diceRoll}!")
    
    val mySecondDice = Dice(20)
    println("Your ${mySecondDice.numSides} sided dice rolled ${mySecondDice.roll()}!")
}

class Dice (val numSides: Int) {

    fun roll(): Int {
        val randomNumber = (1..numSides).random()
        return randomNumber
    }

    fun roll(): Int {
    return (1..numSides).random()
}
}

```

```
- Almost everything you see on the screen of your app is a *View*.
- A *TextView* is a UI element for displaying text in your app.
- A *ConstraintLayout* is a container for other UI elements.
- Views need to be constrained horizontally and vertically within a ConstraintLayout.
- One way to position a View is with a *margin*.
- The *Resource Manager* in Android Studio helps you add and organize your images and other resources.
- An *ImageView* is a UI element for displaying images in your app.
- *ImageViews* should have a **content description** to help make your app more accessible.
- Text should be extracted into a **string resource** to make it easier to translate your app into other languages.
- Call the random() function on an IntRange to generate a random number: (1..6).random()
- Resource IDs are of the form R.<type>.<name>; for example, R.string.roll. For View IDs, the <type> is id, for example, R.id.button.
- When it assigns an object to a variable, Kotlin doesn't copy the entire object each time, it saves a reference to the object. You can think of a reference as being like a Social Security number or other national ID number: the number refers to a person, but it isn't the person itself. When you copy the number, you don't copy the person.
- If enabling auto imports didn't work, Button will be highlighted in red. You can manually add the correct import by putting the text cursor within the word Button, then pressing Alt+Enter (Option+Enter on a Mac).
- Use setImageResource() to change the image that's displayed in an ImageView
- 
```

[kotlin vocabulary](https://codelabs.developers.google.com/codelabs/basic-android-kotlin-training-vocab/)

They are the same. Kotlin interpret firs as second.
```kotlin
val diceRange = 1..6
val diceRange: IntRange = 1..6
val randomNumber = diceRange.random()
println("Random number: ${randomNumber}")
```

[Kotlin Style Guide for Android Developers](https://developer.android.com/kotlin/style-guide)

General form of if-else:
```kotlin
if (condition-is-true) {

execute-this-code

} else if (condition-is-true) {

execute-this-code

} else {

execute-this-code

}
```

```kotlin
When statement:

when (variable) {

matches-value -> execute-this-code

matches-value -> execute-this-code

...

}
```


