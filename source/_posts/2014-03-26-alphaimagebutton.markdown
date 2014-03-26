---
layout: post
title: "AlphaImageButton"
date: 2014-03-26 10:50:47 -0700
comments: true
categories: [Code Snippet, View]
author: Chris Arriola
---

Showing different view states (pressed, focused, disabled, etc.) can be a bit cumbersome and tedious when styling views. As a way to reduce the number of states to customize, we created a subclass of a View (an `ImageButton` in this case but can be any other View subclass) that sets the alpha value depending on the enabled state - 1.0 if enabled, 0.5 if disabled. This way, the View is translucent when disabled and a custom drawable/asset is not required.

```
import android.content.Context;
import android.util.AttributeSet;
import android.widget.ImageButton;

public class AlphaImageButton extends ImageButton {

    private static final float ENABLED_ALPHA = 1.0f;
    private static final float DISABLED_ALPHA = 0.5f;

    public AlphaImageButton(Context context) {
        super(context);
    }

    public AlphaImageButton(Context context, AttributeSet attrs) {
        super(context, attrs);
    }

    public AlphaImageButton(Context context, AttributeSet attrs, int defStyle) {
        super(context, attrs, defStyle);
    }

    @Override
    public void setEnabled(boolean enabled) {
        super.setEnabled(enabled);
        setAlpha((enabled ? ENABLED_ALPHA : DISABLED_ALPHA));
    }
}
```

https://gist.github.com/arriolac/9790179