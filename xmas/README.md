# xmas.c

## Original Article
https://udel.edu/~mm/xmas/

## Build

`gcc xmas.c -o xmas`

## Run

`./xmas`

## Context

In 1988 an impressive piece of C code named xmas.c was a winner in the International Obfuscated C Code Contest. After years of being impressed by the program (I first saw it around 2000), in November 2008, with some spare time on my hands, I decided to rip apart the code and figure out what was going on.

## The code

```c
/*
Least likely to compile successfully: <ian@unipalm.co.uk> Ian Phillipps

    Ian Phillipps
    Cambridge Consultants Ltd
    Science Park
    Milton Road
    Cambridge CB4 4DW
    England

Compile and run without parameters.

The program is smaller than even the 'compressed' form of its output,
and thus represents a new departure in text compression standards.

The judges thought that this program looked like what you would get
by pounding on the keys of an old typewriter at random.

Copyright (c) 1988, Landon Curt Noll & Larry Bassel.
All Rights Reserved.  Permission for personal, educational or non-profit use
is granted provided this this copyright and notice are included in its entirety
and remains unaltered.  All other uses must receive prior permission in
writing from both Landon Curt Noll and Larry Bassel.
*/

#include <stdio.h>
main(t,_,a)
char
*
a;
{
        return!

0<t?
t<3?

main(-79,-13,a+
main(-87,1-_,
main(-86, 0, a+1 )


+a)):

1,
t<_?
main(t+1, _, a )
:3,

main ( -94, -27+t, a )
&&t == 2 ?_
<13 ?

main ( 2, _+1, "%s %d %d\n" )

:9:16:
t<0?
t<-72?
main( _, t,
"@n'+,#'/*{}w+/w#cdnr/+,{}r/*de}+,/*{*+,/w{%+,/w#q#n+,/#{l,+,/n{n+,/+#n+,/#;\
#q#n+,/+k#;*+,/'r :'d*'3,}{w+K w'K:'+}e#';dq#'l q#'+d'K#!/+k#;\
q#'r}eKK#}w'r}eKK{nl]'/#;#q#n'){)#}w'){){nl]'/+#n';d}rw' i;# ){nl]!/n{n#'; \
r{#w'r nc{nl]'/#{l,+'K {rw' iK{;[{nl]'/w#q#\
\
n'wk nw' iwk{KK{nl]!/w{%'l##w#' i; :{nl]'/*{q#'ld;r'}{nlwb!/*de}'c ;;\
{nl'-{}rw]'/+,}##'*}#nc,',#nw]'/+kd'+e}+;\
#'rdq#w! nr'/ ') }+}{rl#'{n' ')# }'+}##(!!/")
:
t<-50?
_==*a ?
putchar(31[a]):

main(-65,_,a+1)
:
main((*a == '/') + t, _, a + 1 )
:

0&#60;t?

main ( 2, 2 , "%s")
:*a=='/'||

main(0,

main(-61,*a, "!ek;dc i@bK'(q)-[w]*%n+r3#l,{}:\nuwloca-O;m
.vpbks,fxntdCeghiry")

,a+1);}
```

## The Output
Amazingly, the output is

```
[mm@noise]$ xmas
On the first day of Christmas my true love gave to me
a partridge in a pear tree.

On the second day of Christmas my true love gave to me
two turtle doves
and a partridge in a pear tree.

On the third day of Christmas my true love gave to me
three french hens, two turtle doves
and a partridge in a pear tree.

On the fourth day of Christmas my true love gave to me
four calling birds, three french hens, two turtle doves
and a partridge in a pear tree.

On the fifth day of Christmas my true love gave to me
five gold rings;
four calling birds, three french hens, two turtle doves
and a partridge in a pear tree.

On the sixth day of Christmas my true love gave to me
six geese a-laying, five gold rings;
four calling birds, three french hens, two turtle doves
and a partridge in a pear tree.

On the seventh day of Christmas my true love gave to me
seven swans a-swimming,
six geese a-laying, five gold rings;
four calling birds, three french hens, two turtle doves
and a partridge in a pear tree.

On the eigth day of Christmas my true love gave to me
eight maids a-milking, seven swans a-swimming,
six geese a-laying, five gold rings;
four calling birds, three french hens, two turtle doves
and a partridge in a pear tree.

On the ninth day of Christmas my true love gave to me
nine ladies dancing, eight maids a-milking, seven swans a-swimming,
six geese a-laying, five gold rings;
four calling birds, three french hens, two turtle doves
and a partridge in a pear tree.

On the tenth day of Christmas my true love gave to me
ten lords a-leaping,
nine ladies dancing, eight maids a-milking, seven swans a-swimming,
six geese a-laying, five gold rings;
four calling birds, three french hens, two turtle doves
and a partridge in a pear tree.

On the eleventh day of Christmas my true love gave to me
eleven pipers piping, ten lords a-leaping,
nine ladies dancing, eight maids a-milking, seven swans a-swimming,
six geese a-laying, five gold rings;
four calling birds, three french hens, two turtle doves
and a partridge in a pear tree.

On the twelfth day of Christmas my true love gave to me
twelve drummers drumming, eleven pipers piping, ten lords a-leaping,
nine ladies dancing, eight maids a-milking, seven swans a-swimming,
six geese a-laying, five gold rings;
four calling birds, three french hens, two turtle doves
and a partridge in a pear tree.
```

