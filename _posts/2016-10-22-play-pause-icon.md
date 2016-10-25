---
layout: post
title: 'Play Pause Icon'
date: 2016-10-22
permalink: /2016/10/play-pause-icon.html
related: ['/2013/08/fragment-transaction-commit-state-loss.html',
    '/2013/04/retaining-objects-across-config-changes.html',
    '/2016/08/contextcompat-getcolor-getdrawable.html']
---

<!--morestart-->

asdf

<!--more-->

The pause icon:

```xml
<!-- res/drawable/ic_pause.xml -->
<vector
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:width="24dp"
    android:height="24dp"
    android:viewportHeight="24"
    android:viewportWidth="24"
    android:tint="?attr/colorControlNormal">

    <group
        android:name="rotationGroup"
        android:pivotX="12"
        android:pivotY="12">

        <path
            android:name="leftPath"
            android:fillColor="@android:color/white"
            android:pathData="M9,8 L11,8 L11,16 L9,16 Z"/>

        <path
            android:name="rightPath"
            android:fillColor="@android:color/white"
            android:pathData="M13,8 L15,8 L15,16 L13,16 Z"/>

    </group>

</vector>
```

The play icon:

```xml
<!-- res/drawable/ic_play.xml -->
<?xml version="1.0" encoding="utf-8"?>
<vector
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:width="24dp"
    android:height="24dp"
    android:viewportHeight="24"
    android:viewportWidth="24"
    android:tint="?attr/colorControlNormal">

    <group
        android:name="rotationGroup"
        android:pivotX="12"
        android:pivotY="12"
        android:rotation="90"
        android:translateX="1">

        <path
            android:name="leftPath"
            android:fillColor="@android:color/white"
            android:pathData="M12,8 L12,8 L12,16 L7,16 Z"/>

        <path
            android:name="rightPath"
            android:fillColor="@android:color/white"
            android:pathData="M12,8 L12,8 L17,16 L12,16 Z"/>

    </group>

</vector>
```

The pause-to-play `AnimatedVectorDrawable`:

```xml
<!-- res/drawable/avd_pause_to_play.xml-->
<animated-vector
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:aapt="http://schemas.android.com/aapt"
    android:drawable="@drawable/ic_pause">

    <target android:name="rotationGroup">
        <aapt:attr name="android:animation">
            <set>
                <objectAnimator
                    android:duration="@android:integer/config_shortAnimTime"
                    android:interpolator="@android:interpolator/decelerate_quad"
                    android:propertyName="rotation"
                    android:valueFrom="0"
                    android:valueTo="90"/>
                <objectAnimator
                    android:duration="@android:integer/config_shortAnimTime"
                    android:interpolator="@android:interpolator/decelerate_quad"
                    android:propertyName="translateX"
                    android:valueFrom="0"
                    android:valueTo="1"/>
            </set>
        </aapt:attr>
    </target>


    <target android:name="leftPath">
        <aapt:attr name="android:animation">
            <objectAnimator
                android:duration="@android:integer/config_shortAnimTime"
                android:interpolator="@android:interpolator/decelerate_quad"
                android:propertyName="pathData"
                android:valueFrom="@string/path_pause_left"
                android:valueTo="@string/path_play_left"
                android:valueType="pathType"/>
        </aapt:attr>
    </target>

    <target android:name="rightPath">
        <aapt:attr name="android:animation">
            <objectAnimator
                android:duration="@android:integer/config_shortAnimTime"
                android:interpolator="@android:interpolator/decelerate_quad"
                android:propertyName="pathData"
                android:valueFrom="@string/path_pause_right"
                android:valueTo="@string/path_play_right"
                android:valueType="pathType"/>
        </aapt:attr>
    </target>

</animated-vector>
```

The play-to-pause `AnimatedVectorDrawable`:

