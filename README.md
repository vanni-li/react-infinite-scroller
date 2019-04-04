react-infinite-scroller-improve
=======================

This is fork of [React-Infinite-Scroller](https://github.com/CassetteRocks/react-infinite-scroller)

Infinitely load content using a React Component. This fork maintains a simple, lightweight infinite scroll package that supports both `window` and scrollable elements.

- [Demo](https://cassetterocks.github.io/react-infinite-scroller/demo/)
- [Demo Source](https://github.com/CassetteRocks/react-infinite-scroller/blob/master/docs/src/index.js)

## Update
之前没有对请求异常情况做处理，当获取列表失败后，会一直停留在 loading 状态，没有机会再尝试加载。  
现在在 props 添加 `error`，指定加载失败时的文案显示，显示位置和 `loader` 相同。设置 `error` 时，自动加载效果会暂时失效，需要手动点错误文案加载。加载成功后会继续支持滚动加载。


The request exception condition has not been processed before. When the data request fails, it will stay in the loading state and there is no chance to try to load again.  
Now add `error` to props to specify the tips of error when the load fails, and the display position is the same as `loader`. When `error` is set, the autoloading effect will temporarily become invalid, and you need to manually click the tips to load data. infinite scroller load will continue to be supported after successful loading.

## Installation

```
npm install react-infinite-scroller-improve --save
```
```
yarn add react-infinite-scroller-improve
```

## How to use

```js
import InfiniteScroll from 'react-infinite-scroller';
```

### Window scroll events

```js
<InfiniteScroll
    pageStart={0}
    loadMore={loadFunc}
    hasMore={true || false}
    loader={<div className="loader" key={0}>Loading ...</div>}
>
    {items} // <-- This is the content you want to load
</InfiniteScroll>
```

### DOM scroll events

```js
<div style="height:700px;overflow:auto;">
    <InfiniteScroll
        pageStart={0}
        loadMore={loadFunc}
        hasMore={true || false}
        loader={<div className="loader" key={0}>Loading ...</div>}
        useWindow={false}
    >
        {items}
    </InfiniteScroll>
</div>
```

### Custom parent element

You can define a custom `parentNode` element to base the scroll calulations on.

```js
<div style="height:700px;overflow:auto;" ref={(ref) => this.scrollParentRef = ref}>
    <div>
        <InfiniteScroll
            pageStart={0}
            loadMore={loadFunc}
            hasMore={true || false}
            loader={<div className="loader" key={0}>Loading ...</div>}
            useWindow={false}
            getScrollParent={() => this.scrollParentRef}
        >
            {items}
        </InfiniteScroll>
    </div>
</div>
```

## Props

| Name             | Type          | Default    | Description|
|:----             |:----          |:----       |:----|
| `element`        | `Component`      | `'div'`    | Name of the element that the component should render as.|
| `hasMore`        | `Boolean`     | `false`    | Whether there are more items to be loaded. Event listeners are removed if `false`.|
| `initialLoad`    | `Boolean`     | `true`     | Whether the component should load the first set of items.|
| `isReverse`      | `Boolean`     | `false`    | Whether new items should be loaded when user scrolls to the top of the scrollable area.|
| `loadMore`       | `Function`    |            | A callback when more items are requested by the user. Receives a single parameter specifying the page to load e.g. `function handleLoadMore(page) { /* load more items here */ }` }|
| `loader`         | `Component`   |            | A React component to render while more items are loading. The parent component must have a unique key prop. |
| `pageStart`      | `Number`      | `0`        | The number of the first page to load, With the default of `0`, the first page is `1`.|
| `getScrollParent`   | `Function`|           | Override method to return a different scroll listener if it's not the immediate parent of InfiniteScroll. |
| `threshold`      | `Number`     | `250`      | The distance in pixels before the end of the items that will trigger a call to `loadMore`.|
| `useCapture`     | `Boolean`     | `false`     | Proxy to the `useCapture` option of the added event listeners.|
| `useWindow`      | `Boolean`     | `true`     | Add scroll listeners to the window, or else, the component's `parentNode`.|
| `error`            | `Component` or `String`     | `null`     |  Error message displayed at the bottom when the interface request fails |