## Analysis
So, how in the world was this accomplished? First, the code needs to be rewritten in a more legible manner. Let's replace all a ? b : c constructs with explicit if-then-else blocks. Additionally, it is helpful to define character strings whose names will become clear shortly.

```c
#include <stdio.h>

char *words =
"@n'+,#'/*{}w+/w#cdnr/+,{}r/*de}+,/*{*+,/w{%+,/w#q#n+,/#{l+,/n{n+,/+#n+,/#\
;#q#n+,/+k#;*+,/'r :'d*'3,}{w+K w'K:'+}e#';dq#'l \
q#'+d'K#!/+k#;q#'r}eKK#}w'r}eKK{nl]'/#;#q#n'){)#}w'){){nl]'/+#n';d}rw' i;# \
){nl]!/n{n#'; r{#w'r nc{nl]'/#{l,+'K {rw' iK{;[{nl]'/w#q#n'wk nw' \
iwk{KK{nl]!/w{%'l##w#' i; :{nl]'/*{q#'ld;r'}{nlwb!/*de}'c \
;;{nl'-{}rw]'/+,}##'*}#nc,',#nw]'/+kd'+e}+;#'rdq#w! nr'/ ') }+}{rl#'{n' ')# \
}'+}##(!!/";

char *shift = "!ek;dc i@bK'(q)-[w]*%n+r3#l,{}:\nuwloca-O;m .vpbks,fxntdCeghiry";

main() {
    xmas(1, 0, '\0');
}

xmas(int t, int _, char *a) {

    if (t < -72) {
        return xmas(_, t, words);
    }

    if (t < -50) {
        if (_ == *a) {
            return putchar(a[31]);
        } else {
            return xmas(-65, _, a+1);
        }
    }

    if (t < 0) {
        return xmas((*a == '/')+t, _, a+1);
    }

    if (t == 0) {
        if (*a == '/') {
            return 1;
        } else {
            return xmas(0, xmas(-61, *a, shift), a+1);
        }
    }

    if (t == 1) {
        return xmas(2, 2, "%s");
    }

    if (t == 2)
        xmas(-79, -13, a + xmas(-87, 1-_, a + xmas(-86, 0, a+1)));

    if (t < _)
        xmas(t+1, _, a);

    if (xmas(-94, -27+t, a) && t == 2) {
        if (_ < 13)
            return xmas(2, _+1, "%s %d %d\n");
        else
            return 9;
    } else {
        return 16;
    }
}
```

Already we can see some hint of what is happening. The variable `t` has special significance in controlling the direction of recursion. The first conditional, `if (t < -72)`, is just misdirection mostly for the fun of it. It swaps the first two arguments and recurses using the encrypted string of words for the final argument. The utility of the conditional is how it allows nested recursion as seen in the `if (t == 2)` block by ignoring the third argument.

The second block has more real work going on. If the character stored in the variable `_` does not match the first character of the string `a`, the code recurses in such a way that this same block of code will again be entered. That is, `t=-65` forces a return to the `if (t < -50)` block. The recursion steps through string `a`, character by character. When finally `_ == a`, the character at `a+31` is printed and returned.

Further study shows why this is done. The string I renamed to shift is really two strings concatenated. A character found in the first half of the string is 31 places away from its decoded equivalent. For instance, the exclamation point at the first place in the string is followed 31 places later by a newline. So the string offers the solution to a substitution cipher.

In the code below, comments are added. The variable shift has a comment under it lining up the decoded (shifted by 31) values of the string. For example, under the first character `!`, is character in the string shifted by 31 places, the newline character. The encoded/decoded halves of the string are separated at the colon character.

The other variable, newly named words in the code below, is the set of encrypted words used to print the Christmas carol lyrics. Using the cipher solution string, the words have been decoded in the comments of the source code below. Notice that the ordinal numbers and lines of verses are separated by slash characters.

