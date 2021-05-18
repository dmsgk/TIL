# Trie

- 검색트리의 일종으로 일반적으로 키가 문자열인, 동적 배열 또는 연관 배열을 저장하는 데 사용되는 정렬된 트리자료구조
- 전형적인 다진트리의 구조를 띤다. 
- 자연어 처리(NLP)분야에서 문자열 탐색을 위한 자료구조로 많이 사용됨

![img](https://camo.githubusercontent.com/7024b55e64516062054e9b5bccf35dc72d5e7a4cca88c8f57810804b955cb849/68747470733a2f2f74312e6461756d63646e2e6e65742f6366696c652f746973746f72792f323433353445333335383333413743463137)



>**정수형**에서 이진탐색트리를 이용하면 시간복잡도 O(logN)
>하지만 **문자열**에서 적용했을 때, 문자열 최대 길이가 M이면 **O(M*logN)**이 된다.
>
>**트라이**를 활용하면? → **O(M)**으로 문자열 검색이 가능



### References

- 박상길, 2020, 파이썬 알고리즘 인터뷰, 책만.
- https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Data%20Structure/Trie.md