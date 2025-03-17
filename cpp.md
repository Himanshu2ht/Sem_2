# Program 1

```
#include <iostream>
#include <cstdlib>
using namespace std;
double compute_series_sum(int n) {
    double series_sum = 0.0;    
    
    for (int i = 1; i <= n; i++) {
        
        if (i % 2 == 1) {
            series_sum += 1.0 / (i * i); 
        } else {
            series_sum -= 1.0 / (i * i); 
        }
    }    
    return series_sum;
}
int main(int argc, char* argv[]) {
    int n;
    if (argc > 1) {
        n = atoi(argv[1]); 
    } else {
       
        cout << "Enter the number of terms (n): ";
        cin >> n;
    }
    double result = compute_series_sum(n);
    cout << "The sum of the first " << n << " terms of the series is: " << result << endl;
    return 0;
}
```

# Program 2

```
#include <iostream>
#include <unordered_set>
#include <vector>
using namespace std;
void removeDuplicates(int arr[], int& n) {
   
    unordered_set<int> uniqueElements;
    int index = 0; // Index to keep track of the new array without duplicates
    for (int i = 0; i < n; i++) {
       
        if (uniqueElements.find(arr[i]) == uniqueElements.end()) {
            uniqueElements.insert(arr[i]);
            arr[index++] = arr[i];
        }
    }
  
    n = index;
}
void printArray(int arr[], int n) {
    for (int i = 0; i < n; i++) {
        cout << arr[i] << " ";
    }
    cout << endl;
}
int main() {
    int n;
   
    cout << "Enter the number of elements in the array: ";
    cin >> n;
    int arr[n];
   
    cout << "Enter the elements of the array: ";
    for (int i = 0; i < n; i++) {
        cin >> arr[i];
    }
   
    removeDuplicates(arr, n);
  
    cout << "Array after removing duplicates: ";
    printArray(arr, n);
    return 0;
}
```

