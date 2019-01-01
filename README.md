# Competitive C++ Manifesto: A Style Guide


There are many style guides for C++ out there, but we can't really use them as competitive programmers. We just want to write our code correctly as fast as possible! Trying to hack people here on codeforces, I realized there is a need for a style guide! Our goal is to write correct, fast, clear and consistent code.

> #### Disclaimer
> This is not a rulebook. You can integrate parts of it into your coding style. 
> Don't overthink it, especially during a contest!

I'm going to use this guide for myself and to [teach my students](https://in.harbour.space/computer-science/modern-c-programming-hossein-yousefi/). I'm planning to make some good stuff in the future following these principles! Stay tuned!

## Compiler
Make use of C++17. Use `-Wall -Wextra -Wshadow` flags for compilation, and try to eliminate all of the warning messages, this will prevent you from having some silly bugs.

## Naming
C++ libraries use snake_case for functions and classes, in order to differentiate the user-defined code from the standard library, we will use CamelCase.

* Types use UpperCamelCase: `Point`, `SegTree`
* Functions and variables use lowerCamelCase: `someMethod`, `someVariable`
* Macros and constants use all capital letters seperated by `_`: `SOME_MACRO`, `MAX_N`, `MOD`
* Use meaningful names or at least meaningful enough for you.

###### Example
```c++
#define LOCAL
const double PI = 3.14;

struct MyPoint {
    int x, y;
    bool someProperty;
    
    int someMethod() {
        return someProperty ? x : y;
    }
};
```

> #### Note
> Using snake_case is fine, but be consistent!

## Comments
In competitive programming, you usually don't want to write long comments, but in case you do want to write some comments, write them using `//` instead of `/* */`. Using `//` enables you to comment out a chunk of code with `/* */` while debugging, and `/* /* ... */ */` is a bug!

###### Example
```c++
/* commenting out a block of code - no problem!
 
// some comment about the function below...
void someFunction() {
    // do something
}

*/
```

## Spacing

> Control flow statements are `if / else / for / while / ...`

* Indent using 2 or 4 spaces uniformly. Avoid using tabs since it might make the code stretched out in different websites (e.g. *Codeforces*) and also in print (e.g. *ICPC*). Set your editor to emit spaces when you hit the tab key.
* Braces always open on the same line but close on a new line.
* Preferably always use braces for control flow statement blocks even if it's **currently** only one line.
* `else` should start on the same line after closing brace of `if` block.
* Keep lines a reasonable length, some say 80 columns!
* There should be exactly one blank line between methods. This helps you to organize your code better.
* There should be no blank line after an opening brace or before a closing brace.
* Binary operations should be spaced from both sides.
* Unary operations should **only** be spaced from the left side.
* Brackets `<> [] {}` are a part of their identifier like `a[5]`, `vector<int>` or `pair{1, 2}`.
* Parentheses should **only** be spaced from outside like `(-a[3] + b) * (c + d)`.
* Semicolons and commas should **only** be spaced from the right side.
* Question marks and colons should be spaced from both sides (unlike English!). The only exceptions are labels like `public:` or switch cases `case 10:`.
* There should not be any extra spaces at the end of each line.
* Add a single newline character at the end of the file.
* There should be exactly one space after control flow statements like `if (flag)`.
* In contrast to control flow statements, function calls should not be spaced like `func(arg)`.
* Preprocess statements should be written like `#define SOME_MACRO` and `#include <iostream>`.
* Templates should be written like `template <typename T>` and a new line.
* Scope resolution operator `::` is a part of the identifier and should not be spaced.
* Pointer and reference are a part of the type, space accordingly! Like `int* ptr` and `const string& str`. To avoid bugs, declare only one pointer per line.
* `.` and `->` operator should not be spaced. When `->` is used to show return type (like in lambda expressions) it should be spaced from both sides.
* Lambda expressions should be written like `[](int x) -> int { return x + 1; }`. The return type can be omitted most of the times. Feel free to expand the body exactly like a function if it has more than 1 line of code.
* When overloading operators, treat them like functions, no spacing in the name like `bool operator!();`
* Ellipsis `...` should **only** be spaced from the left side.

