```c++
#include<iostream>
using namespace std;

class A
{
    public:
    static uint32_t m_cnt;
    void *operator new(size_t size)
    {
        m_cnt++;
        return  (malloc(size));
    }
    void operator delete(void *ptr)
    {
        m_cnt--;
        free(ptr);
    }
};
uint32_t A::m_cnt=0;

int main()
{
    A a1;
    A *a2 = new A;
    A *a3 = (A *)malloc(sizeof(A));
    cout << A::m_cnt << endl;
    delete a2;
    free(a3);
    cout << A::m_cnt << endl;
    return 0;
}
```