# Program 3
```
#include <iostream>
#include <cctype> 
#include <string>
#include <map>
using namespace std;
void countAlphabetOccurrences(const string& text) {
    map<char, int> frequency;
  
    for (char ch : text) {
       
        ch = tolower(ch);   
      
        if (isalpha(ch)) {
            frequency[ch]++;  
        }
    }
    // Print the table of occurrences
    cout << "Alphabet Occurrences:" << endl;
    cout << "Letter | Occurrences" << endl;
    cout << "----------------------" << endl;
    for (char letter = 'a'; letter <= 'z'; letter++) {
        // If the letter exists in the map, print its frequency
        if (frequency.find(letter) != frequency.end()) {
            cout << letter << "      | " << frequency[letter] << endl;
        } else {
            cout << letter << "      | 0" << endl;
        }
    }
}
int main(int argc, char* argv[]) {
    // Check if any command line arguments were provided
    if (argc < 2) {
        cout << "Please provide a text input as a command line argument." << endl;
        return 1; 
    }
    // Concatenate the command line arguments into a single string
    string text = "";
    for (int i = 1; i < argc; i++) {
        text += string(argv[i]) + " ";  
    }
   
    countAlphabetOccurrences(text);
    return 0;
}
```
# Program 4
```
#include <iostream>
#include <cstring>
using namespace std;


void showCharacterAddresses(const char* str) {
    cout << "Addresses of each character in the string:" << endl;
    while (*str != '\0') {
        cout << (void*)str << " -> " << *str << endl;
        str++;
    }
}


void concatenateStrings(char* str1, const char* str2) {
    while (*str1 != '\0') {
        str1++;
    }
    while (*str2 != '\0') {
        *str1 = *str2;
        str1++;
        str2++;
    }
    *str1 = '\0'; 
}


int compareStrings(const char* str1, const char* str2) {
    while (*str1 != '\0' && *str2 != '\0') {
        if (*str1 != *str2) {
            return (*str1 - *str2); 
        }
        str1++;
        str2++;
    }
    return (*str1 - *str2);  
}


int calculateLength(const char* str) {
    const char* ptr = str;
    int length = 0;
    while (*ptr != '\0') {
        length++;
        ptr++;
    }
    return length;
}

 
void convertToUppercase(char* str) {
    while (*str != '\0') {
        if (*str >= 'a' && *str <= 'z') {
            *str = *str - 'a' + 'A'; 
        }
        str++;
    }
}


void reverseString(char* str) {
    int length = calculateLength(str);
    int start = 0, end = length - 1;
    while (start < end) {
       
        char temp = str[start];
        str[start] = str[end];
        str[end] = temp;
        start++;
        end--;
    }
}

// Function to insert a string at a user-specified position
void insertStringAtPosition(char* str1, const char* str2, int position) {
    int length1 = calculateLength(str1);
    int length2 = calculateLength(str2);
   
    for (int i = length1; i >= position; i--) {
        str1[i + length2] = str1[i];
    }
  
    for (int i = 0; i < length2; i++) {
        str1[position + i] = str2[i];
    }
    str1[length1 + length2] = '\0'; 
}

int main() {
    int choice;
    char str1[100], str2[100];
    int position;
    int result; 

    do {
        cout << "\nMenu: \n";
        cout << "1. Show address of each character in string\n";
        cout << "2. Concatenate two strings\n";
        cout << "3. Compare two strings\n";
        cout << "4. Calculate length of the string\n";
        cout << "5. Convert all lowercase characters to uppercase\n";
        cout << "6. Reverse the string\n";
        cout << "7. Insert a string in another string at a user-specified position\n";
        cout << "8. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;
        cin.ignore(); 

        switch (choice) {
            case 1:
                cout << "Enter a string: ";
                cin.getline(str1, 100);
                showCharacterAddresses(str1);
                break;
            case 2:
                cout << "Enter first string: ";
                cin.getline(str1, 100);
                cout << "Enter second string: ";
                cin.getline(str2, 100);
                concatenateStrings(str1, str2);
                cout << "Concatenated string: " << str1 << endl;
                break;
            case 3:
                cout << "Enter first string: ";
                cin.getline(str1, 100);
                cout << "Enter second string: ";
                cin.getline(str2, 100);
                result = compareStrings(str1, str2); 
                if (result == 0) {
                    cout << "The strings are equal." << endl;
                } else if (result < 0) {
                    cout << "The first string is lexicographically smaller." << endl;
                } else {
                    cout << "The first string is lexicographically larger." << endl;
                }
                break;
            case 4:
                cout << "Enter a string: ";
                cin.getline(str1, 100);
                cout << "Length of the string: " << calculateLength(str1) << endl;
                break;
            case 5:
                cout << "Enter a string: ";
                cin.getline(str1, 100);
                convertToUppercase(str1);
                cout << "String after conversion to uppercase: " << str1 << endl;
                break;
            case 6:
                cout << "Enter a string: ";
                cin.getline(str1, 100);
                reverseString(str1);
                cout << "Reversed string: " << str1 << endl;
                break;
            case 7:
                cout << "Enter the string: ";
                cin.getline(str1, 100);
                cout << "Enter the string to insert: ";
                cin.getline(str2, 100);
                cout << "Enter the position to insert: ";
                cin >> position;
                insertStringAtPosition(str1, str2, position);
                cout << "String after insertion: " << str1 << endl;
                break;
            case 8:
                cout << "Exiting program." << endl;
                break;
            default:
                cout << "Invalid choice. Please try again." << endl;
        }
    } while (choice != 8);
    
    return 0;
}
```

# Program 5
```
#include <iostream>
using namespace std;

void mergeArrays(int arr1[], int n1, int arr2[], int n2, int merged[]) {
    int i = 0, j = 0, k = 0;
   
    while (i < n1 && j < n2) {
        if (arr1[i] < arr2[j]) {
            merged[k++] = arr1[i++];
        } else {
            merged[k++] = arr2[j++];
        }
    }
    // If there are remaining elements in arr1, add them
    while (i < n1) {
        merged[k++] = arr1[i++];
    }
    // If there are remaining elements in arr2, add them
    while (j < n2) {
        merged[k++] = arr2[j++];
    }
}
// Function to print an array
void printArray(int arr[], int size) {
    for (int i = 0; i < size; i++) {
        cout << arr[i] << " ";
    }
    cout << endl;
}
int main() {
    int n1, n2;
    // Input the size and elements of the first array
    cout << "Enter the size of the first array: ";
    cin >> n1;
    int arr1[n1];
    cout << "Enter the elements of the first array in sorted order: ";
    for (int i = 0; i < n1; i++) {
        cin >> arr1[i];
    }
    // Input the size and elements of the second array
    cout << "Enter the size of the second array: ";
    cin >> n2;
    int arr2[n2];
    cout << "Enter the elements of the second array in sorted order: ";
    for (int i = 0; i < n2; i++) {
        cin >> arr2[i];
    }
    // Create an array to hold the merged result
    int merged[n1 + n2];
    // Merge the arrays
    mergeArrays(arr1, n1, arr2, n2, merged);
    // Output the merged array
    cout << "Merged array: ";
    printArray(merged, n1 + n2);
    return 0;
}
```
# Program 6
## 1. with recursion

