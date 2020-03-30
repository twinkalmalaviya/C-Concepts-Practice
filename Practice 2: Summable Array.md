```c++
#include <iostream>
#include <initializer_list>
using namespace std;

template<typename T,size_t N > 
class array
{
/*member elements of array */
    	T elems[N];
      size_t array_size{N};
public:
       array() = default;       
       array(T int_value) {
           for(auto &input_v:elems)
           input_v=int_value;
           cout << "T int_value Constructor\n";
       }
           array(initializer_list<T> l){ 
             int i=0;
             for(auto &input_l:l)
            // for(auto &input_v:elems)
             elems[i++]=input_l;             
           cout << "T 5 int_value Constructor\n";
    }
       template<size_t N1>
       array(T int_value,array<T, N1> input)
      // array(T int_value,int i,int i2,int i3,int i4) 
       {   int i=0;
           for(auto &input_v:elems)
           input_v=input[i++];
           cout << "T 5 int_value Constructor\n";
       }

/*member methods of array */
        size_t size() {
            return array_size;
        }
        // void display(){
        //     cout << "["<< " ";
        //     for (size_t i = 0; i < array_size; i++) 
        //     cout << elems[i] << " ";
        //     cout << "]"<< endl;
        // }
/*Operations of array */
        T &operator[](size_t position) {
            if(position<array_size)
                return elems[position];
            else
                cout << "Out of array range"<< endl;
            return elems[0];
        }
        // template<size_t N1>
        // void operator=( array<T, N1> input) {
            
        //     for (size_t i = 0; i < array_size; i++)
        //         if(i<N1)
        //             elems[i]=input[i];
        //         else
        //             break;
        // }


};

template<typename T1,size_t N2,size_t N3>
array<T1,(N2+N3)> operator+( array<T1, N2> &lhs, array<T1, N3> &rhs) {

    array<T1, (N2+N3)> Temp;
    size_t i,j;

    for (i = 0; i < lhs.size(); i++)
    Temp[i]=lhs[i];
    for (j=0; j < rhs.size();j++, i++)
    Temp[i]=rhs[j];

    return Temp;
}

int main()
{
array<int, 5> arr1 = {1, 2, 3, 4, 5};
    arr1[0] = 0;
    cout << arr1[0] << endl;

    array<int, 5> arr2 = {6, 7, 8, 9, 10};
    
    array<int, 10> arr3;

    arr3 = arr1 + arr2; // arr3 = {1,2,3,4,5,6,7,8,9,10}
    for (size_t i = 0; i < arr3.size(); i++)
    {
        cout << arr3[i] << " ";
    }
    cout<<endl;

    array<int, 5> arr4;
    arr4 = arr2 = arr1;


    for (size_t i = 0; i < arr4.size(); i++)
    {
        cout << arr4[i] << " ";
    }
    cout<<endl;
    return 0;

}
```
