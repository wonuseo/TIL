---
tags:  
  - DB  
  - FTS  
---
#TIL   
# 개요  
**대량의 텍스트 데이터에서 특정 단어나 문구를 빠르고 효과적으로 찾아내는 검색 기술.**    
문서 또는 데이터베이스에서 전체 텍스트를 대상으로 검색을 수행하는 방법. 문서의 모든 단어를 인덱싱하고, 사용자의 질의어가 포함된 문서를 빠르게 찾을 수 있다.  
***  
# 구성 요소  
* **Indexer**  
    * 텍스트 데이터를 검색 할 수 있는 인덱스로 변환.  
    * 원본 데이터에서 검색 키워드를 추출하고, 위치, 빈도 등의 메타데이터와 함께 저장.  
    * ex) "John loves pizza and Mary loves pasta"  
       * 문장을 토큰화  
       * 'John', 'loves', 'pizza', 'and', 'Mary', 'pasta'  
    ***  
* **Query Processor**  
    * 사용자의 검색 요구를 분석하고, 인덱스가 이해할 수 있는 형태로 변환.  
    * 쿼리의 단어를 소문자 변화, 불용어 제거, 어근 추출, 형태소 분석, 동의어 처리, 표현식 확장 등 과 같은 정규화 진행.  
    ***  
* **Search Engine**  
    * 인덱스를 사용하여 실제 데이터를 검색.  
    ***  
* **Relevance Ranking**  
    * 검색 결과의 관련성을 평가하고 있는 순위를 매기는 과정.  
    * 키워드의 빈도, 위치, 문서의 신선도, 사용자의 행동 등 다양한 요인을 고려.  
    ***  
# MariaDB  
Ref : [MariaDB Full-Text Index Overview](https://mariadb.com/kb/en/full-text-index-overview/#in-natural-language-mode)  
## 주요 내용  
* **구문**  
    * ==MATCH (col1,col2,...) AGAINST (expr [search_modifier])==  
    * search_modifier  
       * **IN NATURAL LANGUAGE MODE**  
          * 키워드 생략 가능.  
          * 관련성이 높은 순서대로 반환.  
          ***  
       * **IN BOOLEAN MODE**  
          * 특수 연산자로 검색 옵션 부여.  
             * ' +, -, <, >, (), ~, " ", * '  
          * 검색어는 관련성 순으로 반화되지 않고 50% 제한도 적용되지 않는다.  
          ***  
       * **WITH QUERY EXPANSION**  
          * 자연어 검색의 변형.  
          * 일반적인 자연어 검색을 수행하고, 검색에서 반환된 가장 관련성이 높은 행의 단어가 검색 문자열에 추가되고 검색이 다시 수행되어 두 번쨰 검색의 행을 반환.



