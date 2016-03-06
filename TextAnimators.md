# Introduction #
In this guideline, you will learn a shear number of syllable and line effects you can do with this script.  It's based on how you configure your animators.

# Auto Zero-Space Control #
The addition of zero-spacing into text animators enables you to perform effect on the entire syllable rather than individual characters.  To enable per-syllable effect, you must do the following:
  1. Text -> More Options -> Anchor Point Grouping
  1. Set that to "Word"
  1. Alternative, you can add in space="true" in `<layer>`.
  1. It will now be treated as per-syllable effect.  Note you need to use Word as a mode effect.
```
<layer name="karaoke" space="yes">
</layer>
```

Basically, with this feature enabled, the script will add spaces after every syllable.  You can then adjust the spacing using your defined slider control.  The point of this is to enable Per-syllable effect, i.e. the entire syllable is affected rather than just the character or word itself.

# Per-Character Effect #
This allows the per-character effects when singing on the syllable, so that the effects will start from the first character and end at the last character.  To use this feature, make sure you do the following:
  * Range Selector -> Advanced -> Mode = Characters: This allows effects to be performed on the character-basis
  * Range Selector -> Advanced -> Mode = Characters Excluding Space: This allows effects to be performed on the character-basis without spaces.  This works.
  * This feature also works if Auto Zero-Space Control is used.

# Per-Syllable Effect #
This allows the per-sylalble effect when singing on the syllable, so that the effects will shine exactly on the syllable.  It's good if you're planning to scale on syllable.  To use this feature, make sure you do the following:

  * See Space Control
  * Make sure you adjust the space control so that your syllables are as close as possible.  You can get an exact number by copying and pasting that line into your template layer and compare the lengths. :)
  * Set: Text->More Options->Anchor Point Grouping to Word -- This enables properly scaling of the syllables.
  * Set: Range Selector->Advanced->Based On to "Word": Now the effect is applied to the overall syllable.

# Text Animators Line Lead-in and Lead-out transition Effects #

To use this feature, create two layers.  One is called "In" and the other is called "Out".  Basically, you can create nice transition effects using text animators.
  * In: Range Selector->Advanced->Shape = Ramp Up; keyframes for selectors: Start = 0% to 100% at start, End = 100% at all times.
  * Out: Range Selector->Advanced->Shape = Ramp Down; keyframes for selectors: Start = 0% at all times, End = 0% to 100% at the end.
  * <a />

# Fixed Syllable timings #
There are two ways to do this.
  1. XML Configuration:
```
<a name="animator" syl="true" fixed="{FIXED}" />
```
  1. Range Selector's Name is {FIXED}.  The default name is Range Selector 1.  Replace it with {FIXED}, as shown below.  Note: with the release of version 0.64, you can add as many range selectors as you want to, not limiting to 1.
{FIXED} can be the following:
  * ^: beginning of the line (the keyframes on the [ marker will be the start of the syllable/line timing)
  * $: end of the line (keyframes on the ] marker will be the end of the syllable/line timing)
  * start is synonym to ^ (for those who don't know about regular expressions)
  * end is synonym to $ (for those who don't know about regular expressions)
  * Number (i.e., 50): It's a percentage of the syllable.  The timing always starts at [ marker.
  * Note: 0 is synonym to start and ^.
  * Number with a percent (i.e., 50%): same as the number, but with this, you can add in any text with this percent value instead of saying a number. For example: Cool Start 10%.


# One Layered Syllable Effects #
The settings are as follows:

  * start = 0 to 100% at the end (]) marker
  * end = 0 to 100% at the start ([) marker.
  * Range Selector->Advanced->Mode = Add

# On/Off Layered Syllable Effects #
Do the following:
  * Create an animator called "on" with transform.opacity.
    * Set the opacity to 0%
    * Check off EYE (Hide it)
  * Create an animator called "off" with opacity.
    * Set the opacity to 100%
    * Check off EYE (Hide it)
  * Create an animator called "kon" with opacity.
    * Set the opacity to 100%
    * start = 0 to 100% at the end (]) marker
    * end = 0 to 100% at the start ([) marker.
    * Range Selector->Advanced->Mode = Add
    * Check off EYE (Hide it)
  * Create an animator called "koff" with opacity.
    * Set the opacity to 0%
    * start = 0 to 100% at the end (]) marker
    * end = 0 to 100% at the start ([) marker.
    * Range Selector->Advanced->Mode = Add
    * Check off EYE (Hide it)
  * Use the following codes: (say, Karaoke is your template layer name)
```
<layer name="Karaoke" alias="karaoke_on">
	<a name="on" syl="yes" />
	<a name="kon" syl="yes" />
</layer>

<!-- I use alias so that these layers 
can be referenced later on.
Or else, KRK will automatically make 
Karaoke_2 as the alias for the following layer -->

<layer name="Karaoke" alias="karaoke_off">
	<a name="off" syl="yes" />
	<a name="koff" syl="yes" />
</layer>
```