* Trie树讲解: https://www.jianshu.com/p/6f81da81bd02
* 标准的Trie的模板

```c++
class Trie {
public:
    /** Initialize your data structure here. */
    Trie() {
        root = new TrieNode();
    }
    
    /** Inserts a word into the trie. */
    void insert(string word) {
        TrieNode* p = root;
        for(auto c : word){
            if(p->children[c-'a'] == NULL){
                p->children[c-'a'] = new TrieNode();
            }
            p = p->children[c-'a'];
        }
        p->is_word = true;
    }
    
    /** Returns if the word is in the trie. */
    bool search(string word) {
        TrieNode* p = find(word);
        return p != NULL && p->is_word;
    }
    
    /** Returns if there is any word in the trie that starts with the given prefix. */
    bool startsWith(string prefix) {
        return find(prefix) != NULL;
    }
    
private:
    struct TrieNode{
        TrieNode() : is_word(false), children(26, NULL){}
        bool is_word;
        vector<TrieNode*> children;
    };
    
    TrieNode* root;
    
    TrieNode* find(string& key){
        TrieNode* p = root;
        for(char c : key){
            p = p->children[c-'a'];
            if(p == NULL)
                break;
        }
        return p;
    }
};

```

### 相关题目

* [642. Design Search Autocomplete System](https://leetcode.com/problems/design-search-autocomplete-system/)
* [208. Implement Trie (Prefix Tree)](hhttps://leetcode.com/problems/implement-trie-prefix-tree/?tab=Description)

