# React Typist Component

Create typewriter effect by setting up a component's children directly.

## Caveat ⚠

This package is not production-ready, Use it with caution.

## Install

```bash
npm install react-typist-component
# or
yarn add react-typist-component
```

## Example

```jsx
import Typist from 'react-typist-component';

const MyComponent = () => {
  return (
    <Typist typingDelay={100} cursor={<span className="cursor">|</span>}>
      This is a typo
      <br />
      <Typist.Backspace count={5} />
      <Typist.Delay ms={1500} />
      react component
      <Typist.Paste>
        <div>
          use
          <div>deeper div</div>
        </div>
      </Typist.Paste>
    </Typist>
  );
};
```

## API reference

### `Typist`

```ts
type TypistProps = {
  children: React.ReactNode;
  typingDelay?: number;
  backspaceDelay?: number;
  loop?: boolean;
  pause?: boolean;
  startDelay?: number;
  finishDelay?: number;
  onTypingDone?: () => void;
  splitter?: (s: string) => string[];
  cursor?: string | React.ReactElement;
  disabled?: boolean;
};
```

#### `children`

The contents that will be rendered with typewriter effect. It accepts nested elements, so you can easily style your contents.

Note that `Typist` treats the element whose children is `null` or `undefined` as a single token. For example:

```jsx
const Foo = () => {
  return <div>Foo</div>;
};

// The text "Foo" will be displayed after "123" immediately instead of displayed seperately
const App = () => {
  return (
    <Typist>
      123
      <Foo />
    </Typist>
  );
};
```

#### `typingDelay`

**Default**: `75`

The delay after typing a token.

#### `backspaceDelay`

**Default**: `75`

The delay after backspacing a token.

#### `loop`

**Default**: `false`

`Typist` will automatically restart the typing animation if this value is `true`.

#### `pause`

**Default**: `false`

Set to `true` if you want to pause the typing animation.

#### `startDelay`

**Default**: `0`

If this value is larger than `0`, then `Typist` will wait for this delay before starting the typing animation.

#### `finishDelay`

**Default**: `0`

If this value is larger than `0`, then `Typist` will wait for this delay after finishing the typing animation.

#### `onTypingDone`

**Default**: `() => {return}`

This function will be called when the typing animation finishes.

#### `splitter`

**Default**: `(str: string) => str.split('')`

`Typist` will use this to get tokens from strings. It may be useful when you want to split your string in different way. For example, you can use [grapheme-splitter](https://github.com/orling/grapheme-splitter) to split string if your string contains emoji.

#### `cursor`

Will be inserted after the last typed token.

#### `disabled`

**Default**: `false`

Set to `true` if you don't want the typing animation anymore.

### `Typist.Backspace`

```ts
type Props = {
  count: number;
};
```

#### `count`

The number of tokens that will be backspaced.

### `Typist.Delay`

```ts
type Props = {
  ms: number;
};
```

#### `ms`

The duration of the delay in milliseconds.

### `Typist.Paste`

```ts
type Props = {
  children: React.ReactNode;
};
```

#### `children`

Children inside this component will be pasted without typewriter effect.
