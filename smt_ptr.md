```c++
#include <iostream>

template<typename T>
class smart_ptr
{
    T *ptr;

public:
    smart_ptr()=default;
    smart_ptr(T* in_ptr)
    {
         ptr = in_ptr;
    }
    smart_ptr(const smart_ptr &rhs)
    {
        ptr = new T;
        *ptr = *rhs.ptr;
        std::cout<<"user def copy construct\n";
    }
    smart_ptr &operator =(const smart_ptr &rhs)
    {
        if(this != &rhs)
        {
            *ptr=*rhs.ptr;
            std::cout << "user def assignment\n";
        }
        
        return *this;
    }
    T &operator *()
    {
        return *ptr;
    }
    T *operator ->()
    {
        return ptr;
    }

};

int main()
{
    // 1. Should work with primitive data types
    smart_ptr<int> i_ptr(new int);

    *i_ptr = 5;

    std::cout << *i_ptr << std::endl;

    // 2. Should work with class & struct
    struct test
    {
        int var;
        test() { std::cout << "C\n"; }
        ~test() { std::cout << "D\n"; }
    };

    smart_ptr<test> t_ptr(new test);

    t_ptr->var = 10;

    std::cout << t_ptr->var << std::endl;

    // 3. Copy construction
    auto ptr = i_ptr;

    std::cout << *ptr << std::endl;

    // 4. Assignment chain
    ptr = i_ptr = ptr;
    std::cout<<"ending the program\n";
    return 0;
}
```