```xml
<!-- res/drawable/avd_play_to_pause.xml-->
<animated-vector
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:aapt="http://schemas.android.com/aapt"
    android:drawable="@drawable/ic_play">

    <target android:name="rotationGroup">
        <aapt:attr name="android:animation">
            <set>
                <objectAnimator
                    android:duration="@android:integer/config_shortAnimTime"
                    android:interpolator="@android:interpolator/decelerate_quad"
                    android:propertyName="rotation"
                    android:valueFrom="90"
                    android:valueTo="180"/>
                <objectAnimator
                    android:duration="@android:integer/config_shortAnimTime"
                    android:interpolator="@android:interpolator/decelerate_quad"
                    android:propertyName="translateX"
                    android:valueFrom="1"
                    android:valueTo="0"/>
            </set>
        </aapt:attr>
    </target>


    <target android:name="leftPath">
        <aapt:attr name="android:animation">
            <objectAnimator
                android:duration="@android:integer/config_shortAnimTime"
                android:interpolator="@android:interpolator/decelerate_quad"
                android:propertyName="pathData"
                android:valueFrom="@string/path_play_left"
                android:valueTo="@string/path_pause_left"
                android:valueType="pathType"/>
        </aapt:attr>
    </target>

    <target android:name="rightPath">
        <aapt:attr name="android:animation">
            <objectAnimator
                android:duration="@android:integer/config_shortAnimTime"
                android:interpolator="@android:interpolator/decelerate_quad"
                android:propertyName="pathData"
                android:valueFrom="@string/path_play_right"
                android:valueTo="@string/path_pause_right"
                android:valueType="pathType"/>
        </aapt:attr>
    </target>

</animated-vector>
```

The animated icon w/o rotation or translation:

<svg xmlns:xlink="http://www.w3.org/1999/xlink" width="50%" height="50%" viewBox="0 0 24 24">

  <path id="icon1" fill="#000" fill-opacity=".54"/>

  <animate xlink:href="#icon1" attributeName="d" dur="1200ms" repeatCount="indefinite" fill="freeze" keyTimes="0; .1666; .5; .6666; 1" calcMode="spline" keySplines="0 0 1 1; .4 0 .2 1; 0 0 1 1; .4 0 .2 1" values="M9,8 L11,8 L11,16 L9,16 L9,8 M13,8 L15,8 L15,16 L13,16 L13,8; M9,8 L11,8 L11,16 L9,16 L9,8 M13,8 L15,8 L15,16 L13,16 L13,8; M12,8 L12,8 L12,16 L7,16 L12,8 M12,8 L12,8 L17,16 L12,16 L12,8; M12,8 L12,8 L12,16 L7,16 L12,8 M12,8 L12,8 L17,16 L12,16 L12,8; M9,8 L11,8 L11,16 L9,16 L9,8 M13,8 L15,8 L15,16 L13,16 L13,8"/>

</svg>

The final result:

<svg xmlns:xlink="http://www.w3.org/1999/xlink" width="50%" height="50%" viewBox="0 0 24 24">

  <path id="icon2" fill="#000" fill-opacity=".54"/>

  <animate xlink:href="#icon2" attributeName="d" dur="1200ms" repeatCount="indefinite" fill="freeze" keyTimes="0; .1666; .5; .6666; 1" calcMode="spline" keySplines="0 0 1 1; .4 0 .2 1; 0 0 1 1; .4 0 .2 1" values="M9,8 L11,8 L11,16 L9,16 L9,8 M13,8 L15,8 L15,16 L13,16 L13,8; M9,8 L11,8 L11,16 L9,16 L9,8 M13,8 L15,8 L15,16 L13,16 L13,8; M12,8 L12,8 L12,16 L7,16 L12,8 M12,8 L12,8 L17,16 L12,16 L12,8; M12,8 L12,8 L12,16 L7,16 L12,8 M12,8 L12,8 L17,16 L12,16 L12,8; M9,8 L11,8 L11,16 L9,16 L9,8 M13,8 L15,8 L15,16 L13,16 L13,8"/>

  <animateTransform xlink:href="#icon2" attributeName="transform" dur="1200ms" attributeType="XML" type="translate" repeatCount="indefinite" fill="freeze" keyTimes="0; .1666; .5; .6666; 1" calcMode="spline" keySplines="0 0 1 1; .4 0 .2 1; 0 0 1 1; .4 0 .2 1" values="0; 0; 1; 1; 0;" additive="sum"/>

  <animateTransform xlink:href="#icon2" attributeName="transform" attributeType="XML" type="rotate" dur="1200ms" repeatCount="indefinite" fill="freeze" keyTimes="0; .1666; .5; .6666; 1" calcMode="spline" keySplines="0 0 1 1; .4 0 .2 1; 0 0 1 1; .4 0 .2 1" values="0 12 12; 0 12 12; 90 12 12; 90 12 12; 180 12 12" additive="sum"/>

