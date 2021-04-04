1. 깃 폴더로 이동


2. rebase 명령어를 입력

   ```
   $ git rebase HEAD~[거슬러 올라가고 싶은 커밋 수] -i
   ```

   예를 들어, 바로 전 커밋의 메세지를 재작성하고 싶다면

   ```
   $ git rebase HEAD~1 -i
   ```

   이렇게 한다.

3. 이 때 뜨는 화면에서 **pick**이라는 단어를 **reword**로 변경한다.

   ![image](https://user-images.githubusercontent.com/43662673/116249826-27435300-a7a8-11eb-8798-89083e427e73.png)

   여기 맨 위의 pick을 

   ![image](https://user-images.githubusercontent.com/43662673/116249876-33c7ab80-a7a8-11eb-9af1-a156599fb031.png)

   reword로 수정!

   ```
   참고로, 키보드 i를 누르면 --insert--모드가 되어 글을 수정할 수 있다.
   글을 다 수정한 뒤에는 ESC 버튼을 누르고 :wq!를 써주면 저장하고 나갈 수 있다.
   ```

   ​

4. 그 다음 커밋 메세지가 기록되어 있는 화면이 보이면, 여기서 커밋 메세지를 수정한다.

   ![image](https://user-images.githubusercontent.com/43662673/116249977-49d56c00-a7a8-11eb-9bc0-c9f321ff75bc.png)

   ```
   참고로, 키보드 i를 누르면 --insert--모드가 되어 글을 수정할 수 있다.
   글을 다 수정한 뒤에는 ESC 버튼을 누르고 :wq!를 써주면 저장하고 나갈 수 있다.
   ```

   ​

5. 강제 **push** 하여 수정 내용을 현재 브랜치에 강제 푸시한다.

   ```
   $ git push origin [브랜치명] -f
   ```

   원격 저장소에 반영하려면

   ````
   $ git push --force
   ````

   하면 된다고 하는데, 위에 있는 명령어만 해도 원격 저장소에 바뀌었다..!