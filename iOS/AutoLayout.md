# AutoLayout

## AutoLayout의 기본

- 뷰의 x, y 위치
- 뷰의 크기

위와 같은 두 가지를 알면 레이아웃을 자동으로 계산하여 보여준다.



## FirstItem, SecondItem, Relation

오토레이아웃을 잘 쓰기 위해서는 다음과 같은 관계를 이해해야한다.![](https://images.velog.io/images/dmsgk/post/b150f3da-279b-4045-aa10-35c117a782b6/img1.daumcdn.png)

간단하게 요약하자면 FirstItem의 Attribute와 SecondItem의 Attribute와의 y = ax+b와 같은 꼴인 선형관계식으로 오토레이아웃이 설정된다는 것이다. 여기서 생각해야 할 점은 화면의 좌표는 원점은 화면 왼쪽 구석이고, x값이 오른쪽으로 그리고 y값이 아래로 갈수록 숫자가 커지는 형태로 구성되어 있다는 점이다. 아래 TextView끼리 오토레이아웃을 설정한 예시를 통해 살펴보자. 

| ![](https://images.velog.io/images/dmsgk/post/084f0382-956c-4def-a1d2-487918373053/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-05-27%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%209.22.59.png) | ![](https://images.velog.io/images/dmsgk/post/0047bcb8-a8c1-4928-8a76-d231fc546120/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-05-27%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%209.21.09.png) |
| ------------------------------------------------------------ | ------------------------------------------------------------ |

 First item.attribute는 파란색 왼쪽이고, Second item.attribute는 초록색 왼쪽이다. 그리고 여기서 계수는 1로 설정되어있고, 상수값은 60으로 되어있다. 이는  First item.attribute이 Second item.attribute보다 양(+)의 방향으로 60만큼 떨어져있다는 이야기이다. 음(-)으로 60 설정하면 다음과 같이 변하게 된다. 

| ![](https://images.velog.io/images/dmsgk/post/f8b21a18-9314-45e2-8053-455917f15e70/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-05-27%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%2010.04.18.png) | ![](https://images.velog.io/images/dmsgk/post/c8f63c6c-37ac-4b3d-9162-eed51bf40366/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-05-27%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%2010.09.32.png) |
| ------------------------------------------------------------ | ------------------------------------------------------------ |



## Attributes and Others

<img src="https://developer.apple.com/library/archive/documentation/UserExperience/Conceptual/AutolayoutPG/Art/attributes_2x.png" alt="image: ../Art/attributes_2x.png" style="zoom:50%;" />

- UIKit에서는 width, height보다 anchor를 우선순위로 둔다. 





### References

- https://www.youtube.com/watch?v=1McZ6ukrmFo&list=PLgOlaPUIbynpvYsyKTrH2bpVlOCHkz6OY
- https://zeddios.tistory.com/380