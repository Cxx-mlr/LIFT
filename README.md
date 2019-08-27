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

void c_out() { std::cout << " hello `c_out` "; }

int main() {
    auto function = LIFT([] { std::cout << " hello `lambda` "; });
    function();

    auto copy = LIFT(function);
    copy();
}
```
