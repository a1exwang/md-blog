# URL Syntax

- tags: url, uri, ietf, rfc

------

#### 摘抄自[RFC1738](http://www.ietf.org/rfc/rfc1738.txt), 删去了不常用的协议, 文法的解释在[RFC822](http://www.ietf.org/rfc/rfc822.txt)

## BNF for specific URL schemes (1994年)

##### 可见早期RFC并未规定URL中http query string的格式, 只规定了query能使用的字符

   This is a BNF-like description of the Uniform Resource Locator
   syntax, using the conventions of RFC822, except that "|" is used to
   designate alternatives, and brackets \[\] are used around optional or
   repeated elements. Briefly, literals are quoted with "", optional
   elements are enclosed in \[brackets\], and elements may be preceded
   with < n> * to designate n or more repetitions of the following
   element; n defaults to 0.


    ; The generic form of a URL is:

    genericurl     = scheme ":" schemepart

    ; Specific predefined schemes are defined here; new schemes
    ; may be registered with IANA

    url            = httpurl | ftpurl | newsurl |
                     nntpurl | telneturl | gopherurl |
                     waisurl | mailtourl | fileurl |
                     prosperourl | otherurl

    ; new schemes follow the general syntax
    otherurl       = genericurl

    ; the scheme is in lower case; interpreters should use case-ignore
    scheme         = 1*[ lowalpha | digit | "+" | "-" | "." ]

    schemepart     = *xchar | ip-schemepart

    ; URL schemeparts for ip based protocols:

    ip-schemepart  = "//" login [ "/" urlpath ]

    login          = [ user [ ":" password ] "@" ] hostport
    hostport       = host [ ":" port ]
    host           = hostname | hostnumber
    hostname       = *[ domainlabel "." ] toplabel
    domainlabel    = alphadigit | alphadigit *[ alphadigit | "-" ] alphadigit
    toplabel       = alpha | alpha *[ alphadigit | "-" ] alphadigit
    alphadigit     = alpha | digit
    hostnumber     = digits "." digits "." digits "." digits
    port           = digits
    user           = *[ uchar | ";" | "?" | "&" | "=" ]
    password       = *[ uchar | ";" | "?" | "&" | "=" ]
    urlpath        = *xchar    ; depends on protocol see section 3.1

    ; The predefined schemes:

    ; FTP (see also RFC959)

    ftpurl         = "ftp://" login [ "/" fpath [ ";type=" ftptype ]]
    fpath          = fsegment *[ "/" fsegment ]
    fsegment       = *[ uchar | "?" | ":" | "@" | "&" | "=" ]
    ftptype        = "A" | "I" | "D" | "a" | "i" | "d"

    ; FILE

    fileurl        = "file://" [ host | "localhost" ] "/" fpath

    ; HTTP

    httpurl        = "http://" hostport [ "/" hpath [ "?" search ]]
    hpath          = hsegment *[ "/" hsegment ]
    hsegment       = *[ uchar | ";" | ":" | "@" | "&" | "=" ]
    search         = *[ uchar | ";" | ":" | "@" | "&" | "=" ]

    ; MAILTO (see also RFC822)

    mailtourl      = "mailto:" encoded822addr
    encoded822addr = 1*xchar               ; further defined in RFC822

    ; Miscellaneous definitions

    lowalpha       = "a" | "b" | "c" | "d" | "e" | "f" | "g" | "h" |
                     "i" | "j" | "k" | "l" | "m" | "n" | "o" | "p" |
                     "q" | "r" | "s" | "t" | "u" | "v" | "w" | "x" |
                     "y" | "z"
    hialpha        = "A" | "B" | "C" | "D" | "E" | "F" | "G" | "H" | "I" |
                     "J" | "K" | "L" | "M" | "N" | "O" | "P" | "Q" | "R" |
                     "S" | "T" | "U" | "V" | "W" | "X" | "Y" | "Z"

    alpha          = lowalpha | hialpha
    digit          = "0" | "1" | "2" | "3" | "4" | "5" | "6" | "7" |
                     "8" | "9"
    safe           = "$" | "-" | "_" | "." | "+"
    extra          = "!" | "*" | "'" | "(" | ")" | ","
    national       = "{" | "}" | "|" | "\\" | "^" | "~" | "[" | "]" | "`"
    punctuation    = "<" | ">" | "#" | "%" | <">


    reserved       = ";" | "/" | "?" | ":" | "@" | "&" | "="
    hex            = digit | "A" | "B" | "C" | "D" | "E" | "F" |
                     "a" | "b" | "c" | "d" | "e" | "f"
    escape         = "%" hex hex

    unreserved     = alpha | digit | safe | extra
    uchar          = unreserved | escape
    xchar          = unreserved | reserved | escape
    digits         = 1*digit

