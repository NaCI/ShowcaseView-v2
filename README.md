# ShowcaseView-v2

ShowcaseView library updated to v2. 

**Changes in the new version:**

- [x] Migrate to AndroidX
- [x] Migrated to Kotlin
- [x] Add Sequence
- [x] Bug Fixes
- [x] Add animations
- [x] Update Sample
- [x] Code cleared
- [x] Add Builder pattern to ShowcaseView


![Screenshot1](screenshots/showcaseview_ss_1.png?raw=true){:height="50%" width="50%"}
![Screenshot2](screenshots/showcaseview_ss_2.png?raw=true){:height="50%" width="50%"}
![Screenshot3](screenshots/showcaseview_ss_3.png?raw=true){:height="50%" width="50%"}
![Screenshot4](screenshots/showcaseview_ss_4.png?raw=true){:height="50%" width="50%"}

Sequence Demo

![Whole Video](/screenshots/showcaseviewgif.gif?raw=true)

This ShowcaseView library can be used to showcase any specific part of the UI or can even be used during OnBoarding of a user to give a short intro about different widgets visible on the screen. You may add any number of views (ImageView, TextView, FrameLayout, etc displaying images, videos, GIF, text etc) to describe the showcasing view.

## Gradle

1. Add the jitpack repo to your your project's build.gradle at the end of repositories

**/build.gradle**

```groovy
allprojects {
    repositories {
        jcenter()
        maven { url "https://jitpack.io" }
    }
}
```

2. Add this dependency to your module's build.gradle.

**/app/build.gradle**

```groovy
dependencies {
  implementation 'com.naci.showcaseview:showcaseview:1.4.0'
}
```

## Usage

For a working implementation of this project see the /app folder

### Single Usage Example

Initialise the ShowcaseView as follows:
      
```kotlin
val showcaseView = ShowcaseView.Builder(this)
            .setTargetView(targetView)
            .setBackgroundOverlayColor(Color.GRAY)
            .setRingColor(Color.BLUE)
            .setShowCircles(true)
            .setHideOnTouchOutside(false)
            .setShowcaseShape(ShowcaseView.SHAPE_CIRCLE)
            .setRingWidth(
                TypedValue.applyDimension(
                    TypedValue.COMPLEX_UNIT_DIP,
                    2f,
                    resources.displayMetrics
                )
            )
            .setDelay(500)
            .setDistanceBetweenShowcaseCircles(10)
            .setShowcaseListener(object :
                IShowcaseListener {
                override fun onShowcaseDisplayed(showcaseView: ShowcaseView) {
                    //TODO : do something..
                }

                override fun onShowcaseDismissed(showcaseView: ShowcaseView) {
                    //TODO : do something..
                }

                override fun onShowcaseSkipped(showcaseView: ShowcaseView) {
                    //TODO : do something..
                }
            })
            .addCustomView(R.layout.layout_showcase_body, Gravity.CENTER)
            .build()

showcaseView.show()
```
  
Register click listeners on the customView added as follows:
        
```kotlin
showcaseView!!.setClickListenerOnView(
    R.id.btn,
    View.OnClickListener {
        // showcaseView!!.showcaseSkipped() // Use this when skip button clicked 
        showcaseView!!.hide() 
    }
)
```
    
To hide the showcaseView just call:
        
```kotlin
showcaseView.hide()
```

## Properties

| Name        | Description                    | Default Value |
|-------------|--------------------------------|---------------|
|setTargetView    | Sets the view which needs to be showcased (**This method must be called inorder to use showcaseview**)          | NA |
|setBackgroundOverlayColor   | Sets the color of the overlay to be shown   | 0 |
|setRingColor   | Set color of the focus highlight rings   | 0 |
|setRingWidth  | Set width of the focus highlight rings   | 10f |
|setShowcaseShape  | Set shape of showcase focus : SHAPE_SKEW or SHAPE_CIRCLE   | SHAPE_CIRCLE |
|setHideOnTouchOutside   | Set whether hide or not on touch showcase area   | false |
|setDistanceBetweenShowcaseCircles   | Set distance value between 2 highlight circles   | 48 |
|setDelay  | Delay in ms for Showcaseview to be shown  | 0 |
|setShowCircles   | Set whether or not show the highlight circles fır SHAPE_CIRCLE  | true |
|setShowcaseListener  | Set listener to listen showcase states : *onShowcaseDisplayed*, *onShowcaseDismissed*, *onShowcaseSkipped* | NA |
|setClickListenerOnView   | Sets clicklistener on the components of the customView(s) added   | NA |
|addCustomView  | Sets the custom description view/layout to describe the showcaseView. Also, sets a gravity for the view (TOP, LEFT, RIGHT, BOTTOM) around the showcasing view  | NA |
|setShowcaseMargin  | Sets the custom description view margin from the showcaseView in the direction of the gravity defined, if any. If no gravity defined, then no point in using this method.  | 12f |  

