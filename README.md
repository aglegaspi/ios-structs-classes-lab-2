# Structs and Classes Lab - 2


## Question 1 √

Using the Room struct below, write code that demonstrates that it is a value type.

```swift
struct Room {
    let maxOccupancy: Int
    let length: Double
    let width: Double
}
ß
var myRoom = Room(maxOccupancy: 1, length: 20.5, width: 25.5)
myRoom.maxOccupancy
myRoom.length
myRoom.width
myRoom = Room(maxOccupancy: 2, length: 20.5, width: 25.5)
myRoom.maxOccupancy

let theirRoom = Room(maxOccupancy: 2, length: 30.7, width: 26.7)
theirRoom.maxOccupancy
theirRoom.length
theirRoom.width
```

## Question 2 √

Using the Bike class below, write code that demonstrates that it is a reference type.

```swift
class Bike {
    var wheelNumber = 2
    var hasBell = false
}

let myBike = Bike()
myBike.hasBell
myBike.wheelNumber
myBike.hasBell = true
myBike.hasBell
```

## Question 3 √

a. Given the Animal class below, create a Bird subclass with a new `canFly` property.

b. Override the printDescription method to have the instance of the Bird object print out its name and whether it can fly

c. Create a Robin subclass of Bird.  Its name should always be "Robin".

```swift
class Animal {
    var name: String = ""
    var printDescription: Void {
        print("I am an animal named \(name)")
    }
    init(name: String) {
        self.name = name
    }
}

class Bird: Animal {
    var canFly: Bool
    
    init(name: String, canFly: Bool) {
        self.canFly = canFly
        super.init(name: name)
    }
    
    override var printDescription: Void {
        if canFly {
            print("\(name) can fly.")
        } else {
            print("\(name) can't fly")
        }
    }
    
}

let uglyBird = Bird(name: "the Alexander", canFly: false)
uglyBird.printDescription
uglyBird.canFly

//Create a Robin subclass of Bird.  Its name should always be "Robin".

class Robin: Bird {
    
    override init(name: String, canFly: Bool) {
    super.init(name: "Robin", canFly: canFly)
    }
}

let newRobin = Robin(name: "Robin", canFly: true)

newRobin.name = "Hobin"
newRobin.name

let newRobin2 = Robin(name: "Jobin", canFly: true)
newRobin2.name

```

## Question 4 √

class Bike {
  let wheelNumber = 2
  let wheelWidth = 1.3
  var hasBell = true
  func ringBell() {
    if hasBell {
      print("Ring!")
    }
  }
}

a. Create a LoudBike subclass of Bike. When you call ringBell it should ring the bell in all caps.

b. Give LoudBike a new method called ringBell(times:) that rings the bell a given number of times

```swift
class Bike {
    let wheelNumber = 2
    let wheelWidth = 1.3
    var hasBell = true
    func ringBell() {
        if hasBell {
            print("Ring!")
        }
    }
}

class LoudBike: Bike {
    override func ringBell() {
        print("RING!")
    }
    func ringsBell(times: Int) {
        for _ in 1...times {
            ringBell()
        }
    }
}

var loudAssBike = LoudBike()
//loudAssBike.ringBell()
loudAssBike.ringsBell(times: 3)
```
## Question 5 √

```swift
class Shape {
    var name: String {
        return "This is a generic shape" }
    var area: Double {
        fatalError("Subclasses must override the area") }
    var perimeter: Double {
        fatalError("Subclasses must override the perimeter") }
}

//a. Given the Shape object above, create a subclass Square with a property sideLength with a default value of 5.

//b. Override the area and perimeter computed values so the return the area/perimeter of the square as appropriate

//c. Override the name property of Square so that it returns a String containing its name ("Square") and its area and perimeter

class Square: Shape {
    var sideLength: Double = 5
    
    override var area: Double {
        return sideLength * sideLength
    }
    override var perimeter: Double {
        return sideLength * 4.0
    }
    
    override var name: String {
        return "Square"
    }
}
let newSquare = Square()
print(newSquare.name)

//d. Create a class Rectangle that subclasses from Shape. Give it a width property with a default value of 6 and a height property with a default value of 4

//e. Override the name property of Rectangle so that it returns a String containing its name ("Rectangle") and its area and perimeter.

class Rectangle: Shape {
    var width:Double = 6
    var height:Double = 4
    
    override var area: Double {
        return width * height
    }
    override var perimeter: Double {
        return (width + height) * 2.0
    }
    
    override var name: String {
        return "Rectangle"
    }
}

let newRectangle = Rectangle()
print(newRectangle.name)


////f. (BONUS) What happens when you run the code below? Explain why.

var myShapes = [Shape]()

myShapes.append(Square())
myShapes.append(Rectangle())

for shape in myShapes {
    print("This is a \(shape.name) with an area of \(shape.area) and a perimeter of \(shape.perimeter)")
}

// When the code runs it runs through each element which is each instance/subclass of Shape (Square and Rectangle). Then prints the interpolation of each property value of each elements overwritten values.
```



