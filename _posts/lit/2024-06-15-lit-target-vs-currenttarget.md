---
title: '[Lit] target vs currentTarget'
date: 2024-06-09 00:00:00 +0000
categories: [Lit, Js]
tags: [Lit, Js]
author: Sakua7
mermaid: true
---

<span style="color: #007bff; font-weight: bold;">본 게시물은 틀린 부분이 있을 수 있습니다, 참고 부탁드립니다. 🥹</span>

## 개발환경
* m1 mac
  
## target vs currentTarget

* target - 실제로 event가 발생한 요소를 지칭한다, 예를 들어 버튼을 클릭하면 target은 실제 클릭된 버튼 요소를 가리킨다.
* currentTarget - 현재 이벤트 핸들러가 등록된 요소를 가리킨다.

```js
import {LitElement, html} from 'lit'

class MyElement extends LitElement {
  static properties = {
    clicked: {},
  };

  constructor() {
    super();
    this.clicked = '';
  }

  _clickDiv(event) {
    console.log('div.target -> ', event.target)
    console.log('div.currentTarget -> ', event.currentTarget)
  }

  _clickBtn(event) {
    console.log('btn.target -> ', event.target)
    console.log('btn.currentTarget -> ', event.currentTarget)
  }

  render() {
    return html`
      <div @click=${this._clickDiv}>
        <button @click=${this._clickBtn}>BtnA</button>
        <button @click=${this._clickBtn}>BtnB</button>
        <button @click=${this._clickBtn}>BtnC</button>
      </div>
    `;
  }

}
customElements.define('my-element', MyElement);
```

위 코드에서 각각 div와 button에 click 이벤트를 달아주었다.


![B](/assets/img/2024-06-15/target_1.png)

![C](/assets/img/2024-06-15/target_2.png)

button을 클릭했을때 btn의 target과 currentTarget 둘 다 button으로 나오지만 div의 target은 그대로 button으로 currentTarget은 \<div>...\</div> 가 나오는걸 볼 수 있다.

![A](/assets/img/2024-06-15/target_3.png)

![D](/assets/img/2024-06-15/target_4.png)

div를 클릭했을땐 div의 target은 클릭 대상인 \<div>...\</div> 이며 currentTarget 역시 마찬가지로 \<div>...\</div>

즉 
target: 이 속성은 실제로 이벤트가 발생한 요소를 가리킨다. 예를 들어, 버튼을 클릭하면 target은 클릭된 버튼 요소를 가리키는데 이것은 이벤트의 실제 대상이다.

(위의 예시에서 btn, div의 target 모두 클릭한 요소를 target으로 보여 주고있다.)

currentTarget: 이 속성은 현재 이벤트 핸들러가 등록된 요소를 가리킨다. 이벤트 핸들러가 실제로 연결된 요소이며, 이벤트가 발생한 요소와는 상관없이 항상 이벤트 핸들러가 등록된 요소를 가리키며 주로 이벤트를 캡처하거나 버블링하는 동안 이벤트 핸들러가 등록된 요소를 식별하는 데 사용된다.

(button을 클릭했을때 div.currentTarget이 \<button>BtnB\</button> 이 아닌 이유는 div의 이벤트 핸들러가 \<div>...\</div> 이곳에 등록되있기 때문이다.)