</svg>

The `CheckableImageButton`:

```java
/** An extension of {@link ImageButton} that implements the {@link Checkable} interface. */
public class CheckableImageButton extends ImageButton implements Checkable {
  private static final int[] CHECKED_STATE_SET = {android.R.attr.state_checked};

  private boolean isChecked;

  public CheckableImageButton(Context context, AttributeSet attrs) {
    super(context, attrs);
  }

  @Override
  public boolean isChecked() {
    return isChecked;
  }

  @Override
  public void setChecked(boolean isChecked) {
    if (this.isChecked != isChecked) {
      this.isChecked = isChecked;
      refreshDrawableState();
    }
  }

  @Override
  public void toggle() {
    setChecked(!isChecked);
  }

  @Override
  public boolean performClick() {
    // Code copied from CompoundButton#performClick().
    toggle();

    final boolean handled = super.performClick();
    if (!handled) {
      // View only makes a sound effect if the onClickListener was
      // called, so we'll need to make one here instead.
      playSoundEffect(SoundEffectConstants.CLICK);
    }

    return handled;
  }

  @Override
  public int[] onCreateDrawableState(int extraSpace) {
    final int[] drawableState = super.onCreateDrawableState(extraSpace + 1);
    if (isChecked()) {
      mergeDrawableStates(drawableState, CHECKED_STATE_SET);
    }
    return drawableState;
  }
}
```

And the `AnimatedStateListDrawable`:

```xml
<!-- res/drawable/asl_play_pause.xml-->
<animated-selector
    xmlns:android="http://schemas.android.com/apk/res/android">

    <item
        android:id="@+id/pause"
        android:drawable="@drawable/ic_pause"
        android:state_checked="true"/>

    <item
        android:id="@+id/play"
        android:drawable="@drawable/ic_play"/>

    <transition
        android:drawable="@drawable/avd_pause_to_play"
        android:fromId="@id/pause"
        android:toId="@id/play"/>

    <transition
        android:drawable="@drawable/avd_play_to_pause"
        android:fromId="@id/play"
        android:toId="@id/pause"/>

</animated-selector>
```

On API 21+, you can set the drawable in XML by referencing `@drawable/asl_play_pause`.

On API 19 and below, you'll need to manually set and start the animated vector drawables
in your activity yourself:

```java
final CheckableImageButton icon = (CheckableImageButton) findViewById(R.id.icon);
final AnimatedVectorDrawableCompat pauseToPlay =
    AnimatedVectorDrawableCompat.create(this, R.drawable.avd_pause_to_play);
final AnimatedVectorDrawableCompat playToPause =
    AnimatedVectorDrawableCompat.create(this, R.drawable.avd_play_to_pause);
icon.setImageDrawable(playToPause);
icon.setOnClickListener(view -> {
    final AnimatedVectorDrawableCompat avd = icon.isChecked() ? pauseToPlay : playToPause;
    icon.setImageDrawable(avd);
    avd.start();
});
```