## Question 6 √

a. Given the Point object below, complete the `distance` method so that it returns the distance between a given point.

The equation for the distance formula can be found [here](https://www.mathsisfun.com/algebra/distance-2-points.html) and is give by:

```swift
let horizontalDistance = pointOneXValue - pointTwoXValue
let verticalDistance = pointOneYValue - pointTwoYValue
let distanceBetweenTwoPoints = sqrt(horizontalDistance * horizontalDistance + verticalDistance * verticalDistance)
```

`sqrt` is a method in Swift that gives the square root.  Make sure to have `import Foundation` or `import UIKit` to use this method.

```swift
struct Point {
    let x: Double
    let y: Double
    
    func distance(to point: Point) -> Double {
        let horizontal = self.x - point.x
        let vertical = self.y - point.y
        return sqrt(horizontal * horizontal + vertical * vertical)
    }
}

print(pointOne.distance(to: pointTwo)) //Prints 14.142135623730951
```


b. Given the above Point object, and Circle object below, add a `contains` method that returns whether or not a given point is on the circle

c. Add another method to `Circle` that returns a random point on the circle


```swift
struct Circle {
    let radius: Double
    let center: Point
    func contains(_ point: Point) -> Bool {
        if center.distance(to: point) == radius {
            return true
        } else {
            return false
        }
    }
    
    func getRandomPoint() -> Point {
    
    let x: Double = Double.random(in: (0-radius)...radius)
    let y: Double = sqrt((radius * radius) - (x * x))
    return Point(x: x, y: y)
    //√(r^2) - (x^2)
    
    }
}

let pointOne = Point(x: 0, y: 0)
let circleOne = Circle(radius: 5, center: pointOne)
let pointTwo = Point(x: 5, y: 0)
let pointThree = Point(x: 4, y: 0)
let pointFour = Point(x: sqrt(12.5), y: sqrt(12.5))
circleOne.contains(pointTwo) //true
circleOne.contains(pointThree) // false
circleOne.contains(pointFour) //true
```


Hint: Given the radius of a circle and the x value of a point on the circle, the y value of the point is defined by:

```
√(r^2) - (x^2)
```

```swift
circleOne.contains(circleOne.getRandomPoint()) //Should always be true
```


## Question 7 √

```swift

//a. Create a struct called HangmanModel with 3 properties `targetWord: String`, `numberOfIncorrectGuesses: Int` and `guessedLetters: [Character]`.

//b. Add a method called `playerWon` that returns whether all of the characters in `targetWord` are in `guessedLetters`

//c. Add a method called `printDisplayVersionOfWord` that prints the `targetWord` replacing characters that are not in `guessedLetters` with "_"

struct HangmanModel {
    var targetWord: String
    var numberOfIncorrectGuesses: Int
    var guessedLetters: [Character]
    
    func playerWon() {
        var boolVales = [Bool]()
        
        for letter in targetWord {
            if guessedLetters.contains(letter) {
                boolVales.append(true)
            } else {
                boolVales.append(false)
            }
        }
        
        if boolVales.contains(false) {
            print(false)
        } else {
            print(true)
        }
    }
    
    func printDisplayVersionOfWord() {
        var display = ""
        
        for letter in targetWord {
            if guessedLetters.contains(letter) {
                display += String(letter)
            } else {
                display += "_"
            }
        }
        print(display)
    }
    
    //d. Add a method called `guess(_:)` that takes in a character as input, and updates `guessedLetters` and `numberOfIncorrectGuesses` as appropriate.
    
     mutating func guess(_ inputChar: Character) {
        guessedLetters.append(inputChar)
        
        if !targetWord.contains(inputChar) {
            numberOfIncorrectGuesses += 1
        }
        
        printDisplayVersionOfWord()
        playerWon()
        print(numberOfIncorrectGuesses)
    }
}

var model = HangmanModel(targetWord: "helli", numberOfIncorrectGuesses: 0, guessedLetters: ["h","e","l","l"])

//b)
model.targetWord = "hello"
model.guessedLetters = ["h","e","o","l"]
model.playerWon() //true

//c)
model.targetWord = "hello"
model.guessedLetters = ["h","l"]
model.printDisplayVersionOfWord()
//prints h_ll_

//d)
model.targetWord = "hello"
model.guess("h")
model.guess("a")
model.guessedLetters // ["h", "a"]
model.numberOfIncorrectGuesses // 1

//e. Have `guess(_:)` also print out the current display version of the word, the number of incorrect guesses and if the player has won.

model.guess("o")
```
