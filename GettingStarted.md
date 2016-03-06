# Introduction #
Welcome to the world of karaoke automation.  In this document, you will find out how to get started with this script.

# Requirement #
A good understanding of After-Effects.

# Files Contents #
  * **Karaoke\_json.html** - Karaoke json generator from .ass karaoke.
  * **karaoke.jsx** - AFX Karaoke generator script

# After-Effects Design #

Add a new composition.  The best way is to add in with a video clip.  In this getting started, we will use the basic settings:

  1. the resolution is set to 704X400
  1. the time length is set to one minute and thirty seconds.

Rename the composition to "Karaoke" without the quotes.

Add a new text layer.  Position the text layer on top and center it.  Change it to center in the paragraph.  Change the name of the text layer.  Let's call it "K" (yes, capital "K" without the quotes)

Next, add markers.  Add a marker at 15 seconds and another marker at 75 seconds place.  Change the chapter of the first marker to "[" and the chapter of the second marker to "]" without quotes.  You can do so by double clicking on the marker.  These markers indicate the start and end time of the karaoke line and karaoke syllable with respect to the length of the current text layer (90 seconds), so eventually you're allowing 25% lead-in and 25% lead-out.

Next, create a new text animator.  To create a text animator, click the arrow key next to "Animate."  Select Fill Color->RGB.  The red should be created under the new text animator you created.  Rename the text animate and call it "anim" (in all lower case and without any quote).  Expand the text animator to show everything.

Expand "Range Selector 1" under that text animator.  Go to the first marker (at 15sec), click the clock icon next to 'end.'  This will add a keyframe to 'end' at 15sec area.  Change the value to 0.  Next, add another keyframe, to say at 30sec area.  Change that value to 100.  CTRL-ALT click to set it as HOLD keyframe. (optional)  Now go all the way to 45sec, click the clock icon next to 'start' to add a keyframe to 'start' at 45sec area.  Change the value to 0.  Then go to the second marker which is at 60sec, add another keyframe to 'start' and change that value to 100.  This will allow the karaoke to start at 0,0 at 0%; 0,100 at 25% to 75%; and end at 100,100 at 100%.  0 in the 'start' and 'end' value means that it's beginning of the syllable.  The 100 in the 'start' and 'end value means that it's at the end of the current syllable.  Then check off the 'eye' icon for the current text animator to hide the effect.  In this example, it is not important to do that, but if you decide to use the same layer with different effects on other layers, then you'll need to make sure you do this part.

Ok, enough of the text animators.  Let's move on to basic line lead-in and lead-out effect: fading.  Go to Transform/Opacity.  Add a new keyframe at the beginning of the text layer K.  Change the value to "0."  At both markers, add keyframes and change values to "100."  At the end of the text layer, add a new keyframe of value of 0 too.

You're done for the design.  Let's move to the coding.

# JSON Generator #

Before you begin this part, make sure your .ass is properly styled.
All the different types of karaoke must use different styles. (English, Kanji, Romaji).
You must pick a font for each of the styles. It doesn't matter in this example, but when you need the positions of the syllables, then it matters.

Start up Karaoke\_json.html in any web browsers you like (tested on IE, Firefox, Opera, and Safari).  The script requirement is that the .ass file must have {\k} timings.  Copy and paste everything from the .ass file into the text box.  Click generator.  You will see a new window or a new tab popped up with one line text.

# After-Effects Coding #

Let's start off by creating a new project.  In the project, create a new Composition.  Rename the composition to "KRK" without the quotes.

Next, add a Text Layer.  Under the text layer, go to Text and then Source Text.  Alt-click the clock to bring up the expression.  Copy and paste the result from Karaoke\_json.html into the expression box.  Check off the "=" sign so that the expression won't get evaluated.  You can collapse the text layer to hide the ugly expression.

You can either have the text layer created as a regular text layer or paragraph layer.  I prefer paragraph because it wraps the text around, but it doesn't matter in this case.  Type the following codes into your text layer.
```
shift( -10 )
add( "Karaoke" )
```
The first line means that you will be shifting the Karaoke by -10 seconds.  You can ignore this line, but I'm showing what the script is capable of now.  The next line will add the Composition Karaoke into the KRK Project.

Next, go back to Composition Karaoke, add a new text layer just like before, but this time rename the text layer to "KRK" (without the quotes).  Type in the following codes in there:
```
add( "K" )
.a( "anim" , true )
.p( "transform.opacity" )
.l( "romaji" )
```
  * The first line adds a text layer K for the karaoke template.
  * The next line adds a text animator you created for the karaoke.  The true in that line means that you are created as a syllable-timing instead of line-timing.  If you don't include true, it won't animate as the karaoke.
  * The third line means that you are animating the transform.opacity that you created (keyframes).  You can get these names easily by showing the expressions, which will reveal the names of the properties you're adding. Note: this is case-sensitive.
  * The fourth line means that you are creating lines through "romaji" style.  Note: all style cases have been converted to lower case.  This is for convenient reasons because .ass is case-insensitive.

# Generate #

Now, run through the script.  If there are mistakes in your codes, it will let you know.  If it doesn't have any mistakes, you can continue generating the Karaoke after you click "Yes."  It may take a few minutes before the karaoke is generated.  Once the karaoke is generated, you'll see a lot of generated layers with your temjplates on the top (the ordering is based on the order you define your 'add' in your codes)  Below those templates is the KRK text layer.  KRK text layer has only two purposes now, but I'll be adding more when there's a need.

If you find any mistakes in your effects, you can do so by editing the template.  Do not edit the generated layers, because they'll get deleted everytime you regenerate your karaoke.  All the editing should go to the KRK and your templtes, not the generated layers.

# Conclusion #

This wraps up about the Karaoke generator.  Thanks for reading this short tutorial, and I hope you enjoy using this initial release.