*  ```isalnum(s[i])```: Check if character is alphanumeric(数字或者字母)
* ```toupper(s[i])```
* ```int isdigit ( int c )``` : Check if character is decimal digit
* ```int isalpha ( int c )```: Check if character is alphabetic
* ```size_t find_first_of (const string& str, size_t pos = 0) const;```
* ```size_t find_last_of (const string& str, size_t pos = 0) const;``` 


>
> 1. Searches the string for the first character that matches any of the characters specified in its arguments.
> 2. When pos is specified, the search only includes characters at or after position pos, ignoring any possible occurrences before pos.
> 3. Notice that it is enough for one single character of the sequence to match (not all of them). See string::find for a function that matches entire sequences.
```c++
// 把元音都换成*
// string::find_first_of
#include <iostream>       // std::cout
#include <string>         // std::string
#include <cstddef>        // std::size_t

int main ()
{
  std::string str ("Please, replace the vowels in this sentence by asterisks.");
  std::size_t found = str.find_first_of("aeiou");
  while (found!=std::string::npos)
  {
    str[found]='*';
    found=str.find_first_of("aeiou",found+1);
  }

  std::cout << str << '\n';

  return 0;
}

```
* ```int isspace ( int c )```: Check if character is a white-space
* ```int stoi (const string&  str, size_t* idx = 0, int base = 10)``` string convert to int;
*  char convert to string: string(1, c)