```
#include <iostream>
using namespace std;
// Function for binary search with recursion
int binarySearchRecursive(int arr[], int low, int high, int target) {
    // Base case: element is not found
    if (low > high) {
        return -1;
    }
    // Find the middle element
    int mid = low + (high - low) / 2;
    // Check if the target is at the middle
    if (arr[mid] == target) {
        return mid;
    }
    // If target is smaller, search in the left half
    else if (arr[mid] > target) {
        return binarySearchRecursive(arr, low, mid - 1, target);
    }
    // If target is larger, search in the right half
    else {
        return binarySearchRecursive(arr, mid + 1, high, target);
    }
}
int main() {
    int n, target;
    // Input the number of elements
    cout << "Enter the number of elements: ";
    cin >> n;
    int arr[n];
    // Input the sorted elements
    cout << "Enter the sorted elements: ";
    for (int i = 0; i < n; i++) {
        cin >> arr[i];
    }
    // Input the target element to search for
    cout << "Enter the element to search for: ";
    cin >> target;
    // Binary search with recursion
    int resultRecursive = binarySearchRecursive(arr, 0, n - 1, target);
    if (resultRecursive != -1) {
        cout << "Element found at index (recursive): " << resultRecursive << endl;
    } else {
        cout << "Element not found (recursive)." << endl;
    }
    return 0;
}
```

## 2. without recursion
```
#include <iostream>
using namespace std;
// Function for binary search without recursion
int binarySearchIterative(int arr[], int n, int target) {
    int low = 0, high = n - 1;
    // Continue searching while the range is valid
    while (low <= high) {
        int mid = low + (high - low) / 2;
        // Check if the target is at the middle
        if (arr[mid] == target) {
            return mid;
        }
        // If target is smaller, search in the left half
        else if (arr[mid] > target) {
            high = mid - 1;
        }
        // If target is larger, search in the right half
        else {
            low = mid + 1;
        }
    }
    // If the element is not found, return -1
    return -1;
}
int main() {
    int n, target;
    // Input the number of elements
    cout << "Enter the number of elements: ";
    cin >> n;
    int arr[n];
    // Input the sorted elements
    cout << "Enter the sorted elements: ";
    for (int i = 0; i < n; i++) {
        cin >> arr[i];
    }
    // Input the target element to search for
    cout << "Enter the element to search for: ";
    cin >> target;
    // Binary search without recursion
    int resultIterative = binarySearchIterative(arr, n, target);
    if (resultIterative != -1) {
        cout << "Element found at index (iterative): " << resultIterative << endl;
    } else {
        cout << "Element not found (iterative)." << endl;
    }
    return 0;
}
```

# Program 7
## 1. with recursion
```
#include <iostream>
using namespace std;
// Recursive function to calculate GCD using Euclidean algorithm
int gcdRecursive(int a, int b) {
   // Base case: If b is 0, the GCD is a
   if (b == 0) {
       return a;
   }
   // Recursive case: Call gcd on b and the remainder of a divided by b
   return gcdRecursive(b, a % b);
}
int main() {
   int a, b;
   cout << "Enter two numbers: ";
   cin >> a >> b;
   int result = gcdRecursive(a, b);
   cout << "GCD of " << a << " and " << b << " is: " << result << endl;
   return 0;
}
```
## 2. without recursion
```
#include <iostream>
using namespace std;
// Iterative function to calculate GCD using Euclidean algorithm
int gcdIterative(int a, int b) {
   // Keep applying the Euclidean algorithm until b becomes 0
   while (b != 0) {
       int temp = b;
       b = a % b; // Find remainder
       a = temp;  // Update a to b's value
   }
   return a; // When b becomes 0, a is the GCD
}
int main() {
   int a, b;
   cout << "Enter two numbers: ";
   cin >> a >> b;
   int result = gcdIterative(a, b);
   cout << "GCD of " << a << " and " << b << " is: " << result << endl;
   return 0;
}

```

