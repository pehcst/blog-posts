---
title: "React: Understanding useLayoutEffect vs. useEffect"
seoTitle: "React useEffect vs. useLayoutEffect: Understanding Differences and Bes"
seoDescription: "Discover the differences between React's useEffect and useLayoutEffect hooks. Learn when to use each one and best practices for optimal rendering."
datePublished: Mon Jul 24 2023 16:31:21 GMT+0000 (Coordinated Universal Time)
cuid: clkh34tlo000309lb67kobz1z
slug: react-understanding-uselayouteffect-vs-useeffect
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1690216156968/10493198-5f33-4424-907c-d545119cfbab.jpeg
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1690216199607/7c2b6eaf-0436-4cde-97c1-4cad5dfb8811.jpeg
tags: javascript, tips, reactjs, frontend-development, reacthooks

---

There are two hooks in React, `useEffect` and `useLayoutEffect`, which appears to work similarly.

The way you call them seems the same:

```javascript
useEffect(() => {
  // side effects
  return () => /* cleanup */
}, [dependency, array]);

useLayoutEffect(() => {
  // side effects
  return () => /* cleanup */
}, [dependency, array]);
```

However, they are not the same. Let's see what makes them different and when to use each one. (tl; dr: most of the time you want to use `useEffect`)

The Difference Between `useEffect` and `useLayoutEffect` It's all about the timing of execution.

`useEffect` is executed asynchronously and after a rendering is painted on the screen.

So it looks like this:

You trigger a rendering somehow (change the state or the parent component is rendered again). React renders your component (calls your component). The screen is visually updated. **ONLY THEN** `useEffect` is executed.

`useLayoutEffect`, on the other hand, is executed synchronously after a rendering but before the screen update. This means:

You trigger a rendering somehow (change the state or the parent component is rendered again). React renders your component (calls your component). `useLayoutEffect` is executed, and React waits for it to finish. The screen is visually updated.

99% of the Time, `useEffect` In most cases, your effect is synchronizing some state or object with something that doesn't need to happen IMMEDIATELY or doesn't visually affect the page.

For example, if you are fetching data from a server, it won't result in an immediate change.

Or if you are setting up an event handler.

Or if you are resetting some state when a modal dialog appears or disappears.

Most of the time, `useEffect` is the right way to go.

When to use `useLayoutEffect` What is the right time to use `useLayoutEffect`? You'll know when you see it. Literally ;)

If your component flickers when the state is updated—meaning, it is first rendered in a partially ready state and then rendered again in its final state—that's a good clue that it's time to switch to useLayoutEffect.

Here's an example (artificial) so you can understand what I mean.

When you click on the page (\[A\]), the state immediately changes (value is reset to 0), which re-renders the component, and then the effect is executed—which sets the value to some random number and is rendered again.

The result is that two renderings happen in quick succession.

```javascript
import React, { useState, useLayoutEffect } from 'react';
import ReactDOM from 'react-dom';

const BlinkyRender = () => {
  const [value, setValue] = useState(0);

  useLayoutEffect(() => {
    if (value === 0) {
      setValue(10 + Math.random() * 200);
    }
  }, [value]);

  console.log('render', value);

  return (
    <div onClick={() => setValue(0)}>
      value: {value}
    </div>
  );
};

ReactDOM.render(
  <BlinkyRender />,
  document.querySelector('#root')
);
```

\[A\]: In general, putting onClick handlers on divs is bad for accessibility (use buttons!), this is a disposable demo. I just wanted to mention it!

Try both versions:

Version with useLayoutEffect — No visual flicker (link: [**https://codesandbox.io/s/uselayouteffect-no-flash-ylyyg**](https://codesandbox.io/s/uselayouteffect-no-flash-ylyyg))

Version with useEffect — Visual flicker (link: [**https://codesandbox.io/s/useeffect-flash-on-render-yluoi**](https://codesandbox.io/s/useeffect-flash-on-render-yluoi))

Notice how the `useLayoutEffect` version visually updates only once, even though the component has been rendered twice. The `useEffect` version, on the other hand, visually renders twice, where you can briefly see the value as 0.

Should I Use `useEffect` or `useLayoutEffect`? Most of the time, `useEffect` is the right choice. If your code is causing rendering flickers, switch to `useLayoutEffect` and see if that helps.

Since `useLayoutEffect` is synchronous (blocks rendering), and the app won't visually update until the effect finishes executing... this can cause performance issues if you have slow code in your effect. Along with the fact that most effects don't need the world to pause while they happen.