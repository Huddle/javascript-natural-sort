Javascript Natural Sort
=======================

A natural-sort comparator algorithm.

This version is forked from [overset / javascript-natural-sort](https://github.com/overset/javascript-natural-sort)

We endevour to keep this fork compatible with original however if requirements confict then the Huddle ones will get preference. User beware. 

## Changes in this fork

[Huddle / javascript-natural-sort](https://github.com/Huddle/javascript-natural-sort)

### Localisation

Tokenised string fragments are compared using the native JavaScript [`localeCompare`](https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Global_Objects/String/localeCompare) method. This helps ensure that extended characters are sorted as per users expectations.

The localeCompare sort is disabled when the `naturalSort.insensitive` flag is `false` as it appears to interleave uppercase with lowercase (e.g. A,a,B,b)

Note: Chrome currently does not implement localeCompare as we might expect (it uses char code comparison). We expect this to be fixed soon, see: http://code.google.com/p/v8/issues/detail?id=459

### Negative numbers as strings

A parseInt coercion has been added to tokens whose value is string zero `'0'`. This ensures that -ve number strings are compared by number value rather than dash prefixed string.


## Example use

    // setting case insensitive
    naturalSort.insensitive = true;

    // Simple numerics
    >>> ['10',9,2,'1','4'].sort(naturalSort)
    ['1',2,'4',9,'10']

    // Floats
    >>> ['10.0401',10.022,10.042,'10.021999'].sort(naturalSort)
    ['10.021999',10.022,'10.0401',10.042]

    // Float & decimal notation
    >>> ['10.04f','10.039F','10.038d','10.037D'].sort(naturalSort)
    ['10.037D','10.038d','10.039F','10.04f']

    // Scientific notation
    >>> ['1.528535047e5','1.528535047e7','1.528535047e3'].sort(naturalSort)
    ['1.528535047e3','1.528535047e5','1.528535047e7']

    // IP addresses
    >>> ['192.168.0.100','192.168.0.1','192.168.1.1'].sort(naturalSort)
    ['192.168.0.1','192.168.0.100','192.168.1.1']

    // Filenames
    >>> ['car.mov','01alpha.sgi','001alpha.sgi','my.string_41299.tif'].sort(naturalSort)
    ['001alpha.sgi','01alpha.sgi','car.mov','my.string_41299.tif'

    // Dates
    >>> ['10/12/2008','10/11/2008','10/11/2007','10/12/2007'].sort(naturalSort)
    ['10/11/2007', '10/12/2007', '10/11/2008', '10/12/2008']

    // Money
    >>> ['$10002.00','$10001.02','$10001.01'].sort(naturalSort)
    ['$10001.01','$10001.02','$10002.00']

    // Movie Titles
    >>> ['1 Title - The Big Lebowski','1 Title - Gattaca','1 Title - Last Picture Show'].sort(naturalSort)
    ['1 Title - Gattaca','1 Title - Last Picture Show','1 Title - The Big Lebowski']

    // By default - case-sensitive sorting
    >>> ['a', 'B'].sort(naturalSort);
    ['B', 'a']

    // To enable case-insensitive sorting
    >>> naturalSort.insensitive = true;
    >>> ['a', 'B'].sort(naturalSort);
    ['a', 'B']

