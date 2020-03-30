Que: Make cout+5; statement to work as cout<<5
Concept:Operator overloading 
Solution:
```c++
#include <iostream> 
using namespace std;
template <typename T>
ostream& operator+(ostream& os, T a)
{
  os<<a;
  return os;
}
int main() {
  cout+'c'+1;
  return 0;
}
```
