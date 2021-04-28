구글 웹폰트는 엄청 구리고 종류가 적기 때문에 나는 눈누 웹폰트를 사용한다.

\1. 원하는 폰트 복사

(@font-face 로 시작하는것밖에 안해봤는데 다른건 어떻게 하는지 추가 예정)

![img](https://postfiles.pstatic.net/MjAyMTA0MTZfMjE4/MDAxNjE4NTUzNzYxNDAx.XlY8QTKxTmyzSrg57gFmjLReGnw7z6WDQil7cWOgmvwg.VEtUClOZ6ashamxddMr4YqIU2qSLlyOKl-gKfpHTUU4g.PNG.evanmacmillan/font.png?type=w966)

\2. style 태그 안에 붙여넣기

<style type='text/css'>
@font-face {
    font-family: 'HeirofLightBold';
    src: url('https://cdn.jsdelivr.net/gh/projectnoonnu/noonfonts_20-07@1.0/HeirofLightBold.woff') format('woff');
    font-weight: normal;
    font-style: normal;
}
</style>

\3. css적용

<style type='text/css'>
.적용할클래스이름{
  font-family: 'HeirofLightBold'; //이부분은 2번의 font-family랑 똑같음
}
</style>



https://noonnu.cc/
