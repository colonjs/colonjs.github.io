<!-- ![Banner](./images/banner.png) -->

# :colon - JavaScript template engine.

[![Travis-ci](https://travis-ci.org/colonjs/colon.svg?branch=master)](https://travis-ci.org/colonjs/colon)

## Usage

```html
<div class="app">
    <div class="profile">
        <div class="avatar">
            <img :src="user.avatar" alt="{{ user.firstName }}">
        </div>
        <p><span :text="fullName"></span></p>
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
        firstName: `Just`,
        lastName: `Me`,
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

colon({
    template: `.app`,
    data,
    computed: {
        fullName() {
            return this.firstName + this.lastName;
        },
    },
});
```

```html
<div class="colon">
    <div class="profile">
        <div class="avatar">
            <img src="./images/avatar.jpg" alt="Just">
        </div>
        <p><span>Just Me</span></p>
    </div>
    <ul class="moments">
        <li style="display: block;">Hello World</li>
        <li style="display: none;">Hello World</li>
        <li style="display: block;">Hello World</li>
    </ul>
</div>
```

## Directives

### `if`

> Not render in DOM

```html
<span :if="true">Just Me.</span>
```

### `each`

> The variables in each list are `item`

```html
<li :each="comments">{{ item.content }}</li>
```

### `show`

> :show="true" => display: block;

> :show="false" => display: none;

```html
<span :show="true">Just Me.</span>
<span :show="false">Hello World.</span>
```

### `text`

> Updates the element's textContent.

```html
<span :ext="message"></span>
<!-- same as -->
<span>{{ message }}</span>
```

### `src`

> Avoid image rendering failed before the template engine work.

```html
<img :src="avatar" alt="Just">
<!-- If use interpolation in `src`, -->
<!-- the picture will fail to render before the template engine works -->
<img src="{{ avatar }}" alt="Just">
```
