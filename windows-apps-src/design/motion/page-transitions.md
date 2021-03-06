---
author: serenaz
Description: Learn how to use page transitions in your UWP apps.
title: Page transitions in UWP apps
template: detail.hbs
ms.author: sezhen
ms.date: 04/08/2018
ms.topic: article
ms.prod: windows
ms.technology: uwp
keywords: windows 10, uwp
pm-contact: stmoy
ms.localizationpriority: medium
---

# Page transitions

Page transitions are animations that play when users navigate between pages in an app, providing feedback as the relationship between pages. Page transitions help users understand if they are at the top of a navigation hierarchy, moving between sibling pages, or navigating deeper into the page hierarchy.

Two different animations are provided for navigation between pages in an app, *page refresh* and *drill*, and are represented by subclasses of [NavigationTransitionInfo](/uwp/api/windows.ui.xaml.media.animation.navigationtransitioninfo).

## Page refresh

Page refresh is a combination of a slide up animation and a fade in animation for the incoming content. The desired feeling is that the user has started over.

Use page refresh when the user is taken to the top of a navigational stack, such as navigating between [tabs](../controls-and-patterns/tabs-pivot.md) or [left-nav](../controls-and-patterns/navigationview.md) items. By default, [Frame.Navigate()](/uwp/api/windows.ui.xaml.controls.frame.navigate) uses page refresh.

![page refresh animation](images/page-refresh.gif)

The page refresh animation is represented by the [EntranceNavigationTransitionInfoClass](/uwp/api/windows.ui.xaml.media.animation.entrancenavigationtransitioninfo).

```csharp
// Explicitly play the page refresh animation
myFrame.Navigate(typeof(Page2), null, new EntranceNavigationTransitionInfo());
```

## Drill

Use drill when users navigate deeper into an app, such as displaying more information after selecting an item.

The desired feeling is that the user has gone deeper into the app.

![drill animation](images/drill.gif)

The drill animation is represented by the [DrillInNavigationTransitionInfo](/uwp/api/windows.ui.xaml.media.animation.drillinnavigationtransitioninfo) class.

```csharp
// Play the drill in animation
myFrame.Navigate(typeof(Page2), null, new DrillInNavigationTransitionInfo());
```

## Suppress

Suppressing the animation is useful if you are building your own transition using [Connected Animations](connected-animation.md) or implicit show/hide animations.

To avoid playing any animation during navigation, use [SuppressNavigationTransitionInfo](/uwp/api/windows.ui.xaml.media.animation.suppressnavigationtransitioninfo) in the place of other [NavigationTransitionInfo](/uwp/api/windows.ui.xaml.media.animation.navigationtransitioninfo) subtypes.

```csharp
// Suppress the default animation
myFrame.Navigate(typeof(Page2), null, new SuppressNavigationTransitionInfo());
```

## Backwards navigation

By default, [Frame.GoBack()](/uwp/api/windows.ui.xaml.controls.frame.goback) plays the corresponding "go back" animation based on the animation played to navigate to the page. For example, an app that uses drill in to navigate into a page will see a drill out when users navigate backwards.

To play a specific transition when navigating backwards, use `Frame.GoBack(NavigationTransitionInfo)`. This can be useful when you modify navigation behavior dynamically based on screen size, for example, in a responsive master/detail scenario.

## Related topics

- [Navigate between two pages](../basics/navigate-between-two-pages.md)
- [Motion in UWP apps](index.md)