# Program 8
```
#include <iostream>
#include <vector>
#include <stdexcept>
using namespace std;
class Matrix {
private:
    int rows, cols;
    vector<vector<int>> mat;
public:
    // Constructor to initialize the matrix with given dimensions and values
    Matrix(int r, int c) : rows(r), cols(c) {
        mat.resize(rows, vector<int>(cols));
    }
    // Function to input values into the matrix
    void inputMatrix() {
        cout << "Enter elements of the matrix (" << rows << "x" << cols << "):\n";
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                cin >> mat[i][j];
            }
        }
    }
    // Function to display the matrix
    void displayMatrix() const {
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                cout << mat[i][j] << " ";
            }
            cout << endl;
        }
    }
    // Function to perform matrix addition
    Matrix add(const Matrix& m) {
        if (rows != m.rows || cols != m.cols) {
            throw invalid_argument("Matrices dimensions do not match for addition.");
        }
        Matrix result(rows, cols);
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                result.mat[i][j] = mat[i][j] + m.mat[i][j];
            }
        }
        return result;
    }
    // Function to perform matrix multiplication
    Matrix multiply(const Matrix& m) {
        if (cols != m.rows) {
            throw invalid_argument("Matrices dimensions are incompatible for multiplication.");
        }
        Matrix result(rows, m.cols);
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < m.cols; j++) {
                result.mat[i][j] = 0;
                for (int k = 0; k < cols; k++) {
                    result.mat[i][j] += mat[i][k] * m.mat[k][j];
                }
            }
        }
        return result;
    }
    // Function to perform matrix transpose
    Matrix transpose() {
        Matrix result(cols, rows);
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                result.mat[j][i] = mat[i][j];
            }
        }
        return result;
    }
};
int main() {
    int choice;
    Matrix* m1 = nullptr;
    Matrix* m2 = nullptr;
    while (true) {
        cout << "\nMatrix Operations Menu:\n";
        cout << "1. Add Matrices\n";
        cout << "2. Multiply Matrices\n";
        cout << "3. Transpose Matrix\n";
        cout << "4. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;
        switch (choice) {
            case 1: { // Sum of matrices
                int r, c;
                cout << "Enter dimensions of matrix 1 (rows columns): ";
                cin >> r >> c;
                m1 = new Matrix(r, c);
                m1->inputMatrix();

                cout << "Enter dimensions of matrix 2 (rows columns): ";
                cin >> r >> c;
                m2 = new Matrix(r, c);
                m2->inputMatrix();
                try {
                    Matrix result = m1->add(*m2);
                    cout << "Result of addition:\n";
                    result.displayMatrix();
                } catch (const invalid_argument& e) {
                    cout << "Error: " << e.what() << endl;
                }
                delete m1;
                delete m2;
                break;
            }
            case 2: { // Product of matrices
                int r1, c1, r2, c2;
                cout << "Enter dimensions of matrix 1 (rows columns): ";
                cin >> r1 >> c1;
                m1 = new Matrix(r1, c1);
                m1->inputMatrix();
                cout << "Enter dimensions of matrix 2 (rows columns): ";
                cin >> r2 >> c2;
                m2 = new Matrix(r2, c2);
                m2->inputMatrix();
                try {
                    Matrix result = m1->multiply(*m2);
                    cout << "Result of multiplication:\n";
                    result.displayMatrix();
                } catch (const invalid_argument& e) {
                    cout << "Error: " << e.what() << endl;
                }
                delete m1;
                delete m2;
                break;
            }
            case 3: { // Transpose of matrix
                int r, c;
                cout << "Enter dimensions of matrix (rows columns): ";
                cin >> r >> c;
                m1 = new Matrix(r, c);
                m1->inputMatrix();
                Matrix result = m1->transpose();
                cout << "Transpose of the matrix:\n";
                result.displayMatrix();
                delete m1;
                break;
            }
            case 4: { // Exit
                cout << "Exiting program.\n";
                return 0;
            }
            default:
                cout << "Invalid choice, please try again.\n";
                break;
        }
    }
    return 0;
}

```

