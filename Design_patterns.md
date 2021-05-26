# **Design Patterns Used In JavaScript**

![JavaScript image](img1.png)
# **Introduction** 

**Design patterns** are advanced *object-oriented* solutions to commonly occurring software problems.

The **Design patterns** help us build upon the combined experience of many developers that came before us and ensure we structure our code in an optimized way, meeting the need of problems we're attempting to solve and gives common vocabulary used to describe solutions to our problems than describing the syntax and semantics of our code.

# What is Gang Of Four (GOF)?

In 1994, four authors _**Erich Gamma,**_ _**Richard Helm,**_ _**Ralph Johnson,**_ and _**John Vlissides**_ published a book titled _**Design Patterns - Elements of Reusable Object-Oriented Software**_ which initiated
the concept of Design Patterns in Software development.

The authors are collectively known as **Gang of Four (GOF)**.

The book can be found [here](https://books.google.co.in/books/about/Design_Patterns.html?id=6oHuKQe3TjQC&redir_esc=y).

# Benefits of using Design patterns
- **They are widely applicable.** You can solve a multitude of common problems with the generic templates that they provide.

- **They are reusable.** Other developers can easily build upon a design pattern. Since they aren’t tied to a specific problem, they can be reused throughout your code.

- **They solve problems elegantly.** Design patterns reduce the size of a codebase through optimized solutions. 

- **They are proven solutions.** The results are reliable and efficient. That is because they are  derived from the best practices of other experienced developers. You can be certain they’ll work when implemented. 

- **They eradicate the need to refactor code.** Design patterns are the most tested, optimal solution for a given problem, so it’s unlikely that you’ll need to refactor the code.

# Categories of Design patterns

Design patterns are divided into many categories, but the most common are **Creational**, **Structural**, and **Behavioral**.

## **1.Creational Pattern**
 These design patterns provide a way to create objects while hiding the creation logic, rather than instantiating objects directly using the "**new**" operator. This gives the program more flexibility in deciding which objects need to be created for a given use case.

Some of the popular design patterns in this category are :
- Constructor Pattern
- Singleton 
- Factory Method
- Builder 
- Prototype


## **2. Structural Design Patterns**
Structural patterns are concerned with object composition and typically identify simple ways to implement a relationship between different objects. This helps to ensure that when one part of a system changes, the entire structure doesn’t need to do the same.

Some of the popular design patterns in this category are :
- Adapter
- Bridge
- Composite
- Decorator
- Facade


## **3. Behavioral Design Patterns**
Behavioral design patterns are concerned with handling communications between two different objects in a system. They ensure that disparate parts of a system have synchronized information.

Some of the popular design patterns in this category are :
- Chain of responsibility
- Command
- Iterator
- Mediator
- Memento

### With this understanding of the categorization, let’s examine some JavaScript Creational design patterns.

## **1. The Constructor Pattern**
The Constructor Pattern is one of the most simple, popular, and modern JS design patterns.
As the name suggests the purpose of this pattern is to aid in the constructor creation.

The **Constructor pattern**, as the name defines, is a class-based pattern that uses the constructors present in the class to create specific types of objects.

A **Constructor** is a special method used to initialize a newly created object once the memory has been allocated to it.

### Example :

```
function Human(name, age, occupation)
{
    // Defining properties inside the constructor 
    // As well as initializing them inside the constructor
    this.name= name;
    this.age=age;
    this.occupation=occupation;

    //Defining a method inside the constructor function

    this.describe = function( )
    {
        console.log ( ‘ ${this.name} is a ${this.age} year old ${this.occupation} ‘);
    }   
}

// Creating  different objects using the Human constructor

var person= new Human(“Adam” , “23”, “Engineer”);
var newperson = new Human("Joe", "13","Painter");

// Callinng the describe function for the created objects
person.describe(); 
newperson.describe();
```
In the above example, the constructor function is defined and has the following properties
name, age, occupation, describe( ).

When a person object is created it will have its name, age, occupation properties set to the arguments passed to the constructor function and the describe( ) is invoked to display the contents.


## **2. The Singleton Pattern**
The Singleton pattern restricts the instantiation of a class to a single object. 

It creates a new instance of the class if one doesn’t exist and if existing already, it simply returns a reference to it. 

It is also known as the **Strict Pattern**.

A Singleton pattern solves two problems at a time
1. Guarantees that there is only a single instance of a class.
2. Provide a global access point to this instance.

A real-world example would be a single database object shared by different parts of the program. There is no need to create a new instance of a database when one is already existing.

### Example : 
```
//Singleton class
var Singleton = (function () 
{
    var instance;
    function createDBInstance() 
    {
        var object = new Object("I am the DataBase instance");
        return object;
    }

    return 
    {
        getDBInstance: function () 
        {
            if (!instance) 
            {
                instance = createDBInstance();
            }
            return instance;
        }
    };
}
)();

function run() 
{
    var instance1 = Singleton.getDBInstance();
    var instance2 = Singleton.getDBInstance();
}
run();

```
In the above example whenever we try to create an *instance* of the *DataBase*, the **Singleton** class checks whether an instance of the class is present or not. If present it returns the address of the instance, else it creates the object and then returns the address.

In any situation, only one instance of the object will be present.


## **3. Factory Pattern**
The Factory pattern provides a template that can be used to create objects. It is used in complex situations where the type of object required can vary and needs to be specified in each case.

It does not use the "*new* " keyword directly to instantiate objects; hence, it does not explicitly require the use of a constructor to create objects. Instead, it provides a generic interface that delegates the object creation responsibility to the corresponding sub-class.

Example : 
```
class CarFactory 
{
    constructor() 
    {
      this.createcar = function(type) 
        {
          let car;
          if (type === 'sedan')
          {
            car = new sedan();
          } 
          else if (type === 'sportscar')
          {
            car = new sportscar();
          } 
          else if (type === 'convertible')
          {
            car = new convertible();
          }
          return car;
        };
    }
}

// Creating objects
const CarFactory = new CarFactory();

const sedan = CarFactory.createcar('sedan');
const sportscar = CarFactory.createcar('sportscar');
const convertible = CarFactory.createcar('convertible');

```
In the above example, the basic functions of the cars are the same but they have different features and functions.

Here we are not directly creating the instance of the car using the *new* keyword. Rather a *CarFactory* object is used which creates the instance of the object according to the different cars(cases).

## **4. Builder Pattern**
A Builder pattern is a design pattern that lets us extract the object construction out of its class (its representation) so that it can be used for multiple different representations.

Builder pattern builds a complex object using simple objects by providing a step-by-step approach.

One advantage to using this pattern is that it lets us build objects with one operation on top of another where we don’t need to call all operations simultaneously, only the ones that are needed to produce a particular output.

Example : 
```
class Calculator 
{
    constructor(props)
    {
        this.result = 0 ;
    }

    add(number)
    {
        this.result = this.result + number ;
        return this ;
    }

    subtract(number)
    {
        this.result = this.result - number ;
        return this;
    }

    divide(number)
    {
        this.result = this.result / number ;
        return this;
    }

    multiply(number)
    {
        this.result = this.result * number ;
        return this;
    }
    compute()
    {
        return this.result;
    }
}

let calculator = new Calculator()
let result = calculator.add(5).subtract(1).divide(2).compute()
```

In the above example, the variables add, subtract, divide, multiply are extracted outside the constructor and they are initiated separately. Here the multiply variable is not initialized and it is automatically set to zero.

This instantiates a calculator and performs multiple operations on top of one another and finally computes something.

When we call the *new Calculator( )*, the result is instantiated with 0 and then any number of operations can be performed on top of it, to compute the final result.

## **5. Prototype Pattern**
JavaScript does not support classes in its native form like  *Java*.

Inheritance between objects is implemented using *Prototype-based* programming.

The Prototype object is used as a blueprint for each object the constructor creates.

The Prototype pattern creates new objects, but rather than creating non-initialized objects it returns objects that are initialized with values it copied from a prototype - or sample - object. The Prototype pattern is also referred to as the Properties pattern.

An example of where the Prototype pattern is useful is the initialization of business objects with values that match the default values in the database. The prototype object holds the default values that are copied over into a newly created business object.

```
var personPrototype = 
{
    sayHi: function() 
    {
        console.log("Hello, my name is " + this.name + ", and I am " + this.age);
    }
    sayBye: function() 
    {
        console.log("Bye Bye!");
    }
};

function Person(name, age) 
{
    name = name || "John Doe";
    age = age || 26;

    function constructorFunction(name, age) 
    {
        this.name = name;
        this.age = age;
    };

    constructorFunction.prototype = personPrototype;

    var instance = new constructorFunction(name, age);
    return instance;
}

var person1 = Person();
var person2 = Person("Bob", 38);

person1.sayHi();
// Prints out Hello, my name is John Doe, and I am 26
person2.sayHi();
// Prints out Hello, my name is Bob, and I am 38

```
In the above example whenever we create a *Person* object, correspondingly *PersonPrototype* object is also instantiated inside of it. Hence the functions of the *PersonPrototype* are inherited inside the Person class and we can perform actions using the functions.

## **Conclusion**
Here I have explained some of the  design patterns used in JavaScript.

While it’s important to know various design patterns, it’s also equally important  not to overuse them. Before using a design pattern, you should carefully consider if your problem fits that design pattern or not. 

To know if a pattern fits your problem, you should study the design pattern as well as the applications of that design pattern.


## **References**
- [JavaScript Design Patterns](https://www.dofactory.com/javascript/design-patterns)
- [The Comprehensive Guide to JavaScript Design Patterns](https://www.toptal.com/javascript/comprehensive-guide-javascript-design-patterns)
- [7 JavaScript Design Patterns Every developer should know](https://codesource.io/javascript-design-patterns/)
- [Acing the JavaScript Design Interview](https://www.educative.io/collection/page/5429798910296064/5725579815944192/5546411429986304)



