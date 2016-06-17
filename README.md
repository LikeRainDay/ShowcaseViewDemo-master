ShowcaseViewDemo
================
This is a demo of [ShowcaseView](https://github.com/amlcurran/ShowcaseView) using Android Studio 0.8.6. 


![](https://raw.githubusercontent.com/Beeder/ShowcaseViewDemo/master/Screenshot.PNG)

Picture 1 is the MainActivity, Picture 2 is a default implementation of ShowcaseView, Picture 3 is a custom implementation of ShowcaseView.

Some discussion about `How do you create a transparent demo screen for an Android app?`:
* [http://stackoverflow.com/questions/12013334/how-do-you-create-a-transparent-demo-screen-for-an-android-app](http://stackoverflow.com/questions/12013334/how-do-you-create-a-transparent-demo-screen-for-an-android-app)
* [http://stackoverflow.com/questions/26293836/how-to-add-a-semi-transparent-demo-screen-using-showcaseview](http://stackoverflow.com/questions/26293836/how-to-add-a-semi-transparent-demo-screen-using-showcaseview)
* [https://github.com/amlcurran/ShowcaseView/issues/238](https://github.com/amlcurran/ShowcaseView/issues/238)

If you see [the wiki](https://github.com/amlcurran/ShowcaseView/wiki) of ShowcaseView, you may know how to work out Picture2, but if you don't want to set a specific target, you just want to show a semi-transparent demo screen to users, just like Picture3, follow me.

###Steps
1. If you are using Android Studio, add [ShowcaseView](https://github.com/amlcurran/ShowcaseView) library as a dependency by:


		compile 'com.github.amlcurran.showcaseview:library:5.0.0'

	Otherwise, see [this](https://github.com/amlcurran/ShowcaseView#project-set-up)
2. New three Acitvity: MainActivity, DefaultActivity, CustomActivity.
3. There is a button in DefaultActivity, you want to target it like Picture2, just code like this:
	```java
	Button get_src_bn = (Button)findViewById(R.id.get_source_bn);
			get_src_bn.setOnClickListener(new View.OnClickListener() {
				@Override
				public void onClick(View view) {
					Uri uri = Uri.parse("https://github.com/Beeder/ShowcaseViewDemo");
					Intent intent = new Intent(Intent.ACTION_VIEW,uri);
					startActivity(intent);
				}
			});

	new ShowcaseView.Builder(this)
			.setTarget(new ViewTarget(get_src_bn))//set button as target
			.setContentTitle("Default ShowcaseView")
			.setContentText("This is highlighting the button view.\nIn Default ShowcaseView, you must set the Target you want to highlight!")
			.hideOnTouchOutside()
			.build();
	```
	It's the default using of ShowcaseView, you set button as target.
4. In CustomActivity, you have nothing to target, so code like this:
	```java
	ShowcaseView showcaseView = new ShowcaseView.Builder(this)
								.setStyle(R.style.Custom_semi_transparent_demo)//setStyle instead of setTarget!
								.hideOnTouchOutside()
								.build();

	//showcaseView.setBackground(getResources().getDrawable(R.drawable.swipe_back_en));//minAPI=16
	showcaseView.setBackgroundDrawable(getResources().getDrawable(R.drawable.swipe_back_en));//deprecated.
	```
	You don't have to set any target, instead, you setStyle and then **manually setBackground(Drawable) on the ShowcaseView once created**. The `Custom_semi_transparent_demo` style like this:
	```xml
	<!--look at this: https://github.com/amlcurran/ShowcaseView/issues/159-->
	<style name="Custom_semi_transparent_demo" parent="ShowcaseView.Light">
		<item name="sv_backgroundColor">#663d4353</item> <!--you can customize it-->
		<item name="sv_showcaseColor">#25467A</item> <!--you can customize it-->
		<item name="sv_buttonText">Close</item> <!--you can customize it-->
	</style>
	```

It's done! The `R.drawable.swipe_back_en` is the semi-transparent demo screen you want to add.

Feel free to download my project source.

该项目的中文说明请看[这篇博客](http://beeder.github.io/2014/11/11/how-to-add-a-semi-transparent-demo-screen-using-showcaseview/)。