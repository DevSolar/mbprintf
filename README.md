# mbprintf

Multibyte-capable printf for bash scripts

## Purpose

The bash builtin printf function has a significant bug:

When strings contain multibyte (non-ASCII-7) characters, the formatting
is off -- because bash printf counts bytes, not printable characters.

Since this is all kinds of annoying, I wrote a shell function mbprintf
that does fix this error.

## Implementation

The mbprintf function iterates through the format string, eating either
a verbatim sequence or a conversion specifier. Conversion specifiers
that are not 's' specifiers are forwarded to printf, while 's' specifiers
are handled by a helper function that does the formatting manually, using
${#string} to determine the string length in printable characters instead
of bytes.

## Status

I didn't bother to add extra handling for 'c' conversions, as I figured
they would not be commonly used in bash scripts.

Other than that, the function _should_ work, and so I consider this code
to be beta quality.
