```c++
#include<iostream>
using namespace std;

template <typename T>
class smart_ptr
{
    T *ptr;
    
    public:
    smart_ptr()=default;
    smart_ptr(T *in_ptr)
    {
        ptr = in_ptr;
    }
    smart_ptr(const smart_ptr<T> &in_ptr)
    {
        ptr = new T;
        *ptr = *in_ptr.ptr;
        cout<<"user def con\n";
    }
    smart_ptr &operator=(const smart_ptr &rhs)
    {
        if(this != &rhs)
        {
            *ptr = *rhs.ptr;
        }
        cout<<"user def assign\n";
        return *this;
    }
    T &operator*()
    {
        return *ptr;
    }
    T *operator->()
    {
        return ptr;
    }
};

int main()
{
    // 1. Should work with primitive data types
    smart_ptr<int> i_ptr(new int);

    *i_ptr = 5;

    cout << *i_ptr << endl;

    // 2. Should work with class & struct
    struct test
    {
        int var;
        test() { cout << "C\n"; }
        ~test() { cout << "D\n"; }
    };

    smart_ptr<test> t_ptr(new test);

    t_ptr->var = 10;

    cout << t_ptr->var << endl;

    // 3. Copy construction
    auto ptr = i_ptr;

    cout << *ptr << endl;

    // 4. Assignment chain
    i_ptr = i_ptr = i_ptr;
    return 0;
}
```