## Sequence

Prepare ShowcaseView's first then call,

```kotlin
val sequence = ShowcaseSequence(this)
sequence.addSequenceItem(showcaseView1!!)
sequence.addSequenceItem(showcaseView2!!)
sequence.addSequenceItem(showcaseView3!!)
sequence.addSequenceItem(showcaseView4!!)
sequence.start()
```

Sequence will handle to show all showcases one by one with animation

If you want to show the sequel only **for one time** then create it with sequenceID as showed below,

```kotlin
val sequence = ShowcaseSequence(this, "sequenceID")
sequence.addSequenceItem(showcaseView1!!)
...
sequence.start()
```

**Note:** Sequence will be end if u call `showcaseView!!.showcaseSkipped()` method 

## Things to keep in mind

- Call the `showcaseViewBuilder.show()` only after adding all the customViews.
- `setRingWidth(float width)` and other margin setters take pixels as parameters. So make sure to send into density independent pixels (dp) value to support multiple screen sizes (See the sample code snippet above for reference)
- Once `showcaseViewBuilder.hide()` is called, all the click listeners get **deregistered**
- Thus, you will have to set them back if showing it again. Better to register all the click listeners in a single method which can be called when showing the showcaseView.

#Method Definitions
<ul>
  <li>
    <p><code>setTargetView(View v)</code>: Sets the view which needs to be showcased.</p>
  </li>
  <li>
    <p><code>setBackgroundOverlayColor(int color)</code>: Sets the color of the overlay to be shown.</p>
  </li>
  <li>
    <p><code>setRingColor(int color)</code>: Sets the color of the ring around the showcaseView.</p>
  </li>
  <li>
    <p><code>setRingWidth(float width)</code>: Sets the width of the ring around the showcaseView. Default value is 10px</p>
  </li>
  <li>
    <p><code>setMarkerDrawable(Drawable drawable, int gravity)</code>: Sets the marker drawable if any to point the showcaseView. Also, sets a gravity for the drawable (TOP, LEFT, RIGHT, BOTTOM) around the showcasing view.</p>
  </li>
  <li>
    <p><code>setDrawableLeftMargin(float margin)</code>: Sets the marker drawable left margin.</p>
  </li>
  <li>
    <p><code>setDrawableTopMargin(float margin)</code>: Sets the marker drawable top margin.</p>
  </li>
  <li>
    <p><code>addCustomView(View view, int gravity)</code>: Sets the custom description view to describe the showcaseView. Also, sets a gravity for the view (TOP, LEFT, RIGHT, BOTTOM) around the showcasing view.</p>
  </li>
  <li>
    <p><code>addCustomView(View view)</code>: Sets the custom description view to describe the showcaseView. This doesn't takes any gravity as an argument and renders the view as per the gravity defined in the layout file.</p>
  </li>
  <li>
    <p><code>setCustomViewMargin(int margin)</code>: Sets the custom description view margin from the showcaseView in the direction of the gravity defined, if any. If no gravity defined, then no point in using this method.</p>
  </li>
  <li>
    <p><code>setHideOnTouchOutside(boolean hide)</code>: Sets the flag which decide whether to hide the showcase overlay when user touches on the screen anywhere.</p>
  </li>
  <li>
    <p><code>setClickListenerOnView(int id, View.OnClickListener clickListener)</code>: Sets clicklistener on the components of the customView(s) added.</p>
  </li>
  <li>
    <p><code>show()</code>: Start showcasing the targetView.</p>
  </li>
  <li>
    <p><code>hide()</code>: Stop showcasing the targetView.</p>
  </li>
</ul>

**Note :** There is an unused Activity in sample app which is written in Java

# Authors

[Aashish Totla](https://github.com/outlander24)

[Naci Özyıldırım](https://github.com/NaCI)

#License
--------

    Copyright 2020 Naci Özyıldırım

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
