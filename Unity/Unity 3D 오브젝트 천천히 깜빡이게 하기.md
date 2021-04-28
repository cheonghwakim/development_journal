오브젝트를 투명도를 조절하기 위해선 알파값을 변경해 주면 되는데, 일단 아래처럼 변경하는 것이다.

```
Color currentColor = obj.GetComponent<MeshRenderer>().material.color;
currentColor.a = (0-1사이의 숫자);
```



0에 가까울수록 투명한거고, 1에 가까울수록 불투명하다.

따라서 천천히 사라졌다가 천천히 나타나게 하는 코드는 아래처럼 짜면 된다.

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Constellation : MonoBehaviour
{
    // 오브젝트 이름
    public GameObject constell;

    //천천히 깜빡이는 방향(나타나거나 사라지거나... 나는 true를 나타내고, false를 사라지는 방향으로 했다.)
    public bool dir = false;

    void Start()
    {
        
    }

    void Update()
    {
        if (dir==true) //나타내기
        {
            show(constell);
        }
        else //사라지기
        {
            hide(constell);
        }
    }

    void show(GameObject obj)
    {
        Color currentColor = obj.GetComponent<MeshRenderer>().material.color;
        //1은 불투명
        currentColor.a += 0.003f;//크게할수록 빨리 나타남
        if(currentColor.a >= 1){//완전히 불투명이 되면, 사라지는쪽으로 방향을 바꿈
            dir = false;
        }
        obj.GetComponent<MeshRenderer>().material.color = currentColor;
    }

    void hide(GameObject obj)
    {
        Color currentColor = obj.GetComponent<MeshRenderer>().material.color;
        //0은 투명
        currentColor.a -= 0.003f;//크게할수록 빨리 사라짐
        if(currentColor.a <= 0.2){//완전히 사라졌다가 나타나고 싶으면 0.2가 아니라 0으로하면 된다.
            dir = true;
        }
        obj.GetComponent<MeshRenderer>().material.color = currentColor;
    }
}
```



나는 천천히 반짝이는 별자리를 표현하려고 살짝 사라졌다가 선명하게 나타내기 위해서 알파값이 0.2 밑으로 떨어지지 않게 했다.

완전히 사라지고 싶게 하면 if(currentColor.a <= 0.2) 부분을 if(currentColor.a <= 0)으로 바꿀것.

+@ 참고로, Update()함수는 1초에 60번 실행되기 때문에, 0.003f 이부분은 눈치껏 바꾸자

크게할수록 빨리 깜빡이고, 작게할수록 느리게 깜빡인다. 나같은 경우는 0.003f가 적당했다.

(참고)

<https://docs.unity3d.com/ScriptReference/Color-a.html>