The third conditional, `if (t < 0)` is used to find `|t|` slash characters and then after `t` recursions, to return `xmas(0, _, a+1)`, where `a+1` is the string starting at the character after the slash. Again, through recursion it simply gets us to the character after `|t|`'th slash. The next call goes into the conditional block described next.

The fourth conditional, `if (t == 0)`, uses recursion with the 2nd conditional block, `t < -50`, to print out the decoded string up to the next slash and then returns 1.

The `t == 1` block is used just a single time at the start to get the recursion going properly, that is, with `xmas(2, 2, "%s")` where the string is unimportant because it is never used.

The `t == 2` block is used to print `"On the [ordinal] day of Christmas my true love gave to me\n"`.

The final two conditional blocks keep the recursion running in two directions. First, the final block counts up to day 12. The second to last block, counts down from the current day to print lyrics of the current verse in reverse order.

```c
#include <stdio.h>

/*
 * Substitution cipher solution.  Letters up to and including the colon are
 * shifted by 31 places to the right to find the decoded value.
 */
char *shift = "!ek;dc i@bK'(q)-[w]*%n+r3#l,{}:\nuwloca-O;m .vpbks,fxntdCeghiry";
         /*  "\nuwloca-O;m .vpbks,fxntdCeghiry"; */

char *words =
"@n'+,#'/*{}w+/w#cdnr/+,{}r/*de}+,/*{*+,/w{%+,/w#q#n+,/#{l+,/n{n+,/+#n+,/#\
;#q#n+,/+k#;*+,/'r :'d*'3,}{w+K w'K:'+}e#';dq#'l \
q#'+d'K#!/+k#;q#'r}eKK#}w'r}eKK{nl]'/#;#q#n'){)#}w'){){nl]'/+#n';d}rw' i;# \
){nl]!/n{n#'; r{#w'r nc{nl]'/#{l,+'K {rw' iK{;[{nl]'/w#q#n'wk nw' \
iwk{KK{nl]!/w{%'l##w#' i; :{nl]'/*{q#'ld;r'}{nlwb!/*de}'c \
;;{nl'-{}rw]'/+,}##'*}#nc,',#nw]'/+kd'+e}+;#'rdq#w! nr'/ ') }+}{rl#'{n' ')# \
}'+}##(!!/";

/*
  Decoded values of 'words' using the substitution cipher string 'shift':

"@n'+,#'/*{}w+/w#cdnr/+,{}r/*de}+,/*{*+,/w{%+,/w#q#n+,/#{l+,/n{n+,/+#n+,/#\
 On the /first/second/third/fourth/fifth/sixth/seventh/eigth/ninth/tenth/e

;#q#n+,/+k#;*+,/'r :'d*'3,}{w+K w'K:'+}e#';dq#'l \
leventh/twelfth/ day of Christmas my true love ga

q#'+d'K#!/+k#;q#'r}eKK#}w'r}eKK{nl]'/#;#q#n'){)#}w'){){nl]'/+#n';d}rw' i;# \
ve to me0/twelve drummers drumming, /eleven pipers piping, /ten lords a-lea

){nl]!/n{n#'; r{#w'r nc{nl]'/#{l,+'K {rw' iK{;[{nl]'/w#q#n'wk nw' \
ping,0/nine ladies dancing, /eight maids a-milking, /seven swans a\

iwk{KK{nl]!/w{%'l##w#' i; :{nl]'/*{q#'ld;r'}{nlwb!/*de}'c \
-swimming,0/six geese a-laying, /five gold rings;0/four ca


;;{nl'-{}rw]'/+,}##'*}#nc,',#nw]'/+kd'+e}+;#'rdq#w! nr'/ ') }+}{rl#'{n' ')# \
lling birds, /three french hens, /two turtle doves0and /a partridge in a pea

}'+}##(!!/";
r tree.00/

*/

main() {
    xmas(1, 0, '\0');
}

xmas(int t, int _, char *a) {

    /* Swap first two args and use new 3rd. */
    if (t < -72) {
        return xmas(_, t, words);
    }

    /*
     * Loop through a till a==_, then print char at a+31.
     * That is, given character in variable '_' and substitution cipher
     * solution in 'a', decode character '_' and print & return it.
     */
    if (t < -50) {
        if (_ == *a) {
            return putchar(a[31]);
        } else {
            /* Loop until _ == *a. */
            return xmas(-65, _, a+1);
        }
    }

    /*
     * Loop until finding -t number of slash characters in a[] and
     * return string starting at character after that slash.
     */
    if (t < 0) {
        return xmas((*a == '/')+t, _, a+1);
    }

    /*
     * Decode & print word up to next slash character and then return 1.
     */
    if (t == 0) {
        if (*a == '/') {
            return 1;
        } else {
            return xmas(0, xmas(-61, *a, shift), a+1);
        }
    }

    /*
     * Start off recursion.  Only called once at very start.
     */
    if (t == 1) {
        return xmas(2, 2, "%s");
    }

    if (t == 2)
        xmas(-79, /* " day of Christmas my true love gave to me\n" */
             -13,
             a + xmas(-87, /* print which day of Christmas it is */
                      1-_,
                      a + xmas(-86, 0, a+1))); /* "On the " */

    /*
     * Recurse, count down days of Christmas
     * from '_' to print lyrics of current verse in reverse day order.
     * I.e., day 12, day 11, etc.
     */
    if (t < _)
        xmas(t+1, _, a);

    /*
     * Print phrase for current verse.
     * E.g., t == 2: "a partridge in a pear tree\n\n"
     * etc.
     */
    if (xmas(-94, -27+t, a) && t == 2) {
        if (_ < 13)
            /* Recurse to next higher day of Christmas.  String not used. */
            return xmas(2, _+1, "%s %d %d\n");
        else
            /* Just misdirection, return value not used. */
            return 9;
    } else {
        /* More misdirection! */
        return 16;
    }
}
```

