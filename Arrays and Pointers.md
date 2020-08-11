# Arrays in C

Arrays are initialized by writing, `type array_name[size] = {list of values};` while initializing the array at the time of declaration, the programmer may
omit the size of the array, but note that if the number of values provided is less than the number of elements in the array, the un-assigned elements are filled with zeros, `int marks [5] = {0};`, for example.

### 1D arrays for inter-function communication

- Passing individual elements
  
  - Passing data values
  
  - Passing adresses
    
    ```c
    int main()
    {
      int arr[5] ={1, 2, 3, 4, 5};
      func(&arr[3]);
    }
    void func(int *num) 
    {
      printf("%d , *num);
    }
    ```

> In C the array name refers to the first byte of the array in the memory.

* Passing the entire array

Therefore, when we need to pass an entire array to a function, we can simply pass the name of the array.

```c
main()
{        
    int arr[5] ={1, 2, 3, 4, 5};
    func(arr);
}
void func(int arr[5])
{
    int i;
    for(i= ;i<5;i++)
        printf("%d", arr[i]);    
}
```

A function that accepts an array can declare the formal parameter in either of the two following ways. `func(int arr[]);` or `func(int *arr);`

When we pass the name of an array to a function, the address of the zeroth element of the array is copied to the local pointer variable in the function.

> An array name is often known to be a constant pointer.

In case of one-dimensional arrays, we have discussed that if the array is completely initialized, we may omit the size of the array. The same concept can be applied to a two-dimensional array, except that only the size of the first dimension can be omitted.

`int marks[][3]={{90,87,78},{68, 62, 71}};`

### Pointers and arrays

Array notation is a form of pointer notation. 

*The name of the array is the starting address of the array in memory. It is also known as the base address.*

```c
main()
{
    int arr[]={1,2,3,4,5};
    printf("\n Address of array = %p %p %p", arr, &arr[0], &arr);

    int *ptr = &arr[0];
    ptr++;
    printf("\n The value of the second element of the array is %d",
    *ptr);
}
```

```c
//For example, while we can write
ptr = arr; // ptr = &arr[0]
//we cannot write
arr = ptr;
//This is because while ptr is a variable, arr is a constant.
```

### Array of pointers

```c
//An array of pointers to int
int main()
{
    int arr1[]={1,2,3,4,5};
    int arr2[]={0,2,4,6,8};
    int arr3[]={1,3,5,7,9};
    int *parr[3] = {arr1, arr2, arr3};
    int i;
    for(i = 0; i < 3; i++)
        printf("%d", *parr[i]);
    return 0;
}
```

### Two dimensional arrays

In case of one-dimensional arrays, we have discussed that if the array is completely initialized, we may omit the size of the array. The same concept can be applied to a two-dimensional array, except that only the size of the first dimension can be omitted.

```c
//Declare
int marks[][3]={{90,87,78},{68, 62, 71}};
//Initialize
int marks[2][3] = {0};
```

### Passing 2D arrays to functions

* Passing individual elements

* Passing a row

```c
main()
{
int arr[2][3] = ({1, 2, 3}, {4, 5, 6});
        func(arr[1]);
}
void func(int arr[])
{
    int i;
    for(i= ;i<3;i++)
    printf("%d", arr[i] * 1 );
}
```

* Passing the entire 2D array

To pass a two-dimensional array to a function, we use the array name as the actual parameter (the way we did in case of a 1D array). However, the parameter in the called function must indicate that the array has two dimensions.

### Pointers and 2D arrays

```c
int mat[5][5];
int **ptr;

//Access
mat[i][j] or
*(*(mat + i) + j) or
*(mat[i]+j);
```

Here int **ptr is an array of pointers (to one-dimensional arrays), while int mat[5][5] is a 2D array. They are not the same type and are not interchangeable.

```c
#include <stdio.h>
int main()
{
    int arr[2][2]={{1,2}, {3,4}};
    int i, (*parr)[2];
    parr = arr;
    for(i = 0; i < 2; i++)
    {
    for(j = 0; j < 2 ;j++)
        printf(" %d", (*(parr+i))[j]); //arr[i][j] = (*(arr+i))[j] = 
                                                        //*((*arr+i))+j)
    }
    return 0;
}
//Output 1 2 3 4
```

> If we declare an array of pointers using, `data_type *array_name[SIZE];` Here SIZE represents the number of rows and the space for columns that can be dynamically allocated.
> 
> If we declare a pointer to an array using, data_type `(*array_name)[SIZE];`
> Here SIZE represents the number of columns and the space for rows that may be dynamically allocated.

A double pointer cannot be used as a 2D array. Therefore, it is wrong to declare: ‘int **mat’ and then use ‘mat’ as a 2D array. These are two very different data types used to access different locations in memory. So running such a code may abort the program with a ‘memory access violation’ error.

# Pointers in C

Note that `int (*ptr)[10];` declares ptr to be a pointer to an array of 10 integers. This is different from `int *ptr[10];` which would make ptr the name of an array of 10 pointers to type int.

A two-dimensional array is not the same as an array of pointers to 1D arrays.

```c
&arr[0][0] + 1 //points to arr[0][1]
arr[0] + 1 //points to arr[0][1]
arr + 1 //points to arr[1][0]
&arr[0] + 1 //points to arr[1][0]
```

The golden rule to access an element of a two-dimensional array can be given as
`arr[i][j] = (*(arr+i))[j] = *((*arr+i))+j) = *(arr[i]+j)`

-------

Seen that pointer to a one-dimensional array can be declared as,

```c
int arr[]={1,2,3,4,5};
int *parr;
parr = arr;
```

Similarly, pointer to a two-dimensional array can be declared as,

```c
int arr[2][2]={{1,2},{3,4}};
int (*parr)[2];
parr = arr;
```

A pointer to a three-dimensional array can be declared as,

```c
int arr[2][2][2]={1,2,3,4,5,6,7,8};
int (*parr)[2][2];
parr = arr;
```

We can access an element of a three-dimensional array by writing, `arr[i][j][k] = *(*(*(arr+i)+j)+k)`
