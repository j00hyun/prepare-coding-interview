# 팰린드롬 페어 - leetcode 336

- 풀이 
``` python
import collections
from typing import List

class TrieNode:
    def __init__(self):
        self.children = collections.defaultdict(TrieNode)
        self.word_id = -1
        self.palindrome_word_ids = []

class Trie:
    def __init__(self):
        self.root = TrieNode()

    @staticmethod
    def is_palindrome(word: str) -> bool:
        return word[::] == word[::-1]

    # 단어 삽입
    def insert(self, index: int, word: str) -> None:
        node = self.root

        for i, char in enumerate(reversed(word)):
            # 팰린드롬 단어일 경우 palindrome_word_ids에 인덱스 추가
            if self.is_palindrome(word[0:len(word) - i]):
                node.palindrome_word_ids.append(index)

            node = node.children[char]

        # 단어 맨 마지막 word_id에 인덱스 넣기
        node.word_id = index

    def search(self, index: int, word: str) -> List[List[int]]:
        result = []
        node = self.root

        while word:
            # 3. 탐색 중간에 word_id가 있고 나머지 문자가 팰린드롬인 경우 ex) d(cbc)/d
            if node.word_id >= 0:
                if self.is_palindrome(word):
                    result.append([index, node.word_id])

            if not word[0] in node.children:
                return result

            node = node.children[word[0]]
            word = word[1:]

        # 1. 끝까지 탐색했을 때 word_id가 있는 경우 ex) bbcd/dcbb
        if node.word_id >= 0 and node.word_id != index:
            result.append([index, node.word_id])

        # 2. 끝까지 탐색했을 때 palindrome_word_ids가 있는 경우 ex) d/(cbbc)d, dcbb/(c)bbcd
        for palindrome_word_id in node.palindrome_word_ids:
            result.append([index, palindrome_word_id])

        return result

class Solution:
    def palindromePairs(self, words: List[str]) -> List[List[int]]:
        trie = Trie()

        for i, word in enumerate(words):
            trie.insert(i, word)

        results = []

        for i, word in enumerate(words):
            results.extend(trie.search(i, word))

        return results

```
