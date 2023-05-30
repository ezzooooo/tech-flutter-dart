# 플러터 UI

## 플러터 위젯

* 플러터 위젯은 React에서 영감을 받아 개발됨
* 핵심 아이디어는 위젯으로 UI를 구축한다는 것
* 위젯은 현재 구성 및 상태가 어떻게 보여야하는지 나타냄
* 위젯의 상태가 변하면 상태 변경에 영향을 받는 최소한의 부분을 리빌딩

## Hello World

* runApp() 함수로 위젯을 호출하는 최소한의 Flutter App

> void runApp(Widget app) : 인자로 전달된 위젯을 위젯 트리 최상단(화면)에 띄우는 함수
>> runApp을 두 번 호출하게 될 경우 기존에 있던 Root 위젯이 화면에서 떼어내지고 전달받은 위젯이 그 위치를 대신하게 된다. 새로운 위젯 트리는 이전 위젯트리와 비교한 후 모든 차이점이 렌더 트리에 적용된다. 이는 StatefulWidget이 setState 함수를 호출한 뒤 리빌딩 되는 것 과 유사하다.

```dart
import 'package:flutter/material.dart';

void main() {
    runApp(
        const Center(
            child: Text(
                'Hello, world!',
                textDirection: TextDirection.ltr,
            ),
        ),
    );
}
```

위 예제 코드에서는 Center 위젯과 그 하위 위젯인 Text 위젯, 2개의 위젯이 위젯 트리를 구성하게 됨. 프레임워크는 루트 위젯이 화면을 덮도록 강제함. 즉 "Hello, world"라는 Text 위젯이 화면 정중앙에 위치함. 현재 예제에서는 MaterialApp 위젯을 사용하지 않았기 때문에 textDirection을 별도로 지정해줘야 함.

위젯의 중요한 일은 build() 함수를 구현하는 것이다. 즉, 하위 수준의 위젯(RenderObject) 관점에서 이 위젯을 설명하는 것이다. 프레임워크는 기초가 되는 최하단 RenderObject 위젯이 나타날 때까지 차례대로 빌드를 진행한다.

> Widget build(BuildContext context) : 이 위젯이 UI에 어떻게 나타날지를 설명하는 함수
>
> * StatelessWidget class와 State class의 abstract method이기 때문에 반드시 구현을 해야한다.  
> * 이 함수는 위젯이 지정된 BuildContext 트리에 삽입되거나, 위젯의 종속성이 변경되었을 때(참조하던 Inherited 위젯이 변경) 호출된다. 이 함수는 매 프레임마다 호출될 수 있고, 위젯을 빌드하는 것 이외에 어느 Side Effects도 가져선 안된다.  
> * 프레임워크는 Build 함수에서 반환 된 위젯으로 기존 서브트리를 업데이트하거나, 기존 서브트리를 제거한 후 새로운 서브트리를 팽창하여 이 위젯 아래의 서브트리를 대체한다. 서브트리를 업데이트 할 수 있는지의 여부는 Widget.canUpdate 함수를 통해 결정된다.
>
>> bool canUpdate(Widget oldWidget, Widget newWidget) : newWidget을 사용하여 oldWidget의 현재 구성된 Element를 업데이트 할 수 있는지 여부를 판단하는 함수
>>
>> * Widget class의 static method
>> * runtimeType과 key가 같은 두 Widget의 Element는 다른 Widget의 구성 Element로 사용될 수 있다.
>> * 만약 두 Widget의 key 값이 null이라면 완전히 다른 두 Widget이어도 runtimeType이 동일한지만 고려한다.
>>
>>> Element class
>>>
>>> * 모든 Widget의 인스턴스화, 업데이트, 소멸 등을 처리하는 클래스
>>> * Widget을 사용하여 트리를 구성한다.
>>> * Flutter의 기본 위젯이라고 할 수 있는 StatelessWidget, StatefulWidget, InheritedWidget은 각각 StatelessElement, StatefulElement, InheritedElement에 의해 관리된다.
>>> * StatefulElement의 경우 State 객체를 통해 UI를 업데이트한다.

RenderObject란?
> RenderObject에 대한 설명
