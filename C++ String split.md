```C++
#include <string>
#include <sstream>
#include <vector>
//不能区分多个分隔符的情况
	void split(const std::string &sentence, char delim, vector<string>& result) {
		stringstream ss(sentence);
		string item;
		while (getline(ss, item, delim)) {
			result.push_back(item);
		}
	}

//自己实现的，可以去除前后中间多个分隔符的情况
vector<string> split(string& s, char delim) {
	int len = s.length();
	vector<string> res;
	int begin = 0, end = len - 1;
	while (s[begin] == delim) begin++;
	for (int i = begin, j = begin; i < len && j<len;) {
		while (j < len && s[j] != delim) j++;
		res.push_back(s.substr(i, j - i));
		i = j;
		while (j < len && (s[j] == delim)) {
			i++;
			j++;
		}
	}

	return res;
}

#include <boost/algorithm/string.hpp>
* 或者用boost

    vector<string> split(string s){
        vector<string> res;
        boost::split(res, s, boost::is_any_of(" "));
        return res;
    }

```