## Collected ABNF for URI(From [RFC3986](https://tools.ietf.org/html/rfc3986))

##### 这个是更晚定义的URI(2005年一月)

    URI           = scheme ":" hier-part [ "?" query ] [ "#" fragment ]

    hier-part     = "//" authority path-abempty
                  / path-absolute
                  / path-rootless
                  / path-empty

    URI-reference = URI / relative-ref

    absolute-URI  = scheme ":" hier-part [ "?" query ]

    relative-ref  = relative-part [ "?" query ] [ "#" fragment ]

    relative-part = "//" authority path-abempty
                  / path-absolute
                  / path-noscheme
                  / path-empty

    scheme        = ALPHA *( ALPHA / DIGIT / "+" / "-" / "." )

    authority     = [ userinfo "@" ] host [ ":" port ]
    userinfo      = *( unreserved / pct-encoded / sub-delims / ":" )
    host          = IP-literal / IPv4address / reg-name
    port          = *DIGIT

    IP-literal    = "[" ( IPv6address / IPvFuture  ) "]"

    IPvFuture     = "v" 1*HEXDIG "." 1*( unreserved / sub-delims / ":" )

    IPv6address   =                            6( h16 ":" ) ls32
                  /                       "::" 5( h16 ":" ) ls32
                  / [               h16 ] "::" 4( h16 ":" ) ls32
                  / [ *1( h16 ":" ) h16 ] "::" 3( h16 ":" ) ls32
                  / [ *2( h16 ":" ) h16 ] "::" 2( h16 ":" ) ls32
                  / [ *3( h16 ":" ) h16 ] "::"    h16 ":"   ls32
                  / [ *4( h16 ":" ) h16 ] "::"              ls32
                  / [ *5( h16 ":" ) h16 ] "::"              h16
                  / [ *6( h16 ":" ) h16 ] "::"

    h16           = 1*4HEXDIG
    ls32          = ( h16 ":" h16 ) / IPv4address
    IPv4address   = dec-octet "." dec-octet "." dec-octet "." dec-octet

    dec-octet     = DIGIT                 ; 0-9
                  / %x31-39 DIGIT         ; 10-99
                  / "1" 2DIGIT            ; 100-199
                  / "2" %x30-34 DIGIT     ; 200-249
                  / "25" %x30-35          ; 250-255

    reg-name      = *( unreserved / pct-encoded / sub-delims )

    path          = path-abempty    ; begins with "/" or is empty
                  / path-absolute   ; begins with "/" but not "//"
                  / path-noscheme   ; begins with a non-colon segment
                  / path-rootless   ; begins with a segment
                  / path-empty      ; zero characters

    path-abempty  = *( "/" segment )
    path-absolute = "/" [ segment-nz *( "/" segment ) ]
    path-noscheme = segment-nz-nc *( "/" segment )
    path-rootless = segment-nz *( "/" segment )
    path-empty    = 0<pchar>

    segment       = *pchar
    segment-nz    = 1*pchar
    segment-nz-nc = 1*( unreserved / pct-encoded / sub-delims / "@" )
                  ; non-zero-length segment without any colon ":"

    pchar         = unreserved / pct-encoded / sub-delims / ":" / "@"

    query         = *( pchar / "/" / "?" )

    fragment      = *( pchar / "/" / "?" )

    pct-encoded   = "%" HEXDIG HEXDIG

    unreserved    = ALPHA / DIGIT / "-" / "." / "_" / "~"
    reserved      = gen-delims / sub-delims
    gen-delims    = ":" / "/" / "?" / "#" / "[" / "]" / "@"
    sub-delims    = "!" / "$" / "&" / "'" / "(" / ")"
                  / "*" / "+" / "," / ";" / "="
