
<a href="https://www.callstack.com/open-source?utm_campaign=generic&utm_source=github&utm_medium=referral&utm_content=react-native-pager-view" align="center">
   <picture>
     <img alt="React Native PagerView" src="https://github.com/user-attachments/assets/1f0f7b9f-5723-4a9c-b0f1-99ed472f3122">
   </picture>
</a>

# react-native-pager-view <img src="img/viewpager-logo.png" alt="ViewPager" width="24" height="24">

[![npm package](https://badge.fury.io/js/react-native-pager-view.svg)](https://badge.fury.io/js/react-native-pager-view)
[![Lean Core Extracted](https://img.shields.io/badge/Lean%20Core-Extracted-brightgreen.svg)](https://github.com/facebook/react-native/issues/23313)
[![License](https://img.shields.io/github/license/callstack/react-native-pager-view?color=blue)](https://github.com/callstack/react-native-pager-view/blob/master/LICENSE)

[![Lint](https://github.com/callstack/react-native-pager-view/actions/workflows/main.yml/badge.svg)](https://github.com/callstack/react-native-pager-view/actions/workflows/main.yml)
[![iOS Build](https://github.com/callstack/react-native-pager-view/actions/workflows/ios.yml/badge.svg)](https://github.com/callstack/react-native-pager-view/actions/workflows/ios.yml)
[![Android Build](https://github.com/callstack/react-native-pager-view/actions/workflows/android.yml/badge.svg)](https://github.com/callstack/react-native-pager-view/actions/workflows/android.yml)

This component allows the user to swipe left and right through pages of data. Under the hood it is using the native [Android ViewPager](https://developer.android.com/jetpack/androidx/releases/viewpager2) and the [iOS UIPageViewController](https://developer.apple.com/documentation/uikit/uipageviewcontroller) implementations. [See it in action!](https://github.com/callstack/react-native-pager-view#preview)

<br/>
<p align="center">
  <img src="img/vp-carousel.gif" alt="ViewPager" width="300">
</p>

<br/>

## Versions

| 4.x        | 5.x and above |
| ---------- | ------------- |
| iOS        | iOS support   |
| ViewPager1 | ViewPager2    |

## Migration

In version **6.x** support for `transitionStyle` property has been dropped. More information [here](https://github.com/callstack/react-native-pager-view/blob/master/MIGRATION.md).

`"@react-native-community/viewpager"` library has been changed to `react-native-pager-view`. Here you can find more information, how to migrate pager view to the latest [version](https://github.com/callstack/react-native-pager-view/blob/master/MIGRATION.md)

## Getting started
Bun: 

`bun add react-native-pager-view`

Yarn:

 `yarn add react-native-pager-view`

## Linking

### >= 0.60

Autolinking will just do the job.

### < 0.60

#### Mostly automatic

`react-native link react-native-pager-view`

#### Manual linking

<details>
<summary>Manually link the library on iOS</summary>
</br>

Follow the [instructions in the React Native documentation](https://facebook.github.io/react-native/img/linking-libraries-ios#manual-linking) to manually link the framework or link using [Cocoapods](https://cocoapods.org) by adding this to your `Podfile`:

```ruby
pod 'react-native-pager-view', :path => '../node_modules/react-native-pager-view'
```

</details>

<details>
<summary>Manually link the library on Android</summary>
</br>
Make the following changes:

#### `android/settings.gradle`

```groovy
include ':react-native-pager-view'
project(':react-native-pager-view').projectDir = new File(rootProject.projectDir, '../node_modules/react-native-pager-view/android')
```

#### `android/app/build.gradle`

```groovy
dependencies {
   ...
   implementation project(':react-native-pager-view')
}
```

#### `android/app/src/main/.../MainApplication.java`

On top, where imports are:

Add `import com.reactnativepagerview.PagerViewPackage;`

Add the `PagerViewPackage` class to your list of exported packages.

```java
@Override
protected List<ReactPackage> getPackages() {
  return Arrays.<ReactPackage>asList(
    new MainReactPackage(),
    new PagerViewPackage()
  );
}
```

</details>

## Usage

```js
import React from 'react';
import { StyleSheet, View, Text } from 'react-native';
import PagerView from 'react-native-pager-view';

const MyPager = () => {
  return (
    <PagerView style={styles.pagerView} initialPage={0}>
      <View key="1">
        <Text>First page</Text>
      </View>
      <View key="2">
        <Text>Second page</Text>
      </View>
    </PagerView>
  );
};

const styles = StyleSheet.create({
  pagerView: {
    flex: 1,
  },
});
```

**Attention:** Note that you can only use `View` components as children of `PagerView` (cf. folder _/example_)
. For Android if `View` has own children, set prop `collapsable` to false <https://reactnative.dev/docs/view#collapsable-android>, otherwise react-native might remove those children views and and its children will be rendered as separate pages

## Advanced usage

For advanced usage please take a look into our [example project](https://github.com/callstack/react-native-pager-view/blob/master/example/src/BasicPagerViewExample.tsx)

## API

| Prop                                                                 |                                                                                                                             Description                                                                                                                             | Platform |
| -------------------------------------------------------------------- | :-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: | :------: |
| `initialPage`                                                        |                                                                                                            Index of initial page that should be selected                                                                                                            |   both   |
| `scrollEnabled: boolean`                                             |                                                                                                            Should pager view scroll, when scroll enabled                                                                                                            |   both   |
| `onPageScroll: (e: PageScrollEvent) => void`                         |                                                    Executed when transitioning between pages (either because the animation for the requested page has changed or when the user is swiping/dragging between pages)                                                    |   both   |
| `onPageScrollStateChanged: (e: PageScrollStateChangedEvent) => void` |                                                                                                      Function called when the page scrolling state has changed                                                                                                      |   both   |
| `onPageSelected: (e: PageSelectedEvent) => void`                     |                                                                                      This callback will be called once the ViewPager finishes navigating to the selected page                                                                                       |   both   |
| `pageMargin: number`                                                 |                                                                                                                Blank space to be shown between pages                                                                                                                |   both   |
| `keyboardDismissMode: ('none' / 'on-drag')`                          |                                                                                                Determines whether the keyboard gets dismissed in response to a drag                                                                                                 |   both   |
| `orientation: Orientation`                                           |                                                                                       Set `horizontal` or `vertical` scrolling orientation (it does **not** work dynamically)                                                                                       |   both   |
| `overScrollMode: OverScrollMode`                                     |                                                                              Used to override default value of overScroll mode. Can be `auto`, `always` or `never`. Defaults to `auto`                                                                              | Android  |
| `offscreenPageLimit: number`                                         | Set the number of pages that should be retained to either side of the currently visible page(s). Pages beyond this limit will be recreated from the adapter when needed. Defaults to RecyclerView's caching strategy. The given value must either be larger than 0. | Android  |
| `overdrag: boolean`                                                  |                                                                                   Allows for overscrolling after reaching the end or very beginning or pages. Defaults to `false`                                                                                   |   iOS    |
| `layoutDirection: ('ltr' / 'rtl' / 'locale')`                        |                                                      Specifies layout direction. Use `ltr` or `rtl` to set explicitly or `locale` to deduce from the default language script of a locale. Defaults to `locale`                                                      |   both   |

| Method                                     |                                                                                                         Description                                                                                                          | Platform |
| ------------------------------------------ | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: | :------: |
| `setPage(index: number)`                   |                                                                      Function to scroll to a specific page in the PagerView. Invalid index is ignored.                                                                       |   both   |
| `setPageWithoutAnimation(index: number)`   |                                                                      Function to scroll to a specific page in the PagerView. Invalid index is ignored.                                                                       |   both   |
| `setScrollEnabled(scrollEnabled: boolean)` | A helper function to enable/disable scroll imperatively. The recommended way is using the scrollEnabled prop, however, there might be a case where a imperative solution is more useful (e.g. for not blocking an animation) |   both   |

## Contributing

See the [contributing guide](CONTRIBUTING.md) to learn how to contribute to the repository and the development workflow.

## Known Issues

- `flex:1` does not work for child views, please use `width: '100%', height: '100%'` [instead](https://github.com/callstack/react-native-pager-view/issues/186#issuecomment-675320732)

- [iOS]: In case of `UIViewControllerHierarchyInconsistency` error, please use below fix:

```
requestAnimationFrame(() => refPagerView.current?.setPage(index));
```

## Preview

### Android

|                            horizontal                             |                                  vertical                                  |
| :---------------------------------------------------------------: | :------------------------------------------------------------------------: |
| <img src="img/android-viewpager.gif" alt="ViewPager" width="325"> | <img src="img/android-viewpager-vertical.gif" alt="ViewPager" width="325"> |

### iOS

|                              horizontal                              |                                vertical                                |
| :------------------------------------------------------------------: | :--------------------------------------------------------------------: |
| <img src="img/ios-viewpager-scroll.gif" alt="ViewPager" width="325"> | <img src="img/ios-viewpager-vertical.gif" alt="ViewPager" width="325"> |

## Reanimated onPageScroll handler

An example can be found [here](https://github.com/callstack/react-native-pager-view/blob/master/example/src/ReanimatedOnPageScrollExample.tsx)

#### Instructions

To attach reanimated handler with `onPageScroll` follow the below steps.

```jsx
// 1. Define the handler
function usePageScrollHandler(handlers, dependencies) {
  const { context, doDependenciesDiffer } = useHandler(handlers, dependencies);
  const subscribeForEvents = ['onPageScroll'];

  return useEvent(
    (event) => {
      'worklet';
      const { onPageScroll } = handlers;
      if (onPageScroll && event.eventName.endsWith('onPageScroll')) {
        onPageScroll(event, context);
      }
    },
    subscribeForEvents,
    doDependenciesDiffer
  );
}

// 2. Attach the event handler
import PagerView from 'react-native-pager-view';
import Animated from 'react-native-reanimated';
const AnimatedPagerView = Animated.createAnimatedComponent(PagerView);

const pageScrollHandler = usePageScrollHandler({
  onPageScroll: (e) => {
    'worklet';
    offset.value = e.offset;
    console.log(e.offset, e.position);
  },
});

<AnimatedPagerView onPageScroll={pageScrollHandler} />;
```

## usePagerView Hook Usage
The `usePagerView` hook is a convenient way to manage the state and control the behavior of the `<PagerView />` component. It provides functions and variables to interact with the pager, such as navigating between pages and enabling/disabling scrolling.

Below is an example of how to use the usePager hook:

```jsx
export function PagerHookExample() {
  const { AnimatedPagerView, ref, ...rest } = usePagerView({ pagesAmount: 10 });
  
  return (
    <SafeAreaView style={styles.container}>
      <AnimatedPagerView
        testID="pager-view"
        ref={ref}
        style={styles.PagerView}
        initialPage={0}
        layoutDirection="ltr"
        overdrag={rest.overdragEnabled}
        scrollEnabled={rest.scrollEnabled}
        onPageScroll={rest.onPageScroll}
        onPageSelected={rest.onPageSelected}
        onPageScrollStateChanged={rest.onPageScrollStateChanged}
        pageMargin={10}
        orientation="horizontal"
      >
        {useMemo(
          () =>
            rest.pages.map((_, index) => (
              <View
                testID="pager-view-content"
                key={index}
                style={{
                  flex: 1,
                  backgroundColor: '#fdc08e',
                  alignItems: 'center',
                  padding: 20,
                }}
                collapsable={false}
              >
                <LikeCount />
                <Text testID={`pageNumber${index}`}>
                  {`page number ${index}`}
                </Text>
              </View>
            )),
          [rest.pages]
        )}
      </AnimatedPagerView>
      <NavigationPanel {...rest} />
    </SafeAreaView>
  );
}
```
### How the Example Works:

- **Pager View Setup**: The `AnimatedPagerView` component wraps `PagerView` in React Native's animation capabilities. It accepts multiple props from the `usePager` hook, such as `overdragEnabled`, `scrollEnabled`, `onPageScroll`, `onPageSelected`, and others to manage pager behavior.

- **Rendering Pages**: The pages are dynamically generated using the `rest.pages` array (initialized by `usePager`). The `useMemo` hook ensures the pages are only recomputed when necessary for performance reasons.

### Conclusion

The `usePager` hook makes it easy to handle pagination with dynamic views. This example demonstrates how to set up a simple paginated interface where users can scroll through pages, interact with page elements, and control the pager with external navigation.


## License

MIT
