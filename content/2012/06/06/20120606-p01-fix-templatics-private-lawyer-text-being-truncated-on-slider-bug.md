+++
title = "Fix Templatic's Private Lawyer text-being-truncated-on-slider bug"
date = "2012-06-06"
slug = "fix-templatics-private-lawyer-text-being-truncated-on-slider-bug"
tags = ["php", "private lawyer theme", "templatic", "wordpress", "wordpress theme"]
+++




I was having problems with the Coda Slider in the [Private Lawyer Wordpress Theme](http://templatic.com/cms-themes/private-lawyer/) by [Templatic](http://templatic.com/). (The slider is called the __T Anything Slider__ widget by the theme.) Text was being truncated even when the text length was less than the number of characters specified on the widget settings.

A small modification to the `bm_better_excerpt` function in `wp-content/themes/PrivateLaweyer/library/functions/custom_functions.php` solves the problem.


File:  wp-content/themes/PrivateLaweyer/library/functions/custom_functions.php
```php
<?php
// Excerpt length
function bm_better_excerpt($length, $ellipsis) {
$text = get_the_content();
//
// fix weird bug that caused substr to chop
// text even if $length was greater than string length
if (strlen($text) > $length) {
$text = strip_tags($text);
$text = substr($text, 0, $length);
$text = substr($text, 0, strrpos($text, " "));
$text = $text.$ellipsis;
}
return $text;
}
?>
```