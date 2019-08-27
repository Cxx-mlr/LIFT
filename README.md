# LIFT

```cpp
#include <iostream>
#include <utility>

template <class type>
struct Wrapper
{
    private:
        const type ptr_B;

    public:
        constexpr Wrapper(type ptr_f) : ptr_B(ptr_f) {}

        template <class... types>
        constexpr auto operator()(types&& ... args) const noexcept(noexcept(ptr_B( std::forward <types>(args)...))) -> decltype(ptr_B(std::forward <types>(args)...)) {
            return ptr_B( std::forward <types>(args)... );
        }
};

#define LIFT(X) Wrapper{X}

void c_out(int r) { std::cout << " hello `c_out` " << r << ' '; }

int sum(int x, int y) {
    return x + y;
}

int main() {
    auto lambda = LIFT([] { std::cout << " hello `lambda` "; });
    lambda(); // hello `lambda`

    auto copy = LIFT(lambda);
    copy(); // hello `lambda`
    
    auto function = LIFT(c_out);
    function(sum(3, 6)); // hello `c_out` 9
}
```

- msvc -> std:c++latest
- clang
- gcc
