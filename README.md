https://clarebee.github.io/storybook-basics

*This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).*

From:
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


### Testing UI

From website:
- **Visual tests** rely on developers to manually look at a component to verify it for correctness. They help us sanity check a component’s appearance as we build.
- **Snapshot tests with Storyshots** capture a component’s rendered markup. They help us stay abreast of markup changes that cause rendering errors and warnings.
- **Unit tests with Jest** verify that the output of a component remains the same given an fixed input. They’re great for testing the functional qualities of a component.
- **Visual Regression tests** to catch changes in appearance, e.g. via Chromatic addon.

### Addons

- https://storybook.js.org/docs/addons/addon-gallery/
- https://github.com/storybookjs/storybook/tree/next/dev-kits

Register addons in `.storybook/addons.js` (order matters)

**Knobs** - makes it interactive (can accept different input types from user, e.g. object - useful for testing edge cases too!)

> the object knob type accepts a label and a default object as parameters. The label is constant and shows up to the left of a text field in your addons panel. The object you've passed will be represented as an editable JSON blob. As long as you submit valid JSON, your component will adjust based upon the data being passed to the object!

### Creating Addons
- register in .storybook/addons.js
- include in .storybook/addons/filename.js

e.g. via
`yarn add @storybook/api @storybook/components @storybook/theming @babel/preset-react`

Fromm "@storybook/api":
`.addParameters();` - inject custom parameters into stories
`.useStorybookState();`
`.useAddonState();` - persists local state

From "@storybook/components":
AddonPanel - to display
ActionBar - to change between items

### Deploying
>To deploy Storybook we first need to export it as a static web app. This functionality is already built into Storybook, we just need to activate it by adding a script to package.json.

```json
{
  "scripts": {
    "build-storybook": "build-storybook -c .storybook"
  }
}
```
#### Static App
e.g. w Github + https://github.com/storybookjs/storybook-deployer

#### CI
e.g. w Netlify


### Resources
- [Workflow advice](https://blog.hichroma.com/the-delightful-storybook-workflow-b322b76fd07)
