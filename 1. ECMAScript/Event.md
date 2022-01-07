# DOM 이벤트 흐름

![image](https://i.stack.imgur.com/rUhpq.png)

ref. from [sof](https://stackoverflow.com/questions/38861601/how-to-only-trigger-parent-click-event-when-a-child-is-clicked), [W3](https://www.w3.org/TR/DOM-Level-3-Events/#dom-event-architecture)

## 문제

드래그 스크롤 가능한 div가 있다. 이 div 안에는 자식 div가 여러 개 나열되어 있다. 그런데 드래그를 하려고 클릭을 하면 필연적으로 자식 div를 건드릴 수 빆에 없는데 이때 불필요하게 자식 div의 이벤트를 발생시키게 된다. 이 때 부모 div만 이벤트를 발생시키고 자식은 가만히 둘 수는 없을까?

## 이벤트 발생과 DOM 이벤트 흐름

예시 코드

        <div id="granny">
            <div id="daddy">
                <div id="me">
                    family
                </div>
            </div>
        </div>
        <script>
            document.getElementById('granny').addEventListener('mouseup', () => console.log('granny'))
            document.getElementById('daddy').addEventListener('mouseup', () => console.log('daddy'))
            document.getElementById('me').addEventListener('mouseup', () => console.log('me'))
        </script>

이벤트 흐름은 3단계로 구분된다

- capture: root인 window 노드부터 시작하여 선택된 맨 끝단의 **부모**노드까지 도달하는 단계
- target: 맨 끝단의 노드(타겟 노드)에 이벤트가 도착하는 단계
- bubbling: 타겟 노드에서부터 root 노드까지 역순으로 이벤트가 전파되는 단계

기본적으로 이벤트가 발생하면 타겟의 이벤트가 가장 먼저 실행된다. 그 다음 bubbling 단계에 따라 말단 노드부터 루트 노드까지 역순으로 이벤트가 실행된다.

    > me
    > daddy
    > grammy

만약 capture 단계에서 이벤트를 발생시켜야 한다면 addEventLister의 3번째 인자인 useCapture를 true로 놓으면 된다. 그럼 capture 단계에서 root부터 말단 노드로 내려가는 도중에 이벤트가 발새하게 되는 것이다.

    document.getElementById('granny').addEventListener('mouseup', () => console.log('granny'))
    document.getElementById('daddy').addEventListener('mouseup', () => console.log('daddy'), true)
    document.getElementById('me').addEventListener('mouseup', () => console.log('me'))

    > daddy
    > me
    > grammy


## 이벤트의 전파 중단: stopPropagation()
capture와 bubbling은 발생한 이벤트를 전파하는 단계이다. 이 단계에서는 stopPropagation이라는 기능을 사용해서 전파를 끊을 수 있다. 만약 capture 단계에서 전파를 끊는다면 중간 노드에서 더 이상 자식 노드로 이벤트를 전파하지 않을 것이다. bubbling 단계에서 전파를 끊는다면 말단 노드에 이벤트를 발생시키는 과정에서 부모 노드에 이벤트를 발생시키지 않을 것이다.

    document.getElementById('granny')
        .addEventListener('mouseup', () => console.log('granny'))
    document.getElementById('daddy')
        .addEventListener('mouseup', (e) => {console.log('daddy'); e.stopPropagation()})
    document.getElementById('me')
        .addEventListener('mouseup', () => console.log('me'))

    > me
    > daddy

타겟에서 이벤트가 실행된 다음 bubbling되는 과정에서 daddy가 더이상 위로 bubbling을 하지 못하도록 stopPropagation을 했다. 그 결과 granny는 이벤트를 실행하지 못하게 되었다.

    document.getElementById('granny')
        .addEventListener('mouseup', () => console.log('granny'), true)
    document.getElementById('daddy')
        .addEventListener('mouseup', (e) => {console.log('daddy'); e.stopPropagation()}, true)
    document.getElementById('me')
        .addEventListener('mouseup', () => console.log('me'))

    > granny
    > daddy

이번엔 granny와 daddy 모두 capture 단계에서 이벤트를 발생시키도록 했다. 그 다음 daddy가 이벤트 전파를 끊어버리도록 했다. 그 결과 root에서 말단 방향으로 실행되었으나 중간에서 전파가 끊겨 결국 타겟 노드에 이벤트가 도달하지 못하고 끊겨버레기 되었다. 