# Program 9
```
#include <iostream>
#include <string>
using namespace std;
// Base class Person
class Person {
protected:
    string name; // Data member to store name
public:
    // Constructor to initialize the name
    Person(string n) : name(n) {}
    // Virtual function for runtime polymorphism
    virtual void display() {
        cout << "Name: " << name << endl;
    }
    // Destructor (virtual to ensure proper cleanup in derived classes)
    virtual ~Person() {}
};
// Derived class Student
class Student : public Person {
private:
    string course;
    float marks;
    int year;
public:
    // Constructor to initialize attributes
    Student(string n, string c, float m, int y) : Person(n), course(c), marks(m), year(y) {}
    // Overriding display method to show Student's attributes
    void display() override {
        cout << "Student Name: " << name << endl;
        cout << "Course: " << course << endl;
        cout << "Marks: " << marks << endl;
        cout << "Year: " << year << endl;
    }
};
// Derived class Employee
class Employee : public Person {
private:
    string department;
    float salary;
public:
    // Constructor to initialize attributes
    Employee(string n, string d, float s) : Person(n), department(d), salary(s) {}
    // Overriding display method to show Employee's attributes
    void display() override {
        cout << "Employee Name: " << name << endl;
        cout << "Department: " << department << endl;
        cout << "Salary: " << salary << endl;
    }
};
// Main function
int main() {
    // Creating objects of Student and Employee classes
    Person* p1 = new Student("Alice", "Computer Science", 88.5, 2);
    Person* p2 = new Employee("Bob", "IT", 50000);
    // Displaying the details using runtime polymorphism
    cout << "Displaying Student details:" << endl;
    p1->display();
    cout << "\nDisplaying Employee details:" << endl;
    p2->display();
    // Cleaning up the dynamically allocated memory
    delete p1;
    delete p2;
    return 0;
}
```

