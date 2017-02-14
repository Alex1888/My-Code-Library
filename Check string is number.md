
```C++
using namespace std;

// 不带+-号的检测
bool is_number(const std::string& s)
{
	std::string::const_iterator it = s.begin();
	while (it != s.end() && std::isdigit(*it)) ++it;
	return !s.empty() && it == s.end();
}

// 带正负号
/* strtol: http://www.cplusplus.com/reference/cstdlib/strtol/
long int strtol (const char* str, char** endptr, int base);
Convert string to long integer
*/
bool isInteger(const std::string & s)
{
	if (s.empty() || ((!isdigit(s[0])) && (s[0] != '-') && (s[0] != '+'))) return false;

	char * p;
	strtol(s.c_str(), &p, 10);

	return (*p == 0);
}
```
