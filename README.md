# Colorgen
## Generate an SCSS color theme

###Description

Generates color themes based on a keyword.
Include the scss-partial in your styles to quickly preview themes and their permutations.

Leave the script running while you preview your site, and simply press ```<Enter>``` or ```<p + Enter>``` to move to the next theme or permutation.

    ---
      app.scss
    ---
    [...]
    @import "generated-colors";
    [...]

###Example output :
    ---
      _generated-colors.scss
    ---
    // Generated from the keyword(s): blue
    // Title: (◕〝◕)
    // User: sugar!
    // Permutation:0
    $sugarheartsyou: #FE4365;
    $partyconfetti: #FC9D9A;
    $sugarchampagne: #F9CDAD;
    $burstsofeuphoria: #C8C8A9;
    $happyballoons: #83AF9B;
    $generated-color-1: $sugarheartsyou;
    $generated-color-2: $partyconfetti;
    $generated-color-3: $sugarchampagne;
    $generated-color-4: $burstsofeuphoria;
    $generated-color-5: $happyballoons;

###Installation
* ```gem install thor```
* ```thor install Thorfile```

###Usage :

    $ thor color:palette blue

###Running the script

* ```< Enter > requests a new theme```
* ```< p + Enter > to get next permutation```
* ```< q > to quit:```

Colorgen is powered by:

[COLOURlovers API](http://www.colourlovers.com/api "COLOURlovers API")