

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
