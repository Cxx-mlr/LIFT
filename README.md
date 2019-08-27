# LIFT

```cpp
#include <utility>

#define LIFT(X) [](auto&&... args)\
    noexcept(noexcept(overload(std::forward <decltype(args)>(args)...)))\
        -> decltype(overload(std::forward <decltype(args)>(args)...)) { return overload(std::forward <decltype(args)>(args)...); }

void overload(int) { puts("int"); };
void overload(float) { puts("float"); }
void overload(double) { puts("double"); }

int main() {
    auto function = LIFT(overload);
    
    function(0);
    function(0.);
    function(0.f);
}
```

- msvc -> std:c++latest
- clang
- gcc