## Simpler
With new understanding of what's going on, the program can be simplified by using some iteration and C string library routines. I have to admit to preferring recursion myself, but since the analysis has gone this far, let's not stop now. Here's what we might see after further simplification:

```c
#include <stdio.h>
#include <string.h>

char *words =
"@n'+,#'/*{}w+/w#cdnr/+,{}r/*de}+,/*{*+,/w{%+,/w#q#n+,/#{l+,/n{n+,/+#n+,/#\
;#q#n+,/+k#;*+,/'r :'d*'3,}{w+K w'K:'+}e#';dq#'l \
q#'+d'K#!/+k#;q#'r}eKK#}w'r}eKK{nl]'/#;#q#n'){)#}w'){){nl]'/+#n';d}rw' i;# \
){nl]!/n{n#'; r{#w'r nc{nl]'/#{l,+'K {rw' iK{;[{nl]'/w#q#n'wk nw' \
iwk{KK{nl]!/w{%'l##w#' i; :{nl]'/*{q#'ld;r'}{nlwb!/*de}'c \
;;{nl'-{}rw]'/+,}##'*}#nc,',#nw]'/+kd'+e}+;#'rdq#w! nr'/ ') }+}{rl#'{n' ')# \
}'+}##(!!/";

char *shift = "!ek;dc i@bK'(q)-[w]*%n+r3#l,{}:\nuwloca-O;m .vpbks,fxntdCeghiry";

main() {
    xmas(2, 2, "");
}

xmas(int t, int _, char *a) {

    /*
     * Loop until finding |t| number of slash characters in a[] and
     * return string starting at character after that slash.
     */
    if (t < 0) {
        while (t++ < 0)
            a = 1 + index(a, '/');
        return xmas(0, _, a);
    }

    /*
     * Decode & print word up to next slash character and return 0 or any int.
     */
    if (t == 0) {
        while (*a != '/')
            putchar(index(shift, *a++)[31]); /* Decode *a and print it. */
        return 0;
    }

    if (t == 2) {
        /* 2nd arg is a don't-care since it's unused. */
        xmas(0, 0, words); /* "On the " */
        xmas(1-_, 0, words); /* print which day of Christmas it is */
        xmas(-13, 0, words); /* " my true love gave to me\n" */
    }

    /*
     * Recurse and count down days of Christmas
     * from '_' down to and including day 2.
     */
    if (t < _)
        xmas(t+1, _, a);

    /*
     * t==2: "a partridge in a pear tree\n\n"
     * etc.
     */
    xmas(-27+t, 0, words);
    if (t == 2 && _ < 13)
        return xmas(2, _+1, ""); /* Next higher day of Christmas. */
}
```

## In Conclusion...
This could go on till the ultimate simplification of doing nothing more than printing out the lyrics, but you get the idea. This is one of the better obfuscated C programs I've come across because of using the substitution cipher along with recursion. That was followed by the addition of a small bit of unnecessary code and use of random arguments when the arguments were in fact not made use of. A very nice little bundle of C code!

Understanding what's happening is still a long way from writing it. What a great example of creativity.

Merry Christmas!
Mike Markowski, mike.ab3ap -A- gmail -D- com