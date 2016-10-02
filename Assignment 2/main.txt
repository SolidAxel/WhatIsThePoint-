

#include <iostream>
#include <cmath>
using namespace std;

////Problem 1a.
int main()
{
    int arr[3] = { 5, 10, 15 };
    int* ptr = arr;

    *ptr = 10;          // set arr[0] to 10
    *(ptr + 1) = 20;      // set arr[1] to 20         //Parenthesis are needed so it's not (*ptr) + 1.
    ptr += 2;
    ptr[0] = 30;        // set arr[2] to 30

    while (ptr >= arr)
    {
        cout << ' ' << *ptr;    // print values
        ptr--;                                    // Decrease ptr AFTER printing or else first print will be missing.
    }
    cout << endl;
}

////Problem 1b.
void findDisorder(int arr[], int n, int * &p)     //Pointer needs to be passed by reference or else when main tries to print it, it will not be the correct address.
{
    
    for (int k = 0; k < n; k++)
    {
        if (arr[k] < arr[k+1])
        {

            p = arr + k;
            return;
        }
    }
    p = nullptr;
    
}

int main()
{
    int nums[6] = { 10, 20, 20, 40, 30, 50 };
    int* ptr;
    
    findDisorder(nums, 6, ptr);
    if (ptr == nullptr)
        cout << "The array is ordered" << endl;
    else
    {
        cout << "The disorder is at address " << ptr << endl;
        cout << "It's at index " << ptr - nums << endl;
        cout << "The item's value is " << *ptr << endl;
    }
}

//// Problem 1c.
void hypotenuse(double leg1, double leg2, double* resultPtr)
{
    *resultPtr = sqrt(leg1*leg1 + leg2*leg2);
}

int main()
{   double tempPoint;
    double* p = &tempPoint;                       //Pointer needs to point at something or else hypotenuse will think p is a double, not a pointer to a double.
    hypotenuse(1.5, 2.0, p);
    cout << "The hypotenuse is " << *p << endl;
}

////Problem 1d.
//// return true if two C strings are equal
bool match(const char str1[], const char str2[])
{   const char *ptr1 = str1;
    const char *ptr2 = str2;
    while (*ptr1 != 0  &&  *ptr2 != 0)  // zero bytes at ends             //Original function was attempting to see if whole arrays were not equal to zero.
    {
        if (*ptr1 != *ptr2){  // compare corresponding characters         //Original function attempted to compare whole arrays directly, not each character, which can't be done.
            return false;
        }
        ptr1++;            // advance to the next character               //Orignal function was attempting to increment pointers which can't be done.
        ptr2++;
    }
    return *ptr1 == *ptr2;   // both ended at same time?                  //Original function attempted to compare whole arrays directly, which can't be done.

}

int main()
{
    char a[10] = "pointy";
    char b[10] = "pointless";
    
    if (match(a,b))
        cout << "They're the same!\n";
}

// 1e. arr is local to computeSquares. This means that the pointer *ptr cannot be made equal to the result of computeSquares since computeSquares returns the array arr and arr is out of main's scope.

////Problem 2
int main(){
    string *fp;                 //2a
    string fish[5];             //2b
    fp = &fish[4];              //2c
    *fp = "yellowtail";         //2d
    *(fish +3) = "mackerel";    //2e
    fp -= 3;                    //2f
    fp[2] = "cod";              //2g
    fp[1] = "eel";              //2h
    bool d = fp == fish;        //2i
    bool b = *fp == *(fp+1);    //2j
}

////Problem 3a
double computeAverage(const double* scores, int nScores)
{
    const double* ptr = scores;
    double tot = 0;
    for (int i = 0; i < nScores; i++) {
        tot += *(ptr + i);
    }
    return tot/nScores;
}

////Problem 3b
// This function searches through str for the character chr.
// If the chr is found, it returns a pointer into str where
// the character was first found, otherwise nullptr (not found).
const char* findTheChar(const char *(str), char chr)
{
    const char* var = str;
    for (int k = 0; *(var+k) != 0; k++)
        if (*(var+k) == chr)
            return (var+k);
    
    return nullptr;
}

////Problem 3c
const char* findTheChar(const char *(str), char chr)
{
    while(*str != 0)
    {
        if (*str == chr){
            
            return str;
        }
        str++;
    }
    return NULL;
}

////Problem 4

int* minimart(int* a, int* b)
{
    if (*a < *b)
        return a;
    else
        return b;
}

void swap1(int* a, int *b)
{
    int* temp = a;
    a = b;
    b = temp;
}

void swap2(int* a, int *b)
{
    int temp = *a;
    *a = *b;
    *b = temp;
}

int main()
{
    int array[6] = { 5, 3, 4, 17, 22, 19 };               // Initializing array of 6 elements
    int* ptr = minimart(array, &array[2]);                // Pointer points to function minimart with pointer array and address of array[2] passed to it.
    ptr[1] = 9;                                           // Element at array index 3 set equal to 9
    ptr += 2;                                             // Pointer moved to array index 4
    *ptr = -1;                                            // Element at index 4 set to -1, changed from 22
    *(array+1) = 79;                                      // Array index 1 and that value is set to 79, changed from 3.
    cout << "diff=" << &array[5] - ptr << endl; // The difference between &array[5] and ptr is only 1. This means ptr is currently giving the address of array[4]
                                                // and is one address away.
    swap1(&array[0], &array[1]);                // Swaps memory but only affects the local variables of swap1, a and b.
    swap2(array, &array[2]);                    // 5 stored into temp. Sets first element of array to equal element at index 2, so 5 turns into 4. Then element at array index 2 set equal to temp. So 4 turns
                                                // into 5.
    for (int i = 0; i < 6; i++)                 //Prints out array in order from index 0 to 5.
        cout << array[i] << endl;
}

////Problem 5
void deleteG(char arr[]) {
    char *ptr = arr;
    while (*ptr != 0)                        //not pointing to end
    {
        if (*ptr == 'g' || *ptr == 'G')
        {
            while(*ptr != 0)                 //not pointing to end
            {
                *ptr = *(ptr+1);             //shifts everything to remove the g
                ptr++;
            }
            ptr = arr;                       //without resetting the pointer like this only the first g would be removed
        }
        ptr++;
    }
}
int main()
{
    char msg[100] = "I recall the glass gate next to Gus in Lagos, near the gold bridge.";
    deleteG(msg);
    cout << msg;  // prints   I recall the lass ate next to us in Laos, near the old bride.
}



