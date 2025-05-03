# Fonts for MicroPython
Pyx is a set of seven proportional (variable-width) sans-serif bitmap fonts with the basic ASCII 32-126 character set and x-heights of 8, 9, 10, 11, 12, 13 & 15 pixels with some larger sets of numerals at 18, 21 & 24 pixels. 
They are straightforward in use intended to provide simple high-quality text on screen. The examples here are set up for the Waveshare LCD displays but should be easily adaptable.  
The function `graf()` writes the text to the screen and has an argument set that includes a basic overwrite, a fixed width option (for numerals), foreground and background colours with global colour settings, and tracking and space width adjustment. Currently there are no options for text alignment or word wrap.  
`graf0()` is a minimal version that has all the options removed.
![Screen images of examples of each font](/Images/pyx_screenshots.png)
# Details
To be memory efficient, each font is encoded as a single tuple of hex strings (one string for each glyph) with each hex character encoding four pixels. Only the active area of each glyph is encoded, through a pair of offset parameters, and unneeded characters can simply be deleted so different sized fonts can be combined whilst keeping the total size manageable. `pyx_graf.py` includes a demo that displays almost 500 different characters on a Pico (shown above) using the stock Waveshare 320&nbsp;×&nbsp;240 display driver, with its >150&nbsp;kB memory footprint. Sizes 8, 9, 11, 13, & 15 make a very useful set. `pyx_fonts.py` contains the complete font set. Each font has an alternative modern 'a' glyph with a d-like bowl.
# Notes
+ The actual size on screen depends on the pixel density so the font sizes are expressed as x-heights in pixels. For example, pyx10 has an x-height of 10&nbsp;px then the numeral height (& caps height) is 14&nbsp;px and an ‘8’ is 14&nbsp;×&nbsp;9&nbsp;px. However, for a display with a pixel pitch of 0.2&nbsp;mm pyx10 will happen to result in a font size of ~10&nbsp;pt.
+ The first line of each font definition is an index string used to select the glyph. If a glyph is deleted the corresponding character in the index string must be deleted. In fact, any key can be mapped to any glyph and the ° is mapped to  ¬ (keyboard top left). The final glyph ? should be retained as this acts as the missing character symbol. The first character is a dummy to offset the indexing. The single-quote and backslash characters are escaped with a \\.
+ The second line represents the space but also passes the overall character height (just for the overwrite) and parameters for adjusting the tracking (character spacing) and space width.
+ Overwrite simply writes a filled rectangle of background colour, the size of the full text height, from the start of the new text over the length in pixels defined by the value passed.
+ Fixed width is intended only for numeric display where a static character position is preferred.
+ Pyx outlines are based on Deja Vu but have been extensively redrawn.
+ Acknowledgements to Les Wright, Tony Goodhew and others:  
https://github.com/leswright1977/picofont  
https://thepihut.com/blogs/raspberry-pi-tutorials/advanced-text-with-micropython-on-raspberry-pi-pico-displays  
Peter Hinch has more advanced screen and font methods and also provides a 4-bit LCD driver that uses only a fraction of the memory used by the Waveshare drivers.
https://github.com/peterhinch/micropython-font-to-py
