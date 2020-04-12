```c++
#include <iostream>

class Square
{
    uint32_t m_side{0};
    Square(uint32_t s) : m_side{s} {}

public:
    uint32_t area()
    {
        return m_side * m_side;
    }

    friend std::ostream &operator<<(std::ostream &os,  Square &input);
    friend class SquareFactory;
};

std::ostream &operator<<(std::ostream &os,  Square &input)
{
    os << input.area();
    return os;
}


class SquareFactory
{
public:
     static Square create(uint32_t s)
    {
        return {s};
    }
};

int main()
{
    // Following statement should give compilation error
    // Square object should not be allowed to create directly
    // Rather it should be created using SquareFactory
   // Square s1(5); // Comment once give compilation error

    auto s2 = SquareFactory::create(5);
    std::cout << s2.area() << std::endl;
    std::cout << s2 << std::endl;

    return 0;
}
```
