<img src="logo.png" width="260" />

![NPM version badge](https://img.shields.io/npm/v/html-to-react-components.svg?style=flat-square)

Extract annotated portions of HTML into React components as separate modules. The structure of HTML is preserved by importing child components and replacing appropriate pieces of HTML with them. As a result you get an entire components tree ready to be rendered.

![usage example animation](sample.gif)

## When to use it

This utility was designed to free React developers from a boring work of translating HTML into components.

Imagine you just got a pile of HTML from your designers. The first thing you will do is break HTML into React components. This is boring and we can automate this.

## Installation

```
$ npm i html-to-react-components
```

## Usage

HTML components should be annotated with `data-component` attribute. The value of the attribute is the name of the React component.

See `test.js` file for usage example with more options.

```js
import extractReactComponents from 'html-to-react-components';

extractReactComponents(
`<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Document</title>
</head>
<body>

  <header class="header" data-component="Header">

    <h1 class="heading" data-component="Heading">Hello, world!</h1>

    <nav class="nav" data-component="Nav">
      <ul class="list">
        <li class="list-item" data-component="ListItem">#1</li>
        <li class="list-item" data-component="ListItem">#2</li>
      </ul>
    </nav>

  </header>

</body>
</html>
`, { componentType: 'stateless' });

/*
{ Header: 'const Header = () => <header className="header">\n\n    <Heading></Heading>\n\n    <Nav></Nav>\n\n  </header>;',
  Heading: 'const Heading = () => <h1 className="heading">Hello, world!</h1>;',
  Nav: 'const Nav = () => <nav className="nav">\n      <ul className="list">\n        <ListItem></ListItem>\n        <ListItem></ListItem>\n      </ul>\n    </nav>;',
  ListItem: 'const ListItem = () => <li className="list-item">#2</li>;' }
*/
```

## Options

### componentType

Type of generated React components.

Values:

- `stateless`
- `es5` (default)
- `es6`

### moduleType

Type of generated JavaScript modules.

Values:

- `false` (do not extract components as modules)
- `es6` (default)
- `cjs` (CommonJS)

### moduleFileNameDelimiter

Delimiter character to be used in modules filename.

Default value is `-`.

### output

Configuration options for output to file system.

#### path

Output directory path.

#### fileExtension

Output files extension.

Default value is `js`.

## License

MIT
