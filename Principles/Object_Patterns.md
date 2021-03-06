Object Patterns

Private and Privileged Members
All object properties in JavaScript are public, and there’s no explicit way to indicate that a property shouldn’t be accessed from outside a particular object. At some point, however, you might not want data to be public.

One way to avoid this is by using naming conventions. However, there are ways of hiding data that don’t rely on convention and are therefore more “bulletproof” in preventing the modification of private information.

The Module Pattern
The module pattern is an object-creation pattern designed to create singleton objects with private data. The basic approach is to use an IIFE that returns an object. That function expression can contain any number of local variables that aren’t accessible from outside that function. Because the returned object is defined within that function, the object’s methods have access to the data. Methods that access private data in this way are called privileged methods. You accomplish this by creating closure functions as object methods. The variables and functions that accesses those variables are declared within the IIFE.

Private Members for Constructors
You can use a pattern that’s similar to the module pattern inside the constructor to create instance-specific private data.

Mixins
There is also a type of pseudoinheritance accomplished through mixins. Mixins occur when one object acquires the properties of another without modifying the prototype chain. The first object (a receiver) actually receives the properties of the second object (the supplier) by copying those properties directly. This pattern is used frequently for adding new behaviors to JavaScript objects that already exist on other objects.

Scope-Safe Constructors
Many built-in constructors, such as Array and RegExp, also work without new because they are written to be scope safe. A scope-safe constructor can be called with or without new and returns the same type of object in either case.

When new is called with a function, the newly created object represented by this is already an instance of the custom type represented by the constructor. So you can use instanceof to determine whether new was used in the function call:

function Person(name) {
    if (this instanceof Person) {
        // called with "new"
    } else {
        // called without "new"
    }
}