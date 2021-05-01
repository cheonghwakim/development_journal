redis value에 담겨있는 값을 Object로 Mapping하다가 이런 에러를 만났다.

```java
com.fasterxml.jackson.databind.exc.UnrecognizedPropertyException: Unrecognized field "@class" (class com.web.mongdok.dto.RedisUserDto), not marked as ignorable (6 known properties: "id", "email", "kakaoId", "promise", "nickname", "category"])
 at [Source: (String)"{"@class":"com.web.mongdok.dto.RedisUserDto","id":"94de64ca-1ba6-4f36-b36a-45ec66aa4320","email":"asder36@naver.com","kakaoId":"1710970888","nickname":"cheonghwa","category":"N","promise":"JGS"}"; line: 1, column: 12] (through reference chain: com.web.mongdok.dto.RedisUserDto["@class"])
```



redis value에 넣기 위해 직렬화 하는 과정에서 "@class"가 붙어서 그랬다.

```
{"@class":"com.web.mongdok.dto.RedisUserDto","id":"94de64ca-1ba6-4f36-b36a-45ec66aa4320","email":"asder36@naver.com","kakaoId":"1710970888","nickname":"cheonghwa","category":"N","promise":"JGS"}
```



해결방법: class에 @JsonIgnoreProperties(ignoreUnknown = true)를 붙여준다.



![image](https://user-images.githubusercontent.com/43662673/116775837-37a54780-aaa0-11eb-8cff-c42989a91ebc.png)