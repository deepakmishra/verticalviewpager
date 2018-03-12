# VerticalViewPager
This is a VerticalViewPager implementation for Android. It extends the default Android ViewPager to support very smooth vertical scrolling instead of horizontal scrolling. To implement this the inbuilt ViewPager should be excluded from your project.

## Implementation
Add the following lines inside the dependencies part of your build.gradle file to exclude the default Android ViewPager from your project
```
dependencies {
	configurations {
		all*.exclude module: "support-core-ui"
	}
}
```
Now copy the files from the [android/support/v4](https://github.com/deepakmishra/verticalviewpager/blob/2adf04aa2728bbaf3368539ae4f3b1d840f98f27/app/src/main/java/android/support/v4) folder of **support-core-ui v26.1.0** in this projects java folder and add them to you personal project's java folder. This should be done to supplement the code that was excluded above.

While adding a ViewPager to your layout xml file, add the new VerticalViewPager that you included from this project instead of the default Android ViewPager, like this :
```
<com.viewpager.VerticalViewPager
	android:id="@+id/view_pager"
	android:layout_width="match_parent"
	android:layout_height="match_parent" />
```
 While adding a reference to the VerticalViewPager to your java file, you may use it the same way you would use a normal ViewPager, like this: 
 ``` ViewPager viewPager = findViewById(R.id.view_pager); ```

## Understanding
The [ViewPager](https://github.com/deepakmishra/verticalviewpager/blob/2adf04aa2728bbaf3368539ae4f3b1d840f98f27/app/src/main/java/android/support/v4/view/ViewPager.java) used in this project is the default Android ViewPager and it is kept effectively the same as before. Only some of the values are extracted as instance variables so that they can be changed through reflection.

For example, in the [onInterceptTouchEvent](https://github.com/deepakmishra/verticalviewpager/blob/2adf04aa2728bbaf3368539ae4f3b1d840f98f27/app/src/main/java) method, the instance variable [minYXRatioForIntercept](https://github.com/deepakmishra/verticalviewpager/blob/2adf04aa2728bbaf3368539ae4f3b1d840f98f27/app/src/main/java/android/support/v4/view/ViewPager.java#L1875) has been added to the ViewPager file so that it can be easily modified through reflection. 

[minYXRatioForIntercept](https://github.com/deepakmishra/verticalviewpager/blob/2adf04aa2728bbaf3368539ae4f3b1d840f98f27/app/src/main/java/android/support/v4/view/ViewPager.java#L1875)  can be modified to change the minimum swipe distance required to move the page up or down.

Similarly, in the onTouchEvent method, the instance variable [minYXRatioForTouch](https://github.com/deepakmishra/verticalviewpager/blob/2adf04aa2728bbaf3368539ae4f3b1d840f98f27/app/src/main/java/android/support/v4/view/ViewPager.java#L2008) has been added to the ViewPager file so that it can be easily modified through reflection.

In the [VerticalViewPager](https://github.com/deepakmishra/verticalviewpager/blob/2adf04aa2728bbaf3368539ae4f3b1d840f98f27/app/src/main/java/com/viewpager/VerticalViewPager.java) file in this project, we swap the values of x and y in the [onInterceptTouchEvent](https://github.com/deepakmishra/verticalviewpager/blob/2adf04aa2728bbaf3368539ae4f3b1d840f98f27/app/src/main/java/com/viewpager/VerticalViewPager.java#L121) and [onTouchEvent](https://github.com/deepakmishra/verticalviewpager/blob/2adf04aa2728bbaf3368539ae4f3b1d840f98f27/app/src/main/java/com/viewpager/VerticalViewPager.java#L128) methods, and edit the required values through reflection in the [init](https://github.com/deepakmishra/verticalviewpager/blob/2adf04aa2728bbaf3368539ae4f3b1d840f98f27/app/src/main/java/com/viewpager/VerticalViewPager.java#L29) method.

