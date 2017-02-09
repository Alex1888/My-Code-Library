```C++

	void split(const std::string &s, char delim, vector<string>& result) {
		std::stringstream ss;
		ss.str(s);
		std::string item;
		while (std::getline(ss, item, delim)) {
			result.push_back(item);
		}
	}
```
