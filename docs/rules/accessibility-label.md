# Accessibility Label

The [accessibilityLabel](https://reactnative.dev/docs/accessibility#accessibilitylabel) is the text that assistive technology reads when the component is focused and AMA requires it by tappable elements.

## The problem

Let's consider the following example:

```jsx
<Pressable onPress={contactUs} accessibilityRole="button">
    Contact us
</Pressable>
```

When testing the button with both VoiceOver and TalkBack, they both read:

> button, Contact us, double-tap to activate

Because the component has no `accessibilityLabel`, only the `accessibilityRole` is announced; they read the inner text if any, and in this case: **Contact us**. Finally, the last part tells the user that the component can be interacted with by performing a double-tap.

<br />

**What's happen if no text is available?**

```jsx
<Pressable onPress={goBack} accessibilityRole="button">
    <SVGIcon />
</Pressable>
```

When testing the button with both VoiceOver and TalkBack, they both read:

> button, double-tap to activate

Here the assistive technology only reads the role and the action that can be performed with the component. So there is a complete lack of helpful information about what we're going to trigger.

### Let's fix it!

```jsx
// 1.
<Pressable onPress={contactUs} accessibilityRole="button" accessibilityLabel="Contact US">
    Contact us
</Pressable>

// 2.
<Pressable onPress={goBack} accessibilityRole="button" accessibilityLabel="Go back">
    <SVGIcon />
</Pressable>
```

When testing with the assistive technology, this happens:

> Contact us button, double-tap to activate
> Go back button, double-tap to activate

The `accessibilityLabel` is announced first, then the __role__ and the action that can be performed at the end.

For this reason, AMA requires that tappable elements have the `accessibilityLabel` defined.


## NO_ACCESSIBILITY_LABEL

This error is used when a pressable element has no [accessibilityLabel](https://reactnative.dev/docs/accessibility#accessibilitylabel) defined.

:::note

This rule is mandatory and cannot be turned off!
:::