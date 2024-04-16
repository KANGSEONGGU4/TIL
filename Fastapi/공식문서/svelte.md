## Svelte란?

Svelte는 React, Vue.js 등과 비슷한 역할을 하는 프론트엔드용 웹 프레임워크이다. 2016년에 Rich Harris에 의해 최초 발표되었으며 현재 꾸준한 인기를 얻고 있는 프레임워크이다.

Svelte의 장점
- write less code - 다른 프론트엔트 프레임워크에 비하여 작성해야 할 코드들이 적다. 어떤 기능을 구현하기 위해 가독성은 떨어지지만 어쩔 수 없이 작성해야 하는 틀에 짜인 코드를 boilerplate 코드라고 하는데 Svelte는 이러한 부분들이 거의 없다. 단순하고 이해하기 쉬운 코드만이 존재한다.
- No vitual Dom - React나 Vue.js와 같은 프레인워크는 가상돔을 사용하지만 Svelte는 가상돔을 사용하지 않는다. Sevelte는 가상돔을 사용하지 않는 대신 실제 Dom을 반영한다. Svelte는 앱을 실행 시전에서 해석하지 않고 빌드 시전에서 Vanilla JavaScript Bundle로 컴파일하여 속도가 빠르고 따로 라이브러리를 배포할 필요가 없어 간편하다.
- Truly reactive - 복잡한 상태 관리를 위한 지식 및 라이브러리들이 필요없다. Svelte는 순수 자바스크립트만으로 그 기능을 이해하기 쉽게 구현했다.
