---
layout: post
title: "Tip: Static Factory Methods"
date: 2014-04-09 17:33:29 -0700
comments: true
categories: [Tip, Design Pattern]
author: Chris Arriola
---

Static factory methods are a creational design pattern. They are a good way to construct an instance of an object by calling a static method of the class. A good example of this is when constructing a new Fragment:

```
public static SomeFragment newInstance(int id) {

	final SomeFragment f = new SomeFragment();
	
	final Bundle args = new Bundle();
	args.putInt("key_id", id);
	f.setArguments(args);

	return f;
}

```

Some benefits of using this design pattern are:

* The caller doesn't have to write all this boilerplate code. It can simple call `SomeFragment.newInstance(...)` to construct a new `SomeFragment` instance.
* Decouples the Bundle String key **key_id** from the caller. This way, only `SomeFragment` needs to "know" the key for **id** and the callers do not.

Another example of this is when launching a new Activity:

```
public class SomeActivity extends Activity {

	public static void launch(Activity callerActivity, int id) {
		final Intent intent = new Intent(callerActivity, SomeActivity.class);
		intent.putExtra("key_id", id);
		callerActivity.startActivity(intent);
	}
}
```