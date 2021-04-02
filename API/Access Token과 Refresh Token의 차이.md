#### Access Token 

Access Token(JWT)을 통한 인증 방식의 문제는 제 3자에게 탈취당할 경우 보안에 취약하다는 점이다. 유효기간이 짦은 token의 경우 그만큼 사용자는 로그인을 자주 해서 새롭게 token을 발급받아야 하므로 불편하다. 하지만, 유효기간을 늘리자면 토큰을 탈취당했을 때 보안에 더 취약해진다.

이 때, 유효기간을 짧게 하면서 좋은 방법?을 찾은 것이 **refresh token**이다.

Refresh Token은 Access Token과 똑같은 형태의 JWT이다. 처음에 로그인을 완료했을 때 Access Token과 동시에 발급되는 Refresh Token은 긴 유효기간을 가지면서, Access Token이 만료됐을 때 새로 발급해주는 열쇠가 된다.

간단한 예시)
Refresh Token의 유효기간은 2주, Access Token의 유효기간은 1시간이라 하자.
사용자는 API 요청을 하다가 1시간이 지나게 되면, 가지고 있는 Access Token은 만료된다. 그래도 Refresh Token의 유효기간 전까지는 Access Token을 새롭게 발급받을 수 있다. 

```
** Access Token은 탈취당하면 정보가 유출된다. 다만 짧은 유효기간 안에만 사용이 가능하기에 더 안전하다. 

** Refresh Token의 유효기간이 만료됐다면, 사용자는 새로 로그인해야 한다. Refresh Token도 탈취될 가능성이 있기 때문에 적절한 유효기간 설정이 필요하다.(보통 2주)
```

