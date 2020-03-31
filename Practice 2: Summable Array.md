```c++
#include <iostream>
//#include <array>
using namespace std;

template <typename T, size_t N>
class array
{
public:
    /*member elements of array */
    T elems[N];
    size_t array_size{N};


    array() = default;
    array(T int_value)
    {
        for (auto &input_v : elems)
            input_v = int_value;
    }
    array(initializer_list<T> l)
    {
        int i = 0;
        for (auto &input_l : l)
            elems[i++] = input_l;
    }
    template <typename T1, size_t N1>
    array &operator=( const array<T1,N1> &rhs);
    array &operator=( const array &rhs)
    {

            
        for (size_t i = 0; i < array_size; i++)
            if (i < N)
                elems[i] = rhs.elems[i];

        else 
                break;
        cout << "user defi inside\n";
        return *this;
    }
    size_t size()
    {
        return array_size;
    }

    /*Operations of array */
    T &operator[](size_t position)
    {
        if (position < array_size)
            return elems[position];
        else
            cout << "Out of array range" << endl;
        return elems[0];
    }

};
template <typename T, size_t N>
template <typename T1, size_t N1>
array<T,N> &array<T,N>::operator=(const array<T1, N1> &rhs)
{
    for (size_t i = 0; i < array_size; i++)
        if (i < N)
            elems[i] = rhs.elems[i];

        else
            break;

    cout << "user defi diff\n";
    return *this;
}

template <typename T1, size_t N2, size_t N3>
array<T1, (N2 + N3)> operator+(array<T1, N2> &lhs, array<T1, N3> &rhs)
{

    array<T1, (N2 + N3)> Temp;
    size_t i, j;

    for (i = 0; i < lhs.size(); i++)
        Temp[i] = lhs[i];
    for (j = 0; j < rhs.size(); j++, i++)
        Temp[i] = rhs[j];

    return Temp;
}

int main()
{
    array<int, 5> arr1 = {1, 2, 3, 4, 5};
    arr1[0] = 0;
    cout << arr1[0] << endl;

    array<int, 5> arr2 = {6, 7, 8, 9, 10};

    array<int, 10> arr3;

    arr3 = arr1;

    arr3 = arr1 + arr2; // arr3 = {1,2,3,4,5,6,7,8,9,10}
    for (size_t i = 0; i < arr3.size(); i++)
    {
        cout << arr3[i] << " ";
    }
    cout << endl;

    array<int, 5> arr4;
    arr4 = arr2 = arr1;

    for (size_t i = 0; i < arr4.size(); i++)
    {
        cout << arr4[i] << " ";
    }
    cout << endl;
    return 0;
}
```
