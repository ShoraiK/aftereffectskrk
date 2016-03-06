## Change in v0.52 ##
  * You can now do properties linking to different comps or layers.  How to use it:
```
.p( "propertyName" , {link: ["compName" , "templateLayerName" , "property"]} ) ;
```

The point of this is to be able to link properties to another on different templates or layera.  I made it this way so that one can link positional data quickly without re-generating the data over again on another template, since this process is very slow.  It only requires that the linked template has to contain all of the pertaining layers to the current layer.

# Major Changes in v0.50 #

  * You no longer are required to paste your JSON.  You can now paste your .ass into your text layer in KRK comp. (source text is recommended because of the UTF-8)  The program will parse the .ass internally.
  * Positions are obtained directly in AFX.  The default property for positions are Point expression control named "Position".  This process is extremely slow, so be warn about it.  Note, if your layer names contain an underscore, positions won't be processed.  The reason for this is because if you are using the same layer over and over again, the program will add an underscore to it, so essentially, it's pointless to generate the positions over and over again.
  * Positions linking from non-text layers must link to an existing text layers with those syllables -- commands-- .p( "effect.Position" , {syl: true, pos: "layerName"} )
  * Auto-zero word spacing is implemented.  Just set your Text, More Options, Anchor Point Grouping to "Word."  It will obtain zero-word spacing transparently, allowing you to do per syllable effects.  Spacing control has been deprecated in this version.  (i.e., it no longer works)


# Features #

  * In-Composition Coding for the generator: you do not need to do anything outside of the Project.

  * The .ass timings are first converted into JSON, and have the data stored in the project.  This way, no external files will be necessary.

  * Keyframes renormalizations: you will be able to design the Karaoke visually.

  * Syllable per Layer Capability

  * No-presets, nothing: the outcome depends how good you can design a karaoke!

  * Easy-to-script, and minimal coding

  * Syllable and line positioning with expressions

  * Two Karaoke styles (Romaji\nKanji) in one layer is workable: .l( "romaji" , {2:"kanji"} )

  * Word effect with "Spacing" controls.  Note, it adds an empty space to every syllable and you can adjust it to make them as close as possible with a slider control from main template layer to all of the layers.

  * Run once, and done!  You do not need to do anything after processing.  You can, however, but those work needs to be separate out. (i.e. store into another Composition or precompose)

# Notes #

  * codes can either be in expression or in source text.  The karaoke data can either be in expressions or source text.  Since there's a limit to how much expressions you can have, you might want to force the karaoke data into the source text.  If you do not have enough memory for this operation.  Hide the layer first before pasting the JSON in the source text.  You can do so by double clicking the hidden text layer and hitting CTRL-V.

# Change Logs #0.55: Fixed more bugs (Syllables per layer, text animators with correct spaces)
0.54: Fixed properties linking, do spaces on text animators
0.53: Forces an average for the SPACE widths/heights, since they're 0.
0.52: Minor mistakes
0.51: Added Property linking .p( "property" , {link: ['comp','layer','property'] ) VIA expressions <comp is optional>
0.50: You can now insert .ass into your project
      Auto-word tracking is implemented--for per-syllable effects
      Auto-positioning is implemented using the layer
0.46: Fixed a couple of bugs.
0.45: Added Syllable per layer to line timing: longer effects.
0.44: Fixed text animators for syllable per layer.
      Added Karaoke text as markers on the generated layer for debugging purpose
0.43: Fixed Line timing for two-lined effect (still broken--due to how ranges are added)
      Recursive Property names search
      Added some newbie error checks.
0.42: Added Slider control for syllable spacing,
      In-composition scripting
      Correctly generated text animators using basedOn property.
0.41: Added Autodeletion and Correct markers of generated layers
0.40:  Embeddable scripts
0.30:  Complete objects redesigns
0.20:  Revitalize the script changes
0.1a: Changed to all associative arrays.
0.10:  Initial script}}}```