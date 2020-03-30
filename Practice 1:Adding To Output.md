Que: Make cout+5; statement to work as cout<<5
Concept:Operator overloading 
Solution:
...
#include <iostream>
using namespace std;

ostream &operator+(ostream &os, int a)
{
    os << a;
    return os;
}
int main()
{
    cout + 5;
    return 0;
}
...

