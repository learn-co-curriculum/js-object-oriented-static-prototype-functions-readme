# Static Prototype Functions

## Objectives

1. The Difference between Instance Functions and Static Functions
2. Defining a Static Prototype Function
3. Build a Batch Constructor

### Prototype Functions

We learned that a function can act as a constructor to create instances of itself based on a prototype.

```js
function User(name, email){
  this.name = name
  this.email = email
}

let sarah = new User("Sarah", "sarah@flatironschool.com")
sarah.constructor //= > [Function: User]
```

The instance of the `User` `sarah` has the constructor of `User`. This is how javascript prototypes works where the `User` function is acting as a blueprint and a factory for all users in our program.

We tend to keep the constructor function for a prototype simple, requiring only the most common and neccessary arguments and logic to create a functioning instance of itself.

How might we implement the ability to create many users at once, known as a batch creation? You can imagine the logic required, given an array of raw data for users, we would want to iterate through it and create a user and return them all.

```js
function User(name, email){
  this.name = name
  this.email = email
}

const data = [
  ["Avi", "avi@flatironschool.com"],
  ["Grace", "grace@hopper.com"],
  ["Alan", "alan@xparc.com"]
]

// Iterate over all the users and collect new users instances
let users = data.map(function(userData){
  return new User(userData[0], userData[1])
})

users //=> [ User { name: 'Avi', email: 'avi@flatironschool.com' },
    //     User { name: 'Grace', email: 'grace@hopper.com' },
    //     User { name: 'Alan', email: 'alan@xparc.com' } ]
```

That works great, but how might we add that logic to the `User` function and properly encapsulate the behavoir within? Wouldn't it be great if we could simply say: `User.BatchCreate([["Grace", "grace@hopper.com"], ["Alan", "alan@xparc.com"]])`. We can, we just need to attach the `BatchCreate` function to the `User` object.

### Static Prototype Function

Because `User` is a function it can have properties like any other object in Javascript. To attach a function to it as a property, we can declare it

```js
function User(name, email){
  this.name = name
  this.email = email
}

User.BatchCreate = function(data){
  return data.map(function(userData){
    return new User(userData[0], userData[1])
  })
}

const data = [
  ["Avi", "avi@flatironschool.com"],
  ["Grace", "grace@hopper.com"],
  ["Alan", "alan@xparc.com"]
]

let users = User.BatchCreate(data)

users //=> [ User { name: 'Avi', email: 'avi@flatironschool.com' },
    //     User { name: 'Grace', email: 'grace@hopper.com' },
    //     User { name: 'Alan', email: 'alan@xparc.com' } ]
```

Functions attached directly to the main function we are using as a class are called static functions or class functions. They can provide a lot of useful behavoir that relates to the class in general rather than instances, such as advanced constructors, like a batch create demonstrated above, finders, and more.

## Resources

* [Factory Functions vs Constructor Functions](https://medium.com/javascript-scene/javascript-factory-functions-vs-constructor-functions-vs-classes-2f22ceddf33e)