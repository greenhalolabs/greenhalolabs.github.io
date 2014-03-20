---
layout: post
title: "AutoNextTextWatcher"
date: 2014-03-18 23:01:05 -0700
comments: true
categories: textwatcher
---

A useful `TextWatcher` for going to the next view once a certain length has been reached.

```
import android.text.Editable;
import android.text.TextWatcher;
import android.view.View;
import android.widget.EditText;
 
/**
 * Created by chris on 3/13/14.
 */
public class AutoNextTextWatcher implements TextWatcher {
 
    private EditText mEditText;
    private int mMaxLength;
 
    public AutoNextTextWatcher(EditText editText, int maxLength) {
        mEditText = editText;
        mMaxLength = maxLength;
        editText.addTextChangedListener(this);
    }
 
    @Override
    public void beforeTextChanged(CharSequence s, int start, int count, int after) {
    }
 
    @Override
    public void onTextChanged(CharSequence s, int start, int before, int count) {
        if (mEditText.getText().length() >= mMaxLength) {
            final View nextView = mEditText.focusSearch(View.FOCUS_DOWN);
            if (nextView != null) {
                nextView.requestFocus();
            }
        }
    }
 
    @Override
    public void afterTextChanged(Editable s) {
    }
}

```

https://gist.github.com/arriolac/9636241