###### Example
```c++
#include <bits/stdc++.h>

using namespace std;

const int DIFF = 10;

template <typename T>
struct Point {
    T x, y;
    
    Point(T _x, T _y) : x(_x), y(_y) {}
    
    friend ostream& operator<<(ostream& os, const Point& p) {
        return os << "(" << p.x << ", " << p.y << ")";
    }
};

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);
    vector<Point<int>> v;
    for (int i = 0; i < 5; ++i) {
        v.push_back({i, i + DIFF});
    }
    for (auto p : v) {
        if (p.x + DIFF == p.y) {
            cout << p << '\n';
        } else {
            cout << "huh!?\n"; // will never get printed!
        }
    }
}
```

###### Output

```
(0, 10)
(1, 11)
(2, 12)
(3, 13)
(4, 14)
```
## Competitive Coding Recommendations

* Use `#include <bits/stdc++.h>` instead of many includes. 
* Use `using namespace std;` instead of typing `std::` every time.
* Use `using` instead of `typedef`, for example `using ll = long long;`. *Rationale: It's more consistent with the style of modern C++.*
* Use `struct` instead of `class`.
*Rationale: It defaults to public, and you don't need encapsulation in competitive programming!*
* Don't use too many macros but don't be afraid of using macros!
*Rationale: It's not easy to debug and read a code full of ugly macros. but we're hackers after all!*
* Use `const` for defining a constant instead of `#define`.
*Rationale: consts have a type, and they are evaluated at compile time.*
* To avoid bugs, you can use curly braces for each case of `switch` statement.
* Use `auto` to increase readability and decrease code size.
* Use braced initializer lists.
* Use `emplace` and `emplace_back` for containers when dealing with pairs and tuples.
*Rationale: `(elem1, elem2, ...)` instead of `({elem1, elem2, ...})`.*
* Use lambda functions! They're especially useful when passing functions as arguments like in `sort`. **Don't repeat yourself**, use lambda functions in your code instead of copy/pasting.
* Use `nullptr` instead of `NULL` or `0`.
* Boolean values are `true` and `false`!
* Use `ios::sync_with_stdio(false);` and `cin.tie(nullptr);` for a faster I/O using `cin/cout`.
* Use builtin functions starting with `__builtin`.
* GCD and LCM are available in C++ under `gcd` and `lcm`.
* Use C++11 for-each style for loops `for (auto& elem : vec)`.
* Use C++17 binding style like `for (auto& [key, val] : dic)` and `auto [x, y] = myPoint;`
* Use C++17 template argument deduction `pair p{1, 2.5};` instead of `pair<int, double> p{1, 2.5};`.
* If you have a lot of nested loops and conditions, refactor! You probably should be using functions.
* Never use `goto`! But be brave enough to use `goto` when you want to break from several nested loops (in case you just can't refactor it)!
* Some websites like codeforces use the flag `-DONLINE_JUDGE` to compile your code, this means that you can remove your `cerr`s or your debug functions automatically or redirect input/output to file instead of stdin/stdout, etc.

```c++
#ifdef ONLINE_JUDGE
#define cerr if (false) cerr
#endif 
// Alternatively this can be done using a local -DLOCAL flag
// when compiling on your machine, and using #ifndef LOCAL instead.
```

* Prefer using normal operators like `!, &&, ||, ^, ...` instead of their alternative representations `not, and, or, xor, ...`.
*Rationale: We're not coding in python!*
* Break down your code into different smaller functions. Your code will be cleaner and easier to debug.
* **Don't try to be too clever!**
* **Don't reinvent the wheel!** &mdash; *Make use of standard library!*
* **Use common sense and be consistent!**

## Read more
* [Stroustrup: C++](http://www.stroustrup.com/C++.html) by Bjarne Stroustrup
* [C++11 for programming contests...](https://codeforces.com/blog/entry/10124) by [user:mukel]
* [C++ Tricks](https://codeforces.com/blog/entry/15643) by [user:Swift]
* [C++17, competitive programming edition](https://codeforces.com/blog/entry/57729) by [user:Igorjan94]

## Contribution
Any suggestions are welcome. You can contribute to this post by commenting or [using GitHub](https://github.com/HosseinYousefi/CompetitiveCPPManifesto).
