```c++
#include <iostream>

template <typename T, size_t N>
class array
{
    public:
    T element[N];

    array() = default;
    array(std::initializer_list<T> in_list)
    {
        std::copy(in_list.begin(), in_list.end(), element);
    }
    size_t size()
    {
        return N;
    }
    T &operator[](size_t position)
    {
        if (position < N)
        {
            return element[position];
        }
        else
        {
            std::cout << "out of range\n";
        }
        return element[0];
    }
    template <size_t N1>
    array<T,N+N1> operator+(array<T,N1> &rhs)
    {
        array<T,(N+N1)> Temp;
        std::copy(std::begin(element), std::end(element), Temp.element);
        std::copy(std::begin(rhs.element), std::end(rhs.element), Temp.element+N);

        return Temp;
    }
    array &operator=(const array &rhs)
    {
        std::copy(std::begin(rhs.element), std::end(rhs.element), element);
        return *this;
    }
};

int main()
{
    array<int, 5> arr1 = {1, 2, 3, 4, 5};
    arr1[0] = 0;
    std::cout << arr1[0] << std::endl;

    array<int, 5> arr2 = {6, 7, 8, 9, 10};

    array<int, 10> arr3;

    arr3 = arr1 + arr2; // arr3 = {1,2,3,4,5,6,7,8,9,10}
    for (size_t i = 0; i < arr3.size(); i++)
    {
        std::cout << arr3[i] << " ";
    }
    std::cout << std::endl;

    array<int, 5> arr4;
    arr4 = arr2 = arr1;

    for (size_t i = 0; i < arr4.size(); i++)
    {
        std::cout << arr4[i] << " ";
    }
    std::cout << std::endl;
    return 0;
}
```
