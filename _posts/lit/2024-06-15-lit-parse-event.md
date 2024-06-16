---
title: '[Lit] 자식에서 부모로 이벤트 보내기'
date: 2024-06-15 00:00:00 +0000
categories: [Lit]
tags: [Lit]
author: Sakua7
mermaid: true
---

<span style="color: #007bff; font-weight: bold;">본 게시물은 틀린 부분이 있을 수 있습니다, 참고 부탁드립니다. 🥹</span>

## 개발환경
* m1 mac

## 자식에서 부모로 이벤트 보내기

컴포넌트 구조를 사용해 개발을 하다 보면 자식 컴포넌트에서 발생한 이벤트를 부모에게 알려줘야 하는 경우가 있다, 다음 코드는 my-element에서 사용하는 my-item 컴포넌트의 버튼에서 click event가 발생했을 때 my-element에 결과를 알려주는 방법을 소개한다.

![customEvent_1](/assets/img/2024-06-15/customEvent_1.png)

Item1, Item2, Item3 버튼은 각각 독립적인 my-item 컴포넌트로 구성되어 있고 "Clicked: " 부분은 부모인 my-element에서 현재 클릭된 버튼이 무엇인지 보여주는 부분이다.

![customEvent_2](/assets/img/2024-06-15/customEvent_2.png)

자식 컴포넌트인 Item 버튼들을 클릭했을 때 부모의 "Clicked: " 가 변경된다.


## CustomEvent 소개

CustomEvent는 JavaScript에서 사용자가 직접 정의한 사용자 정의 이벤트를 생성하는 객체이다. 일반적으로 DOM 요소에 이벤트를 전달할 때 사용된다. CustomEvent를 사용하여 사용자 정의 이벤트를 생성할 때는 다음과 같은 단계를 따른다:

1. CustomEvent 생성자를 사용하여 새로운 사용자 정의 이벤트 객체를 만든다.
2. 생성자의 인자로 이벤트의 이름과 설정을 포함하는 옵션 객체를 전달한고 필요에 따라 추가적인 데이터를 이벤트 객체에 포함시킨다.
3. 생성된 이벤트 객체를 이벤트를 발생시키고자 하는 요소에 dispatchEvent() 메서드를 사용하여 전달한다.

아래 코드는 CustomEvent를 사용하여 'item-click'이라는 이름의 사용자 정의 이벤트를 생성하는 예시이다,

```javascript
_onClickBtn() {
    const event = new CustomEvent('item-click', {
        detail: { buttonName: this.buttonName },
        bubbles: false,
        composed: true
    })
    this.shadowRoot.dispatchEvent(event)
}
```

'item-click' 로 새로운 커스텀 이벤트 이름을 지정하고 세부 옵션을 설정해준 뒤 dispatchEvent()로 전달해준다.

* detail: detail 속성은 이벤트에 추가 데이터를 전달하는 데 사용됩니다. 이 속성은 이벤트 객체의 detail 속성에 포함되며, 이벤트 핸들러에서 해당 데이터를 사용할 수 있다.

* bubbles: bubbles 속성은 이벤트가 버블링되는지 여부를 결정한다. 즉, 해당 이벤트가 발생한 요소에서 상위 요소로 이벤트가 전파되는지 여부를 나타내는데 true로 설정하면 이벤트가 상위 요소로 버블링되며, false로 설정하면 이벤트가 상위 요소로 버블링되지 않는다.

* composed: composed 속성은 이벤트가 Shadow DOM 경계를 통과하여 외부로 전파되는지 여부를 결정한다. Shadow DOM을 사용하는 경우 기본적으로 이벤트는 Shadow DOM 내부에서만 처리되는데 true로 설정하면 이벤트가 Shadow DOM을 무시하고 외부로 전파되며, false로 설정하면 이벤트가 Shadow DOM 내부에 제한된다.


### 예시 코드

```javascript
// my-element.js
import {LitElement, html} from 'lit'
import { MyItem } from './my-item.js'

class MyElement extends LitElement {
  static properties = {
    clicked: {},
  };

  constructor() {
    super();
    this.clicked = '';
  }

  _clickHandler(e) {
    const buttonName = e.detail.buttonName
    this.clicked = buttonName
  }

  render() {
    return html`
      <div @click=${this._clickContainer}>
        <my-item @item-click=${this._clickHandler} .buttonName=${"Item1"}></my-item>
        <my-item @item-click=${this._clickHandler} .buttonName=${"Item2"}></my-item>
        <my-item @item-click=${this._clickHandler} .buttonName=${"Item3"}></my-item>
      </div>
      <p>Clicked: ${this.clicked}</p>
    `;
  }

}
customElements.define('my-element', MyElement);
```

```javascript
// my-item.js
import { LitElement, html } from "lit";

export class MyItem extends LitElement {
    static get properties() {
        return {
            buttonName: { type: String }
        }
    }

    constructor() {
        super();
        this.buttonName = ''
    }

    _onClickBtn() {
        const event = new CustomEvent('item-click', {
            detail: { buttonName: this.buttonName },
            bubbles: false,
            composed: true
        })
        this.shadowRoot.dispatchEvent(event)
    }

    render() {
        return html`
            <button @click=${this._onClickBtn}>${this.buttonName}</button>
        `
    }
}

customElements.define('my-item', MyItem)
```

### 결론

CustomEvent를 이용하면 부모-자식 간의 통신이 가능하다.

