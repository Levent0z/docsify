# Things to watch out for in C#

1. When using the `TPL` library, make sure that all `async` methods return a `Task` so that the caller has the ability to `await` on it.
2. When writing property getters, be careful with case sensitivity of the property name and the internal backing field in order to avoid an infinite recursion and stack overflow.
3. Avoid using `dynamic` types as they bypass the strong-typing and all of its compile-time benefits and incur runtime performance hits.
4. Use the facilities offered by the language, such as safe null-coalescing and null-conditional operators.
5. When `new`ing instances, make sure to check the metadata for `IDisposable` and, as applicable, use the `using` clause for automatic disposing of the generated classes even in the case of an exception.
6. Be knowledgeable about LINQ and use proper overloads.
7. Use OOP concepts wisely. Describe intent using the method modifiers `public`, `protected` and `private` appropriately, as well as the `readonly` keyword. 
8. For all public methods, check the validity of the argument.
9. Be consistent with error handling, use correct exception types.
10. Avoid catching generic exceptions as those can hide real programming errors.
11. Adopt a coding style (or your team's coding style) and stick to it for better readability and maintainability of the code.
12. When writing switch statements, consider the `default` case, even if it's not valid. For switches on enum values, having a default case that throws as applicable will future-proof the code in case more values are added to the enum.
13. Prefer `assert`, `debug`, or `trace` in place of comments wherever possible.
14. Don't implement your own data-structures when .Net provides one.
15. Avoid using of `tuple`s as your return type because it's not clear what `Item1` and `Item2` represent. Instead define a class. If you're using later versions of C#, methods can return multiple values, make use of that.
