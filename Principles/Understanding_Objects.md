Understanding Objects

[[Name]] internal operation syntax.

Defining Properties
	[[Put]] method => Creates a new property and adds the value.
	[[Set]] method => Changes an existing property value

Detecting Properties
	in operator => checks for a property, both own properties and prototype properties, with a given name and returns true if it finds it. 
	hasOwnProperty => returns true only if the given property exists and is an own property.

Removing Properties
	delete operator => remove a property from an object.

Enumeration
By default, all properties that you add to an object are enumerable. Enumerable properties have their internal [[Enumerable]] attributes set to true. Most of the native methods on objects have their [[Enumerable]] attribute set to false, and own properties are set as enumerable by default.
	for-in loop => enumerates all enumerable properties on an object, both prototype properties and own properties, assigning the property name to a variable. 
	Object.keys() => returns and array with the own (instance) properties names.

Types of Properties
	Data properties contain a value. The default behavior of the [[Put]] method is to create a data property.
	Accessor properties don’t contain a value but instead define a function to call when the property is read (called a getter), and a function to call when the property is written to (called a setter). Accessor properties only require either a getter or a setter, though they can have both.

Property Attributes
Common Attributes
There are two property attributes shared between data and accessor properties. 
	[[Enumerable]] => determines whether you can iterate over the property.
	[[Configurable]] => determines whether the property can be changed.

Data Property Attributes
Data properties possess two additional attributes that accessors do not. 
	[[Value]] => holds the property value.
	[[Writable]] => a Boolean value indicating whether the property can be written to.   In other words whether the value can change.

Accessor Property Attributes
Accessor properties also have two additional attributes.
	[[Get]] => contains the getter function.
	[[Set]] => contains the setter function.

Defining a Property

const person1 = {};

// data property to store data
Object.defineProperty(person1, "_name", {
	value: "Nicholas",
	enumerable: true,
	configurable: true,
	writable: true
});

// accessor property
Object.defineProperty(person1, "name", {
		get: function() {
			console.log("Reading name");
			return this._name;
		},
		set: function(value) {
			console.log("Setting name to %s", value);
			this._name = value;
		},
		enumerable: true,
		configurable: true
		}
});

Defining Multiple Properties
Object.defineProperties(person1, {
	// data property to store data
	_name: {
		value: "Nicholas",
		enumerable: true,
		configurable: true,
		writable: true
	},
	// accessor property
	name: {
		get: function() {
			console.log("Reading name");
			return this._name;
		},
          set: function(value) {
			console.log("Setting name to %s", value);
			this._name = value;
		},
		enumerable: true,
		configurable: true
		}
});

When you are defining a new property with Object.defineProperty() and Object.defineProperties(), it’s important to specify all of the attributes because Boolean attributes automatically default to false otherwise.

Retrieving Property Attributes
Fetch property attributes, by using Object.getOwnPropertyDescriptor(). This method accepts two arguments: the object to work on and the property name to retrieve. If the property exists, you should receive a descriptor object with four properties: configurable, enumerable, and the two others appropriate for the type of property.

Preventing Object Modification
Objects have internal attributes that govern their behavior. 

	[[Extensible]] attribute => a Boolean value indicating if the object itself can be modified. 

Objects are extensible by default.

Preventing Extensions using Object.preventExtensions()
	The [[Extensible]] attribute is set to false.
	Once you use this method on an object, you’ll never be able to add any new properties to it again. 
	You can check the value of [[Extensible]] by using Object.isExtensible()

Sealing Objects using Object.seal()
	Not only can you not add new properties to the object, but you also can’t remove properties or change their type (from data to accessor or vice versa). If an object is sealed, you can only read from and write to its properties
	The [[Extensible]] attribute is set to false, and all properties have their [[Configurable]] attribute set to false.
	You can check to see whether an object is sealed using Object.isSealed().

Freezing Objects using Object.freeze() 
	 A frozen object is a sealed object where data properties are also read-only.
	Frozen objects can’t become unfrozen.
	You can check to see whether an object is frozen by using Object.isFrozen().

