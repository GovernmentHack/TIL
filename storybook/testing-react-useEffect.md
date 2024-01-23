# How to spy on functions called within a `useEffect` hook

## Problem

Essentially, StoryBook tests run in `play` will run _post_ render of a component. This means an initial `useEffect` will have been defined _before_ you are able to spy on or mock any functions inside of the `useEffect`.

For example, take this component with a function inside the `useEffect`:
```tsx
export function DumbComponent() {
  useEffect(() => {
    testModule.spyOnMe();
  }, []);

  return (
    <div data-testid="test">
      {'test'}
    </div>
  );
}
```

This Storybook test will fail:

```tsx
export const Base: Story = {
  play: async () => {
    spyOnMeMock = spyOn(testModule, 'spyOnMe').mockImplementation(() => {
      console.log("I've mocked SpyOnMe!");
    });
    await waitFor(async () => {
      await expect(spyOnMeMock).toBeCalledTimes(1);
    });
  },
};
```

## Solution

Instead you need to initialize your spies and mocks from a _decorator_ first. then inside the test you will be able to succeessfully spy on your mocked function:

```tsx
let spyOnMeMock: MockInstance;
export const Base: Story = {
  decorators: [
    (Story) => {
      spyOnMeMock = spyOn(testModule, 'spyOnMe').mockImplementation(() => {
        console.log("I've mocked SpyOnMe!");
      });
      return <Story />;
    },
  ],
  play: async () => {
    await waitFor(async () => {
      await expect(spyOnMeMock).toBeCalledTimes(1);
    });
  },
};
```
