---
layout: post
title: "Utility: BundleUtil"
date: 2014-08-06 15:22:04 -0700
comments: true
categories: [Utility Class, Bundle]
author: Chris Arriola
---

A utility class for serializing/deserializing Parcelables into/from a Bundle.

Check this out for an example: https://gist.github.com/arriolac/a66515bad322db0ce747

```
import android.os.Bundle;
import android.os.Parcelable;
 
/**
 * Utility class for {@link android.os.Bundle}.
 * Created by chris on 8/6/14.
 */
public class BundleUtil {
 
    private static final String EXTRA_PARCELABLE_COUNT = "parcelable_count";
 
    /**
     * Creates a {@link Bundle} given a list of {@link android.os.Parcelable} objects. This is a
     * convenience method if all the values in the Bundle are Parcelables.
     *
     * @param args the {@link android.os.Parcelable} objects.
     * @return the resulting {@link Bundle}.
     */
    public static Bundle createBundle(Parcelable... args) {
        final Bundle bundle = new Bundle();
 
        // Put Parcelable in bundle
        final int size = args.length;
        for (int i = 0; i < size; i++) {
            bundle.putParcelable(String.valueOf(i), args[i]);
        }
 
        // Put size in bundle (needed when using
        bundle.putInt(EXTRA_PARCELABLE_COUNT, size);
 
        return bundle;
    }
 
    /**
     * NOTE: This method is used in conjunction with {@link #createBundle(android.os.Parcelable...)}.
     *
     * Returns an array of Parcelable objects contained within <code>bundle</code>. The returned
     * array is returned in the same order they are passed in {@link #createBundle(android.os.Parcelable...)}.
     *
     * @param bundle the bundle
     * @return an array of Parcelables contained in <code>bundle</code>.
     */
    public static Parcelable[] getParcelablesFromBundle(Bundle bundle) {
 
        // Count how many Parcelable values in the bundle
        final int numOfParcelables = bundle.getInt(EXTRA_PARCELABLE_COUNT);
 
        // Get list of Parcelables
        final Parcelable[] parcelables = new Parcelable[numOfParcelables];
        for (int i = 0; i < numOfParcelables; i++) {
            parcelables[i] = bundle.getParcelable(String.valueOf(i));
        }
 
        return parcelables;
    }
 
}
```