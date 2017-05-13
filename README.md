<!-- ![Banner](./images/banner.png) -->

# :colon - template engine.

[![Travis-ci](https://travis-ci.org/JustClear/colon.svg?branch=master)](https://travis-ci.org/JustClear/colon)

## Usage

```html
<div class="colon">
    <div class="profile">
        <div class="avatar">
            <img :src="user.avatar" alt="{{ user.name }}">
        </div>
        <p><span :text="user.name"></span></p>
    </div>
    <ul class="moments" :if="moments.length">
        <li :each="moments" :show="item.show">{{ item.content }}</li>
    </ul>
</div>
```

```js
import colon from 'colon';

const data = {
    user: {
        avatar: `./images/avatar.jpg`,
        name: `Just`,
    },
    moments: [{
        content: `Hello World.`,
        show: true,
    }, {
        content: `Hello World.`,
        show: false,
    }, {
        content: `Hello World.`,
        show: true,
    }],
};

colon(`.colon`, data);
```

```html
<div class="colon">
    <div class="profile">
        <div class="avatar">
            <img src="./images/avatar.jpg" alt="Just">
        </div>
        <p><span>Just</span></p>
    </div>
    <ul class="moments">
        <li style="display: block;">Hello World</li>
        <li style="display: none;">Hello World</li>
        <li style="display: block;">Hello World</li>
    </ul>
</div>
```