# Program 10
```
#include <iostream>
#include <cmath>
#include <stdexcept> // For exception handling
using namespace std;
class Triangle {
private:
    double side1, side2, side3;
public:
    // Constructor to initialize the sides of the triangle
    Triangle(double s1, double s2, double s3) {
        if (s1 <= 0 || s2 <= 0 || s3 <= 0) {
            throw invalid_argument("Sides must be greater than 0.");
        }
        if (s1 + s2 <= s3 || s1 + s3 <= s2 || s2 + s3 <= s1) {
            throw invalid_argument("Sum of any two sides must be greater than the third side.");
        }
        side1 = s1;
        side2 = s2;
        side3 = s3;
    }
    // Function to calculate the area of a right-angled triangle
    double calculateArea() const {
        if (isRightAngled()) {
            double base = side1, height = side2;
            return 0.5 * base * height; // Area of right-angled triangle
        }
        throw invalid_argument("Not a right-angled triangle.");
    }
    // Function to calculate the area using Heron's formula
    double calculateAreaUsingHeronsFormula() const {
        double s = (side1 + side2 + side3) / 2; // Semi-perimeter
        double area = sqrt(s * (s - side1) * (s - side2) * (s - side3));
        return area;
    }
    // Function to check if the triangle is right-angled (using Pythagoras theorem)
    bool isRightAngled() const {
        double a = side1, b = side2, c = side3;
        // Check if the triangle satisfies the Pythagoras theorem
        if (a * a + b * b == c * c || a * a + c * c == b * b || b * b + c * c == a * a) {
            return true;
        }
        return false;
    }
    // Overloading the assignment operator
    Triangle& operator=(const Triangle& other) {
        if (this != &other) {
            side1 = other.side1;
            side2 = other.side2;
            side3 = other.side3;
        }
        return *this;
    }
    // Overloading the equality operator
    bool operator==(const Triangle& other) const {
        return (side1 == other.side1 && side2 == other.side2 && side3 == other.side3);
    }
    // Method to display the sides of the triangle
    void display() const {
        cout << "Sides of the triangle: " << side1 << ", " << side2 << ", " << side3 << endl;
    }
};
int main() {
    try {
        // Creating a triangle object
        Triangle t1(3, 4, 5); // Right-angled triangle
        t1.display();
        cout << "Area of the right-angled triangle: " << t1.calculateArea() << endl;
        // Creating another triangle object
        Triangle t2(5, 6, 7); // General triangle
        t2.display();
        cout << "Area using Heron's formula: " << t2.calculateAreaUsingHeronsFormula() << endl;
        // Testing assignment operator
        Triangle t3(0, 0, 0); // Initializing with dummy values
        t3 = t1; // Assignment of t1 to t3
        cout << "\nAfter assignment, t3 is:\n";
        t3.display();
        // Testing equality operator
        if (t1 == t3) {
            cout << "\nt1 and t3 are equal." << endl;
        } else {
            cout << "\nt1 and t3 are not equal." << endl;
        }
    }
    catch (const invalid_argument& e) {
        cout << "Error: " << e.what() << endl;
    }
    return 0;
}

```
# Program 11
```
#include <iostream>
#include <fstream>
#include <string>
using namespace std;
class Student {
private:
    int rollNo;
    string name;
    string studentClass;
    int year;
    float totalMarks;
public:
    // Constructor to initialize a Student object
    Student(int r, string n, string c, int y, float t) 
        : rollNo(r), name(n), studentClass(c), year(y), totalMarks(t) {}
    // Method to write student details to a file
    void writeToFile(ofstream &file) {
        file << rollNo << endl;
        file << name << endl;
        file << studentClass << endl;
        file << year << endl;
        file << totalMarks << endl;
    }
    // Method to read student details from a file
    void readFromFile(ifstream &file) {
        file >> rollNo;
        file.ignore();  // Ignore the newline character after reading rollNo
        getline(file, name);
        getline(file, studentClass);
        file >> year;
        file >> totalMarks;
    }
    // Method to display the student's information
    void display() const {
        cout << "Roll No: " << rollNo << endl;
        cout << "Name: " << name << endl;
        cout << "Class: " << studentClass << endl;
        cout << "Year: " << year << endl;
        cout << "Total Marks: " << totalMarks << endl;
    }
};
int main() {
   
    ofstream outFile("students.txt");
   
    if (!outFile) {
        cerr << "File could not be opened for writing!" << endl;
        return 1;
    }

    Student s1(1, "Alice", "Math", 2023, 450);
    Student s2(2, "Bob", "Science", 2023, 400);
    Student s3(3, "Charlie", "History", 2023, 480);
    Student s4(4, "David", "English", 2023, 470);
    Student s5(5, "Eve", "Computer Science", 2023, 490);
  
    s1.writeToFile(outFile);
    s2.writeToFile(outFile);
    s3.writeToFile(outFile);
    s4.writeToFile(outFile);
    s5.writeToFile(outFile);
 
    outFile.close();
   
    ifstream inFile("students.txt");

    if (!inFile) {
        cerr << "File could not be opened for reading!" << endl;
        return 1;
    }
    cout << "\nStudent records retrieved from file:\n";
  
    Student tempStudent(0, "", "", 0, 0);
   
    for (int i = 0; i < 5; ++i) {
        tempStudent.readFromFile(inFile);
        tempStudent.display();
        cout << "-------------------------------\n";
    }
  
    inFile.close();
    return 0;
}

```
# Program 12
```
#include <iostream>
#include <fstream>
#include <cctype>  
using namespace std;
int main() {
    
    string inputFile = "input.txt";
    string outputFile = "output.txt";
   
    ifstream inFile(inputFile);
  
    if (!inFile) {
        cerr << "Error: Unable to open input file!" << endl;
        return 1;
    }
 
    ofstream outFile(outputFile);
   
    if (!outFile) {
        cerr << "Error: Unable to open output file!" << endl;
        return 1;
    }
    char ch;
  
    while (inFile.get(ch)) {
       
        if (!isspace(ch)) {
            outFile.put(ch);
        }
    }
   
    inFile.close();
    outFile.close();
    cout << "File contents copied successfully without whitespaces." << endl;
    return 0;
}

```

# Program 13
```
#include <iostream>
#include <stdexcept>
using namespace std;
int main() {
    double p, q;

    cout << "Enter two numbers (p and q): ";
    cin >> p >> q;
    try {
      
        if (q == 0) {
            throw runtime_error("Error: Division by zero is not allowed.");
        }
       
        double result = p / q;
        cout << "Result of " << p << " / " << q << " = " << result << endl;
    }
    catch (const runtime_error& e) {
       
        cout << e.what() << endl;
    }
    return 0;
}

```


