# The-case-for-protected-methods-in-Interfaces

What I'm going to present is, I believe, a significant improvement to the OOP capabilities of Kotlin by relaxing a harmful, overly restrictive limitation that prevent developers from expressing contracts.

In essence, Interfaces are a tool to enforce that classes implements a same API subset/module. This is a kind of contract programming.

It is useful to be able to express that a class implements an API as it allows many classes to have this API standardized and this apply *both* for class level APIs and public APIs.
However it is an unfortunate, cultural contingent limitation that such API must necessarily be public.
Standardizing a (partially) private API for many classes is extremelly useful as it allows for the following benefits:
1) Once the developper know the interface shape, he automatically knows its shape for all the classes that implements it, hence this helps to reduce cognitive overhead.
2) This enforce standardization/consistency which make audits easier and is less error prone (you only have to consider once the soundness of a function prototype)
3) It is more productive (the IDE can implement the interface methods instead of having to type them)
4) It is more refactorable, e.g you can rename/change types uniformly

In practice, this harmful limitation imply either one of four consequences:
scenario -> a developer wants to enforce an API contract for two or more classes. 
In the API contract, some methods are public but also,
some methods  should be protected but he currently can't express this. 
decision A: he choose to make that method public which allow him to move it in the interface. This is semantically wrong, unsafe security wise and reduce the signal to noise ratio on autocomplete (and this is even worse for a library).

decision B: he choose to exclude such methods from the interface which make it lose the crucial benefits specified above.

decision C: he determine that without those methods the interface doesn't make sense as a whole anymore semantically and therefore choose to delete the interface which reduce the quality of its program even more.

decision D: he workaround the problem by transforming its interface into an abstract class which is semantically inferior (in this case no need of implementations) and crucially prevents OOP design (no multiple inheritance is possible), this is not future proof at all and is often not even an option.

// doesn't a public method in an interface force the implementing class to also share that method with the rest of the world? If an interface is being used to make the internals of an API more modular it doesn't mean that suddenly the developer wants to expose its internals to the rest of the world. With this limitation a method that has an implementation and is intended to be package-protected (default) is forced to become public because of the interface it is complying to.

note: I can create a KEEP if needed.
