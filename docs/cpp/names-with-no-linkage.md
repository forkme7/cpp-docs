---
title: "Names with No Linkage | Microsoft Docs"
ms.custom: ""
ms.date: "11/04/2016"
ms.technology: ["cpp-language"]
ms.topic: "language-reference"
dev_langs: ["C++"]
helpviewer_keywords: ["functions [C++], parameters", "typedef names, linkage", "enumerators [C++], linkage", "names [C++], with no linkage", "function parameters [C++]"]
ms.assetid: 7174c500-12d2-4572-8c16-63c27c758fb1
author: "mikeblome"
ms.author: "mblome"
ms.workload: ["cplusplus"]
---
# Names with No Linkage
The only names that have no linkage are:  
  
-   Function parameters.  
  
-   Block-scoped names not declared as `extern` or **static**.  
  
-   Enumerators.  
  
-   Names declared in a `typedef` statement. An exception is when the `typedef` statement is used to provide a name for an unnamed class type. The name may then have external linkage if the class has external linkage. The following example shows a situation in which a `typedef` name has external linkage:  
  
    ```  
    // names_with_no_linkage.cpp  
    typedef struct  
    {  
       short x;  
       short y;  
    } POINT;  
  
    extern int MoveTo( POINT pt );  
  
    int main()  
    {  
    }  
    ```  
  
     The `typedef` name, `POINT`, becomes the class name for the unnamed structure. It is then used to declare a function with external linkage.  
  
 Because `typedef` names have no linkage, their definitions can differ between translation units. Because the compilations take place discretely, there is no way for the compiler to detect these differences. As a result, errors of this kind are not detected until link time. Consider the following case:  
  
```  
// Translation unit 1  
typedef int INT  
  
INT myInt;  
...  
  
// Translation unit 2  
typedef short INT  
  
extern INT myInt;  
...  
```  
  
 The preceding code generates an "unresolved external" error at link time.  
  
## Example  
 C++ functions can be defined only in file or class scope. The following example illustrates how to define functions and shows an erroneous function definition:  
  
```  
// function_definitions.cpp  
// compile with: /EHsc  
#include <iostream>  
using namespace std;  
void ShowChar( char ch );    // Declare function ShowChar.  
  
void ShowChar( char ch )     // Define function ShowChar.  
{                            // Function has file scope.  
   cout << ch;  
}  
  
struct Char                  // Define class Char.  
{  
    char Show();             // Declare Show function.  
    char Get();              // Declare Get function.  
    char ch;  
};  
  
char Char::Show()            // Define Show function  
{                            //  with class scope.  
    cout << ch;  
    return ch;  
}  
  
void GoodFuncDef( char ch )  // Define GoodFuncDef  
{                            //  with file scope.  
    int BadFuncDef( int i )  // C2601, Erroneous attempt to  
    {                        //  nest functions.  
        return i * 7;  
    }  
    for( int i = 0; i < BadFuncDef( 2 ); ++i )  
        cout << ch;  
    cout << "\n";  
}  
```  
  
## See Also  
 [Program and Linkage](../cpp/program-and-linkage-cpp.md)