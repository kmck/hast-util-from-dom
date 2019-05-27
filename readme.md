# hast-util-from-dom

[![Build][build-badge]][build]
[![Coverage][coverage-badge]][coverage]
[![Downloads][downloads-badge]][downloads]
[![Size][size-badge]][size]
[![Sponsors][sponsors-badge]][collective]
[![Backers][backers-badge]][collective]
[![Chat][chat-badge]][chat]

[**hast**][hast] utility to transform from a DOM tree.

## Install

[yarn][]:

```sh
yarn add hast-util-from-dom
```

[npm][]:

```sh
npm install hast-util-from-dom
```

## Usage

This utility is similar to [`hast-util-from-parse5`][hast-util-from-parse5], but
is intended for browser use and therefore relies on the native DOM API instead
of an external parsing library.

Say we have the following file, `example.html`:

```html
<!doctype html><title>Hello!</title><h1 id="world">World!<!--after--><script src="example.js" charset="UTF-8"></script>
```

Suppose `example.js` is a bundled version of something like this:

```js
import inspect from 'unist-util-inspect';
import fromDOM from 'hast-util-from-dom';

const hast = fromDOM(document);

console.log(inspect.noColor(hast));
```

Viewing `example.html` in a browser should yield the following in the console:

```text
root[2]
├─ doctype [name="html"]
└─ element[2] [tagName="html"]
   ├─ element[1] [tagName="head"]
   │  └─ element[1] [tagName="title"]
   │     └─ text: "Hello!"
   └─ element[1] [tagName="body"]
      └─ element[3] [tagName="h1"][properties={"id":"world"}]
         ├─ text: "World!"
         ├─ comment: "after"
         └─ element[0] [tagName="script"][properties={"src":"example.js","charSet":"UTF-8"}]
```

## API

### `fromDOM(node)`

Transform a DOM tree to a [**hast**][hast] [*tree*][tree].

This works in a similar way to the [`parse5`][hast-util-from-parse5] version
except that it works directly from the DOM rather than a string of HTML.
Consequently, it does not maintain [positional info][positional-information].

## Contribute

See [`contributing.md` in `syntax-tree/.github`][contributing] for ways to get
started.
See [`support.md`][support] for ways to get help.

This project has a [Code of Conduct][coc].
By interacting with this repository, organisation, or community you agree to
abide by its terms.

## License

[ISC][license] © [Keith McKnight][author]

<!-- Definitions -->

[build-badge]: https://img.shields.io/travis/syntax-tree/hast-util-from-dom.svg

[build]: https://travis-ci.org/syntax-tree/hast-util-from-dom

[coverage-badge]: https://img.shields.io/codecov/c/github/syntax-tree/hast-util-from-dom.svg

[coverage]: https://codecov.io/github/syntax-tree/hast-util-from-dom

[downloads-badge]: https://img.shields.io/npm/dm/hast-util-from-dom.svg

[downloads]: https://www.npmjs.com/package/hast-util-from-dom

[size-badge]: https://img.shields.io/bundlephobia/minzip/hast-util-from-dom.svg

[size]: https://bundlephobia.com/result?p=hast-util-from-dom

[sponsors-badge]: https://opencollective.com/unified/sponsors/badge.svg

[backers-badge]: https://opencollective.com/unified/backers/badge.svg

[collective]: https://opencollective.com/unified

[chat-badge]: https://img.shields.io/badge/join%20the%20community-on%20spectrum-7b16ff.svg

[chat]: https://spectrum.chat/unified/syntax-tree

[yarn]: https://yarnpkg.com/lang/en/docs/install

[npm]: https://docs.npmjs.com/cli/install

[license]: license

[author]: https://keith.mcknig.ht

[contributing]: https://github.com/syntax-tree/.github/blob/master/contributing.md

[support]: https://github.com/syntax-tree/.github/blob/master/support.md

[coc]: https://github.com/syntax-tree/.github/blob/master/code-of-conduct.md

[tree]: https://github.com/syntax-tree/unist#tree

[positional-information]: https://github.com/syntax-tree/unist#positional-information

[hast]: https://github.com/syntax-tree/hast

[hast-util-from-parse5]: https://github.com/syntax-tree/hast-util-from-parse5
