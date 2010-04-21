# Object manager

## Information

A JavaScript library that handles serialization and deserialization of objects,
preserving reference integrity. Ideal for storing a complex data structure as
JSON.

## Example

    var a = {aString: 'hello', aNumber: 12.3, aBool: true,
             anArray: [1, 2, [3, 4]], anObject: {anotherObject: {
             hello: 'world', iAm: 1337}}},
        b = {referenceToArray: a.anArray, referenceToA: a,
             referenceToSubObject: a.anObject.anotherObject,
             anotherString: 'weeee'},
        c = {references: [a, b]},
        d = [a, b, c];

    // Create an ObjectManager instance and register variables a, b, c and
    // d.
    var manager = new ObjectManager();
    manager.register(a, 'a');
    manager.register(b, 'b');
    manager.register(c, 'c');
    manager.register(d, 'd');

    // Serialize and deserialize the registered objects.
    var serialized = manager.serialize();
    var deserialized = ObjectManager.deserialize(serialized);

    // (Support for the console object required)
    // Shows the instances before and after serialization as well as the
    // serialized version of the data.
    console.log({
        before: [a, b, c, d],
        intermediate: serialized,
        after: [deserialized.get('a'), deserialized.get('b'),
                deserialized.get('c'), deserialized.get('d')]
    });

The above example is probably not a practical use case. In a real project, you
would probably convert the result of `manager.serialize()` to JSON, store it
somewhere, then later retrieve it and parse it, and call
`ObjectManager.deserialize(...)` with the resulting object.

## MIT license

This project is licensed under an MIT license.  
<http://www.opensource.org/licenses/mit-license.php>

Copyright (c) 2009-2010 Andreas Blixt <andreas@blixt.org>
