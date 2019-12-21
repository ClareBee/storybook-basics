

This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

https://www.learnstorybook.com/intro-to-storybook/react/en/get-started/

```
# Create our application:
npx create-react-app taskbox
cd taskbox

# Add Storybook:
npx -p @storybook/cli sb init

# Run the test runner (Jest) in a terminal:
yarn test

# Start the component explorer on port 9009:
yarn run storybook

# Run the frontend app proper on port 3000:
yarn start
```
> Component-Driven Development (CDD) methodology. It’s a process that builds UIs from the “bottom up” starting with components and ending with screens

> Visual Test Driven Development - applies the test-driven development process to UI components.

### Stories
- as many stories per component as needed
- `storiesOf()` - registers the component w display name
- `action()` - creates callback to appear in sidepanel or Storybook UI, bundled into `...actions` - & helps you verify interactions when building components in isolation
```javascript
<Task {...actions}> is equivalent to <Task onPinTask={actions.onPinTask} onArchiveTask={actions.onArchiveTask}>.
```
- `add()` - called once per test state, and generates a story

> The action story is a function that returns a rendered element (i.e. a component class with a set of props) in a given state---exactly like a React Stateless Functional Component.

----
### Storyshots
> Snapshot testing refers to the practice of recording the “known good” output of a component for a given input and then flagging the component whenever the output changes in future.

`yarn add --dev @storybook/addon-storyshots react-test-renderer require-context.macro`
`yarn add --dev babel-plugin-macros`
```
// .babelrc

{
  "plugins": ["macros"]
}
```
```javascript
// src/storybook.test.js

import initStoryshots from '@storybook/addon-storyshots';
initStoryshots();
```

```javascript
// .storybook/config.js

import { configure } from '@storybook/react';
import requireContext from 'require-context.macro';

import '../src/index.css';

const req = requireContext('../src/components', true, /\.stories\.js$/);

function loadStories() {
  req.keys().forEach(filename => req(filename));
}

configure(loadStories, module);
```
---
### Decorators
>Decorators (`addDecorator()`) are a way to provide arbitrary wrappers to stories. [...] They can also be used to wrap stories in “providers” –i.e. library components that set React context.
---

### Unit tests w Jest & test renderer Enzyme
- for details e.g. order of rendering in DOM
- elements from stories can be reused in tests
- prefer snapshots/visual regression for UI as less brittle than Unit tests?
