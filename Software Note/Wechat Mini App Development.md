## Skyline

```json
"renderer": "skyline",
"rendererOptions": {
    "skyline": {
      "defaultDisplayBlock": true      
    }
},
"componentFramework": "glass-easel",
"lazyCodeLoading": "requiredComponents",

```

> 瀑布流的问题，实现方式也很简单，官方提供了一个叫做grid-view的组件，只需定义它的*type=“masonry”*即可，但若是在webview下，除了性能不理想以外，还会有一些小BUG，比如经常会出现大块区域的空白。在Skyline下，就不会出现此类问题。

```
<scroll-view type="custom" scroll-y>
  <grid-view type="masonry" main-axis-gap="15" cross-axis-gap="15">
    <view wx:for="{{dataList}}" wx:key="id"></view>
  </grid-view>
</scroll-view>
```