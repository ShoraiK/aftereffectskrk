# Introduction #
When I started this project, I was inspired by Auto3 Karaoke Templater, and I tried to be as competitive as possible in the mean time following its lead.  In this document, I will show you similarities and differences between KRK and Auto4.

Of course since I am not an expert in Auto4, and personally have not really used it, but since I glanced through some of the templates done with Auto4 and played around with them, I have some feel for how Auto4 was designed.  If anyone wants to comment on it, please do so.

# Language #
## Auto4 ##
LUA for the language. .ass as the save format.  .ass for the final product.

## KRK ##
JavaScript for expressions. XML for configurations. .ass for timed.  .aep as the save format.  .avi/.mov/etc for the final product

# Design #

## Auto4 ##
  * Time .ass
  * Style them
  * define code lines
  * define template classes
  * Write your codes into the text field (10th field)
  * run
  * process/encode

## KRK ##
  * Time .ass
  * Copy and Paste them into After-Effects's Text Layer
  * Create template text layers and style them and other Template layers
  * Add effects and animators into the text layer
  * Add expressions associated to the animators and properties for what you want (optional)
  * Configure/tell KRK what to use.  KRK isn't very smart. :)
  * Run KRK to generate the proper layers.
  * Render... All expressions are executed at rendering-time.

# Template Classes #
Template classes are grouped templates that do one thing.
Auto4 breaks up the template classes and define under template fields in event lines (9th field).  KRK never separates them out from separate templates.  They are combined, and are understood based on your configurations.

## line and per-line ##
They apply to line templates and per-line templates.

### Auto4 ###
Define in the template.

### KRK ###
Defaults in the XML tags: 

&lt;line&gt;

.

## Syllable/syl ##

### Auto4 ###
Define in the template.

### KRK ###
Specify syl="yes" in the XML tags: 

&lt;line&gt;

.

## furi ##
### Auto4 ###
Define in the template

### KRK ###
KRK will not and cannot support furi due to the way how After-Effects' text layers are recognized.

# Code Lines #
## once ##
### Auto4 ###
"once" identifier allows executions of codes before any lines were processed

### KRK ###
The best way is to think as static XML configurations.  Prior to version 0.60, I was enabling this by introducing javascript evaluations for configurations, allowing users to write their own codes before the processing starts, but it turned out that it doesn't suit for everyone, so I've decided to move away from this concept.

## line ##
### Auto4 ###
"line" identifier allows executions of codes before any syllables were processed during the lines were processed.

### KRK ###
Expressions in After Effects that utilize any properties that are designated as "line" are executed during rendering-time.

## syl and furi ##
### Auto4 ###
"syl" and "furi" allows execution of codes during processing of syl and furi classes.

### KRK ###
KRK does not support codes for furi, as furi is missing.  However, any expressions written to utilize any properties that are designated as syllables are indeed executed during rendering-time.

# Modifiers #
## loop n/repeat n ##
### Auto4 ###
Allows looping of templates (?)

### KRK ###
This is not implemented currently, but you can trick the rendering-time to think it's looped by using expressions in after-effects.

## multi ##
### Auto4 ###
Allows multiple highlights

### KRK ###
Set more than one text animators and put them into separate <a> tags.<br>
<br>
<h2>char</h2>
<h3>Auto4</h3>
Make per-character effects.<br>
<br>
<h3>KRK</h3>
Define Range Selector -> Advanced -> Mode -> Character or Character Excluding Space.<br>
<br>
<h2>notext</h2>
<h3>Auto4</h3>
The original text is not inserted.<br>
<br>
<h3>KRK</h3>
Use disabled.  <br>
<br>
<layer disabled="yes"><br>
<br>
<br>
<br>
<h2>all</h2>
<h3>Auto 4</h3>
Apply template to any style<br>
<br>
<h3>KRK</h3>
Apply lines to any template layers.  (The design is different here)<br>
<br>
<h2>fx inlinefx</h2>

<h3>Auto4</h3>
Applies inlinefx.  Not sure what it does.<br>
<br>
<h3>KRK</h3>
I think it's doable by defining and configuring your effects from the template layers.<br>
<br>
<h2>noblank</h2>

<h3>Auto4</h3>
Skip blank syllables<br>
<br>
<h3>KRK</h3>
This is automatically skipped due to round-off error bugs in After-Effects if they're not skipped.<br>
<br>
<h2>keeptags</h2>

<h3>Auto4</h3>
Original override tags are kept in the output text.<br>
<br>
<h3>KRK</h3>
Not treated yet.  And, they are always in the output layers by default.<br>
<br>
<h2>fxgroupname</h2>

<h3>Auto4</h3>
Declares a template in the group (?)<br>
<br>
<h3>KRK</h3>
All template layers are designated as groups, which can be reused for other designs.<br>
<br>
<h1>Reference</h1>
Auto 4: <a href='http://malakith.net/aegiwiki/Auto4_kara-templater'>http://malakith.net/aegiwiki/Auto4_kara-templater</a>
KRK: <a href='http://code.google.com/p/aftereffectskrk'>http://code.google.com/p/aftereffectskrk</a>