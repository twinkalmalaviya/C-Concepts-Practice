```c++
#include<iostream>
using namespace std;

struct test
{
public:
    static int static_var;
    int normal_var = 0;

    static void static_method()
    {
        static_var++;
      //  normal_var++;
        cout << "static_method called\n";
    }

    void normal_method()
    {
        static_var++;
        normal_var++;
        cout << "normal_method called\n";
    }

    test& call_chain_1()
    {
        static_var++;
        normal_var++;
        cout << "call_chain_1 called\n";
        return *this;
    }

    void call_chain_2() const
    {
        static_var++;
        //normal_var;
        cout << "call_chain_2 called\n";
    }
};
int test::static_var = 0;
int main()
{
    // Call test::static_method using function pointer here
    void (*function_ptr)() = test::static_method;
    function_ptr();

    // Call test::normal_method using function pointer here
    test obj1;
    void (test::*function_ptr_1)() = test::normal_method;
    (obj1.*function_ptr_1)();
    // Chain calling
    test t;
    t.call_chain_1().call_chain_2(); // This is correct syntax, do not change this. Fix these methods

    return 0;
}
```
