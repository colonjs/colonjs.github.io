<!-- ![Banner](./images/banner.png) -->

# :colon - JavaScript template engine.

[![Travis-ci](https://travis-ci.org/colonjs/colon.svg?branch=master)](https://travis-ci.org/colonjs/colon)
[![npm](https://img.shields.io/npm/v/colon.svg)](https://www.npmjs.com/package/colon)

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
    template: `.app`,
    data,
    computed: {
        fullName() {
            return this.firstName + this.lastName;
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
        <li :each="moments" :show="item.show">{{ item.content }}</li>
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

`colon` has a custom templating syntax (`{{}}`). All attributes (except directives, it use js syntax) and text are compiled for these templates.

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
- Details: Render a set of elements based on the given data. For each item, the variable `item` is used to indicate the value.
- Usage:

```html
<li :each="comments">{{ item.content }}</li>
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
