# BOM과 DOM
## BOM(Browser Object Model)
- 브라우저의 창이나 프레임을 프로그래밍적으로 제어할 수 있게 해주는 객체모델. 이를 통해서 브라우저의 새 창을 열거나 다른 문서로 이동하는 등의 기능을 실행시킬 수 있다.
- 전역객체로 window가 있으며 하위 객체들로 location, navigator, document, screen, history가 포함되어 있다.

## DOM(Document Object Model)
- 웹페이지를 프로그래밍적으로 제어할 수 있게 해주는 객체모델이다. 최상위 인터페이스로 Node가 있다.

- Live DOM Viewer를 사용해서 DOM 트리를 구성해 본것으로 엘리먼트 뿐만 아니라 텍스트 노드와 주석 노드까지 포함하고 있다. 이제 이런 DOM을 다루기 위해선 getElementsById, querySelector, firstElementChild 등 과 같은 브라우저가 제공하는 DOM API를 사용하면 된다.