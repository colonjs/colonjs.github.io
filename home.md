<!-- ![Banner](./images/banner.png) -->

# :colon - JavaScript template engine.

<a href="https://travis-ci.org/colonjs/colon">
    <img src="https://travis-ci.org/colonjs/colon.svg?branch=master" alt="Travis-ci">
</a>
<a href="https://www.npmjs.com/package/colon">
    <img src="https://img.shields.io/npm/v/colon.svg" alt="NPM Version">
</a>
<a href="https://www.npmjs.com/package/colon">
    <img src="https://img.shields.io/npm/dt/colon.svg" alt="NPM Downloads">
</a>
<a href="javascript:;">
    <img src="https://img.shields.io/github/size/colonjs/colon/dist/colon.min.js.svg" alt="size">
</a>
<a href="https://github.com/colonjs/colon/blob/master/LICENSE">
    <img src="https://img.shields.io/github/license/colonjs/colon.svg" alt="MIT License">
</a>

## Installation

### CDN

```html
<!-- Production Build -->
<script src="https://unpkg.com/colon/dist/colon.min.js"></script>

<!-- Development Build -->
<script src="https://unpkg.com/colon/dist/colon.js"></script>
```

### NPM

```bash
$ npm install colon
```

```js
import colon from 'colon';
```

## Getting Started

```html
<body>
    <script src="https://unpkg.com/colon/dist/colon.min.js"></script>
    <script>
        // Our Code Goes Here
    </script>
</body>
```

## Initialization

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
    template: document.querySelector('.app'),
    data,
    computed: {
        fullName() {
            return this.user.firstName + this.user.lastName;
        },
    },
});
```

template:

```html
<div class="app">
    <div class="profile">
        <div class="avatar">
            <img :src="user.avatar" alt="{{ user.firstName }}">
        </div>
        <p><span :text="fullName"></span></p>
    </div>
    <ul class="moments" :if="moments.length">
        <li :each="moment in moments" :show="moment.show">{{ moment.content }}</li>
    </ul>
</div>
```

Render as:

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

## Templates

`colon` has a custom templating syntax `{{}}`. All attributes (except directives, it use js syntax) and text are compiled for these templates.

## Directives

### `if`

- Expects: `any`
- Details: Conditionally render the template based on the truthy-ness of the given expression value.
- Usage:

```html
<span :if="true">Just Me.</span>
```

### `each`

- Expects: `Array`
- Usage:

You can specify an alias by use the special syntax `alias in expression` or use the default alias `item` and `index`.

```html
<li :each="comments" data-index="{{ index }}">{{ item.content }}</li>
<li :each="comment in comments">{{ comment.content }}</li>
<li :each="(comment, aliasIndex) in comments" data-index="{{ aliasIndex }}">{{ comment.content }}</li>
```

### `show`

- Expects: `Array`
- Details: Toggle’s the element's display CSS property based on the truthy-ness of the given expression value.
- Usage:

```html
<span :show="true">Just Me.</span>
<span :show="false">Hello World.</span>
```

### `text`

- Expects: `String`
- Details: Updates the element’s textContent.
- Usage:

```html
<span :text="message"></span>
<!-- same as -->
<span>{{ message }}</span>
```

### `src`

- Expects: `String`
- Details: Updates the image's `src`, this can avoid image rendering failed before `colon` work.
- Usage:

```html
<img :src="avatar" alt="Just">
<!-- If use interpolation in `src`, -->
<!-- the picture will fail to render before the `colon` works -->
<img src="{{ avatar }}" alt="Just">
```

## Class and Style Bindings

### Class Bindings

- Expects: `Object|Array<Object>`
- Details: We can pass an object or an array to `:class` to dynamically update classes:
- Usage:

```html
<span :class="{ active: isActive }"></span>
<span :class="[{ active: isActive }, { 'is-fixed': isFixed }]"></span>
```

And the following data:

```js
data: {
    isActive: true,
    isFixed: true,
}
```

will render as:

```html
<span class="active"></span>
<span class="active is-fixed"></span>
```

### Style Bindings

- Expects: `Object|Array<Object>`
- Details: We can pass an object or an array to `:style` to dynamically update styles. You can use either camelCase or kebab-case (use quotes with kebab-case) for the CSS property names.
- Usage:

```html
<span :style="{ color: activeColor, fontSize: fontSize + 'px' }"></span>
<span :style="[styleObject1, styleObject2]"></span>
```

And the following data:

```js
data: {
    activeColor: '#42b983',
    fontSize: 16,
    styleObject1: {
        color: '#42b983',
        backgroundSize: 'cover',
    },
    styleObject2: {
        fontSize: 16 + 'px',
    },
}
```

will render as:

```html
<span style="color: #42b983; font-size: 16px;"></span>
<span style="color: #42b983; font-size: 16px; background-size: cover;"></span>
```
