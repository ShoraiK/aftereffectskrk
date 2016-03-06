# KRK XML Updates #
The old configuration is obsolete in this version, since it's a hackish way of implemented the configurator.  The new way is described as follows:

  1. The timeline marker is left untouched
  1. KRK Composition needs to have a text layer which has the Karaoke .ass codes only in the source text.
  1. Drag any compositions into KRK Composition if you want them to be processed.  Make sure they're below your text layer containing the .ass lyrics.
  1. Check on Shy Layer if you don't want them to be processed.  Check off the Shy Layer (hide) to process them.
  1. Open Layer comments.
  1. Type in XML Configurations next to the composition to process them.

# XML Guideline #

```
<copy name="K" from="Comp 1" layer="karaoke" />
<layer name="layerName" space="0" no="0">
	<line name="styleName" layer="" syl="0" />
	<animator name="animatorName" syl="1" fixed="start|end" />
	<property name="property.name" syl="1" pos="0" fixed="1" />
	<set name="layerProperty" property="property" value="0" />
</layer>
```

# MAIN XML #

As a side note, you cannot undo any changes made in the comments once you swapped out of the comment mode. To prevent this from happening, please edit these XML configurations with an external editor, then paste the XML config back into the box.

## copy ##
Basically it copies the layers from one composition to another composition.  Single Tag.
  * from: From composition in KRK Comp (default is the current composition)
  * to: To composition in KRK Comp (default is the current composition)
  * layer: Layer name in the 'from' composition
  * name: rename the layer to another name. (default is the source layer's name)
  * replace: true/false (default: TRUE) -- true to replace the existing layer.  False not to (so if it's not replaced, then the old layer won't get overwritten).
Example:
```
<copy name="K" from="Comp 1" layer="karaoke" />
```
## layer ##
Enclosing the following tags.
  * name is the layer's name
  * space is the zero-space override.  Note, you cannot disable zero-space if the anchor point group is set to Word.
  * fixed: "start", "end", "yes" ... start will set the start lead-in fixed timing, end will set the end lead-out fixed timing, and "yes" (boolean) will set all the lead-in/lead-out fixed.  This option is synonymous to { and } markers.
  * no is a little optimization in calculations, where the KRK Syllable won't be generated.  However, if you enable 'no', you won't be able to collect positional values.
  * blend: blending mode.  Available modes: _add, alpha add, classic color burn, classic color dodge, classic difference, color, color burn, color dodge, dancing dissolve, darken, darker color, difference, dissolve, exclusion, hard light, hard mix, hue, lighten, lighter color, linear burn, linear dodge, linear light, luminescent premul, luminosity, multiply, normal, overlay, pin light, saturation, screen, silhouete alpha, silhouette luma, soft light, stencil alpha, stencil luma, vivid light_
  * alias = alias name (instead of based on name + repeated index)
  * threed = true if 3D is enabled, false if 3D is disabled, (default, use the layer's 3D setting)
  * precomp = boolean (True/False) ... If this is true, it will automatically precompose everything one-by-one after everything is run.  Please note: It will create a new folder called KRK.  Everything under here will be deleted initially.  This is to ensure that the precompositions are not re-generated.

### line ###
(aliases: l)
  * name is the style name (alias: style)
  * layer is the layer number in .ass (by default, it selects all layers)
  * line is the line number
  * syl indicates if you want to generate per-syllable. To select certain syllables, put in numbers.  Note syl="0" means syllable #0 in per-syllable mode.

Note: you can add more than one `<line />` if you need more lines.  however, because this script does not check if the lines have been generated on the same layer, make sure you don't have any of the same lines repeated.

```
<line name="romaji" layer="0" line="1,2,3" syl="1,2" />
```
This will generate lines for style romaji, layer 0, lines 1,2, and 3, and syllable 1 and 2.

```
<line name="romaji" syl="syl" />
```
This will generate all syllables for romaji style, all layers, and all lines.

```
<l />
```
You get the idea... This will generate all lines in line mode (non-syllables).  make sure you don't have syl attributes to make it line-effect.

### animate ###
(aliases: animator anim a)
  * name is the text animator's name
  * syl is if it's a syllable timing (if syl=0, then it's a line timing)
  * fixed is if it's fixed timing ("start", "end", or percentages like "50")

```
<a name="MyAnimator" syl="syl" />
```

### property ###
(aliases: prop p)
  * name is the afx eval name for the properties (copy and paste from expressions)
  * syl is if it's a syllable timing (if syl=0, then it's a line timing)
  * fixed is if it's fixed timing ("start", "end", or percentages like "50")
  * pos is to generate positional keys
  * link -- link to another property (it requires either layer OR comp and layer) (if you need the property from the same layer, just make your own expression within the same layer)
  * comp -- comp link
  * layer -- layer link

(Properties need at least one keyframe to process, so make sure you have a dummy keyframe if you want to link properties)

For example, to generate syllable keyframes for a property, do the following:
```
<property name="transform.opacity" syl="syl" /> 
```
For example, to link transform.position (make sure you have keyframes here or else this will be ignored) to effect("Point Control")(1) via automatic expressions in Karaoke composition with a template layer karaokeLayer (name or alias in `<layer>`):
```
<p name="transform.position" link='effect("Point Control")(1)' comp="Karaoke" layer="karaokeLayer" />
```

### set ###
(aliases: setting s)
```
<set name="enabled" value="0" />
```
  * name is the afx object name
  * property is the property of that object
  * value is the set value.


--- OR: (For Layer properties)
```
<set name="effect('Layer Control')(1)" layer="karaoke" />
```
  * name: property name within that layer.
  * layer: Layer template name that the property will set to.

-- Use this to link layers.

### dim ###
(aliases: dimension)
  * pos is the position property (ideally for 2D Point Control)
  * size is the size property (ideally for 2D Point contorl)
  * dur is the duration.
    * If you don't specify dur, it will use the in-point and no keyframes.
    * If you specify dur > 0, it will mean the delta-t between each keyframe is dur, and that it will start at the in-point and ends at the out-point... It might be slow.
    * If you specify dur="syl" or anything, it will only generate the keyframes based on the syllable timings associated to the generated layer.

Note: use scale in text animator to obtain syllable sizes.  This is a helper for the expression using sourceRectAtTime to obtain the size and the position of the layer, which is lacked in expression.  It may be slow, so you need to optimize it a bit.

Example:
```
<dim size='effect("Point Control")(1)' pos='effect("Point Control 2")(1)' dur="syl" />
```

Basically, these XML configurations are similar to old functions, as they're used to call the old funs.