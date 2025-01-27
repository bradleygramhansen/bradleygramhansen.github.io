---
layout: post
title:  "An Introduction to PySPPL"
date:   2018-06-11 
# categories: Notes Python Probabilistic-programming
# author: Bradley
# comments: true
---
<html>
<head><meta charset="utf-8" />
<title>pysppl_walkthrough_1</title><script src="https://cdnjs.cloudflare.com/ajax/libs/require.js/2.1.10/require.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/2.0.3/jquery.min.js"></script>

<style type="text/css">
    /*!
*
* Twitter Bootstrap
*
*/
/*!
 * Bootstrap v3.3.7 (http://getbootstrap.com)
 * Copyright 2011-2016 Twitter, Inc.
 * Licensed under MIT (https://github.com/twbs/bootstrap/blob/master/LICENSE)
 */
/*! normalize.css v3.0.3 | MIT License | github.com/necolas/normalize.css */
html {
  font-family: sans-serif;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
}
body {
  margin: 0;
}
article,
aside,
details,
figcaption,
figure,
footer,
header,
hgroup,
main,
menu,
nav,
section,
summary {
  display: block;
}
audio,
canvas,
progress,
video {
  display: inline-block;
  vertical-align: baseline;
}
audio:not([controls]) {
  display: none;
  height: 0;
}
[hidden],
template {
  display: none;
}
a {
  background-color: transparent;
}
a:active,
a:hover {
  outline: 0;
}
abbr[title] {
  border-bottom: 1px dotted;
}
b,
strong {
  font-weight: bold;
}
dfn {
  font-style: italic;
}
h1 {
  font-size: 2em;
  margin: 0.67em 0;
}
mark {
  background: #ff0;
  color: #000;
}
small {
  font-size: 80%;
}
sub,
sup {
  font-size: 75%;
  line-height: 0;
  position: relative;
  vertical-align: baseline;
}
sup {
  top: -0.5em;
}
sub {
  bottom: -0.25em;
}
img {
  border: 0;
}
svg:not(:root) {
  overflow: hidden;
}
figure {
  margin: 1em 40px;
}
hr {
  box-sizing: content-box;
  height: 0;
}
pre {
  overflow: auto;
}
code,
kbd,
pre,
samp {
  font-family: monospace, monospace;
  font-size: 1em;
}
button,
input,
optgroup,
select,
textarea {
  color: inherit;
  font: inherit;
  margin: 0;
}
button {
  overflow: visible;
}
button,
select {
  text-transform: none;
}
button,
html input[type="button"],
input[type="reset"],
input[type="submit"] {
  -webkit-appearance: button;
  cursor: pointer;
}
button[disabled],
html input[disabled] {
  cursor: default;
}
button::-moz-focus-inner,
input::-moz-focus-inner {
  border: 0;
  padding: 0;
}
input {
  line-height: normal;
}
input[type="checkbox"],
input[type="radio"] {
  box-sizing: border-box;
  padding: 0;
}
input[type="number"]::-webkit-inner-spin-button,
input[type="number"]::-webkit-outer-spin-button {
  height: auto;
}
input[type="search"] {
  -webkit-appearance: textfield;
  box-sizing: content-box;
}
input[type="search"]::-webkit-search-cancel-button,
input[type="search"]::-webkit-search-decoration {
  -webkit-appearance: none;
}
fieldset {
  border: 1px solid #c0c0c0;
  margin: 0 2px;
  padding: 0.35em 0.625em 0.75em;
}
legend {
  border: 0;
  padding: 0;
}
textarea {
  overflow: auto;
}
optgroup {
  font-weight: bold;
}
table {
  border-collapse: collapse;
  border-spacing: 0;
}
td,
th {
  padding: 0;
}
/*! Source: https://github.com/h5bp/html5-boilerplate/blob/master/src/css/main.css */
@media print {
  *,
  *:before,
  *:after {
    background: transparent !important;
    color: #000 !important;
    box-shadow: none !important;
    text-shadow: none !important;
  }
  a,
  a:visited {
    text-decoration: underline;
  }
  a[href]:after {
    content: " (" attr(href) ")";
  }
  abbr[title]:after {
    content: " (" attr(title) ")";
  }
  a[href^="#"]:after,
  a[href^="javascript:"]:after {
    content: "";
  }
  pre,
  blockquote {
    border: 1px solid #999;
    page-break-inside: avoid;
  }
  thead {
    display: table-header-group;
  }
  tr,
  img {
    page-break-inside: avoid;
  }
  img {
    max-width: 100% !important;
  }
  p,
  h2,
  h3 {
    orphans: 3;
    widows: 3;
  }
  h2,
  h3 {
    page-break-after: avoid;
  }
  .navbar {
    display: none;
  }
  .btn > .caret,
  .dropup > .btn > .caret {
    border-top-color: #000 !important;
  }
  .label {
    border: 1px solid #000;
  }
  .table {
    border-collapse: collapse !important;
  }
  .table td,
  .table th {
    background-color: #fff !important;
  }
  .table-bordered th,
  .table-bordered td {
    border: 1px solid #ddd !important;
  }
}
@font-face {
  font-family: 'Glyphicons Halflings';
  src: url('../components/bootstrap/fonts/glyphicons-halflings-regular.eot');
  src: url('../components/bootstrap/fonts/glyphicons-halflings-regular.eot?#iefix') format('embedded-opentype'), url('../components/bootstrap/fonts/glyphicons-halflings-regular.woff2') format('woff2'), url('../components/bootstrap/fonts/glyphicons-halflings-regular.woff') format('woff'), url('../components/bootstrap/fonts/glyphicons-halflings-regular.ttf') format('truetype'), url('../components/bootstrap/fonts/glyphicons-halflings-regular.svg#glyphicons_halflingsregular') format('svg');
}
.glyphicon {
  position: relative;
  top: 1px;
  display: inline-block;
  font-family: 'Glyphicons Halflings';
  font-style: normal;
  font-weight: normal;
  line-height: 1;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
.glyphicon-asterisk:before {
  content: "\002a";
}
.glyphicon-plus:before {
  content: "\002b";
}
.glyphicon-euro:before,
.glyphicon-eur:before {
  content: "\20ac";
}
.glyphicon-minus:before {
  content: "\2212";
}
.glyphicon-cloud:before {
  content: "\2601";
}
.glyphicon-envelope:before {
  content: "\2709";
}
.glyphicon-pencil:before {
  content: "\270f";
}
.glyphicon-glass:before {
  content: "\e001";
}
.glyphicon-music:before {
  content: "\e002";
}
.glyphicon-search:before {
  content: "\e003";
}
.glyphicon-heart:before {
  content: "\e005";
}
.glyphicon-star:before {
  content: "\e006";
}
.glyphicon-star-empty:before {
  content: "\e007";
}
.glyphicon-user:before {
  content: "\e008";
}
.glyphicon-film:before {
  content: "\e009";
}
.glyphicon-th-large:before {
  content: "\e010";
}
.glyphicon-th:before {
  content: "\e011";
}
.glyphicon-th-list:before {
  content: "\e012";
}
.glyphicon-ok:before {
  content: "\e013";
}
.glyphicon-remove:before {
  content: "\e014";
}
.glyphicon-zoom-in:before {
  content: "\e015";
}
.glyphicon-zoom-out:before {
  content: "\e016";
}
.glyphicon-off:before {
  content: "\e017";
}
.glyphicon-signal:before {
  content: "\e018";
}
.glyphicon-cog:before {
  content: "\e019";
}
.glyphicon-trash:before {
  content: "\e020";
}
.glyphicon-home:before {
  content: "\e021";
}
.glyphicon-file:before {
  content: "\e022";
}
.glyphicon-time:before {
  content: "\e023";
}
.glyphicon-road:before {
  content: "\e024";
}
.glyphicon-download-alt:before {
  content: "\e025";
}
.glyphicon-download:before {
  content: "\e026";
}
.glyphicon-upload:before {
  content: "\e027";
}
.glyphicon-inbox:before {
  content: "\e028";
}
.glyphicon-play-circle:before {
  content: "\e029";
}
.glyphicon-repeat:before {
  content: "\e030";
}
.glyphicon-refresh:before {
  content: "\e031";
}
.glyphicon-list-alt:before {
  content: "\e032";
}
.glyphicon-lock:before {
  content: "\e033";
}
.glyphicon-flag:before {
  content: "\e034";
}
.glyphicon-headphones:before {
  content: "\e035";
}
.glyphicon-volume-off:before {
  content: "\e036";
}
.glyphicon-volume-down:before {
  content: "\e037";
}
.glyphicon-volume-up:before {
  content: "\e038";
}
.glyphicon-qrcode:before {
  content: "\e039";
}
.glyphicon-barcode:before {
  content: "\e040";
}
.glyphicon-tag:before {
  content: "\e041";
}
.glyphicon-tags:before {
  content: "\e042";
}
.glyphicon-book:before {
  content: "\e043";
}
.glyphicon-bookmark:before {
  content: "\e044";
}
.glyphicon-print:before {
  content: "\e045";
}
.glyphicon-camera:before {
  content: "\e046";
}
.glyphicon-font:before {
  content: "\e047";
}
.glyphicon-bold:before {
  content: "\e048";
}
.glyphicon-italic:before {
  content: "\e049";
}
.glyphicon-text-height:before {
  content: "\e050";
}
.glyphicon-text-width:before {
  content: "\e051";
}
.glyphicon-align-left:before {
  content: "\e052";
}
.glyphicon-align-center:before {
  content: "\e053";
}
.glyphicon-align-right:before {
  content: "\e054";
}
.glyphicon-align-justify:before {
  content: "\e055";
}
.glyphicon-list:before {
  content: "\e056";
}
.glyphicon-indent-left:before {
  content: "\e057";
}
.glyphicon-indent-right:before {
  content: "\e058";
}
.glyphicon-facetime-video:before {
  content: "\e059";
}
.glyphicon-picture:before {
  content: "\e060";
}
.glyphicon-map-marker:before {
  content: "\e062";
}
.glyphicon-adjust:before {
  content: "\e063";
}
.glyphicon-tint:before {
  content: "\e064";
}
.glyphicon-edit:before {
  content: "\e065";
}
.glyphicon-share:before {
  content: "\e066";
}
.glyphicon-check:before {
  content: "\e067";
}
.glyphicon-move:before {
  content: "\e068";
}
.glyphicon-step-backward:before {
  content: "\e069";
}
.glyphicon-fast-backward:before {
  content: "\e070";
}
.glyphicon-backward:before {
  content: "\e071";
}
.glyphicon-play:before {
  content: "\e072";
}
.glyphicon-pause:before {
  content: "\e073";
}
.glyphicon-stop:before {
  content: "\e074";
}
.glyphicon-forward:before {
  content: "\e075";
}
.glyphicon-fast-forward:before {
  content: "\e076";
}
.glyphicon-step-forward:before {
  content: "\e077";
}
.glyphicon-eject:before {
  content: "\e078";
}
.glyphicon-chevron-left:before {
  content: "\e079";
}
.glyphicon-chevron-right:before {
  content: "\e080";
}
.glyphicon-plus-sign:before {
  content: "\e081";
}
.glyphicon-minus-sign:before {
  content: "\e082";
}
.glyphicon-remove-sign:before {
  content: "\e083";
}
.glyphicon-ok-sign:before {
  content: "\e084";
}
.glyphicon-question-sign:before {
  content: "\e085";
}
.glyphicon-info-sign:before {
  content: "\e086";
}
.glyphicon-screenshot:before {
  content: "\e087";
}
.glyphicon-remove-circle:before {
  content: "\e088";
}
.glyphicon-ok-circle:before {
  content: "\e089";
}
.glyphicon-ban-circle:before {
  content: "\e090";
}
.glyphicon-arrow-left:before {
  content: "\e091";
}
.glyphicon-arrow-right:before {
  content: "\e092";
}
.glyphicon-arrow-up:before {
  content: "\e093";
}
.glyphicon-arrow-down:before {
  content: "\e094";
}
.glyphicon-share-alt:before {
  content: "\e095";
}
.glyphicon-resize-full:before {
  content: "\e096";
}
.glyphicon-resize-small:before {
  content: "\e097";
}
.glyphicon-exclamation-sign:before {
  content: "\e101";
}
.glyphicon-gift:before {
  content: "\e102";
}
.glyphicon-leaf:before {
  content: "\e103";
}
.glyphicon-fire:before {
  content: "\e104";
}
.glyphicon-eye-open:before {
  content: "\e105";
}
.glyphicon-eye-close:before {
  content: "\e106";
}
.glyphicon-warning-sign:before {
  content: "\e107";
}
.glyphicon-plane:before {
  content: "\e108";
}
.glyphicon-calendar:before {
  content: "\e109";
}
.glyphicon-random:before {
  content: "\e110";
}
.glyphicon-comment:before {
  content: "\e111";
}
.glyphicon-magnet:before {
  content: "\e112";
}
.glyphicon-chevron-up:before {
  content: "\e113";
}
.glyphicon-chevron-down:before {
  content: "\e114";
}
.glyphicon-retweet:before {
  content: "\e115";
}
.glyphicon-shopping-cart:before {
  content: "\e116";
}
.glyphicon-folder-close:before {
  content: "\e117";
}
.glyphicon-folder-open:before {
  content: "\e118";
}
.glyphicon-resize-vertical:before {
  content: "\e119";
}
.glyphicon-resize-horizontal:before {
  content: "\e120";
}
.glyphicon-hdd:before {
  content: "\e121";
}
.glyphicon-bullhorn:before {
  content: "\e122";
}
.glyphicon-bell:before {
  content: "\e123";
}
.glyphicon-certificate:before {
  content: "\e124";
}
.glyphicon-thumbs-up:before {
  content: "\e125";
}
.glyphicon-thumbs-down:before {
  content: "\e126";
}
.glyphicon-hand-right:before {
  content: "\e127";
}
.glyphicon-hand-left:before {
  content: "\e128";
}
.glyphicon-hand-up:before {
  content: "\e129";
}
.glyphicon-hand-down:before {
  content: "\e130";
}
.glyphicon-circle-arrow-right:before {
  content: "\e131";
}
.glyphicon-circle-arrow-left:before {
  content: "\e132";
}
.glyphicon-circle-arrow-up:before {
  content: "\e133";
}
.glyphicon-circle-arrow-down:before {
  content: "\e134";
}
.glyphicon-globe:before {
  content: "\e135";
}
.glyphicon-wrench:before {
  content: "\e136";
}
.glyphicon-tasks:before {
  content: "\e137";
}
.glyphicon-filter:before {
  content: "\e138";
}
.glyphicon-briefcase:before {
  content: "\e139";
}
.glyphicon-fullscreen:before {
  content: "\e140";
}
.glyphicon-dashboard:before {
  content: "\e141";
}
.glyphicon-paperclip:before {
  content: "\e142";
}
.glyphicon-heart-empty:before {
  content: "\e143";
}
.glyphicon-link:before {
  content: "\e144";
}
.glyphicon-phone:before {
  content: "\e145";
}
.glyphicon-pushpin:before {
  content: "\e146";
}
.glyphicon-usd:before {
  content: "\e148";
}
.glyphicon-gbp:before {
  content: "\e149";
}
.glyphicon-sort:before {
  content: "\e150";
}
.glyphicon-sort-by-alphabet:before {
  content: "\e151";
}
.glyphicon-sort-by-alphabet-alt:before {
  content: "\e152";
}
.glyphicon-sort-by-order:before {
  content: "\e153";
}
.glyphicon-sort-by-order-alt:before {
  content: "\e154";
}
.glyphicon-sort-by-attributes:before {
  content: "\e155";
}
.glyphicon-sort-by-attributes-alt:before {
  content: "\e156";
}
.glyphicon-unchecked:before {
  content: "\e157";
}
.glyphicon-expand:before {
  content: "\e158";
}
.glyphicon-collapse-down:before {
  content: "\e159";
}
.glyphicon-collapse-up:before {
  content: "\e160";
}
.glyphicon-log-in:before {
  content: "\e161";
}
.glyphicon-flash:before {
  content: "\e162";
}
.glyphicon-log-out:before {
  content: "\e163";
}
.glyphicon-new-window:before {
  content: "\e164";
}
.glyphicon-record:before {
  content: "\e165";
}
.glyphicon-save:before {
  content: "\e166";
}
.glyphicon-open:before {
  content: "\e167";
}
.glyphicon-saved:before {
  content: "\e168";
}
.glyphicon-import:before {
  content: "\e169";
}
.glyphicon-export:before {
  content: "\e170";
}
.glyphicon-send:before {
  content: "\e171";
}
.glyphicon-floppy-disk:before {
  content: "\e172";
}
.glyphicon-floppy-saved:before {
  content: "\e173";
}
.glyphicon-floppy-remove:before {
  content: "\e174";
}
.glyphicon-floppy-save:before {
  content: "\e175";
}
.glyphicon-floppy-open:before {
  content: "\e176";
}
.glyphicon-credit-card:before {
  content: "\e177";
}
.glyphicon-transfer:before {
  content: "\e178";
}
.glyphicon-cutlery:before {
  content: "\e179";
}
.glyphicon-header:before {
  content: "\e180";
}
.glyphicon-compressed:before {
  content: "\e181";
}
.glyphicon-earphone:before {
  content: "\e182";
}
.glyphicon-phone-alt:before {
  content: "\e183";
}
.glyphicon-tower:before {
  content: "\e184";
}
.glyphicon-stats:before {
  content: "\e185";
}
.glyphicon-sd-video:before {
  content: "\e186";
}
.glyphicon-hd-video:before {
  content: "\e187";
}
.glyphicon-subtitles:before {
  content: "\e188";
}
.glyphicon-sound-stereo:before {
  content: "\e189";
}
.glyphicon-sound-dolby:before {
  content: "\e190";
}
.glyphicon-sound-5-1:before {
  content: "\e191";
}
.glyphicon-sound-6-1:before {
  content: "\e192";
}
.glyphicon-sound-7-1:before {
  content: "\e193";
}
.glyphicon-copyright-mark:before {
  content: "\e194";
}
.glyphicon-registration-mark:before {
  content: "\e195";
}
.glyphicon-cloud-download:before {
  content: "\e197";
}
.glyphicon-cloud-upload:before {
  content: "\e198";
}
.glyphicon-tree-conifer:before {
  content: "\e199";
}
.glyphicon-tree-deciduous:before {
  content: "\e200";
}
.glyphicon-cd:before {
  content: "\e201";
}
.glyphicon-save-file:before {
  content: "\e202";
}
.glyphicon-open-file:before {
  content: "\e203";
}
.glyphicon-level-up:before {
  content: "\e204";
}
.glyphicon-copy:before {
  content: "\e205";
}
.glyphicon-paste:before {
  content: "\e206";
}
.glyphicon-alert:before {
  content: "\e209";
}
.glyphicon-equalizer:before {
  content: "\e210";
}
.glyphicon-king:before {
  content: "\e211";
}
.glyphicon-queen:before {
  content: "\e212";
}
.glyphicon-pawn:before {
  content: "\e213";
}
.glyphicon-bishop:before {
  content: "\e214";
}
.glyphicon-knight:before {
  content: "\e215";
}
.glyphicon-baby-formula:before {
  content: "\e216";
}
.glyphicon-tent:before {
  content: "\26fa";
}
.glyphicon-blackboard:before {
  content: "\e218";
}
.glyphicon-bed:before {
  content: "\e219";
}
.glyphicon-apple:before {
  content: "\f8ff";
}
.glyphicon-erase:before {
  content: "\e221";
}
.glyphicon-hourglass:before {
  content: "\231b";
}
.glyphicon-lamp:before {
  content: "\e223";
}
.glyphicon-duplicate:before {
  content: "\e224";
}
.glyphicon-piggy-bank:before {
  content: "\e225";
}
.glyphicon-scissors:before {
  content: "\e226";
}
.glyphicon-bitcoin:before {
  content: "\e227";
}
.glyphicon-btc:before {
  content: "\e227";
}
.glyphicon-xbt:before {
  content: "\e227";
}
.glyphicon-yen:before {
  content: "\00a5";
}
.glyphicon-jpy:before {
  content: "\00a5";
}
.glyphicon-ruble:before {
  content: "\20bd";
}
.glyphicon-rub:before {
  content: "\20bd";
}
.glyphicon-scale:before {
  content: "\e230";
}
.glyphicon-ice-lolly:before {
  content: "\e231";
}
.glyphicon-ice-lolly-tasted:before {
  content: "\e232";
}
.glyphicon-education:before {
  content: "\e233";
}
.glyphicon-option-horizontal:before {
  content: "\e234";
}
.glyphicon-option-vertical:before {
  content: "\e235";
}
.glyphicon-menu-hamburger:before {
  content: "\e236";
}
.glyphicon-modal-window:before {
  content: "\e237";
}
.glyphicon-oil:before {
  content: "\e238";
}
.glyphicon-grain:before {
  content: "\e239";
}
.glyphicon-sunglasses:before {
  content: "\e240";
}
.glyphicon-text-size:before {
  content: "\e241";
}
.glyphicon-text-color:before {
  content: "\e242";
}
.glyphicon-text-background:before {
  content: "\e243";
}
.glyphicon-object-align-top:before {
  content: "\e244";
}
.glyphicon-object-align-bottom:before {
  content: "\e245";
}
.glyphicon-object-align-horizontal:before {
  content: "\e246";
}
.glyphicon-object-align-left:before {
  content: "\e247";
}
.glyphicon-object-align-vertical:before {
  content: "\e248";
}
.glyphicon-object-align-right:before {
  content: "\e249";
}
.glyphicon-triangle-right:before {
  content: "\e250";
}
.glyphicon-triangle-left:before {
  content: "\e251";
}
.glyphicon-triangle-bottom:before {
  content: "\e252";
}
.glyphicon-triangle-top:before {
  content: "\e253";
}
.glyphicon-console:before {
  content: "\e254";
}
.glyphicon-superscript:before {
  content: "\e255";
}
.glyphicon-subscript:before {
  content: "\e256";
}
.glyphicon-menu-left:before {
  content: "\e257";
}
.glyphicon-menu-right:before {
  content: "\e258";
}
.glyphicon-menu-down:before {
  content: "\e259";
}
.glyphicon-menu-up:before {
  content: "\e260";
}
* {
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
}
*:before,
*:after {
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
}
html {
  font-size: 10px;
  -webkit-tap-highlight-color: rgba(0, 0, 0, 0);
}
body {
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
  font-size: 13px;
  line-height: 1.42857143;
  color: #000;
  background-color: #fff;
}
input,
button,
select,
textarea {
  font-family: inherit;
  font-size: inherit;
  line-height: inherit;
}
a {
  color: #337ab7;
  text-decoration: none;
}
a:hover,
a:focus {
  color: #23527c;
  text-decoration: underline;
}
a:focus {
  outline: 5px auto -webkit-focus-ring-color;
  outline-offset: -2px;
}
figure {
  margin: 0;
}
img {
  vertical-align: middle;
}
.img-responsive,
.thumbnail > img,
.thumbnail a > img,
.carousel-inner > .item > img,
.carousel-inner > .item > a > img {
  display: block;
  max-width: 100%;
  height: auto;
}
.img-rounded {
  border-radius: 3px;
}
.img-thumbnail {
  padding: 4px;
  line-height: 1.42857143;
  background-color: #fff;
  border: 1px solid #ddd;
  border-radius: 2px;
  -webkit-transition: all 0.2s ease-in-out;
  -o-transition: all 0.2s ease-in-out;
  transition: all 0.2s ease-in-out;
  display: inline-block;
  max-width: 100%;
  height: auto;
}
.img-circle {
  border-radius: 50%;
}
hr {
  margin-top: 18px;
  margin-bottom: 18px;
  border: 0;
  border-top: 1px solid #eeeeee;
}
.sr-only {
  position: absolute;
  width: 1px;
  height: 1px;
  margin: -1px;
  padding: 0;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  border: 0;
}
.sr-only-focusable:active,
.sr-only-focusable:focus {
  position: static;
  width: auto;
  height: auto;
  margin: 0;
  overflow: visible;
  clip: auto;
}
[role="button"] {
  cursor: pointer;
}
h1,
h2,
h3,
h4,
h5,
h6,
.h1,
.h2,
.h3,
.h4,
.h5,
.h6 {
  font-family: inherit;
  font-weight: 500;
  line-height: 1.1;
  color: inherit;
}
h1 small,
h2 small,
h3 small,
h4 small,
h5 small,
h6 small,
.h1 small,
.h2 small,
.h3 small,
.h4 small,
.h5 small,
.h6 small,
h1 .small,
h2 .small,
h3 .small,
h4 .small,
h5 .small,
h6 .small,
.h1 .small,
.h2 .small,
.h3 .small,
.h4 .small,
.h5 .small,
.h6 .small {
  font-weight: normal;
  line-height: 1;
  color: #777777;
}
h1,
.h1,
h2,
.h2,
h3,
.h3 {
  margin-top: 18px;
  margin-bottom: 9px;
}
h1 small,
.h1 small,
h2 small,
.h2 small,
h3 small,
.h3 small,
h1 .small,
.h1 .small,
h2 .small,
.h2 .small,
h3 .small,
.h3 .small {
  font-size: 65%;
}
h4,
.h4,
h5,
.h5,
h6,
.h6 {
  margin-top: 9px;
  margin-bottom: 9px;
}
h4 small,
.h4 small,
h5 small,
.h5 small,
h6 small,
.h6 small,
h4 .small,
.h4 .small,
h5 .small,
.h5 .small,
h6 .small,
.h6 .small {
  font-size: 75%;
}
h1,
.h1 {
  font-size: 33px;
}
h2,
.h2 {
  font-size: 27px;
}
h3,
.h3 {
  font-size: 23px;
}
h4,
.h4 {
  font-size: 17px;
}
h5,
.h5 {
  font-size: 13px;
}
h6,
.h6 {
  font-size: 12px;
}
p {
  margin: 0 0 9px;
}
.lead {
  margin-bottom: 18px;
  font-size: 14px;
  font-weight: 300;
  line-height: 1.4;
}
@media (min-width: 768px) {
  .lead {
    font-size: 19.5px;
  }
}
small,
.small {
  font-size: 92%;
}
mark,
.mark {
  background-color: #fcf8e3;
  padding: .2em;
}
.text-left {
  text-align: left;
}
.text-right {
  text-align: right;
}
.text-center {
  text-align: center;
}
.text-justify {
  text-align: justify;
}
.text-nowrap {
  white-space: nowrap;
}
.text-lowercase {
  text-transform: lowercase;
}
.text-uppercase {
  text-transform: uppercase;
}
.text-capitalize {
  text-transform: capitalize;
}
.text-muted {
  color: #777777;
}
.text-primary {
  color: #337ab7;
}
a.text-primary:hover,
a.text-primary:focus {
  color: #286090;
}
.text-success {
  color: #3c763d;
}
a.text-success:hover,
a.text-success:focus {
  color: #2b542c;
}
.text-info {
  color: #31708f;
}
a.text-info:hover,
a.text-info:focus {
  color: #245269;
}
.text-warning {
  color: #8a6d3b;
}
a.text-warning:hover,
a.text-warning:focus {
  color: #66512c;
}
.text-danger {
  color: #a94442;
}
a.text-danger:hover,
a.text-danger:focus {
  color: #843534;
}
.bg-primary {
  color: #fff;
  background-color: #337ab7;
}
a.bg-primary:hover,
a.bg-primary:focus {
  background-color: #286090;
}
.bg-success {
  background-color: #dff0d8;
}
a.bg-success:hover,
a.bg-success:focus {
  background-color: #c1e2b3;
}
.bg-info {
  background-color: #d9edf7;
}
a.bg-info:hover,
a.bg-info:focus {
  background-color: #afd9ee;
}
.bg-warning {
  background-color: #fcf8e3;
}
a.bg-warning:hover,
a.bg-warning:focus {
  background-color: #f7ecb5;
}
.bg-danger {
  background-color: #f2dede;
}
a.bg-danger:hover,
a.bg-danger:focus {
  background-color: #e4b9b9;
}
.page-header {
  padding-bottom: 8px;
  margin: 36px 0 18px;
  border-bottom: 1px solid #eeeeee;
}
ul,
ol {
  margin-top: 0;
  margin-bottom: 9px;
}
ul ul,
ol ul,
ul ol,
ol ol {
  margin-bottom: 0;
}
.list-unstyled {
  padding-left: 0;
  list-style: none;
}
.list-inline {
  padding-left: 0;
  list-style: none;
  margin-left: -5px;
}
.list-inline > li {
  display: inline-block;
  padding-left: 5px;
  padding-right: 5px;
}
dl {
  margin-top: 0;
  margin-bottom: 18px;
}
dt,
dd {
  line-height: 1.42857143;
}
dt {
  font-weight: bold;
}
dd {
  margin-left: 0;
}
@media (min-width: 541px) {
  .dl-horizontal dt {
    float: left;
    width: 160px;
    clear: left;
    text-align: right;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
  }
  .dl-horizontal dd {
    margin-left: 180px;
  }
}
abbr[title],
abbr[data-original-title] {
  cursor: help;
  border-bottom: 1px dotted #777777;
}
.initialism {
  font-size: 90%;
  text-transform: uppercase;
}
blockquote {
  padding: 9px 18px;
  margin: 0 0 18px;
  font-size: inherit;
  border-left: 5px solid #eeeeee;
}
blockquote p:last-child,
blockquote ul:last-child,
blockquote ol:last-child {
  margin-bottom: 0;
}
blockquote footer,
blockquote small,
blockquote .small {
  display: block;
  font-size: 80%;
  line-height: 1.42857143;
  color: #777777;
}
blockquote footer:before,
blockquote small:before,
blockquote .small:before {
  content: '\2014 \00A0';
}
.blockquote-reverse,
blockquote.pull-right {
  padding-right: 15px;
  padding-left: 0;
  border-right: 5px solid #eeeeee;
  border-left: 0;
  text-align: right;
}
.blockquote-reverse footer:before,
blockquote.pull-right footer:before,
.blockquote-reverse small:before,
blockquote.pull-right small:before,
.blockquote-reverse .small:before,
blockquote.pull-right .small:before {
  content: '';
}
.blockquote-reverse footer:after,
blockquote.pull-right footer:after,
.blockquote-reverse small:after,
blockquote.pull-right small:after,
.blockquote-reverse .small:after,
blockquote.pull-right .small:after {
  content: '\00A0 \2014';
}
address {
  margin-bottom: 18px;
  font-style: normal;
  line-height: 1.42857143;
}
code,
kbd,
pre,
samp {
  font-family: monospace;
}
code {
  padding: 2px 4px;
  font-size: 90%;
  color: #c7254e;
  background-color: #f9f2f4;
  border-radius: 2px;
}
kbd {
  padding: 2px 4px;
  font-size: 90%;
  color: #888;
  background-color: transparent;
  border-radius: 1px;
  box-shadow: inset 0 -1px 0 rgba(0, 0, 0, 0.25);
}
kbd kbd {
  padding: 0;
  font-size: 100%;
  font-weight: bold;
  box-shadow: none;
}
pre {
  display: block;
  padding: 8.5px;
  margin: 0 0 9px;
  font-size: 12px;
  line-height: 1.42857143;
  word-break: break-all;
  word-wrap: break-word;
  color: #333333;
  background-color: #f5f5f5;
  border: 1px solid #ccc;
  border-radius: 2px;
}
pre code {
  padding: 0;
  font-size: inherit;
  color: inherit;
  white-space: pre-wrap;
  background-color: transparent;
  border-radius: 0;
}
.pre-scrollable {
  max-height: 340px;
  overflow-y: scroll;
}
.container {
  margin-right: auto;
  margin-left: auto;
  padding-left: 0px;
  padding-right: 0px;
}
@media (min-width: 768px) {
  .container {
    width: 768px;
  }
}
@media (min-width: 992px) {
  .container {
    width: 940px;
  }
}
@media (min-width: 1200px) {
  .container {
    width: 1140px;
  }
}
.container-fluid {
  margin-right: auto;
  margin-left: auto;
  padding-left: 0px;
  padding-right: 0px;
}
.row {
  margin-left: 0px;
  margin-right: 0px;
}
.col-xs-1, .col-sm-1, .col-md-1, .col-lg-1, .col-xs-2, .col-sm-2, .col-md-2, .col-lg-2, .col-xs-3, .col-sm-3, .col-md-3, .col-lg-3, .col-xs-4, .col-sm-4, .col-md-4, .col-lg-4, .col-xs-5, .col-sm-5, .col-md-5, .col-lg-5, .col-xs-6, .col-sm-6, .col-md-6, .col-lg-6, .col-xs-7, .col-sm-7, .col-md-7, .col-lg-7, .col-xs-8, .col-sm-8, .col-md-8, .col-lg-8, .col-xs-9, .col-sm-9, .col-md-9, .col-lg-9, .col-xs-10, .col-sm-10, .col-md-10, .col-lg-10, .col-xs-11, .col-sm-11, .col-md-11, .col-lg-11, .col-xs-12, .col-sm-12, .col-md-12, .col-lg-12 {
  position: relative;
  min-height: 1px;
  padding-left: 0px;
  padding-right: 0px;
}
.col-xs-1, .col-xs-2, .col-xs-3, .col-xs-4, .col-xs-5, .col-xs-6, .col-xs-7, .col-xs-8, .col-xs-9, .col-xs-10, .col-xs-11, .col-xs-12 {
  float: left;
}
.col-xs-12 {
  width: 100%;
}
.col-xs-11 {
  width: 91.66666667%;
}
.col-xs-10 {
  width: 83.33333333%;
}
.col-xs-9 {
  width: 75%;
}
.col-xs-8 {
  width: 66.66666667%;
}
.col-xs-7 {
  width: 58.33333333%;
}
.col-xs-6 {
  width: 50%;
}
.col-xs-5 {
  width: 41.66666667%;
}
.col-xs-4 {
  width: 33.33333333%;
}
.col-xs-3 {
  width: 25%;
}
.col-xs-2 {
  width: 16.66666667%;
}
.col-xs-1 {
  width: 8.33333333%;
}
.col-xs-pull-12 {
  right: 100%;
}
.col-xs-pull-11 {
  right: 91.66666667%;
}
.col-xs-pull-10 {
  right: 83.33333333%;
}
.col-xs-pull-9 {
  right: 75%;
}
.col-xs-pull-8 {
  right: 66.66666667%;
}
.col-xs-pull-7 {
  right: 58.33333333%;
}
.col-xs-pull-6 {
  right: 50%;
}
.col-xs-pull-5 {
  right: 41.66666667%;
}
.col-xs-pull-4 {
  right: 33.33333333%;
}
.col-xs-pull-3 {
  right: 25%;
}
.col-xs-pull-2 {
  right: 16.66666667%;
}
.col-xs-pull-1 {
  right: 8.33333333%;
}
.col-xs-pull-0 {
  right: auto;
}
.col-xs-push-12 {
  left: 100%;
}
.col-xs-push-11 {
  left: 91.66666667%;
}
.col-xs-push-10 {
  left: 83.33333333%;
}
.col-xs-push-9 {
  left: 75%;
}
.col-xs-push-8 {
  left: 66.66666667%;
}
.col-xs-push-7 {
  left: 58.33333333%;
}
.col-xs-push-6 {
  left: 50%;
}
.col-xs-push-5 {
  left: 41.66666667%;
}
.col-xs-push-4 {
  left: 33.33333333%;
}
.col-xs-push-3 {
  left: 25%;
}
.col-xs-push-2 {
  left: 16.66666667%;
}
.col-xs-push-1 {
  left: 8.33333333%;
}
.col-xs-push-0 {
  left: auto;
}
.col-xs-offset-12 {
  margin-left: 100%;
}
.col-xs-offset-11 {
  margin-left: 91.66666667%;
}
.col-xs-offset-10 {
  margin-left: 83.33333333%;
}
.col-xs-offset-9 {
  margin-left: 75%;
}
.col-xs-offset-8 {
  margin-left: 66.66666667%;
}
.col-xs-offset-7 {
  margin-left: 58.33333333%;
}
.col-xs-offset-6 {
  margin-left: 50%;
}
.col-xs-offset-5 {
  margin-left: 41.66666667%;
}
.col-xs-offset-4 {
  margin-left: 33.33333333%;
}
.col-xs-offset-3 {
  margin-left: 25%;
}
.col-xs-offset-2 {
  margin-left: 16.66666667%;
}
.col-xs-offset-1 {
  margin-left: 8.33333333%;
}
.col-xs-offset-0 {
  margin-left: 0%;
}
@media (min-width: 768px) {
  .col-sm-1, .col-sm-2, .col-sm-3, .col-sm-4, .col-sm-5, .col-sm-6, .col-sm-7, .col-sm-8, .col-sm-9, .col-sm-10, .col-sm-11, .col-sm-12 {
    float: left;
  }
  .col-sm-12 {
    width: 100%;
  }
  .col-sm-11 {
    width: 91.66666667%;
  }
  .col-sm-10 {
    width: 83.33333333%;
  }
  .col-sm-9 {
    width: 75%;
  }
  .col-sm-8 {
    width: 66.66666667%;
  }
  .col-sm-7 {
    width: 58.33333333%;
  }
  .col-sm-6 {
    width: 50%;
  }
  .col-sm-5 {
    width: 41.66666667%;
  }
  .col-sm-4 {
    width: 33.33333333%;
  }
  .col-sm-3 {
    width: 25%;
  }
  .col-sm-2 {
    width: 16.66666667%;
  }
  .col-sm-1 {
    width: 8.33333333%;
  }
  .col-sm-pull-12 {
    right: 100%;
  }
  .col-sm-pull-11 {
    right: 91.66666667%;
  }
  .col-sm-pull-10 {
    right: 83.33333333%;
  }
  .col-sm-pull-9 {
    right: 75%;
  }
  .col-sm-pull-8 {
    right: 66.66666667%;
  }
  .col-sm-pull-7 {
    right: 58.33333333%;
  }
  .col-sm-pull-6 {
    right: 50%;
  }
  .col-sm-pull-5 {
    right: 41.66666667%;
  }
  .col-sm-pull-4 {
    right: 33.33333333%;
  }
  .col-sm-pull-3 {
    right: 25%;
  }
  .col-sm-pull-2 {
    right: 16.66666667%;
  }
  .col-sm-pull-1 {
    right: 8.33333333%;
  }
  .col-sm-pull-0 {
    right: auto;
  }
  .col-sm-push-12 {
    left: 100%;
  }
  .col-sm-push-11 {
    left: 91.66666667%;
  }
  .col-sm-push-10 {
    left: 83.33333333%;
  }
  .col-sm-push-9 {
    left: 75%;
  }
  .col-sm-push-8 {
    left: 66.66666667%;
  }
  .col-sm-push-7 {
    left: 58.33333333%;
  }
  .col-sm-push-6 {
    left: 50%;
  }
  .col-sm-push-5 {
    left: 41.66666667%;
  }
  .col-sm-push-4 {
    left: 33.33333333%;
  }
  .col-sm-push-3 {
    left: 25%;
  }
  .col-sm-push-2 {
    left: 16.66666667%;
  }
  .col-sm-push-1 {
    left: 8.33333333%;
  }
  .col-sm-push-0 {
    left: auto;
  }
  .col-sm-offset-12 {
    margin-left: 100%;
  }
  .col-sm-offset-11 {
    margin-left: 91.66666667%;
  }
  .col-sm-offset-10 {
    margin-left: 83.33333333%;
  }
  .col-sm-offset-9 {
    margin-left: 75%;
  }
  .col-sm-offset-8 {
    margin-left: 66.66666667%;
  }
  .col-sm-offset-7 {
    margin-left: 58.33333333%;
  }
  .col-sm-offset-6 {
    margin-left: 50%;
  }
  .col-sm-offset-5 {
    margin-left: 41.66666667%;
  }
  .col-sm-offset-4 {
    margin-left: 33.33333333%;
  }
  .col-sm-offset-3 {
    margin-left: 25%;
  }
  .col-sm-offset-2 {
    margin-left: 16.66666667%;
  }
  .col-sm-offset-1 {
    margin-left: 8.33333333%;
  }
  .col-sm-offset-0 {
    margin-left: 0%;
  }
}
@media (min-width: 992px) {
  .col-md-1, .col-md-2, .col-md-3, .col-md-4, .col-md-5, .col-md-6, .col-md-7, .col-md-8, .col-md-9, .col-md-10, .col-md-11, .col-md-12 {
    float: left;
  }
  .col-md-12 {
    width: 100%;
  }
  .col-md-11 {
    width: 91.66666667%;
  }
  .col-md-10 {
    width: 83.33333333%;
  }
  .col-md-9 {
    width: 75%;
  }
  .col-md-8 {
    width: 66.66666667%;
  }
  .col-md-7 {
    width: 58.33333333%;
  }
  .col-md-6 {
    width: 50%;
  }
  .col-md-5 {
    width: 41.66666667%;
  }
  .col-md-4 {
    width: 33.33333333%;
  }
  .col-md-3 {
    width: 25%;
  }
  .col-md-2 {
    width: 16.66666667%;
  }
  .col-md-1 {
    width: 8.33333333%;
  }
  .col-md-pull-12 {
    right: 100%;
  }
  .col-md-pull-11 {
    right: 91.66666667%;
  }
  .col-md-pull-10 {
    right: 83.33333333%;
  }
  .col-md-pull-9 {
    right: 75%;
  }
  .col-md-pull-8 {
    right: 66.66666667%;
  }
  .col-md-pull-7 {
    right: 58.33333333%;
  }
  .col-md-pull-6 {
    right: 50%;
  }
  .col-md-pull-5 {
    right: 41.66666667%;
  }
  .col-md-pull-4 {
    right: 33.33333333%;
  }
  .col-md-pull-3 {
    right: 25%;
  }
  .col-md-pull-2 {
    right: 16.66666667%;
  }
  .col-md-pull-1 {
    right: 8.33333333%;
  }
  .col-md-pull-0 {
    right: auto;
  }
  .col-md-push-12 {
    left: 100%;
  }
  .col-md-push-11 {
    left: 91.66666667%;
  }
  .col-md-push-10 {
    left: 83.33333333%;
  }
  .col-md-push-9 {
    left: 75%;
  }
  .col-md-push-8 {
    left: 66.66666667%;
  }
  .col-md-push-7 {
    left: 58.33333333%;
  }
  .col-md-push-6 {
    left: 50%;
  }
  .col-md-push-5 {
    left: 41.66666667%;
  }
  .col-md-push-4 {
    left: 33.33333333%;
  }
  .col-md-push-3 {
    left: 25%;
  }
  .col-md-push-2 {
    left: 16.66666667%;
  }
  .col-md-push-1 {
    left: 8.33333333%;
  }
  .col-md-push-0 {
    left: auto;
  }
  .col-md-offset-12 {
    margin-left: 100%;
  }
  .col-md-offset-11 {
    margin-left: 91.66666667%;
  }
  .col-md-offset-10 {
    margin-left: 83.33333333%;
  }
  .col-md-offset-9 {
    margin-left: 75%;
  }
  .col-md-offset-8 {
    margin-left: 66.66666667%;
  }
  .col-md-offset-7 {
    margin-left: 58.33333333%;
  }
  .col-md-offset-6 {
    margin-left: 50%;
  }
  .col-md-offset-5 {
    margin-left: 41.66666667%;
  }
  .col-md-offset-4 {
    margin-left: 33.33333333%;
  }
  .col-md-offset-3 {
    margin-left: 25%;
  }
  .col-md-offset-2 {
    margin-left: 16.66666667%;
  }
  .col-md-offset-1 {
    margin-left: 8.33333333%;
  }
  .col-md-offset-0 {
    margin-left: 0%;
  }
}
@media (min-width: 1200px) {
  .col-lg-1, .col-lg-2, .col-lg-3, .col-lg-4, .col-lg-5, .col-lg-6, .col-lg-7, .col-lg-8, .col-lg-9, .col-lg-10, .col-lg-11, .col-lg-12 {
    float: left;
  }
  .col-lg-12 {
    width: 100%;
  }
  .col-lg-11 {
    width: 91.66666667%;
  }
  .col-lg-10 {
    width: 83.33333333%;
  }
  .col-lg-9 {
    width: 75%;
  }
  .col-lg-8 {
    width: 66.66666667%;
  }
  .col-lg-7 {
    width: 58.33333333%;
  }
  .col-lg-6 {
    width: 50%;
  }
  .col-lg-5 {
    width: 41.66666667%;
  }
  .col-lg-4 {
    width: 33.33333333%;
  }
  .col-lg-3 {
    width: 25%;
  }
  .col-lg-2 {
    width: 16.66666667%;
  }
  .col-lg-1 {
    width: 8.33333333%;
  }
  .col-lg-pull-12 {
    right: 100%;
  }
  .col-lg-pull-11 {
    right: 91.66666667%;
  }
  .col-lg-pull-10 {
    right: 83.33333333%;
  }
  .col-lg-pull-9 {
    right: 75%;
  }
  .col-lg-pull-8 {
    right: 66.66666667%;
  }
  .col-lg-pull-7 {
    right: 58.33333333%;
  }
  .col-lg-pull-6 {
    right: 50%;
  }
  .col-lg-pull-5 {
    right: 41.66666667%;
  }
  .col-lg-pull-4 {
    right: 33.33333333%;
  }
  .col-lg-pull-3 {
    right: 25%;
  }
  .col-lg-pull-2 {
    right: 16.66666667%;
  }
  .col-lg-pull-1 {
    right: 8.33333333%;
  }
  .col-lg-pull-0 {
    right: auto;
  }
  .col-lg-push-12 {
    left: 100%;
  }
  .col-lg-push-11 {
    left: 91.66666667%;
  }
  .col-lg-push-10 {
    left: 83.33333333%;
  }
  .col-lg-push-9 {
    left: 75%;
  }
  .col-lg-push-8 {
    left: 66.66666667%;
  }
  .col-lg-push-7 {
    left: 58.33333333%;
  }
  .col-lg-push-6 {
    left: 50%;
  }
  .col-lg-push-5 {
    left: 41.66666667%;
  }
  .col-lg-push-4 {
    left: 33.33333333%;
  }
  .col-lg-push-3 {
    left: 25%;
  }
  .col-lg-push-2 {
    left: 16.66666667%;
  }
  .col-lg-push-1 {
    left: 8.33333333%;
  }
  .col-lg-push-0 {
    left: auto;
  }
  .col-lg-offset-12 {
    margin-left: 100%;
  }
  .col-lg-offset-11 {
    margin-left: 91.66666667%;
  }
  .col-lg-offset-10 {
    margin-left: 83.33333333%;
  }
  .col-lg-offset-9 {
    margin-left: 75%;
  }
  .col-lg-offset-8 {
    margin-left: 66.66666667%;
  }
  .col-lg-offset-7 {
    margin-left: 58.33333333%;
  }
  .col-lg-offset-6 {
    margin-left: 50%;
  }
  .col-lg-offset-5 {
    margin-left: 41.66666667%;
  }
  .col-lg-offset-4 {
    margin-left: 33.33333333%;
  }
  .col-lg-offset-3 {
    margin-left: 25%;
  }
  .col-lg-offset-2 {
    margin-left: 16.66666667%;
  }
  .col-lg-offset-1 {
    margin-left: 8.33333333%;
  }
  .col-lg-offset-0 {
    margin-left: 0%;
  }
}
table {
  background-color: transparent;
}
caption {
  padding-top: 8px;
  padding-bottom: 8px;
  color: #777777;
  text-align: left;
}
th {
  text-align: left;
}
.table {
  width: 100%;
  max-width: 100%;
  margin-bottom: 18px;
}
.table > thead > tr > th,
.table > tbody > tr > th,
.table > tfoot > tr > th,
.table > thead > tr > td,
.table > tbody > tr > td,
.table > tfoot > tr > td {
  padding: 8px;
  line-height: 1.42857143;
  vertical-align: top;
  border-top: 1px solid #ddd;
}
.table > thead > tr > th {
  vertical-align: bottom;
  border-bottom: 2px solid #ddd;
}
.table > caption + thead > tr:first-child > th,
.table > colgroup + thead > tr:first-child > th,
.table > thead:first-child > tr:first-child > th,
.table > caption + thead > tr:first-child > td,
.table > colgroup + thead > tr:first-child > td,
.table > thead:first-child > tr:first-child > td {
  border-top: 0;
}
.table > tbody + tbody {
  border-top: 2px solid #ddd;
}
.table .table {
  background-color: #fff;
}
.table-condensed > thead > tr > th,
.table-condensed > tbody > tr > th,
.table-condensed > tfoot > tr > th,
.table-condensed > thead > tr > td,
.table-condensed > tbody > tr > td,
.table-condensed > tfoot > tr > td {
  padding: 5px;
}
.table-bordered {
  border: 1px solid #ddd;
}
.table-bordered > thead > tr > th,
.table-bordered > tbody > tr > th,
.table-bordered > tfoot > tr > th,
.table-bordered > thead > tr > td,
.table-bordered > tbody > tr > td,
.table-bordered > tfoot > tr > td {
  border: 1px solid #ddd;
}
.table-bordered > thead > tr > th,
.table-bordered > thead > tr > td {
  border-bottom-width: 2px;
}
.table-striped > tbody > tr:nth-of-type(odd) {
  background-color: #f9f9f9;
}
.table-hover > tbody > tr:hover {
  background-color: #f5f5f5;
}
table col[class*="col-"] {
  position: static;
  float: none;
  display: table-column;
}
table td[class*="col-"],
table th[class*="col-"] {
  position: static;
  float: none;
  display: table-cell;
}
.table > thead > tr > td.active,
.table > tbody > tr > td.active,
.table > tfoot > tr > td.active,
.table > thead > tr > th.active,
.table > tbody > tr > th.active,
.table > tfoot > tr > th.active,
.table > thead > tr.active > td,
.table > tbody > tr.active > td,
.table > tfoot > tr.active > td,
.table > thead > tr.active > th,
.table > tbody > tr.active > th,
.table > tfoot > tr.active > th {
  background-color: #f5f5f5;
}
.table-hover > tbody > tr > td.active:hover,
.table-hover > tbody > tr > th.active:hover,
.table-hover > tbody > tr.active:hover > td,
.table-hover > tbody > tr:hover > .active,
.table-hover > tbody > tr.active:hover > th {
  background-color: #e8e8e8;
}
.table > thead > tr > td.success,
.table > tbody > tr > td.success,
.table > tfoot > tr > td.success,
.table > thead > tr > th.success,
.table > tbody > tr > th.success,
.table > tfoot > tr > th.success,
.table > thead > tr.success > td,
.table > tbody > tr.success > td,
.table > tfoot > tr.success > td,
.table > thead > tr.success > th,
.table > tbody > tr.success > th,
.table > tfoot > tr.success > th {
  background-color: #dff0d8;
}
.table-hover > tbody > tr > td.success:hover,
.table-hover > tbody > tr > th.success:hover,
.table-hover > tbody > tr.success:hover > td,
.table-hover > tbody > tr:hover > .success,
.table-hover > tbody > tr.success:hover > th {
  background-color: #d0e9c6;
}
.table > thead > tr > td.info,
.table > tbody > tr > td.info,
.table > tfoot > tr > td.info,
.table > thead > tr > th.info,
.table > tbody > tr > th.info,
.table > tfoot > tr > th.info,
.table > thead > tr.info > td,
.table > tbody > tr.info > td,
.table > tfoot > tr.info > td,
.table > thead > tr.info > th,
.table > tbody > tr.info > th,
.table > tfoot > tr.info > th {
  background-color: #d9edf7;
}
.table-hover > tbody > tr > td.info:hover,
.table-hover > tbody > tr > th.info:hover,
.table-hover > tbody > tr.info:hover > td,
.table-hover > tbody > tr:hover > .info,
.table-hover > tbody > tr.info:hover > th {
  background-color: #c4e3f3;
}
.table > thead > tr > td.warning,
.table > tbody > tr > td.warning,
.table > tfoot > tr > td.warning,
.table > thead > tr > th.warning,
.table > tbody > tr > th.warning,
.table > tfoot > tr > th.warning,
.table > thead > tr.warning > td,
.table > tbody > tr.warning > td,
.table > tfoot > tr.warning > td,
.table > thead > tr.warning > th,
.table > tbody > tr.warning > th,
.table > tfoot > tr.warning > th {
  background-color: #fcf8e3;
}
.table-hover > tbody > tr > td.warning:hover,
.table-hover > tbody > tr > th.warning:hover,
.table-hover > tbody > tr.warning:hover > td,
.table-hover > tbody > tr:hover > .warning,
.table-hover > tbody > tr.warning:hover > th {
  background-color: #faf2cc;
}
.table > thead > tr > td.danger,
.table > tbody > tr > td.danger,
.table > tfoot > tr > td.danger,
.table > thead > tr > th.danger,
.table > tbody > tr > th.danger,
.table > tfoot > tr > th.danger,
.table > thead > tr.danger > td,
.table > tbody > tr.danger > td,
.table > tfoot > tr.danger > td,
.table > thead > tr.danger > th,
.table > tbody > tr.danger > th,
.table > tfoot > tr.danger > th {
  background-color: #f2dede;
}
.table-hover > tbody > tr > td.danger:hover,
.table-hover > tbody > tr > th.danger:hover,
.table-hover > tbody > tr.danger:hover > td,
.table-hover > tbody > tr:hover > .danger,
.table-hover > tbody > tr.danger:hover > th {
  background-color: #ebcccc;
}
.table-responsive {
  overflow-x: auto;
  min-height: 0.01%;
}
@media screen and (max-width: 767px) {
  .table-responsive {
    width: 100%;
    margin-bottom: 13.5px;
    overflow-y: hidden;
    -ms-overflow-style: -ms-autohiding-scrollbar;
    border: 1px solid #ddd;
  }
  .table-responsive > .table {
    margin-bottom: 0;
  }
  .table-responsive > .table > thead > tr > th,
  .table-responsive > .table > tbody > tr > th,
  .table-responsive > .table > tfoot > tr > th,
  .table-responsive > .table > thead > tr > td,
  .table-responsive > .table > tbody > tr > td,
  .table-responsive > .table > tfoot > tr > td {
    white-space: nowrap;
  }
  .table-responsive > .table-bordered {
    border: 0;
  }
  .table-responsive > .table-bordered > thead > tr > th:first-child,
  .table-responsive > .table-bordered > tbody > tr > th:first-child,
  .table-responsive > .table-bordered > tfoot > tr > th:first-child,
  .table-responsive > .table-bordered > thead > tr > td:first-child,
  .table-responsive > .table-bordered > tbody > tr > td:first-child,
  .table-responsive > .table-bordered > tfoot > tr > td:first-child {
    border-left: 0;
  }
  .table-responsive > .table-bordered > thead > tr > th:last-child,
  .table-responsive > .table-bordered > tbody > tr > th:last-child,
  .table-responsive > .table-bordered > tfoot > tr > th:last-child,
  .table-responsive > .table-bordered > thead > tr > td:last-child,
  .table-responsive > .table-bordered > tbody > tr > td:last-child,
  .table-responsive > .table-bordered > tfoot > tr > td:last-child {
    border-right: 0;
  }
  .table-responsive > .table-bordered > tbody > tr:last-child > th,
  .table-responsive > .table-bordered > tfoot > tr:last-child > th,
  .table-responsive > .table-bordered > tbody > tr:last-child > td,
  .table-responsive > .table-bordered > tfoot > tr:last-child > td {
    border-bottom: 0;
  }
}
fieldset {
  padding: 0;
  margin: 0;
  border: 0;
  min-width: 0;
}
legend {
  display: block;
  width: 100%;
  padding: 0;
  margin-bottom: 18px;
  font-size: 19.5px;
  line-height: inherit;
  color: #333333;
  border: 0;
  border-bottom: 1px solid #e5e5e5;
}
label {
  display: inline-block;
  max-width: 100%;
  margin-bottom: 5px;
  font-weight: bold;
}
input[type="search"] {
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
}
input[type="radio"],
input[type="checkbox"] {
  margin: 4px 0 0;
  margin-top: 1px \9;
  line-height: normal;
}
input[type="file"] {
  display: block;
}
input[type="range"] {
  display: block;
  width: 100%;
}
select[multiple],
select[size] {
  height: auto;
}
input[type="file"]:focus,
input[type="radio"]:focus,
input[type="checkbox"]:focus {
  outline: 5px auto -webkit-focus-ring-color;
  outline-offset: -2px;
}
output {
  display: block;
  padding-top: 7px;
  font-size: 13px;
  line-height: 1.42857143;
  color: #555555;
}
.form-control {
  display: block;
  width: 100%;
  height: 32px;
  padding: 6px 12px;
  font-size: 13px;
  line-height: 1.42857143;
  color: #555555;
  background-color: #fff;
  background-image: none;
  border: 1px solid #ccc;
  border-radius: 2px;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  -webkit-transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
  -o-transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
  transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
}
.form-control:focus {
  border-color: #66afe9;
  outline: 0;
  -webkit-box-shadow: inset 0 1px 1px rgba(0,0,0,.075), 0 0 8px rgba(102, 175, 233, 0.6);
  box-shadow: inset 0 1px 1px rgba(0,0,0,.075), 0 0 8px rgba(102, 175, 233, 0.6);
}
.form-control::-moz-placeholder {
  color: #999;
  opacity: 1;
}
.form-control:-ms-input-placeholder {
  color: #999;
}
.form-control::-webkit-input-placeholder {
  color: #999;
}
.form-control::-ms-expand {
  border: 0;
  background-color: transparent;
}
.form-control[disabled],
.form-control[readonly],
fieldset[disabled] .form-control {
  background-color: #eeeeee;
  opacity: 1;
}
.form-control[disabled],
fieldset[disabled] .form-control {
  cursor: not-allowed;
}
textarea.form-control {
  height: auto;
}
input[type="search"] {
  -webkit-appearance: none;
}
@media screen and (-webkit-min-device-pixel-ratio: 0) {
  input[type="date"].form-control,
  input[type="time"].form-control,
  input[type="datetime-local"].form-control,
  input[type="month"].form-control {
    line-height: 32px;
  }
  input[type="date"].input-sm,
  input[type="time"].input-sm,
  input[type="datetime-local"].input-sm,
  input[type="month"].input-sm,
  .input-group-sm input[type="date"],
  .input-group-sm input[type="time"],
  .input-group-sm input[type="datetime-local"],
  .input-group-sm input[type="month"] {
    line-height: 30px;
  }
  input[type="date"].input-lg,
  input[type="time"].input-lg,
  input[type="datetime-local"].input-lg,
  input[type="month"].input-lg,
  .input-group-lg input[type="date"],
  .input-group-lg input[type="time"],
  .input-group-lg input[type="datetime-local"],
  .input-group-lg input[type="month"] {
    line-height: 45px;
  }
}
.form-group {
  margin-bottom: 15px;
}
.radio,
.checkbox {
  position: relative;
  display: block;
  margin-top: 10px;
  margin-bottom: 10px;
}
.radio label,
.checkbox label {
  min-height: 18px;
  padding-left: 20px;
  margin-bottom: 0;
  font-weight: normal;
  cursor: pointer;
}
.radio input[type="radio"],
.radio-inline input[type="radio"],
.checkbox input[type="checkbox"],
.checkbox-inline input[type="checkbox"] {
  position: absolute;
  margin-left: -20px;
  margin-top: 4px \9;
}
.radio + .radio,
.checkbox + .checkbox {
  margin-top: -5px;
}
.radio-inline,
.checkbox-inline {
  position: relative;
  display: inline-block;
  padding-left: 20px;
  margin-bottom: 0;
  vertical-align: middle;
  font-weight: normal;
  cursor: pointer;
}
.radio-inline + .radio-inline,
.checkbox-inline + .checkbox-inline {
  margin-top: 0;
  margin-left: 10px;
}
input[type="radio"][disabled],
input[type="checkbox"][disabled],
input[type="radio"].disabled,
input[type="checkbox"].disabled,
fieldset[disabled] input[type="radio"],
fieldset[disabled] input[type="checkbox"] {
  cursor: not-allowed;
}
.radio-inline.disabled,
.checkbox-inline.disabled,
fieldset[disabled] .radio-inline,
fieldset[disabled] .checkbox-inline {
  cursor: not-allowed;
}
.radio.disabled label,
.checkbox.disabled label,
fieldset[disabled] .radio label,
fieldset[disabled] .checkbox label {
  cursor: not-allowed;
}
.form-control-static {
  padding-top: 7px;
  padding-bottom: 7px;
  margin-bottom: 0;
  min-height: 31px;
}
.form-control-static.input-lg,
.form-control-static.input-sm {
  padding-left: 0;
  padding-right: 0;
}
.input-sm {
  height: 30px;
  padding: 5px 10px;
  font-size: 12px;
  line-height: 1.5;
  border-radius: 1px;
}
select.input-sm {
  height: 30px;
  line-height: 30px;
}
textarea.input-sm,
select[multiple].input-sm {
  height: auto;
}
.form-group-sm .form-control {
  height: 30px;
  padding: 5px 10px;
  font-size: 12px;
  line-height: 1.5;
  border-radius: 1px;
}
.form-group-sm select.form-control {
  height: 30px;
  line-height: 30px;
}
.form-group-sm textarea.form-control,
.form-group-sm select[multiple].form-control {
  height: auto;
}
.form-group-sm .form-control-static {
  height: 30px;
  min-height: 30px;
  padding: 6px 10px;
  font-size: 12px;
  line-height: 1.5;
}
.input-lg {
  height: 45px;
  padding: 10px 16px;
  font-size: 17px;
  line-height: 1.3333333;
  border-radius: 3px;
}
select.input-lg {
  height: 45px;
  line-height: 45px;
}
textarea.input-lg,
select[multiple].input-lg {
  height: auto;
}
.form-group-lg .form-control {
  height: 45px;
  padding: 10px 16px;
  font-size: 17px;
  line-height: 1.3333333;
  border-radius: 3px;
}
.form-group-lg select.form-control {
  height: 45px;
  line-height: 45px;
}
.form-group-lg textarea.form-control,
.form-group-lg select[multiple].form-control {
  height: auto;
}
.form-group-lg .form-control-static {
  height: 45px;
  min-height: 35px;
  padding: 11px 16px;
  font-size: 17px;
  line-height: 1.3333333;
}
.has-feedback {
  position: relative;
}
.has-feedback .form-control {
  padding-right: 40px;
}
.form-control-feedback {
  position: absolute;
  top: 0;
  right: 0;
  z-index: 2;
  display: block;
  width: 32px;
  height: 32px;
  line-height: 32px;
  text-align: center;
  pointer-events: none;
}
.input-lg + .form-control-feedback,
.input-group-lg + .form-control-feedback,
.form-group-lg .form-control + .form-control-feedback {
  width: 45px;
  height: 45px;
  line-height: 45px;
}
.input-sm + .form-control-feedback,
.input-group-sm + .form-control-feedback,
.form-group-sm .form-control + .form-control-feedback {
  width: 30px;
  height: 30px;
  line-height: 30px;
}
.has-success .help-block,
.has-success .control-label,
.has-success .radio,
.has-success .checkbox,
.has-success .radio-inline,
.has-success .checkbox-inline,
.has-success.radio label,
.has-success.checkbox label,
.has-success.radio-inline label,
.has-success.checkbox-inline label {
  color: #3c763d;
}
.has-success .form-control {
  border-color: #3c763d;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
}
.has-success .form-control:focus {
  border-color: #2b542c;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 6px #67b168;
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 6px #67b168;
}
.has-success .input-group-addon {
  color: #3c763d;
  border-color: #3c763d;
  background-color: #dff0d8;
}
.has-success .form-control-feedback {
  color: #3c763d;
}
.has-warning .help-block,
.has-warning .control-label,
.has-warning .radio,
.has-warning .checkbox,
.has-warning .radio-inline,
.has-warning .checkbox-inline,
.has-warning.radio label,
.has-warning.checkbox label,
.has-warning.radio-inline label,
.has-warning.checkbox-inline label {
  color: #8a6d3b;
}
.has-warning .form-control {
  border-color: #8a6d3b;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
}
.has-warning .form-control:focus {
  border-color: #66512c;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 6px #c0a16b;
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 6px #c0a16b;
}
.has-warning .input-group-addon {
  color: #8a6d3b;
  border-color: #8a6d3b;
  background-color: #fcf8e3;
}
.has-warning .form-control-feedback {
  color: #8a6d3b;
}
.has-error .help-block,
.has-error .control-label,
.has-error .radio,
.has-error .checkbox,
.has-error .radio-inline,
.has-error .checkbox-inline,
.has-error.radio label,
.has-error.checkbox label,
.has-error.radio-inline label,
.has-error.checkbox-inline label {
  color: #a94442;
}
.has-error .form-control {
  border-color: #a94442;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
}
.has-error .form-control:focus {
  border-color: #843534;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 6px #ce8483;
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 6px #ce8483;
}
.has-error .input-group-addon {
  color: #a94442;
  border-color: #a94442;
  background-color: #f2dede;
}
.has-error .form-control-feedback {
  color: #a94442;
}
.has-feedback label ~ .form-control-feedback {
  top: 23px;
}
.has-feedback label.sr-only ~ .form-control-feedback {
  top: 0;
}
.help-block {
  display: block;
  margin-top: 5px;
  margin-bottom: 10px;
  color: #404040;
}
@media (min-width: 768px) {
  .form-inline .form-group {
    display: inline-block;
    margin-bottom: 0;
    vertical-align: middle;
  }
  .form-inline .form-control {
    display: inline-block;
    width: auto;
    vertical-align: middle;
  }
  .form-inline .form-control-static {
    display: inline-block;
  }
  .form-inline .input-group {
    display: inline-table;
    vertical-align: middle;
  }
  .form-inline .input-group .input-group-addon,
  .form-inline .input-group .input-group-btn,
  .form-inline .input-group .form-control {
    width: auto;
  }
  .form-inline .input-group > .form-control {
    width: 100%;
  }
  .form-inline .control-label {
    margin-bottom: 0;
    vertical-align: middle;
  }
  .form-inline .radio,
  .form-inline .checkbox {
    display: inline-block;
    margin-top: 0;
    margin-bottom: 0;
    vertical-align: middle;
  }
  .form-inline .radio label,
  .form-inline .checkbox label {
    padding-left: 0;
  }
  .form-inline .radio input[type="radio"],
  .form-inline .checkbox input[type="checkbox"] {
    position: relative;
    margin-left: 0;
  }
  .form-inline .has-feedback .form-control-feedback {
    top: 0;
  }
}
.form-horizontal .radio,
.form-horizontal .checkbox,
.form-horizontal .radio-inline,
.form-horizontal .checkbox-inline {
  margin-top: 0;
  margin-bottom: 0;
  padding-top: 7px;
}
.form-horizontal .radio,
.form-horizontal .checkbox {
  min-height: 25px;
}
.form-horizontal .form-group {
  margin-left: 0px;
  margin-right: 0px;
}
@media (min-width: 768px) {
  .form-horizontal .control-label {
    text-align: right;
    margin-bottom: 0;
    padding-top: 7px;
  }
}
.form-horizontal .has-feedback .form-control-feedback {
  right: 0px;
}
@media (min-width: 768px) {
  .form-horizontal .form-group-lg .control-label {
    padding-top: 11px;
    font-size: 17px;
  }
}
@media (min-width: 768px) {
  .form-horizontal .form-group-sm .control-label {
    padding-top: 6px;
    font-size: 12px;
  }
}
.btn {
  display: inline-block;
  margin-bottom: 0;
  font-weight: normal;
  text-align: center;
  vertical-align: middle;
  touch-action: manipulation;
  cursor: pointer;
  background-image: none;
  border: 1px solid transparent;
  white-space: nowrap;
  padding: 6px 12px;
  font-size: 13px;
  line-height: 1.42857143;
  border-radius: 2px;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}
.btn:focus,
.btn:active:focus,
.btn.active:focus,
.btn.focus,
.btn:active.focus,
.btn.active.focus {
  outline: 5px auto -webkit-focus-ring-color;
  outline-offset: -2px;
}
.btn:hover,
.btn:focus,
.btn.focus {
  color: #333;
  text-decoration: none;
}
.btn:active,
.btn.active {
  outline: 0;
  background-image: none;
  -webkit-box-shadow: inset 0 3px 5px rgba(0, 0, 0, 0.125);
  box-shadow: inset 0 3px 5px rgba(0, 0, 0, 0.125);
}
.btn.disabled,
.btn[disabled],
fieldset[disabled] .btn {
  cursor: not-allowed;
  opacity: 0.65;
  filter: alpha(opacity=65);
  -webkit-box-shadow: none;
  box-shadow: none;
}
a.btn.disabled,
fieldset[disabled] a.btn {
  pointer-events: none;
}
.btn-default {
  color: #333;
  background-color: #fff;
  border-color: #ccc;
}
.btn-default:focus,
.btn-default.focus {
  color: #333;
  background-color: #e6e6e6;
  border-color: #8c8c8c;
}
.btn-default:hover {
  color: #333;
  background-color: #e6e6e6;
  border-color: #adadad;
}
.btn-default:active,
.btn-default.active,
.open > .dropdown-toggle.btn-default {
  color: #333;
  background-color: #e6e6e6;
  border-color: #adadad;
}
.btn-default:active:hover,
.btn-default.active:hover,
.open > .dropdown-toggle.btn-default:hover,
.btn-default:active:focus,
.btn-default.active:focus,
.open > .dropdown-toggle.btn-default:focus,
.btn-default:active.focus,
.btn-default.active.focus,
.open > .dropdown-toggle.btn-default.focus {
  color: #333;
  background-color: #d4d4d4;
  border-color: #8c8c8c;
}
.btn-default:active,
.btn-default.active,
.open > .dropdown-toggle.btn-default {
  background-image: none;
}
.btn-default.disabled:hover,
.btn-default[disabled]:hover,
fieldset[disabled] .btn-default:hover,
.btn-default.disabled:focus,
.btn-default[disabled]:focus,
fieldset[disabled] .btn-default:focus,
.btn-default.disabled.focus,
.btn-default[disabled].focus,
fieldset[disabled] .btn-default.focus {
  background-color: #fff;
  border-color: #ccc;
}
.btn-default .badge {
  color: #fff;
  background-color: #333;
}
.btn-primary {
  color: #fff;
  background-color: #337ab7;
  border-color: #2e6da4;
}
.btn-primary:focus,
.btn-primary.focus {
  color: #fff;
  background-color: #286090;
  border-color: #122b40;
}
.btn-primary:hover {
  color: #fff;
  background-color: #286090;
  border-color: #204d74;
}
.btn-primary:active,
.btn-primary.active,
.open > .dropdown-toggle.btn-primary {
  color: #fff;
  background-color: #286090;
  border-color: #204d74;
}
.btn-primary:active:hover,
.btn-primary.active:hover,
.open > .dropdown-toggle.btn-primary:hover,
.btn-primary:active:focus,
.btn-primary.active:focus,
.open > .dropdown-toggle.btn-primary:focus,
.btn-primary:active.focus,
.btn-primary.active.focus,
.open > .dropdown-toggle.btn-primary.focus {
  color: #fff;
  background-color: #204d74;
  border-color: #122b40;
}
.btn-primary:active,
.btn-primary.active,
.open > .dropdown-toggle.btn-primary {
  background-image: none;
}
.btn-primary.disabled:hover,
.btn-primary[disabled]:hover,
fieldset[disabled] .btn-primary:hover,
.btn-primary.disabled:focus,
.btn-primary[disabled]:focus,
fieldset[disabled] .btn-primary:focus,
.btn-primary.disabled.focus,
.btn-primary[disabled].focus,
fieldset[disabled] .btn-primary.focus {
  background-color: #337ab7;
  border-color: #2e6da4;
}
.btn-primary .badge {
  color: #337ab7;
  background-color: #fff;
}
.btn-success {
  color: #fff;
  background-color: #5cb85c;
  border-color: #4cae4c;
}
.btn-success:focus,
.btn-success.focus {
  color: #fff;
  background-color: #449d44;
  border-color: #255625;
}
.btn-success:hover {
  color: #fff;
  background-color: #449d44;
  border-color: #398439;
}
.btn-success:active,
.btn-success.active,
.open > .dropdown-toggle.btn-success {
  color: #fff;
  background-color: #449d44;
  border-color: #398439;
}
.btn-success:active:hover,
.btn-success.active:hover,
.open > .dropdown-toggle.btn-success:hover,
.btn-success:active:focus,
.btn-success.active:focus,
.open > .dropdown-toggle.btn-success:focus,
.btn-success:active.focus,
.btn-success.active.focus,
.open > .dropdown-toggle.btn-success.focus {
  color: #fff;
  background-color: #398439;
  border-color: #255625;
}
.btn-success:active,
.btn-success.active,
.open > .dropdown-toggle.btn-success {
  background-image: none;
}
.btn-success.disabled:hover,
.btn-success[disabled]:hover,
fieldset[disabled] .btn-success:hover,
.btn-success.disabled:focus,
.btn-success[disabled]:focus,
fieldset[disabled] .btn-success:focus,
.btn-success.disabled.focus,
.btn-success[disabled].focus,
fieldset[disabled] .btn-success.focus {
  background-color: #5cb85c;
  border-color: #4cae4c;
}
.btn-success .badge {
  color: #5cb85c;
  background-color: #fff;
}
.btn-info {
  color: #fff;
  background-color: #5bc0de;
  border-color: #46b8da;
}
.btn-info:focus,
.btn-info.focus {
  color: #fff;
  background-color: #31b0d5;
  border-color: #1b6d85;
}
.btn-info:hover {
  color: #fff;
  background-color: #31b0d5;
  border-color: #269abc;
}
.btn-info:active,
.btn-info.active,
.open > .dropdown-toggle.btn-info {
  color: #fff;
  background-color: #31b0d5;
  border-color: #269abc;
}
.btn-info:active:hover,
.btn-info.active:hover,
.open > .dropdown-toggle.btn-info:hover,
.btn-info:active:focus,
.btn-info.active:focus,
.open > .dropdown-toggle.btn-info:focus,
.btn-info:active.focus,
.btn-info.active.focus,
.open > .dropdown-toggle.btn-info.focus {
  color: #fff;
  background-color: #269abc;
  border-color: #1b6d85;
}
.btn-info:active,
.btn-info.active,
.open > .dropdown-toggle.btn-info {
  background-image: none;
}
.btn-info.disabled:hover,
.btn-info[disabled]:hover,
fieldset[disabled] .btn-info:hover,
.btn-info.disabled:focus,
.btn-info[disabled]:focus,
fieldset[disabled] .btn-info:focus,
.btn-info.disabled.focus,
.btn-info[disabled].focus,
fieldset[disabled] .btn-info.focus {
  background-color: #5bc0de;
  border-color: #46b8da;
}
.btn-info .badge {
  color: #5bc0de;
  background-color: #fff;
}
.btn-warning {
  color: #fff;
  background-color: #f0ad4e;
  border-color: #eea236;
}
.btn-warning:focus,
.btn-warning.focus {
  color: #fff;
  background-color: #ec971f;
  border-color: #985f0d;
}
.btn-warning:hover {
  color: #fff;
  background-color: #ec971f;
  border-color: #d58512;
}
.btn-warning:active,
.btn-warning.active,
.open > .dropdown-toggle.btn-warning {
  color: #fff;
  background-color: #ec971f;
  border-color: #d58512;
}
.btn-warning:active:hover,
.btn-warning.active:hover,
.open > .dropdown-toggle.btn-warning:hover,
.btn-warning:active:focus,
.btn-warning.active:focus,
.open > .dropdown-toggle.btn-warning:focus,
.btn-warning:active.focus,
.btn-warning.active.focus,
.open > .dropdown-toggle.btn-warning.focus {
  color: #fff;
  background-color: #d58512;
  border-color: #985f0d;
}
.btn-warning:active,
.btn-warning.active,
.open > .dropdown-toggle.btn-warning {
  background-image: none;
}
.btn-warning.disabled:hover,
.btn-warning[disabled]:hover,
fieldset[disabled] .btn-warning:hover,
.btn-warning.disabled:focus,
.btn-warning[disabled]:focus,
fieldset[disabled] .btn-warning:focus,
.btn-warning.disabled.focus,
.btn-warning[disabled].focus,
fieldset[disabled] .btn-warning.focus {
  background-color: #f0ad4e;
  border-color: #eea236;
}
.btn-warning .badge {
  color: #f0ad4e;
  background-color: #fff;
}
.btn-danger {
  color: #fff;
  background-color: #d9534f;
  border-color: #d43f3a;
}
.btn-danger:focus,
.btn-danger.focus {
  color: #fff;
  background-color: #c9302c;
  border-color: #761c19;
}
.btn-danger:hover {
  color: #fff;
  background-color: #c9302c;
  border-color: #ac2925;
}
.btn-danger:active,
.btn-danger.active,
.open > .dropdown-toggle.btn-danger {
  color: #fff;
  background-color: #c9302c;
  border-color: #ac2925;
}
.btn-danger:active:hover,
.btn-danger.active:hover,
.open > .dropdown-toggle.btn-danger:hover,
.btn-danger:active:focus,
.btn-danger.active:focus,
.open > .dropdown-toggle.btn-danger:focus,
.btn-danger:active.focus,
.btn-danger.active.focus,
.open > .dropdown-toggle.btn-danger.focus {
  color: #fff;
  background-color: #ac2925;
  border-color: #761c19;
}
.btn-danger:active,
.btn-danger.active,
.open > .dropdown-toggle.btn-danger {
  background-image: none;
}
.btn-danger.disabled:hover,
.btn-danger[disabled]:hover,
fieldset[disabled] .btn-danger:hover,
.btn-danger.disabled:focus,
.btn-danger[disabled]:focus,
fieldset[disabled] .btn-danger:focus,
.btn-danger.disabled.focus,
.btn-danger[disabled].focus,
fieldset[disabled] .btn-danger.focus {
  background-color: #d9534f;
  border-color: #d43f3a;
}
.btn-danger .badge {
  color: #d9534f;
  background-color: #fff;
}
.btn-link {
  color: #337ab7;
  font-weight: normal;
  border-radius: 0;
}
.btn-link,
.btn-link:active,
.btn-link.active,
.btn-link[disabled],
fieldset[disabled] .btn-link {
  background-color: transparent;
  -webkit-box-shadow: none;
  box-shadow: none;
}
.btn-link,
.btn-link:hover,
.btn-link:focus,
.btn-link:active {
  border-color: transparent;
}
.btn-link:hover,
.btn-link:focus {
  color: #23527c;
  text-decoration: underline;
  background-color: transparent;
}
.btn-link[disabled]:hover,
fieldset[disabled] .btn-link:hover,
.btn-link[disabled]:focus,
fieldset[disabled] .btn-link:focus {
  color: #777777;
  text-decoration: none;
}
.btn-lg,
.btn-group-lg > .btn {
  padding: 10px 16px;
  font-size: 17px;
  line-height: 1.3333333;
  border-radius: 3px;
}
.btn-sm,
.btn-group-sm > .btn {
  padding: 5px 10px;
  font-size: 12px;
  line-height: 1.5;
  border-radius: 1px;
}
.btn-xs,
.btn-group-xs > .btn {
  padding: 1px 5px;
  font-size: 12px;
  line-height: 1.5;
  border-radius: 1px;
}
.btn-block {
  display: block;
  width: 100%;
}
.btn-block + .btn-block {
  margin-top: 5px;
}
input[type="submit"].btn-block,
input[type="reset"].btn-block,
input[type="button"].btn-block {
  width: 100%;
}
.fade {
  opacity: 0;
  -webkit-transition: opacity 0.15s linear;
  -o-transition: opacity 0.15s linear;
  transition: opacity 0.15s linear;
}
.fade.in {
  opacity: 1;
}
.collapse {
  display: none;
}
.collapse.in {
  display: block;
}
tr.collapse.in {
  display: table-row;
}
tbody.collapse.in {
  display: table-row-group;
}
.collapsing {
  position: relative;
  height: 0;
  overflow: hidden;
  -webkit-transition-property: height, visibility;
  transition-property: height, visibility;
  -webkit-transition-duration: 0.35s;
  transition-duration: 0.35s;
  -webkit-transition-timing-function: ease;
  transition-timing-function: ease;
}
.caret {
  display: inline-block;
  width: 0;
  height: 0;
  margin-left: 2px;
  vertical-align: middle;
  border-top: 4px dashed;
  border-top: 4px solid \9;
  border-right: 4px solid transparent;
  border-left: 4px solid transparent;
}
.dropup,
.dropdown {
  position: relative;
}
.dropdown-toggle:focus {
  outline: 0;
}
.dropdown-menu {
  position: absolute;
  top: 100%;
  left: 0;
  z-index: 1000;
  display: none;
  float: left;
  min-width: 160px;
  padding: 5px 0;
  margin: 2px 0 0;
  list-style: none;
  font-size: 13px;
  text-align: left;
  background-color: #fff;
  border: 1px solid #ccc;
  border: 1px solid rgba(0, 0, 0, 0.15);
  border-radius: 2px;
  -webkit-box-shadow: 0 6px 12px rgba(0, 0, 0, 0.175);
  box-shadow: 0 6px 12px rgba(0, 0, 0, 0.175);
  background-clip: padding-box;
}
.dropdown-menu.pull-right {
  right: 0;
  left: auto;
}
.dropdown-menu .divider {
  height: 1px;
  margin: 8px 0;
  overflow: hidden;
  background-color: #e5e5e5;
}
.dropdown-menu > li > a {
  display: block;
  padding: 3px 20px;
  clear: both;
  font-weight: normal;
  line-height: 1.42857143;
  color: #333333;
  white-space: nowrap;
}
.dropdown-menu > li > a:hover,
.dropdown-menu > li > a:focus {
  text-decoration: none;
  color: #262626;
  background-color: #f5f5f5;
}
.dropdown-menu > .active > a,
.dropdown-menu > .active > a:hover,
.dropdown-menu > .active > a:focus {
  color: #fff;
  text-decoration: none;
  outline: 0;
  background-color: #337ab7;
}
.dropdown-menu > .disabled > a,
.dropdown-menu > .disabled > a:hover,
.dropdown-menu > .disabled > a:focus {
  color: #777777;
}
.dropdown-menu > .disabled > a:hover,
.dropdown-menu > .disabled > a:focus {
  text-decoration: none;
  background-color: transparent;
  background-image: none;
  filter: progid:DXImageTransform.Microsoft.gradient(enabled = false);
  cursor: not-allowed;
}
.open > .dropdown-menu {
  display: block;
}
.open > a {
  outline: 0;
}
.dropdown-menu-right {
  left: auto;
  right: 0;
}
.dropdown-menu-left {
  left: 0;
  right: auto;
}
.dropdown-header {
  display: block;
  padding: 3px 20px;
  font-size: 12px;
  line-height: 1.42857143;
  color: #777777;
  white-space: nowrap;
}
.dropdown-backdrop {
  position: fixed;
  left: 0;
  right: 0;
  bottom: 0;
  top: 0;
  z-index: 990;
}
.pull-right > .dropdown-menu {
  right: 0;
  left: auto;
}
.dropup .caret,
.navbar-fixed-bottom .dropdown .caret {
  border-top: 0;
  border-bottom: 4px dashed;
  border-bottom: 4px solid \9;
  content: "";
}
.dropup .dropdown-menu,
.navbar-fixed-bottom .dropdown .dropdown-menu {
  top: auto;
  bottom: 100%;
  margin-bottom: 2px;
}
@media (min-width: 541px) {
  .navbar-right .dropdown-menu {
    left: auto;
    right: 0;
  }
  .navbar-right .dropdown-menu-left {
    left: 0;
    right: auto;
  }
}
.btn-group,
.btn-group-vertical {
  position: relative;
  display: inline-block;
  vertical-align: middle;
}
.btn-group > .btn,
.btn-group-vertical > .btn {
  position: relative;
  float: left;
}
.btn-group > .btn:hover,
.btn-group-vertical > .btn:hover,
.btn-group > .btn:focus,
.btn-group-vertical > .btn:focus,
.btn-group > .btn:active,
.btn-group-vertical > .btn:active,
.btn-group > .btn.active,
.btn-group-vertical > .btn.active {
  z-index: 2;
}
.btn-group .btn + .btn,
.btn-group .btn + .btn-group,
.btn-group .btn-group + .btn,
.btn-group .btn-group + .btn-group {
  margin-left: -1px;
}
.btn-toolbar {
  margin-left: -5px;
}
.btn-toolbar .btn,
.btn-toolbar .btn-group,
.btn-toolbar .input-group {
  float: left;
}
.btn-toolbar > .btn,
.btn-toolbar > .btn-group,
.btn-toolbar > .input-group {
  margin-left: 5px;
}
.btn-group > .btn:not(:first-child):not(:last-child):not(.dropdown-toggle) {
  border-radius: 0;
}
.btn-group > .btn:first-child {
  margin-left: 0;
}
.btn-group > .btn:first-child:not(:last-child):not(.dropdown-toggle) {
  border-bottom-right-radius: 0;
  border-top-right-radius: 0;
}
.btn-group > .btn:last-child:not(:first-child),
.btn-group > .dropdown-toggle:not(:first-child) {
  border-bottom-left-radius: 0;
  border-top-left-radius: 0;
}
.btn-group > .btn-group {
  float: left;
}
.btn-group > .btn-group:not(:first-child):not(:last-child) > .btn {
  border-radius: 0;
}
.btn-group > .btn-group:first-child:not(:last-child) > .btn:last-child,
.btn-group > .btn-group:first-child:not(:last-child) > .dropdown-toggle {
  border-bottom-right-radius: 0;
  border-top-right-radius: 0;
}
.btn-group > .btn-group:last-child:not(:first-child) > .btn:first-child {
  border-bottom-left-radius: 0;
  border-top-left-radius: 0;
}
.btn-group .dropdown-toggle:active,
.btn-group.open .dropdown-toggle {
  outline: 0;
}
.btn-group > .btn + .dropdown-toggle {
  padding-left: 8px;
  padding-right: 8px;
}
.btn-group > .btn-lg + .dropdown-toggle {
  padding-left: 12px;
  padding-right: 12px;
}
.btn-group.open .dropdown-toggle {
  -webkit-box-shadow: inset 0 3px 5px rgba(0, 0, 0, 0.125);
  box-shadow: inset 0 3px 5px rgba(0, 0, 0, 0.125);
}
.btn-group.open .dropdown-toggle.btn-link {
  -webkit-box-shadow: none;
  box-shadow: none;
}
.btn .caret {
  margin-left: 0;
}
.btn-lg .caret {
  border-width: 5px 5px 0;
  border-bottom-width: 0;
}
.dropup .btn-lg .caret {
  border-width: 0 5px 5px;
}
.btn-group-vertical > .btn,
.btn-group-vertical > .btn-group,
.btn-group-vertical > .btn-group > .btn {
  display: block;
  float: none;
  width: 100%;
  max-width: 100%;
}
.btn-group-vertical > .btn-group > .btn {
  float: none;
}
.btn-group-vertical > .btn + .btn,
.btn-group-vertical > .btn + .btn-group,
.btn-group-vertical > .btn-group + .btn,
.btn-group-vertical > .btn-group + .btn-group {
  margin-top: -1px;
  margin-left: 0;
}
.btn-group-vertical > .btn:not(:first-child):not(:last-child) {
  border-radius: 0;
}
.btn-group-vertical > .btn:first-child:not(:last-child) {
  border-top-right-radius: 2px;
  border-top-left-radius: 2px;
  border-bottom-right-radius: 0;
  border-bottom-left-radius: 0;
}
.btn-group-vertical > .btn:last-child:not(:first-child) {
  border-top-right-radius: 0;
  border-top-left-radius: 0;
  border-bottom-right-radius: 2px;
  border-bottom-left-radius: 2px;
}
.btn-group-vertical > .btn-group:not(:first-child):not(:last-child) > .btn {
  border-radius: 0;
}
.btn-group-vertical > .btn-group:first-child:not(:last-child) > .btn:last-child,
.btn-group-vertical > .btn-group:first-child:not(:last-child) > .dropdown-toggle {
  border-bottom-right-radius: 0;
  border-bottom-left-radius: 0;
}
.btn-group-vertical > .btn-group:last-child:not(:first-child) > .btn:first-child {
  border-top-right-radius: 0;
  border-top-left-radius: 0;
}
.btn-group-justified {
  display: table;
  width: 100%;
  table-layout: fixed;
  border-collapse: separate;
}
.btn-group-justified > .btn,
.btn-group-justified > .btn-group {
  float: none;
  display: table-cell;
  width: 1%;
}
.btn-group-justified > .btn-group .btn {
  width: 100%;
}
.btn-group-justified > .btn-group .dropdown-menu {
  left: auto;
}
[data-toggle="buttons"] > .btn input[type="radio"],
[data-toggle="buttons"] > .btn-group > .btn input[type="radio"],
[data-toggle="buttons"] > .btn input[type="checkbox"],
[data-toggle="buttons"] > .btn-group > .btn input[type="checkbox"] {
  position: absolute;
  clip: rect(0, 0, 0, 0);
  pointer-events: none;
}
.input-group {
  position: relative;
  display: table;
  border-collapse: separate;
}
.input-group[class*="col-"] {
  float: none;
  padding-left: 0;
  padding-right: 0;
}
.input-group .form-control {
  position: relative;
  z-index: 2;
  float: left;
  width: 100%;
  margin-bottom: 0;
}
.input-group .form-control:focus {
  z-index: 3;
}
.input-group-lg > .form-control,
.input-group-lg > .input-group-addon,
.input-group-lg > .input-group-btn > .btn {
  height: 45px;
  padding: 10px 16px;
  font-size: 17px;
  line-height: 1.3333333;
  border-radius: 3px;
}
select.input-group-lg > .form-control,
select.input-group-lg > .input-group-addon,
select.input-group-lg > .input-group-btn > .btn {
  height: 45px;
  line-height: 45px;
}
textarea.input-group-lg > .form-control,
textarea.input-group-lg > .input-group-addon,
textarea.input-group-lg > .input-group-btn > .btn,
select[multiple].input-group-lg > .form-control,
select[multiple].input-group-lg > .input-group-addon,
select[multiple].input-group-lg > .input-group-btn > .btn {
  height: auto;
}
.input-group-sm > .form-control,
.input-group-sm > .input-group-addon,
.input-group-sm > .input-group-btn > .btn {
  height: 30px;
  padding: 5px 10px;
  font-size: 12px;
  line-height: 1.5;
  border-radius: 1px;
}
select.input-group-sm > .form-control,
select.input-group-sm > .input-group-addon,
select.input-group-sm > .input-group-btn > .btn {
  height: 30px;
  line-height: 30px;
}
textarea.input-group-sm > .form-control,
textarea.input-group-sm > .input-group-addon,
textarea.input-group-sm > .input-group-btn > .btn,
select[multiple].input-group-sm > .form-control,
select[multiple].input-group-sm > .input-group-addon,
select[multiple].input-group-sm > .input-group-btn > .btn {
  height: auto;
}
.input-group-addon,
.input-group-btn,
.input-group .form-control {
  display: table-cell;
}
.input-group-addon:not(:first-child):not(:last-child),
.input-group-btn:not(:first-child):not(:last-child),
.input-group .form-control:not(:first-child):not(:last-child) {
  border-radius: 0;
}
.input-group-addon,
.input-group-btn {
  width: 1%;
  white-space: nowrap;
  vertical-align: middle;
}
.input-group-addon {
  padding: 6px 12px;
  font-size: 13px;
  font-weight: normal;
  line-height: 1;
  color: #555555;
  text-align: center;
  background-color: #eeeeee;
  border: 1px solid #ccc;
  border-radius: 2px;
}
.input-group-addon.input-sm {
  padding: 5px 10px;
  font-size: 12px;
  border-radius: 1px;
}
.input-group-addon.input-lg {
  padding: 10px 16px;
  font-size: 17px;
  border-radius: 3px;
}
.input-group-addon input[type="radio"],
.input-group-addon input[type="checkbox"] {
  margin-top: 0;
}
.input-group .form-control:first-child,
.input-group-addon:first-child,
.input-group-btn:first-child > .btn,
.input-group-btn:first-child > .btn-group > .btn,
.input-group-btn:first-child > .dropdown-toggle,
.input-group-btn:last-child > .btn:not(:last-child):not(.dropdown-toggle),
.input-group-btn:last-child > .btn-group:not(:last-child) > .btn {
  border-bottom-right-radius: 0;
  border-top-right-radius: 0;
}
.input-group-addon:first-child {
  border-right: 0;
}
.input-group .form-control:last-child,
.input-group-addon:last-child,
.input-group-btn:last-child > .btn,
.input-group-btn:last-child > .btn-group > .btn,
.input-group-btn:last-child > .dropdown-toggle,
.input-group-btn:first-child > .btn:not(:first-child),
.input-group-btn:first-child > .btn-group:not(:first-child) > .btn {
  border-bottom-left-radius: 0;
  border-top-left-radius: 0;
}
.input-group-addon:last-child {
  border-left: 0;
}
.input-group-btn {
  position: relative;
  font-size: 0;
  white-space: nowrap;
}
.input-group-btn > .btn {
  position: relative;
}
.input-group-btn > .btn + .btn {
  margin-left: -1px;
}
.input-group-btn > .btn:hover,
.input-group-btn > .btn:focus,
.input-group-btn > .btn:active {
  z-index: 2;
}
.input-group-btn:first-child > .btn,
.input-group-btn:first-child > .btn-group {
  margin-right: -1px;
}
.input-group-btn:last-child > .btn,
.input-group-btn:last-child > .btn-group {
  z-index: 2;
  margin-left: -1px;
}
.nav {
  margin-bottom: 0;
  padding-left: 0;
  list-style: none;
}
.nav > li {
  position: relative;
  display: block;
}
.nav > li > a {
  position: relative;
  display: block;
  padding: 10px 15px;
}
.nav > li > a:hover,
.nav > li > a:focus {
  text-decoration: none;
  background-color: #eeeeee;
}
.nav > li.disabled > a {
  color: #777777;
}
.nav > li.disabled > a:hover,
.nav > li.disabled > a:focus {
  color: #777777;
  text-decoration: none;
  background-color: transparent;
  cursor: not-allowed;
}
.nav .open > a,
.nav .open > a:hover,
.nav .open > a:focus {
  background-color: #eeeeee;
  border-color: #337ab7;
}
.nav .nav-divider {
  height: 1px;
  margin: 8px 0;
  overflow: hidden;
  background-color: #e5e5e5;
}
.nav > li > a > img {
  max-width: none;
}
.nav-tabs {
  border-bottom: 1px solid #ddd;
}
.nav-tabs > li {
  float: left;
  margin-bottom: -1px;
}
.nav-tabs > li > a {
  margin-right: 2px;
  line-height: 1.42857143;
  border: 1px solid transparent;
  border-radius: 2px 2px 0 0;
}
.nav-tabs > li > a:hover {
  border-color: #eeeeee #eeeeee #ddd;
}
.nav-tabs > li.active > a,
.nav-tabs > li.active > a:hover,
.nav-tabs > li.active > a:focus {
  color: #555555;
  background-color: #fff;
  border: 1px solid #ddd;
  border-bottom-color: transparent;
  cursor: default;
}
.nav-tabs.nav-justified {
  width: 100%;
  border-bottom: 0;
}
.nav-tabs.nav-justified > li {
  float: none;
}
.nav-tabs.nav-justified > li > a {
  text-align: center;
  margin-bottom: 5px;
}
.nav-tabs.nav-justified > .dropdown .dropdown-menu {
  top: auto;
  left: auto;
}
@media (min-width: 768px) {
  .nav-tabs.nav-justified > li {
    display: table-cell;
    width: 1%;
  }
  .nav-tabs.nav-justified > li > a {
    margin-bottom: 0;
  }
}
.nav-tabs.nav-justified > li > a {
  margin-right: 0;
  border-radius: 2px;
}
.nav-tabs.nav-justified > .active > a,
.nav-tabs.nav-justified > .active > a:hover,
.nav-tabs.nav-justified > .active > a:focus {
  border: 1px solid #ddd;
}
@media (min-width: 768px) {
  .nav-tabs.nav-justified > li > a {
    border-bottom: 1px solid #ddd;
    border-radius: 2px 2px 0 0;
  }
  .nav-tabs.nav-justified > .active > a,
  .nav-tabs.nav-justified > .active > a:hover,
  .nav-tabs.nav-justified > .active > a:focus {
    border-bottom-color: #fff;
  }
}
.nav-pills > li {
  float: left;
}
.nav-pills > li > a {
  border-radius: 2px;
}
.nav-pills > li + li {
  margin-left: 2px;
}
.nav-pills > li.active > a,
.nav-pills > li.active > a:hover,
.nav-pills > li.active > a:focus {
  color: #fff;
  background-color: #337ab7;
}
.nav-stacked > li {
  float: none;
}
.nav-stacked > li + li {
  margin-top: 2px;
  margin-left: 0;
}
.nav-justified {
  width: 100%;
}
.nav-justified > li {
  float: none;
}
.nav-justified > li > a {
  text-align: center;
  margin-bottom: 5px;
}
.nav-justified > .dropdown .dropdown-menu {
  top: auto;
  left: auto;
}
@media (min-width: 768px) {
  .nav-justified > li {
    display: table-cell;
    width: 1%;
  }
  .nav-justified > li > a {
    margin-bottom: 0;
  }
}
.nav-tabs-justified {
  border-bottom: 0;
}
.nav-tabs-justified > li > a {
  margin-right: 0;
  border-radius: 2px;
}
.nav-tabs-justified > .active > a,
.nav-tabs-justified > .active > a:hover,
.nav-tabs-justified > .active > a:focus {
  border: 1px solid #ddd;
}
@media (min-width: 768px) {
  .nav-tabs-justified > li > a {
    border-bottom: 1px solid #ddd;
    border-radius: 2px 2px 0 0;
  }
  .nav-tabs-justified > .active > a,
  .nav-tabs-justified > .active > a:hover,
  .nav-tabs-justified > .active > a:focus {
    border-bottom-color: #fff;
  }
}
.tab-content > .tab-pane {
  display: none;
}
.tab-content > .active {
  display: block;
}
.nav-tabs .dropdown-menu {
  margin-top: -1px;
  border-top-right-radius: 0;
  border-top-left-radius: 0;
}
.navbar {
  position: relative;
  min-height: 30px;
  margin-bottom: 18px;
  border: 1px solid transparent;
}
@media (min-width: 541px) {
  .navbar {
    border-radius: 2px;
  }
}
@media (min-width: 541px) {
  .navbar-header {
    float: left;
  }
}
.navbar-collapse {
  overflow-x: visible;
  padding-right: 0px;
  padding-left: 0px;
  border-top: 1px solid transparent;
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.1);
  -webkit-overflow-scrolling: touch;
}
.navbar-collapse.in {
  overflow-y: auto;
}
@media (min-width: 541px) {
  .navbar-collapse {
    width: auto;
    border-top: 0;
    box-shadow: none;
  }
  .navbar-collapse.collapse {
    display: block !important;
    height: auto !important;
    padding-bottom: 0;
    overflow: visible !important;
  }
  .navbar-collapse.in {
    overflow-y: visible;
  }
  .navbar-fixed-top .navbar-collapse,
  .navbar-static-top .navbar-collapse,
  .navbar-fixed-bottom .navbar-collapse {
    padding-left: 0;
    padding-right: 0;
  }
}
.navbar-fixed-top .navbar-collapse,
.navbar-fixed-bottom .navbar-collapse {
  max-height: 340px;
}
@media (max-device-width: 540px) and (orientation: landscape) {
  .navbar-fixed-top .navbar-collapse,
  .navbar-fixed-bottom .navbar-collapse {
    max-height: 200px;
  }
}
.container > .navbar-header,
.container-fluid > .navbar-header,
.container > .navbar-collapse,
.container-fluid > .navbar-collapse {
  margin-right: 0px;
  margin-left: 0px;
}
@media (min-width: 541px) {
  .container > .navbar-header,
  .container-fluid > .navbar-header,
  .container > .navbar-collapse,
  .container-fluid > .navbar-collapse {
    margin-right: 0;
    margin-left: 0;
  }
}
.navbar-static-top {
  z-index: 1000;
  border-width: 0 0 1px;
}
@media (min-width: 541px) {
  .navbar-static-top {
    border-radius: 0;
  }
}
.navbar-fixed-top,
.navbar-fixed-bottom {
  position: fixed;
  right: 0;
  left: 0;
  z-index: 1030;
}
@media (min-width: 541px) {
  .navbar-fixed-top,
  .navbar-fixed-bottom {
    border-radius: 0;
  }
}
.navbar-fixed-top {
  top: 0;
  border-width: 0 0 1px;
}
.navbar-fixed-bottom {
  bottom: 0;
  margin-bottom: 0;
  border-width: 1px 0 0;
}
.navbar-brand {
  float: left;
  padding: 6px 0px;
  font-size: 17px;
  line-height: 18px;
  height: 30px;
}
.navbar-brand:hover,
.navbar-brand:focus {
  text-decoration: none;
}
.navbar-brand > img {
  display: block;
}
@media (min-width: 541px) {
  .navbar > .container .navbar-brand,
  .navbar > .container-fluid .navbar-brand {
    margin-left: 0px;
  }
}
.navbar-toggle {
  position: relative;
  float: right;
  margin-right: 0px;
  padding: 9px 10px;
  margin-top: -2px;
  margin-bottom: -2px;
  background-color: transparent;
  background-image: none;
  border: 1px solid transparent;
  border-radius: 2px;
}
.navbar-toggle:focus {
  outline: 0;
}
.navbar-toggle .icon-bar {
  display: block;
  width: 22px;
  height: 2px;
  border-radius: 1px;
}
.navbar-toggle .icon-bar + .icon-bar {
  margin-top: 4px;
}
@media (min-width: 541px) {
  .navbar-toggle {
    display: none;
  }
}
.navbar-nav {
  margin: 3px 0px;
}
.navbar-nav > li > a {
  padding-top: 10px;
  padding-bottom: 10px;
  line-height: 18px;
}
@media (max-width: 540px) {
  .navbar-nav .open .dropdown-menu {
    position: static;
    float: none;
    width: auto;
    margin-top: 0;
    background-color: transparent;
    border: 0;
    box-shadow: none;
  }
  .navbar-nav .open .dropdown-menu > li > a,
  .navbar-nav .open .dropdown-menu .dropdown-header {
    padding: 5px 15px 5px 25px;
  }
  .navbar-nav .open .dropdown-menu > li > a {
    line-height: 18px;
  }
  .navbar-nav .open .dropdown-menu > li > a:hover,
  .navbar-nav .open .dropdown-menu > li > a:focus {
    background-image: none;
  }
}
@media (min-width: 541px) {
  .navbar-nav {
    float: left;
    margin: 0;
  }
  .navbar-nav > li {
    float: left;
  }
  .navbar-nav > li > a {
    padding-top: 6px;
    padding-bottom: 6px;
  }
}
.navbar-form {
  margin-left: 0px;
  margin-right: 0px;
  padding: 10px 0px;
  border-top: 1px solid transparent;
  border-bottom: 1px solid transparent;
  -webkit-box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.1), 0 1px 0 rgba(255, 255, 255, 0.1);
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.1), 0 1px 0 rgba(255, 255, 255, 0.1);
  margin-top: -1px;
  margin-bottom: -1px;
}
@media (min-width: 768px) {
  .navbar-form .form-group {
    display: inline-block;
    margin-bottom: 0;
    vertical-align: middle;
  }
  .navbar-form .form-control {
    display: inline-block;
    width: auto;
    vertical-align: middle;
  }
  .navbar-form .form-control-static {
    display: inline-block;
  }
  .navbar-form .input-group {
    display: inline-table;
    vertical-align: middle;
  }
  .navbar-form .input-group .input-group-addon,
  .navbar-form .input-group .input-group-btn,
  .navbar-form .input-group .form-control {
    width: auto;
  }
  .navbar-form .input-group > .form-control {
    width: 100%;
  }
  .navbar-form .control-label {
    margin-bottom: 0;
    vertical-align: middle;
  }
  .navbar-form .radio,
  .navbar-form .checkbox {
    display: inline-block;
    margin-top: 0;
    margin-bottom: 0;
    vertical-align: middle;
  }
  .navbar-form .radio label,
  .navbar-form .checkbox label {
    padding-left: 0;
  }
  .navbar-form .radio input[type="radio"],
  .navbar-form .checkbox input[type="checkbox"] {
    position: relative;
    margin-left: 0;
  }
  .navbar-form .has-feedback .form-control-feedback {
    top: 0;
  }
}
@media (max-width: 540px) {
  .navbar-form .form-group {
    margin-bottom: 5px;
  }
  .navbar-form .form-group:last-child {
    margin-bottom: 0;
  }
}
@media (min-width: 541px) {
  .navbar-form {
    width: auto;
    border: 0;
    margin-left: 0;
    margin-right: 0;
    padding-top: 0;
    padding-bottom: 0;
    -webkit-box-shadow: none;
    box-shadow: none;
  }
}
.navbar-nav > li > .dropdown-menu {
  margin-top: 0;
  border-top-right-radius: 0;
  border-top-left-radius: 0;
}
.navbar-fixed-bottom .navbar-nav > li > .dropdown-menu {
  margin-bottom: 0;
  border-top-right-radius: 2px;
  border-top-left-radius: 2px;
  border-bottom-right-radius: 0;
  border-bottom-left-radius: 0;
}
.navbar-btn {
  margin-top: -1px;
  margin-bottom: -1px;
}
.navbar-btn.btn-sm {
  margin-top: 0px;
  margin-bottom: 0px;
}
.navbar-btn.btn-xs {
  margin-top: 4px;
  margin-bottom: 4px;
}
.navbar-text {
  margin-top: 6px;
  margin-bottom: 6px;
}
@media (min-width: 541px) {
  .navbar-text {
    float: left;
    margin-left: 0px;
    margin-right: 0px;
  }
}
@media (min-width: 541px) {
  .navbar-left {
    float: left !important;
    float: left;
  }
  .navbar-right {
    float: right !important;
    float: right;
    margin-right: 0px;
  }
  .navbar-right ~ .navbar-right {
    margin-right: 0;
  }
}
.navbar-default {
  background-color: #f8f8f8;
  border-color: #e7e7e7;
}
.navbar-default .navbar-brand {
  color: #777;
}
.navbar-default .navbar-brand:hover,
.navbar-default .navbar-brand:focus {
  color: #5e5e5e;
  background-color: transparent;
}
.navbar-default .navbar-text {
  color: #777;
}
.navbar-default .navbar-nav > li > a {
  color: #777;
}
.navbar-default .navbar-nav > li > a:hover,
.navbar-default .navbar-nav > li > a:focus {
  color: #333;
  background-color: transparent;
}
.navbar-default .navbar-nav > .active > a,
.navbar-default .navbar-nav > .active > a:hover,
.navbar-default .navbar-nav > .active > a:focus {
  color: #555;
  background-color: #e7e7e7;
}
.navbar-default .navbar-nav > .disabled > a,
.navbar-default .navbar-nav > .disabled > a:hover,
.navbar-default .navbar-nav > .disabled > a:focus {
  color: #ccc;
  background-color: transparent;
}
.navbar-default .navbar-toggle {
  border-color: #ddd;
}
.navbar-default .navbar-toggle:hover,
.navbar-default .navbar-toggle:focus {
  background-color: #ddd;
}
.navbar-default .navbar-toggle .icon-bar {
  background-color: #888;
}
.navbar-default .navbar-collapse,
.navbar-default .navbar-form {
  border-color: #e7e7e7;
}
.navbar-default .navbar-nav > .open > a,
.navbar-default .navbar-nav > .open > a:hover,
.navbar-default .navbar-nav > .open > a:focus {
  background-color: #e7e7e7;
  color: #555;
}
@media (max-width: 540px) {
  .navbar-default .navbar-nav .open .dropdown-menu > li > a {
    color: #777;
  }
  .navbar-default .navbar-nav .open .dropdown-menu > li > a:hover,
  .navbar-default .navbar-nav .open .dropdown-menu > li > a:focus {
    color: #333;
    background-color: transparent;
  }
  .navbar-default .navbar-nav .open .dropdown-menu > .active > a,
  .navbar-default .navbar-nav .open .dropdown-menu > .active > a:hover,
  .navbar-default .navbar-nav .open .dropdown-menu > .active > a:focus {
    color: #555;
    background-color: #e7e7e7;
  }
  .navbar-default .navbar-nav .open .dropdown-menu > .disabled > a,
  .navbar-default .navbar-nav .open .dropdown-menu > .disabled > a:hover,
  .navbar-default .navbar-nav .open .dropdown-menu > .disabled > a:focus {
    color: #ccc;
    background-color: transparent;
  }
}
.navbar-default .navbar-link {
  color: #777;
}
.navbar-default .navbar-link:hover {
  color: #333;
}
.navbar-default .btn-link {
  color: #777;
}
.navbar-default .btn-link:hover,
.navbar-default .btn-link:focus {
  color: #333;
}
.navbar-default .btn-link[disabled]:hover,
fieldset[disabled] .navbar-default .btn-link:hover,
.navbar-default .btn-link[disabled]:focus,
fieldset[disabled] .navbar-default .btn-link:focus {
  color: #ccc;
}
.navbar-inverse {
  background-color: #222;
  border-color: #080808;
}
.navbar-inverse .navbar-brand {
  color: #9d9d9d;
}
.navbar-inverse .navbar-brand:hover,
.navbar-inverse .navbar-brand:focus {
  color: #fff;
  background-color: transparent;
}
.navbar-inverse .navbar-text {
  color: #9d9d9d;
}
.navbar-inverse .navbar-nav > li > a {
  color: #9d9d9d;
}
.navbar-inverse .navbar-nav > li > a:hover,
.navbar-inverse .navbar-nav > li > a:focus {
  color: #fff;
  background-color: transparent;
}
.navbar-inverse .navbar-nav > .active > a,
.navbar-inverse .navbar-nav > .active > a:hover,
.navbar-inverse .navbar-nav > .active > a:focus {
  color: #fff;
  background-color: #080808;
}
.navbar-inverse .navbar-nav > .disabled > a,
.navbar-inverse .navbar-nav > .disabled > a:hover,
.navbar-inverse .navbar-nav > .disabled > a:focus {
  color: #444;
  background-color: transparent;
}
.navbar-inverse .navbar-toggle {
  border-color: #333;
}
.navbar-inverse .navbar-toggle:hover,
.navbar-inverse .navbar-toggle:focus {
  background-color: #333;
}
.navbar-inverse .navbar-toggle .icon-bar {
  background-color: #fff;
}
.navbar-inverse .navbar-collapse,
.navbar-inverse .navbar-form {
  border-color: #101010;
}
.navbar-inverse .navbar-nav > .open > a,
.navbar-inverse .navbar-nav > .open > a:hover,
.navbar-inverse .navbar-nav > .open > a:focus {
  background-color: #080808;
  color: #fff;
}
@media (max-width: 540px) {
  .navbar-inverse .navbar-nav .open .dropdown-menu > .dropdown-header {
    border-color: #080808;
  }
  .navbar-inverse .navbar-nav .open .dropdown-menu .divider {
    background-color: #080808;
  }
  .navbar-inverse .navbar-nav .open .dropdown-menu > li > a {
    color: #9d9d9d;
  }
  .navbar-inverse .navbar-nav .open .dropdown-menu > li > a:hover,
  .navbar-inverse .navbar-nav .open .dropdown-menu > li > a:focus {
    color: #fff;
    background-color: transparent;
  }
  .navbar-inverse .navbar-nav .open .dropdown-menu > .active > a,
  .navbar-inverse .navbar-nav .open .dropdown-menu > .active > a:hover,
  .navbar-inverse .navbar-nav .open .dropdown-menu > .active > a:focus {
    color: #fff;
    background-color: #080808;
  }
  .navbar-inverse .navbar-nav .open .dropdown-menu > .disabled > a,
  .navbar-inverse .navbar-nav .open .dropdown-menu > .disabled > a:hover,
  .navbar-inverse .navbar-nav .open .dropdown-menu > .disabled > a:focus {
    color: #444;
    background-color: transparent;
  }
}
.navbar-inverse .navbar-link {
  color: #9d9d9d;
}
.navbar-inverse .navbar-link:hover {
  color: #fff;
}
.navbar-inverse .btn-link {
  color: #9d9d9d;
}
.navbar-inverse .btn-link:hover,
.navbar-inverse .btn-link:focus {
  color: #fff;
}
.navbar-inverse .btn-link[disabled]:hover,
fieldset[disabled] .navbar-inverse .btn-link:hover,
.navbar-inverse .btn-link[disabled]:focus,
fieldset[disabled] .navbar-inverse .btn-link:focus {
  color: #444;
}
.breadcrumb {
  padding: 8px 15px;
  margin-bottom: 18px;
  list-style: none;
  background-color: #f5f5f5;
  border-radius: 2px;
}
.breadcrumb > li {
  display: inline-block;
}
.breadcrumb > li + li:before {
  content: "/\00a0";
  padding: 0 5px;
  color: #5e5e5e;
}
.breadcrumb > .active {
  color: #777777;
}
.pagination {
  display: inline-block;
  padding-left: 0;
  margin: 18px 0;
  border-radius: 2px;
}
.pagination > li {
  display: inline;
}
.pagination > li > a,
.pagination > li > span {
  position: relative;
  float: left;
  padding: 6px 12px;
  line-height: 1.42857143;
  text-decoration: none;
  color: #337ab7;
  background-color: #fff;
  border: 1px solid #ddd;
  margin-left: -1px;
}
.pagination > li:first-child > a,
.pagination > li:first-child > span {
  margin-left: 0;
  border-bottom-left-radius: 2px;
  border-top-left-radius: 2px;
}
.pagination > li:last-child > a,
.pagination > li:last-child > span {
  border-bottom-right-radius: 2px;
  border-top-right-radius: 2px;
}
.pagination > li > a:hover,
.pagination > li > span:hover,
.pagination > li > a:focus,
.pagination > li > span:focus {
  z-index: 2;
  color: #23527c;
  background-color: #eeeeee;
  border-color: #ddd;
}
.pagination > .active > a,
.pagination > .active > span,
.pagination > .active > a:hover,
.pagination > .active > span:hover,
.pagination > .active > a:focus,
.pagination > .active > span:focus {
  z-index: 3;
  color: #fff;
  background-color: #337ab7;
  border-color: #337ab7;
  cursor: default;
}
.pagination > .disabled > span,
.pagination > .disabled > span:hover,
.pagination > .disabled > span:focus,
.pagination > .disabled > a,
.pagination > .disabled > a:hover,
.pagination > .disabled > a:focus {
  color: #777777;
  background-color: #fff;
  border-color: #ddd;
  cursor: not-allowed;
}
.pagination-lg > li > a,
.pagination-lg > li > span {
  padding: 10px 16px;
  font-size: 17px;
  line-height: 1.3333333;
}
.pagination-lg > li:first-child > a,
.pagination-lg > li:first-child > span {
  border-bottom-left-radius: 3px;
  border-top-left-radius: 3px;
}
.pagination-lg > li:last-child > a,
.pagination-lg > li:last-child > span {
  border-bottom-right-radius: 3px;
  border-top-right-radius: 3px;
}
.pagination-sm > li > a,
.pagination-sm > li > span {
  padding: 5px 10px;
  font-size: 12px;
  line-height: 1.5;
}
.pagination-sm > li:first-child > a,
.pagination-sm > li:first-child > span {
  border-bottom-left-radius: 1px;
  border-top-left-radius: 1px;
}
.pagination-sm > li:last-child > a,
.pagination-sm > li:last-child > span {
  border-bottom-right-radius: 1px;
  border-top-right-radius: 1px;
}
.pager {
  padding-left: 0;
  margin: 18px 0;
  list-style: none;
  text-align: center;
}
.pager li {
  display: inline;
}
.pager li > a,
.pager li > span {
  display: inline-block;
  padding: 5px 14px;
  background-color: #fff;
  border: 1px solid #ddd;
  border-radius: 15px;
}
.pager li > a:hover,
.pager li > a:focus {
  text-decoration: none;
  background-color: #eeeeee;
}
.pager .next > a,
.pager .next > span {
  float: right;
}
.pager .previous > a,
.pager .previous > span {
  float: left;
}
.pager .disabled > a,
.pager .disabled > a:hover,
.pager .disabled > a:focus,
.pager .disabled > span {
  color: #777777;
  background-color: #fff;
  cursor: not-allowed;
}
.label {
  display: inline;
  padding: .2em .6em .3em;
  font-size: 75%;
  font-weight: bold;
  line-height: 1;
  color: #fff;
  text-align: center;
  white-space: nowrap;
  vertical-align: baseline;
  border-radius: .25em;
}
a.label:hover,
a.label:focus {
  color: #fff;
  text-decoration: none;
  cursor: pointer;
}
.label:empty {
  display: none;
}
.btn .label {
  position: relative;
  top: -1px;
}
.label-default {
  background-color: #777777;
}
.label-default[href]:hover,
.label-default[href]:focus {
  background-color: #5e5e5e;
}
.label-primary {
  background-color: #337ab7;
}
.label-primary[href]:hover,
.label-primary[href]:focus {
  background-color: #286090;
}
.label-success {
  background-color: #5cb85c;
}
.label-success[href]:hover,
.label-success[href]:focus {
  background-color: #449d44;
}
.label-info {
  background-color: #5bc0de;
}
.label-info[href]:hover,
.label-info[href]:focus {
  background-color: #31b0d5;
}
.label-warning {
  background-color: #f0ad4e;
}
.label-warning[href]:hover,
.label-warning[href]:focus {
  background-color: #ec971f;
}
.label-danger {
  background-color: #d9534f;
}
.label-danger[href]:hover,
.label-danger[href]:focus {
  background-color: #c9302c;
}
.badge {
  display: inline-block;
  min-width: 10px;
  padding: 3px 7px;
  font-size: 12px;
  font-weight: bold;
  color: #fff;
  line-height: 1;
  vertical-align: middle;
  white-space: nowrap;
  text-align: center;
  background-color: #777777;
  border-radius: 10px;
}
.badge:empty {
  display: none;
}
.btn .badge {
  position: relative;
  top: -1px;
}
.btn-xs .badge,
.btn-group-xs > .btn .badge {
  top: 0;
  padding: 1px 5px;
}
a.badge:hover,
a.badge:focus {
  color: #fff;
  text-decoration: none;
  cursor: pointer;
}
.list-group-item.active > .badge,
.nav-pills > .active > a > .badge {
  color: #337ab7;
  background-color: #fff;
}
.list-group-item > .badge {
  float: right;
}
.list-group-item > .badge + .badge {
  margin-right: 5px;
}
.nav-pills > li > a > .badge {
  margin-left: 3px;
}
.jumbotron {
  padding-top: 30px;
  padding-bottom: 30px;
  margin-bottom: 30px;
  color: inherit;
  background-color: #eeeeee;
}
.jumbotron h1,
.jumbotron .h1 {
  color: inherit;
}
.jumbotron p {
  margin-bottom: 15px;
  font-size: 20px;
  font-weight: 200;
}
.jumbotron > hr {
  border-top-color: #d5d5d5;
}
.container .jumbotron,
.container-fluid .jumbotron {
  border-radius: 3px;
  padding-left: 0px;
  padding-right: 0px;
}
.jumbotron .container {
  max-width: 100%;
}
@media screen and (min-width: 768px) {
  .jumbotron {
    padding-top: 48px;
    padding-bottom: 48px;
  }
  .container .jumbotron,
  .container-fluid .jumbotron {
    padding-left: 60px;
    padding-right: 60px;
  }
  .jumbotron h1,
  .jumbotron .h1 {
    font-size: 59px;
  }
}
.thumbnail {
  display: block;
  padding: 4px;
  margin-bottom: 18px;
  line-height: 1.42857143;
  background-color: #fff;
  border: 1px solid #ddd;
  border-radius: 2px;
  -webkit-transition: border 0.2s ease-in-out;
  -o-transition: border 0.2s ease-in-out;
  transition: border 0.2s ease-in-out;
}
.thumbnail > img,
.thumbnail a > img {
  margin-left: auto;
  margin-right: auto;
}
a.thumbnail:hover,
a.thumbnail:focus,
a.thumbnail.active {
  border-color: #337ab7;
}
.thumbnail .caption {
  padding: 9px;
  color: #000;
}
.alert {
  padding: 15px;
  margin-bottom: 18px;
  border: 1px solid transparent;
  border-radius: 2px;
}
.alert h4 {
  margin-top: 0;
  color: inherit;
}
.alert .alert-link {
  font-weight: bold;
}
.alert > p,
.alert > ul {
  margin-bottom: 0;
}
.alert > p + p {
  margin-top: 5px;
}
.alert-dismissable,
.alert-dismissible {
  padding-right: 35px;
}
.alert-dismissable .close,
.alert-dismissible .close {
  position: relative;
  top: -2px;
  right: -21px;
  color: inherit;
}
.alert-success {
  background-color: #dff0d8;
  border-color: #d6e9c6;
  color: #3c763d;
}
.alert-success hr {
  border-top-color: #c9e2b3;
}
.alert-success .alert-link {
  color: #2b542c;
}
.alert-info {
  background-color: #d9edf7;
  border-color: #bce8f1;
  color: #31708f;
}
.alert-info hr {
  border-top-color: #a6e1ec;
}
.alert-info .alert-link {
  color: #245269;
}
.alert-warning {
  background-color: #fcf8e3;
  border-color: #faebcc;
  color: #8a6d3b;
}
.alert-warning hr {
  border-top-color: #f7e1b5;
}
.alert-warning .alert-link {
  color: #66512c;
}
.alert-danger {
  background-color: #f2dede;
  border-color: #ebccd1;
  color: #a94442;
}
.alert-danger hr {
  border-top-color: #e4b9c0;
}
.alert-danger .alert-link {
  color: #843534;
}
@-webkit-keyframes progress-bar-stripes {
  from {
    background-position: 40px 0;
  }
  to {
    background-position: 0 0;
  }
}
@keyframes progress-bar-stripes {
  from {
    background-position: 40px 0;
  }
  to {
    background-position: 0 0;
  }
}
.progress {
  overflow: hidden;
  height: 18px;
  margin-bottom: 18px;
  background-color: #f5f5f5;
  border-radius: 2px;
  -webkit-box-shadow: inset 0 1px 2px rgba(0, 0, 0, 0.1);
  box-shadow: inset 0 1px 2px rgba(0, 0, 0, 0.1);
}
.progress-bar {
  float: left;
  width: 0%;
  height: 100%;
  font-size: 12px;
  line-height: 18px;
  color: #fff;
  text-align: center;
  background-color: #337ab7;
  -webkit-box-shadow: inset 0 -1px 0 rgba(0, 0, 0, 0.15);
  box-shadow: inset 0 -1px 0 rgba(0, 0, 0, 0.15);
  -webkit-transition: width 0.6s ease;
  -o-transition: width 0.6s ease;
  transition: width 0.6s ease;
}
.progress-striped .progress-bar,
.progress-bar-striped {
  background-image: -webkit-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: -o-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-size: 40px 40px;
}
.progress.active .progress-bar,
.progress-bar.active {
  -webkit-animation: progress-bar-stripes 2s linear infinite;
  -o-animation: progress-bar-stripes 2s linear infinite;
  animation: progress-bar-stripes 2s linear infinite;
}
.progress-bar-success {
  background-color: #5cb85c;
}
.progress-striped .progress-bar-success {
  background-image: -webkit-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: -o-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
}
.progress-bar-info {
  background-color: #5bc0de;
}
.progress-striped .progress-bar-info {
  background-image: -webkit-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: -o-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
}
.progress-bar-warning {
  background-color: #f0ad4e;
}
.progress-striped .progress-bar-warning {
  background-image: -webkit-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: -o-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
}
.progress-bar-danger {
  background-color: #d9534f;
}
.progress-striped .progress-bar-danger {
  background-image: -webkit-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: -o-linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
  background-image: linear-gradient(45deg, rgba(255, 255, 255, 0.15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, 0.15) 50%, rgba(255, 255, 255, 0.15) 75%, transparent 75%, transparent);
}
.media {
  margin-top: 15px;
}
.media:first-child {
  margin-top: 0;
}
.media,
.media-body {
  zoom: 1;
  overflow: hidden;
}
.media-body {
  width: 10000px;
}
.media-object {
  display: block;
}
.media-object.img-thumbnail {
  max-width: none;
}
.media-right,
.media > .pull-right {
  padding-left: 10px;
}
.media-left,
.media > .pull-left {
  padding-right: 10px;
}
.media-left,
.media-right,
.media-body {
  display: table-cell;
  vertical-align: top;
}
.media-middle {
  vertical-align: middle;
}
.media-bottom {
  vertical-align: bottom;
}
.media-heading {
  margin-top: 0;
  margin-bottom: 5px;
}
.media-list {
  padding-left: 0;
  list-style: none;
}
.list-group {
  margin-bottom: 20px;
  padding-left: 0;
}
.list-group-item {
  position: relative;
  display: block;
  padding: 10px 15px;
  margin-bottom: -1px;
  background-color: #fff;
  border: 1px solid #ddd;
}
.list-group-item:first-child {
  border-top-right-radius: 2px;
  border-top-left-radius: 2px;
}
.list-group-item:last-child {
  margin-bottom: 0;
  border-bottom-right-radius: 2px;
  border-bottom-left-radius: 2px;
}
a.list-group-item,
button.list-group-item {
  color: #555;
}
a.list-group-item .list-group-item-heading,
button.list-group-item .list-group-item-heading {
  color: #333;
}
a.list-group-item:hover,
button.list-group-item:hover,
a.list-group-item:focus,
button.list-group-item:focus {
  text-decoration: none;
  color: #555;
  background-color: #f5f5f5;
}
button.list-group-item {
  width: 100%;
  text-align: left;
}
.list-group-item.disabled,
.list-group-item.disabled:hover,
.list-group-item.disabled:focus {
  background-color: #eeeeee;
  color: #777777;
  cursor: not-allowed;
}
.list-group-item.disabled .list-group-item-heading,
.list-group-item.disabled:hover .list-group-item-heading,
.list-group-item.disabled:focus .list-group-item-heading {
  color: inherit;
}
.list-group-item.disabled .list-group-item-text,
.list-group-item.disabled:hover .list-group-item-text,
.list-group-item.disabled:focus .list-group-item-text {
  color: #777777;
}
.list-group-item.active,
.list-group-item.active:hover,
.list-group-item.active:focus {
  z-index: 2;
  color: #fff;
  background-color: #337ab7;
  border-color: #337ab7;
}
.list-group-item.active .list-group-item-heading,
.list-group-item.active:hover .list-group-item-heading,
.list-group-item.active:focus .list-group-item-heading,
.list-group-item.active .list-group-item-heading > small,
.list-group-item.active:hover .list-group-item-heading > small,
.list-group-item.active:focus .list-group-item-heading > small,
.list-group-item.active .list-group-item-heading > .small,
.list-group-item.active:hover .list-group-item-heading > .small,
.list-group-item.active:focus .list-group-item-heading > .small {
  color: inherit;
}
.list-group-item.active .list-group-item-text,
.list-group-item.active:hover .list-group-item-text,
.list-group-item.active:focus .list-group-item-text {
  color: #c7ddef;
}
.list-group-item-success {
  color: #3c763d;
  background-color: #dff0d8;
}
a.list-group-item-success,
button.list-group-item-success {
  color: #3c763d;
}
a.list-group-item-success .list-group-item-heading,
button.list-group-item-success .list-group-item-heading {
  color: inherit;
}
a.list-group-item-success:hover,
button.list-group-item-success:hover,
a.list-group-item-success:focus,
button.list-group-item-success:focus {
  color: #3c763d;
  background-color: #d0e9c6;
}
a.list-group-item-success.active,
button.list-group-item-success.active,
a.list-group-item-success.active:hover,
button.list-group-item-success.active:hover,
a.list-group-item-success.active:focus,
button.list-group-item-success.active:focus {
  color: #fff;
  background-color: #3c763d;
  border-color: #3c763d;
}
.list-group-item-info {
  color: #31708f;
  background-color: #d9edf7;
}
a.list-group-item-info,
button.list-group-item-info {
  color: #31708f;
}
a.list-group-item-info .list-group-item-heading,
button.list-group-item-info .list-group-item-heading {
  color: inherit;
}
a.list-group-item-info:hover,
button.list-group-item-info:hover,
a.list-group-item-info:focus,
button.list-group-item-info:focus {
  color: #31708f;
  background-color: #c4e3f3;
}
a.list-group-item-info.active,
button.list-group-item-info.active,
a.list-group-item-info.active:hover,
button.list-group-item-info.active:hover,
a.list-group-item-info.active:focus,
button.list-group-item-info.active:focus {
  color: #fff;
  background-color: #31708f;
  border-color: #31708f;
}
.list-group-item-warning {
  color: #8a6d3b;
  background-color: #fcf8e3;
}
a.list-group-item-warning,
button.list-group-item-warning {
  color: #8a6d3b;
}
a.list-group-item-warning .list-group-item-heading,
button.list-group-item-warning .list-group-item-heading {
  color: inherit;
}
a.list-group-item-warning:hover,
button.list-group-item-warning:hover,
a.list-group-item-warning:focus,
button.list-group-item-warning:focus {
  color: #8a6d3b;
  background-color: #faf2cc;
}
a.list-group-item-warning.active,
button.list-group-item-warning.active,
a.list-group-item-warning.active:hover,
button.list-group-item-warning.active:hover,
a.list-group-item-warning.active:focus,
button.list-group-item-warning.active:focus {
  color: #fff;
  background-color: #8a6d3b;
  border-color: #8a6d3b;
}
.list-group-item-danger {
  color: #a94442;
  background-color: #f2dede;
}
a.list-group-item-danger,
button.list-group-item-danger {
  color: #a94442;
}
a.list-group-item-danger .list-group-item-heading,
button.list-group-item-danger .list-group-item-heading {
  color: inherit;
}
a.list-group-item-danger:hover,
button.list-group-item-danger:hover,
a.list-group-item-danger:focus,
button.list-group-item-danger:focus {
  color: #a94442;
  background-color: #ebcccc;
}
a.list-group-item-danger.active,
button.list-group-item-danger.active,
a.list-group-item-danger.active:hover,
button.list-group-item-danger.active:hover,
a.list-group-item-danger.active:focus,
button.list-group-item-danger.active:focus {
  color: #fff;
  background-color: #a94442;
  border-color: #a94442;
}
.list-group-item-heading {
  margin-top: 0;
  margin-bottom: 5px;
}
.list-group-item-text {
  margin-bottom: 0;
  line-height: 1.3;
}
.panel {
  margin-bottom: 18px;
  background-color: #fff;
  border: 1px solid transparent;
  border-radius: 2px;
  -webkit-box-shadow: 0 1px 1px rgba(0, 0, 0, 0.05);
  box-shadow: 0 1px 1px rgba(0, 0, 0, 0.05);
}
.panel-body {
  padding: 15px;
}
.panel-heading {
  padding: 10px 15px;
  border-bottom: 1px solid transparent;
  border-top-right-radius: 1px;
  border-top-left-radius: 1px;
}
.panel-heading > .dropdown .dropdown-toggle {
  color: inherit;
}
.panel-title {
  margin-top: 0;
  margin-bottom: 0;
  font-size: 15px;
  color: inherit;
}
.panel-title > a,
.panel-title > small,
.panel-title > .small,
.panel-title > small > a,
.panel-title > .small > a {
  color: inherit;
}
.panel-footer {
  padding: 10px 15px;
  background-color: #f5f5f5;
  border-top: 1px solid #ddd;
  border-bottom-right-radius: 1px;
  border-bottom-left-radius: 1px;
}
.panel > .list-group,
.panel > .panel-collapse > .list-group {
  margin-bottom: 0;
}
.panel > .list-group .list-group-item,
.panel > .panel-collapse > .list-group .list-group-item {
  border-width: 1px 0;
  border-radius: 0;
}
.panel > .list-group:first-child .list-group-item:first-child,
.panel > .panel-collapse > .list-group:first-child .list-group-item:first-child {
  border-top: 0;
  border-top-right-radius: 1px;
  border-top-left-radius: 1px;
}
.panel > .list-group:last-child .list-group-item:last-child,
.panel > .panel-collapse > .list-group:last-child .list-group-item:last-child {
  border-bottom: 0;
  border-bottom-right-radius: 1px;
  border-bottom-left-radius: 1px;
}
.panel > .panel-heading + .panel-collapse > .list-group .list-group-item:first-child {
  border-top-right-radius: 0;
  border-top-left-radius: 0;
}
.panel-heading + .list-group .list-group-item:first-child {
  border-top-width: 0;
}
.list-group + .panel-footer {
  border-top-width: 0;
}
.panel > .table,
.panel > .table-responsive > .table,
.panel > .panel-collapse > .table {
  margin-bottom: 0;
}
.panel > .table caption,
.panel > .table-responsive > .table caption,
.panel > .panel-collapse > .table caption {
  padding-left: 15px;
  padding-right: 15px;
}
.panel > .table:first-child,
.panel > .table-responsive:first-child > .table:first-child {
  border-top-right-radius: 1px;
  border-top-left-radius: 1px;
}
.panel > .table:first-child > thead:first-child > tr:first-child,
.panel > .table-responsive:first-child > .table:first-child > thead:first-child > tr:first-child,
.panel > .table:first-child > tbody:first-child > tr:first-child,
.panel > .table-responsive:first-child > .table:first-child > tbody:first-child > tr:first-child {
  border-top-left-radius: 1px;
  border-top-right-radius: 1px;
}
.panel > .table:first-child > thead:first-child > tr:first-child td:first-child,
.panel > .table-responsive:first-child > .table:first-child > thead:first-child > tr:first-child td:first-child,
.panel > .table:first-child > tbody:first-child > tr:first-child td:first-child,
.panel > .table-responsive:first-child > .table:first-child > tbody:first-child > tr:first-child td:first-child,
.panel > .table:first-child > thead:first-child > tr:first-child th:first-child,
.panel > .table-responsive:first-child > .table:first-child > thead:first-child > tr:first-child th:first-child,
.panel > .table:first-child > tbody:first-child > tr:first-child th:first-child,
.panel > .table-responsive:first-child > .table:first-child > tbody:first-child > tr:first-child th:first-child {
  border-top-left-radius: 1px;
}
.panel > .table:first-child > thead:first-child > tr:first-child td:last-child,
.panel > .table-responsive:first-child > .table:first-child > thead:first-child > tr:first-child td:last-child,
.panel > .table:first-child > tbody:first-child > tr:first-child td:last-child,
.panel > .table-responsive:first-child > .table:first-child > tbody:first-child > tr:first-child td:last-child,
.panel > .table:first-child > thead:first-child > tr:first-child th:last-child,
.panel > .table-responsive:first-child > .table:first-child > thead:first-child > tr:first-child th:last-child,
.panel > .table:first-child > tbody:first-child > tr:first-child th:last-child,
.panel > .table-responsive:first-child > .table:first-child > tbody:first-child > tr:first-child th:last-child {
  border-top-right-radius: 1px;
}
.panel > .table:last-child,
.panel > .table-responsive:last-child > .table:last-child {
  border-bottom-right-radius: 1px;
  border-bottom-left-radius: 1px;
}
.panel > .table:last-child > tbody:last-child > tr:last-child,
.panel > .table-responsive:last-child > .table:last-child > tbody:last-child > tr:last-child,
.panel > .table:last-child > tfoot:last-child > tr:last-child,
.panel > .table-responsive:last-child > .table:last-child > tfoot:last-child > tr:last-child {
  border-bottom-left-radius: 1px;
  border-bottom-right-radius: 1px;
}
.panel > .table:last-child > tbody:last-child > tr:last-child td:first-child,
.panel > .table-responsive:last-child > .table:last-child > tbody:last-child > tr:last-child td:first-child,
.panel > .table:last-child > tfoot:last-child > tr:last-child td:first-child,
.panel > .table-responsive:last-child > .table:last-child > tfoot:last-child > tr:last-child td:first-child,
.panel > .table:last-child > tbody:last-child > tr:last-child th:first-child,
.panel > .table-responsive:last-child > .table:last-child > tbody:last-child > tr:last-child th:first-child,
.panel > .table:last-child > tfoot:last-child > tr:last-child th:first-child,
.panel > .table-responsive:last-child > .table:last-child > tfoot:last-child > tr:last-child th:first-child {
  border-bottom-left-radius: 1px;
}
.panel > .table:last-child > tbody:last-child > tr:last-child td:last-child,
.panel > .table-responsive:last-child > .table:last-child > tbody:last-child > tr:last-child td:last-child,
.panel > .table:last-child > tfoot:last-child > tr:last-child td:last-child,
.panel > .table-responsive:last-child > .table:last-child > tfoot:last-child > tr:last-child td:last-child,
.panel > .table:last-child > tbody:last-child > tr:last-child th:last-child,
.panel > .table-responsive:last-child > .table:last-child > tbody:last-child > tr:last-child th:last-child,
.panel > .table:last-child > tfoot:last-child > tr:last-child th:last-child,
.panel > .table-responsive:last-child > .table:last-child > tfoot:last-child > tr:last-child th:last-child {
  border-bottom-right-radius: 1px;
}
.panel > .panel-body + .table,
.panel > .panel-body + .table-responsive,
.panel > .table + .panel-body,
.panel > .table-responsive + .panel-body {
  border-top: 1px solid #ddd;
}
.panel > .table > tbody:first-child > tr:first-child th,
.panel > .table > tbody:first-child > tr:first-child td {
  border-top: 0;
}
.panel > .table-bordered,
.panel > .table-responsive > .table-bordered {
  border: 0;
}
.panel > .table-bordered > thead > tr > th:first-child,
.panel > .table-responsive > .table-bordered > thead > tr > th:first-child,
.panel > .table-bordered > tbody > tr > th:first-child,
.panel > .table-responsive > .table-bordered > tbody > tr > th:first-child,
.panel > .table-bordered > tfoot > tr > th:first-child,
.panel > .table-responsive > .table-bordered > tfoot > tr > th:first-child,
.panel > .table-bordered > thead > tr > td:first-child,
.panel > .table-responsive > .table-bordered > thead > tr > td:first-child,
.panel > .table-bordered > tbody > tr > td:first-child,
.panel > .table-responsive > .table-bordered > tbody > tr > td:first-child,
.panel > .table-bordered > tfoot > tr > td:first-child,
.panel > .table-responsive > .table-bordered > tfoot > tr > td:first-child {
  border-left: 0;
}
.panel > .table-bordered > thead > tr > th:last-child,
.panel > .table-responsive > .table-bordered > thead > tr > th:last-child,
.panel > .table-bordered > tbody > tr > th:last-child,
.panel > .table-responsive > .table-bordered > tbody > tr > th:last-child,
.panel > .table-bordered > tfoot > tr > th:last-child,
.panel > .table-responsive > .table-bordered > tfoot > tr > th:last-child,
.panel > .table-bordered > thead > tr > td:last-child,
.panel > .table-responsive > .table-bordered > thead > tr > td:last-child,
.panel > .table-bordered > tbody > tr > td:last-child,
.panel > .table-responsive > .table-bordered > tbody > tr > td:last-child,
.panel > .table-bordered > tfoot > tr > td:last-child,
.panel > .table-responsive > .table-bordered > tfoot > tr > td:last-child {
  border-right: 0;
}
.panel > .table-bordered > thead > tr:first-child > td,
.panel > .table-responsive > .table-bordered > thead > tr:first-child > td,
.panel > .table-bordered > tbody > tr:first-child > td,
.panel > .table-responsive > .table-bordered > tbody > tr:first-child > td,
.panel > .table-bordered > thead > tr:first-child > th,
.panel > .table-responsive > .table-bordered > thead > tr:first-child > th,
.panel > .table-bordered > tbody > tr:first-child > th,
.panel > .table-responsive > .table-bordered > tbody > tr:first-child > th {
  border-bottom: 0;
}
.panel > .table-bordered > tbody > tr:last-child > td,
.panel > .table-responsive > .table-bordered > tbody > tr:last-child > td,
.panel > .table-bordered > tfoot > tr:last-child > td,
.panel > .table-responsive > .table-bordered > tfoot > tr:last-child > td,
.panel > .table-bordered > tbody > tr:last-child > th,
.panel > .table-responsive > .table-bordered > tbody > tr:last-child > th,
.panel > .table-bordered > tfoot > tr:last-child > th,
.panel > .table-responsive > .table-bordered > tfoot > tr:last-child > th {
  border-bottom: 0;
}
.panel > .table-responsive {
  border: 0;
  margin-bottom: 0;
}
.panel-group {
  margin-bottom: 18px;
}
.panel-group .panel {
  margin-bottom: 0;
  border-radius: 2px;
}
.panel-group .panel + .panel {
  margin-top: 5px;
}
.panel-group .panel-heading {
  border-bottom: 0;
}
.panel-group .panel-heading + .panel-collapse > .panel-body,
.panel-group .panel-heading + .panel-collapse > .list-group {
  border-top: 1px solid #ddd;
}
.panel-group .panel-footer {
  border-top: 0;
}
.panel-group .panel-footer + .panel-collapse .panel-body {
  border-bottom: 1px solid #ddd;
}
.panel-default {
  border-color: #ddd;
}
.panel-default > .panel-heading {
  color: #333333;
  background-color: #f5f5f5;
  border-color: #ddd;
}
.panel-default > .panel-heading + .panel-collapse > .panel-body {
  border-top-color: #ddd;
}
.panel-default > .panel-heading .badge {
  color: #f5f5f5;
  background-color: #333333;
}
.panel-default > .panel-footer + .panel-collapse > .panel-body {
  border-bottom-color: #ddd;
}
.panel-primary {
  border-color: #337ab7;
}
.panel-primary > .panel-heading {
  color: #fff;
  background-color: #337ab7;
  border-color: #337ab7;
}
.panel-primary > .panel-heading + .panel-collapse > .panel-body {
  border-top-color: #337ab7;
}
.panel-primary > .panel-heading .badge {
  color: #337ab7;
  background-color: #fff;
}
.panel-primary > .panel-footer + .panel-collapse > .panel-body {
  border-bottom-color: #337ab7;
}
.panel-success {
  border-color: #d6e9c6;
}
.panel-success > .panel-heading {
  color: #3c763d;
  background-color: #dff0d8;
  border-color: #d6e9c6;
}
.panel-success > .panel-heading + .panel-collapse > .panel-body {
  border-top-color: #d6e9c6;
}
.panel-success > .panel-heading .badge {
  color: #dff0d8;
  background-color: #3c763d;
}
.panel-success > .panel-footer + .panel-collapse > .panel-body {
  border-bottom-color: #d6e9c6;
}
.panel-info {
  border-color: #bce8f1;
}
.panel-info > .panel-heading {
  color: #31708f;
  background-color: #d9edf7;
  border-color: #bce8f1;
}
.panel-info > .panel-heading + .panel-collapse > .panel-body {
  border-top-color: #bce8f1;
}
.panel-info > .panel-heading .badge {
  color: #d9edf7;
  background-color: #31708f;
}
.panel-info > .panel-footer + .panel-collapse > .panel-body {
  border-bottom-color: #bce8f1;
}
.panel-warning {
  border-color: #faebcc;
}
.panel-warning > .panel-heading {
  color: #8a6d3b;
  background-color: #fcf8e3;
  border-color: #faebcc;
}
.panel-warning > .panel-heading + .panel-collapse > .panel-body {
  border-top-color: #faebcc;
}
.panel-warning > .panel-heading .badge {
  color: #fcf8e3;
  background-color: #8a6d3b;
}
.panel-warning > .panel-footer + .panel-collapse > .panel-body {
  border-bottom-color: #faebcc;
}
.panel-danger {
  border-color: #ebccd1;
}
.panel-danger > .panel-heading {
  color: #a94442;
  background-color: #f2dede;
  border-color: #ebccd1;
}
.panel-danger > .panel-heading + .panel-collapse > .panel-body {
  border-top-color: #ebccd1;
}
.panel-danger > .panel-heading .badge {
  color: #f2dede;
  background-color: #a94442;
}
.panel-danger > .panel-footer + .panel-collapse > .panel-body {
  border-bottom-color: #ebccd1;
}
.embed-responsive {
  position: relative;
  display: block;
  height: 0;
  padding: 0;
  overflow: hidden;
}
.embed-responsive .embed-responsive-item,
.embed-responsive iframe,
.embed-responsive embed,
.embed-responsive object,
.embed-responsive video {
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  height: 100%;
  width: 100%;
  border: 0;
}
.embed-responsive-16by9 {
  padding-bottom: 56.25%;
}
.embed-responsive-4by3 {
  padding-bottom: 75%;
}
.well {
  min-height: 20px;
  padding: 19px;
  margin-bottom: 20px;
  background-color: #f5f5f5;
  border: 1px solid #e3e3e3;
  border-radius: 2px;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.05);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.05);
}
.well blockquote {
  border-color: #ddd;
  border-color: rgba(0, 0, 0, 0.15);
}
.well-lg {
  padding: 24px;
  border-radius: 3px;
}
.well-sm {
  padding: 9px;
  border-radius: 1px;
}
.close {
  float: right;
  font-size: 19.5px;
  font-weight: bold;
  line-height: 1;
  color: #000;
  text-shadow: 0 1px 0 #fff;
  opacity: 0.2;
  filter: alpha(opacity=20);
}
.close:hover,
.close:focus {
  color: #000;
  text-decoration: none;
  cursor: pointer;
  opacity: 0.5;
  filter: alpha(opacity=50);
}
button.close {
  padding: 0;
  cursor: pointer;
  background: transparent;
  border: 0;
  -webkit-appearance: none;
}
.modal-open {
  overflow: hidden;
}
.modal {
  display: none;
  overflow: hidden;
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 1050;
  -webkit-overflow-scrolling: touch;
  outline: 0;
}
.modal.fade .modal-dialog {
  -webkit-transform: translate(0, -25%);
  -ms-transform: translate(0, -25%);
  -o-transform: translate(0, -25%);
  transform: translate(0, -25%);
  -webkit-transition: -webkit-transform 0.3s ease-out;
  -moz-transition: -moz-transform 0.3s ease-out;
  -o-transition: -o-transform 0.3s ease-out;
  transition: transform 0.3s ease-out;
}
.modal.in .modal-dialog {
  -webkit-transform: translate(0, 0);
  -ms-transform: translate(0, 0);
  -o-transform: translate(0, 0);
  transform: translate(0, 0);
}
.modal-open .modal {
  overflow-x: hidden;
  overflow-y: auto;
}
.modal-dialog {
  position: relative;
  width: auto;
  margin: 10px;
}
.modal-content {
  position: relative;
  background-color: #fff;
  border: 1px solid #999;
  border: 1px solid rgba(0, 0, 0, 0.2);
  border-radius: 3px;
  -webkit-box-shadow: 0 3px 9px rgba(0, 0, 0, 0.5);
  box-shadow: 0 3px 9px rgba(0, 0, 0, 0.5);
  background-clip: padding-box;
  outline: 0;
}
.modal-backdrop {
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 1040;
  background-color: #000;
}
.modal-backdrop.fade {
  opacity: 0;
  filter: alpha(opacity=0);
}
.modal-backdrop.in {
  opacity: 0.5;
  filter: alpha(opacity=50);
}
.modal-header {
  padding: 15px;
  border-bottom: 1px solid #e5e5e5;
}
.modal-header .close {
  margin-top: -2px;
}
.modal-title {
  margin: 0;
  line-height: 1.42857143;
}
.modal-body {
  position: relative;
  padding: 15px;
}
.modal-footer {
  padding: 15px;
  text-align: right;
  border-top: 1px solid #e5e5e5;
}
.modal-footer .btn + .btn {
  margin-left: 5px;
  margin-bottom: 0;
}
.modal-footer .btn-group .btn + .btn {
  margin-left: -1px;
}
.modal-footer .btn-block + .btn-block {
  margin-left: 0;
}
.modal-scrollbar-measure {
  position: absolute;
  top: -9999px;
  width: 50px;
  height: 50px;
  overflow: scroll;
}
@media (min-width: 768px) {
  .modal-dialog {
    width: 600px;
    margin: 30px auto;
  }
  .modal-content {
    -webkit-box-shadow: 0 5px 15px rgba(0, 0, 0, 0.5);
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.5);
  }
  .modal-sm {
    width: 300px;
  }
}
@media (min-width: 992px) {
  .modal-lg {
    width: 900px;
  }
}
.tooltip {
  position: absolute;
  z-index: 1070;
  display: block;
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
  font-style: normal;
  font-weight: normal;
  letter-spacing: normal;
  line-break: auto;
  line-height: 1.42857143;
  text-align: left;
  text-align: start;
  text-decoration: none;
  text-shadow: none;
  text-transform: none;
  white-space: normal;
  word-break: normal;
  word-spacing: normal;
  word-wrap: normal;
  font-size: 12px;
  opacity: 0;
  filter: alpha(opacity=0);
}
.tooltip.in {
  opacity: 0.9;
  filter: alpha(opacity=90);
}
.tooltip.top {
  margin-top: -3px;
  padding: 5px 0;
}
.tooltip.right {
  margin-left: 3px;
  padding: 0 5px;
}
.tooltip.bottom {
  margin-top: 3px;
  padding: 5px 0;
}
.tooltip.left {
  margin-left: -3px;
  padding: 0 5px;
}
.tooltip-inner {
  max-width: 200px;
  padding: 3px 8px;
  color: #fff;
  text-align: center;
  background-color: #000;
  border-radius: 2px;
}
.tooltip-arrow {
  position: absolute;
  width: 0;
  height: 0;
  border-color: transparent;
  border-style: solid;
}
.tooltip.top .tooltip-arrow {
  bottom: 0;
  left: 50%;
  margin-left: -5px;
  border-width: 5px 5px 0;
  border-top-color: #000;
}
.tooltip.top-left .tooltip-arrow {
  bottom: 0;
  right: 5px;
  margin-bottom: -5px;
  border-width: 5px 5px 0;
  border-top-color: #000;
}
.tooltip.top-right .tooltip-arrow {
  bottom: 0;
  left: 5px;
  margin-bottom: -5px;
  border-width: 5px 5px 0;
  border-top-color: #000;
}
.tooltip.right .tooltip-arrow {
  top: 50%;
  left: 0;
  margin-top: -5px;
  border-width: 5px 5px 5px 0;
  border-right-color: #000;
}
.tooltip.left .tooltip-arrow {
  top: 50%;
  right: 0;
  margin-top: -5px;
  border-width: 5px 0 5px 5px;
  border-left-color: #000;
}
.tooltip.bottom .tooltip-arrow {
  top: 0;
  left: 50%;
  margin-left: -5px;
  border-width: 0 5px 5px;
  border-bottom-color: #000;
}
.tooltip.bottom-left .tooltip-arrow {
  top: 0;
  right: 5px;
  margin-top: -5px;
  border-width: 0 5px 5px;
  border-bottom-color: #000;
}
.tooltip.bottom-right .tooltip-arrow {
  top: 0;
  left: 5px;
  margin-top: -5px;
  border-width: 0 5px 5px;
  border-bottom-color: #000;
}
.popover {
  position: absolute;
  top: 0;
  left: 0;
  z-index: 1060;
  display: none;
  max-width: 276px;
  padding: 1px;
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
  font-style: normal;
  font-weight: normal;
  letter-spacing: normal;
  line-break: auto;
  line-height: 1.42857143;
  text-align: left;
  text-align: start;
  text-decoration: none;
  text-shadow: none;
  text-transform: none;
  white-space: normal;
  word-break: normal;
  word-spacing: normal;
  word-wrap: normal;
  font-size: 13px;
  background-color: #fff;
  background-clip: padding-box;
  border: 1px solid #ccc;
  border: 1px solid rgba(0, 0, 0, 0.2);
  border-radius: 3px;
  -webkit-box-shadow: 0 5px 10px rgba(0, 0, 0, 0.2);
  box-shadow: 0 5px 10px rgba(0, 0, 0, 0.2);
}
.popover.top {
  margin-top: -10px;
}
.popover.right {
  margin-left: 10px;
}
.popover.bottom {
  margin-top: 10px;
}
.popover.left {
  margin-left: -10px;
}
.popover-title {
  margin: 0;
  padding: 8px 14px;
  font-size: 13px;
  background-color: #f7f7f7;
  border-bottom: 1px solid #ebebeb;
  border-radius: 2px 2px 0 0;
}
.popover-content {
  padding: 9px 14px;
}
.popover > .arrow,
.popover > .arrow:after {
  position: absolute;
  display: block;
  width: 0;
  height: 0;
  border-color: transparent;
  border-style: solid;
}
.popover > .arrow {
  border-width: 11px;
}
.popover > .arrow:after {
  border-width: 10px;
  content: "";
}
.popover.top > .arrow {
  left: 50%;
  margin-left: -11px;
  border-bottom-width: 0;
  border-top-color: #999999;
  border-top-color: rgba(0, 0, 0, 0.25);
  bottom: -11px;
}
.popover.top > .arrow:after {
  content: " ";
  bottom: 1px;
  margin-left: -10px;
  border-bottom-width: 0;
  border-top-color: #fff;
}
.popover.right > .arrow {
  top: 50%;
  left: -11px;
  margin-top: -11px;
  border-left-width: 0;
  border-right-color: #999999;
  border-right-color: rgba(0, 0, 0, 0.25);
}
.popover.right > .arrow:after {
  content: " ";
  left: 1px;
  bottom: -10px;
  border-left-width: 0;
  border-right-color: #fff;
}
.popover.bottom > .arrow {
  left: 50%;
  margin-left: -11px;
  border-top-width: 0;
  border-bottom-color: #999999;
  border-bottom-color: rgba(0, 0, 0, 0.25);
  top: -11px;
}
.popover.bottom > .arrow:after {
  content: " ";
  top: 1px;
  margin-left: -10px;
  border-top-width: 0;
  border-bottom-color: #fff;
}
.popover.left > .arrow {
  top: 50%;
  right: -11px;
  margin-top: -11px;
  border-right-width: 0;
  border-left-color: #999999;
  border-left-color: rgba(0, 0, 0, 0.25);
}
.popover.left > .arrow:after {
  content: " ";
  right: 1px;
  border-right-width: 0;
  border-left-color: #fff;
  bottom: -10px;
}
.carousel {
  position: relative;
}
.carousel-inner {
  position: relative;
  overflow: hidden;
  width: 100%;
}
.carousel-inner > .item {
  display: none;
  position: relative;
  -webkit-transition: 0.6s ease-in-out left;
  -o-transition: 0.6s ease-in-out left;
  transition: 0.6s ease-in-out left;
}
.carousel-inner > .item > img,
.carousel-inner > .item > a > img {
  line-height: 1;
}
@media all and (transform-3d), (-webkit-transform-3d) {
  .carousel-inner > .item {
    -webkit-transition: -webkit-transform 0.6s ease-in-out;
    -moz-transition: -moz-transform 0.6s ease-in-out;
    -o-transition: -o-transform 0.6s ease-in-out;
    transition: transform 0.6s ease-in-out;
    -webkit-backface-visibility: hidden;
    -moz-backface-visibility: hidden;
    backface-visibility: hidden;
    -webkit-perspective: 1000px;
    -moz-perspective: 1000px;
    perspective: 1000px;
  }
  .carousel-inner > .item.next,
  .carousel-inner > .item.active.right {
    -webkit-transform: translate3d(100%, 0, 0);
    transform: translate3d(100%, 0, 0);
    left: 0;
  }
  .carousel-inner > .item.prev,
  .carousel-inner > .item.active.left {
    -webkit-transform: translate3d(-100%, 0, 0);
    transform: translate3d(-100%, 0, 0);
    left: 0;
  }
  .carousel-inner > .item.next.left,
  .carousel-inner > .item.prev.right,
  .carousel-inner > .item.active {
    -webkit-transform: translate3d(0, 0, 0);
    transform: translate3d(0, 0, 0);
    left: 0;
  }
}
.carousel-inner > .active,
.carousel-inner > .next,
.carousel-inner > .prev {
  display: block;
}
.carousel-inner > .active {
  left: 0;
}
.carousel-inner > .next,
.carousel-inner > .prev {
  position: absolute;
  top: 0;
  width: 100%;
}
.carousel-inner > .next {
  left: 100%;
}
.carousel-inner > .prev {
  left: -100%;
}
.carousel-inner > .next.left,
.carousel-inner > .prev.right {
  left: 0;
}
.carousel-inner > .active.left {
  left: -100%;
}
.carousel-inner > .active.right {
  left: 100%;
}
.carousel-control {
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  width: 15%;
  opacity: 0.5;
  filter: alpha(opacity=50);
  font-size: 20px;
  color: #fff;
  text-align: center;
  text-shadow: 0 1px 2px rgba(0, 0, 0, 0.6);
  background-color: rgba(0, 0, 0, 0);
}
.carousel-control.left {
  background-image: -webkit-linear-gradient(left, rgba(0, 0, 0, 0.5) 0%, rgba(0, 0, 0, 0.0001) 100%);
  background-image: -o-linear-gradient(left, rgba(0, 0, 0, 0.5) 0%, rgba(0, 0, 0, 0.0001) 100%);
  background-image: linear-gradient(to right, rgba(0, 0, 0, 0.5) 0%, rgba(0, 0, 0, 0.0001) 100%);
  background-repeat: repeat-x;
  filter: progid:DXImageTransform.Microsoft.gradient(startColorstr='#80000000', endColorstr='#00000000', GradientType=1);
}
.carousel-control.right {
  left: auto;
  right: 0;
  background-image: -webkit-linear-gradient(left, rgba(0, 0, 0, 0.0001) 0%, rgba(0, 0, 0, 0.5) 100%);
  background-image: -o-linear-gradient(left, rgba(0, 0, 0, 0.0001) 0%, rgba(0, 0, 0, 0.5) 100%);
  background-image: linear-gradient(to right, rgba(0, 0, 0, 0.0001) 0%, rgba(0, 0, 0, 0.5) 100%);
  background-repeat: repeat-x;
  filter: progid:DXImageTransform.Microsoft.gradient(startColorstr='#00000000', endColorstr='#80000000', GradientType=1);
}
.carousel-control:hover,
.carousel-control:focus {
  outline: 0;
  color: #fff;
  text-decoration: none;
  opacity: 0.9;
  filter: alpha(opacity=90);
}
.carousel-control .icon-prev,
.carousel-control .icon-next,
.carousel-control .glyphicon-chevron-left,
.carousel-control .glyphicon-chevron-right {
  position: absolute;
  top: 50%;
  margin-top: -10px;
  z-index: 5;
  display: inline-block;
}
.carousel-control .icon-prev,
.carousel-control .glyphicon-chevron-left {
  left: 50%;
  margin-left: -10px;
}
.carousel-control .icon-next,
.carousel-control .glyphicon-chevron-right {
  right: 50%;
  margin-right: -10px;
}
.carousel-control .icon-prev,
.carousel-control .icon-next {
  width: 20px;
  height: 20px;
  line-height: 1;
  font-family: serif;
}
.carousel-control .icon-prev:before {
  content: '\2039';
}
.carousel-control .icon-next:before {
  content: '\203a';
}
.carousel-indicators {
  position: absolute;
  bottom: 10px;
  left: 50%;
  z-index: 15;
  width: 60%;
  margin-left: -30%;
  padding-left: 0;
  list-style: none;
  text-align: center;
}
.carousel-indicators li {
  display: inline-block;
  width: 10px;
  height: 10px;
  margin: 1px;
  text-indent: -999px;
  border: 1px solid #fff;
  border-radius: 10px;
  cursor: pointer;
  background-color: #000 \9;
  background-color: rgba(0, 0, 0, 0);
}
.carousel-indicators .active {
  margin: 0;
  width: 12px;
  height: 12px;
  background-color: #fff;
}
.carousel-caption {
  position: absolute;
  left: 15%;
  right: 15%;
  bottom: 20px;
  z-index: 10;
  padding-top: 20px;
  padding-bottom: 20px;
  color: #fff;
  text-align: center;
  text-shadow: 0 1px 2px rgba(0, 0, 0, 0.6);
}
.carousel-caption .btn {
  text-shadow: none;
}
@media screen and (min-width: 768px) {
  .carousel-control .glyphicon-chevron-left,
  .carousel-control .glyphicon-chevron-right,
  .carousel-control .icon-prev,
  .carousel-control .icon-next {
    width: 30px;
    height: 30px;
    margin-top: -10px;
    font-size: 30px;
  }
  .carousel-control .glyphicon-chevron-left,
  .carousel-control .icon-prev {
    margin-left: -10px;
  }
  .carousel-control .glyphicon-chevron-right,
  .carousel-control .icon-next {
    margin-right: -10px;
  }
  .carousel-caption {
    left: 20%;
    right: 20%;
    padding-bottom: 30px;
  }
  .carousel-indicators {
    bottom: 20px;
  }
}
.clearfix:before,
.clearfix:after,
.dl-horizontal dd:before,
.dl-horizontal dd:after,
.container:before,
.container:after,
.container-fluid:before,
.container-fluid:after,
.row:before,
.row:after,
.form-horizontal .form-group:before,
.form-horizontal .form-group:after,
.btn-toolbar:before,
.btn-toolbar:after,
.btn-group-vertical > .btn-group:before,
.btn-group-vertical > .btn-group:after,
.nav:before,
.nav:after,
.navbar:before,
.navbar:after,
.navbar-header:before,
.navbar-header:after,
.navbar-collapse:before,
.navbar-collapse:after,
.pager:before,
.pager:after,
.panel-body:before,
.panel-body:after,
.modal-header:before,
.modal-header:after,
.modal-footer:before,
.modal-footer:after,
.item_buttons:before,
.item_buttons:after {
  content: " ";
  display: table;
}
.clearfix:after,
.dl-horizontal dd:after,
.container:after,
.container-fluid:after,
.row:after,
.form-horizontal .form-group:after,
.btn-toolbar:after,
.btn-group-vertical > .btn-group:after,
.nav:after,
.navbar:after,
.navbar-header:after,
.navbar-collapse:after,
.pager:after,
.panel-body:after,
.modal-header:after,
.modal-footer:after,
.item_buttons:after {
  clear: both;
}
.center-block {
  display: block;
  margin-left: auto;
  margin-right: auto;
}
.pull-right {
  float: right !important;
}
.pull-left {
  float: left !important;
}
.hide {
  display: none !important;
}
.show {
  display: block !important;
}
.invisible {
  visibility: hidden;
}
.text-hide {
  font: 0/0 a;
  color: transparent;
  text-shadow: none;
  background-color: transparent;
  border: 0;
}
.hidden {
  display: none !important;
}
.affix {
  position: fixed;
}
@-ms-viewport {
  width: device-width;
}
.visible-xs,
.visible-sm,
.visible-md,
.visible-lg {
  display: none !important;
}
.visible-xs-block,
.visible-xs-inline,
.visible-xs-inline-block,
.visible-sm-block,
.visible-sm-inline,
.visible-sm-inline-block,
.visible-md-block,
.visible-md-inline,
.visible-md-inline-block,
.visible-lg-block,
.visible-lg-inline,
.visible-lg-inline-block {
  display: none !important;
}
@media (max-width: 767px) {
  .visible-xs {
    display: block !important;
  }
  table.visible-xs {
    display: table !important;
  }
  tr.visible-xs {
    display: table-row !important;
  }
  th.visible-xs,
  td.visible-xs {
    display: table-cell !important;
  }
}
@media (max-width: 767px) {
  .visible-xs-block {
    display: block !important;
  }
}
@media (max-width: 767px) {
  .visible-xs-inline {
    display: inline !important;
  }
}
@media (max-width: 767px) {
  .visible-xs-inline-block {
    display: inline-block !important;
  }
}
@media (min-width: 768px) and (max-width: 991px) {
  .visible-sm {
    display: block !important;
  }
  table.visible-sm {
    display: table !important;
  }
  tr.visible-sm {
    display: table-row !important;
  }
  th.visible-sm,
  td.visible-sm {
    display: table-cell !important;
  }
}
@media (min-width: 768px) and (max-width: 991px) {
  .visible-sm-block {
    display: block !important;
  }
}
@media (min-width: 768px) and (max-width: 991px) {
  .visible-sm-inline {
    display: inline !important;
  }
}
@media (min-width: 768px) and (max-width: 991px) {
  .visible-sm-inline-block {
    display: inline-block !important;
  }
}
@media (min-width: 992px) and (max-width: 1199px) {
  .visible-md {
    display: block !important;
  }
  table.visible-md {
    display: table !important;
  }
  tr.visible-md {
    display: table-row !important;
  }
  th.visible-md,
  td.visible-md {
    display: table-cell !important;
  }
}
@media (min-width: 992px) and (max-width: 1199px) {
  .visible-md-block {
    display: block !important;
  }
}
@media (min-width: 992px) and (max-width: 1199px) {
  .visible-md-inline {
    display: inline !important;
  }
}
@media (min-width: 992px) and (max-width: 1199px) {
  .visible-md-inline-block {
    display: inline-block !important;
  }
}
@media (min-width: 1200px) {
  .visible-lg {
    display: block !important;
  }
  table.visible-lg {
    display: table !important;
  }
  tr.visible-lg {
    display: table-row !important;
  }
  th.visible-lg,
  td.visible-lg {
    display: table-cell !important;
  }
}
@media (min-width: 1200px) {
  .visible-lg-block {
    display: block !important;
  }
}
@media (min-width: 1200px) {
  .visible-lg-inline {
    display: inline !important;
  }
}
@media (min-width: 1200px) {
  .visible-lg-inline-block {
    display: inline-block !important;
  }
}
@media (max-width: 767px) {
  .hidden-xs {
    display: none !important;
  }
}
@media (min-width: 768px) and (max-width: 991px) {
  .hidden-sm {
    display: none !important;
  }
}
@media (min-width: 992px) and (max-width: 1199px) {
  .hidden-md {
    display: none !important;
  }
}
@media (min-width: 1200px) {
  .hidden-lg {
    display: none !important;
  }
}
.visible-print {
  display: none !important;
}
@media print {
  .visible-print {
    display: block !important;
  }
  table.visible-print {
    display: table !important;
  }
  tr.visible-print {
    display: table-row !important;
  }
  th.visible-print,
  td.visible-print {
    display: table-cell !important;
  }
}
.visible-print-block {
  display: none !important;
}
@media print {
  .visible-print-block {
    display: block !important;
  }
}
.visible-print-inline {
  display: none !important;
}
@media print {
  .visible-print-inline {
    display: inline !important;
  }
}
.visible-print-inline-block {
  display: none !important;
}
@media print {
  .visible-print-inline-block {
    display: inline-block !important;
  }
}
@media print {
  .hidden-print {
    display: none !important;
  }
}
/*!
*
* Font Awesome
*
*/
/*!
 *  Font Awesome 4.2.0 by @davegandy - http://fontawesome.io - @fontawesome
 *  License - http://fontawesome.io/license (Font: SIL OFL 1.1, CSS: MIT License)
 */
/* FONT PATH
 * -------------------------- */
/* @font-face {
  font-family: 'FontAwesome';
  src: url('../components/font-awesome/fonts/fontawesome-webfont.eot?v=4.2.0');
  src: url('../components/font-awesome/fonts/fontawesome-webfont.eot?#iefix&v=4.2.0') format('embedded-opentype'), url('../components/font-awesome/fonts/fontawesome-webfont.woff?v=4.2.0') format('woff'), url('../components/font-awesome/fonts/fontawesome-webfont.ttf?v=4.2.0') format('truetype'), url('../components/font-awesome/fonts/fontawesome-webfont.svg?v=4.2.0#fontawesomeregular') format('svg');
  font-weight: normal;
  font-style: normal;
} */
.fa {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
/* makes the font 33% larger relative to the icon container */
.fa-lg {
  font-size: 1.33333333em;
  line-height: 0.75em;
  vertical-align: -15%;
}
.fa-2x {
  font-size: 2em;
}
.fa-3x {
  font-size: 3em;
}
.fa-4x {
  font-size: 4em;
}
.fa-5x {
  font-size: 5em;
}
.fa-fw {
  width: 1.28571429em;
  text-align: center;
}
.fa-ul {
  padding-left: 0;
  margin-left: 2.14285714em;
  list-style-type: none;
}
.fa-ul > li {
  position: relative;
}
.fa-li {
  position: absolute;
  left: -2.14285714em;
  width: 2.14285714em;
  top: 0.14285714em;
  text-align: center;
}
.fa-li.fa-lg {
  left: -1.85714286em;
}
.fa-border {
  padding: .2em .25em .15em;
  border: solid 0.08em #eee;
  border-radius: .1em;
}
.pull-right {
  float: right;
}
.pull-left {
  float: left;
}
.fa.pull-left {
  margin-right: .3em;
}
.fa.pull-right {
  margin-left: .3em;
}
.fa-spin {
  -webkit-animation: fa-spin 2s infinite linear;
  animation: fa-spin 2s infinite linear;
}
@-webkit-keyframes fa-spin {
  0% {
    -webkit-transform: rotate(0deg);
    transform: rotate(0deg);
  }
  100% {
    -webkit-transform: rotate(359deg);
    transform: rotate(359deg);
  }
}
@keyframes fa-spin {
  0% {
    -webkit-transform: rotate(0deg);
    transform: rotate(0deg);
  }
  100% {
    -webkit-transform: rotate(359deg);
    transform: rotate(359deg);
  }
}
.fa-rotate-90 {
  filter: progid:DXImageTransform.Microsoft.BasicImage(rotation=1);
  -webkit-transform: rotate(90deg);
  -ms-transform: rotate(90deg);
  transform: rotate(90deg);
}
.fa-rotate-180 {
  filter: progid:DXImageTransform.Microsoft.BasicImage(rotation=2);
  -webkit-transform: rotate(180deg);
  -ms-transform: rotate(180deg);
  transform: rotate(180deg);
}
.fa-rotate-270 {
  filter: progid:DXImageTransform.Microsoft.BasicImage(rotation=3);
  -webkit-transform: rotate(270deg);
  -ms-transform: rotate(270deg);
  transform: rotate(270deg);
}
.fa-flip-horizontal {
  filter: progid:DXImageTransform.Microsoft.BasicImage(rotation=0, mirror=1);
  -webkit-transform: scale(-1, 1);
  -ms-transform: scale(-1, 1);
  transform: scale(-1, 1);
}
.fa-flip-vertical {
  filter: progid:DXImageTransform.Microsoft.BasicImage(rotation=2, mirror=1);
  -webkit-transform: scale(1, -1);
  -ms-transform: scale(1, -1);
  transform: scale(1, -1);
}
:root .fa-rotate-90,
:root .fa-rotate-180,
:root .fa-rotate-270,
:root .fa-flip-horizontal,
:root .fa-flip-vertical {
  filter: none;
}
.fa-stack {
  position: relative;
  display: inline-block;
  width: 2em;
  height: 2em;
  line-height: 2em;
  vertical-align: middle;
}
.fa-stack-1x,
.fa-stack-2x {
  position: absolute;
  left: 0;
  width: 100%;
  text-align: center;
}
.fa-stack-1x {
  line-height: inherit;
}
.fa-stack-2x {
  font-size: 2em;
}
.fa-inverse {
  color: #fff;
}
/* Font Awesome uses the Unicode Private Use Area (PUA) to ensure screen
   readers do not read off random characters that represent icons */
.fa-glass:before {
  content: "\f000";
}
.fa-music:before {
  content: "\f001";
}
.fa-search:before {
  content: "\f002";
}
.fa-envelope-o:before {
  content: "\f003";
}
.fa-heart:before {
  content: "\f004";
}
.fa-star:before {
  content: "\f005";
}
.fa-star-o:before {
  content: "\f006";
}
.fa-user:before {
  content: "\f007";
}
.fa-film:before {
  content: "\f008";
}
.fa-th-large:before {
  content: "\f009";
}
.fa-th:before {
  content: "\f00a";
}
.fa-th-list:before {
  content: "\f00b";
}
.fa-check:before {
  content: "\f00c";
}
.fa-remove:before,
.fa-close:before,
.fa-times:before {
  content: "\f00d";
}
.fa-search-plus:before {
  content: "\f00e";
}
.fa-search-minus:before {
  content: "\f010";
}
.fa-power-off:before {
  content: "\f011";
}
.fa-signal:before {
  content: "\f012";
}
.fa-gear:before,
.fa-cog:before {
  content: "\f013";
}
.fa-trash-o:before {
  content: "\f014";
}
.fa-home:before {
  content: "\f015";
}
.fa-file-o:before {
  content: "\f016";
}
.fa-clock-o:before {
  content: "\f017";
}
.fa-road:before {
  content: "\f018";
}
.fa-download:before {
  content: "\f019";
}
.fa-arrow-circle-o-down:before {
  content: "\f01a";
}
.fa-arrow-circle-o-up:before {
  content: "\f01b";
}
.fa-inbox:before {
  content: "\f01c";
}
.fa-play-circle-o:before {
  content: "\f01d";
}
.fa-rotate-right:before,
.fa-repeat:before {
  content: "\f01e";
}
.fa-refresh:before {
  content: "\f021";
}
.fa-list-alt:before {
  content: "\f022";
}
.fa-lock:before {
  content: "\f023";
}
.fa-flag:before {
  content: "\f024";
}
.fa-headphones:before {
  content: "\f025";
}
.fa-volume-off:before {
  content: "\f026";
}
.fa-volume-down:before {
  content: "\f027";
}
.fa-volume-up:before {
  content: "\f028";
}
.fa-qrcode:before {
  content: "\f029";
}
.fa-barcode:before {
  content: "\f02a";
}
.fa-tag:before {
  content: "\f02b";
}
.fa-tags:before {
  content: "\f02c";
}
.fa-book:before {
  content: "\f02d";
}
.fa-bookmark:before {
  content: "\f02e";
}
.fa-print:before {
  content: "\f02f";
}
.fa-camera:before {
  content: "\f030";
}
.fa-font:before {
  content: "\f031";
}
.fa-bold:before {
  content: "\f032";
}
.fa-italic:before {
  content: "\f033";
}
.fa-text-height:before {
  content: "\f034";
}
.fa-text-width:before {
  content: "\f035";
}
.fa-align-left:before {
  content: "\f036";
}
.fa-align-center:before {
  content: "\f037";
}
.fa-align-right:before {
  content: "\f038";
}
.fa-align-justify:before {
  content: "\f039";
}
.fa-list:before {
  content: "\f03a";
}
.fa-dedent:before,
.fa-outdent:before {
  content: "\f03b";
}
.fa-indent:before {
  content: "\f03c";
}
.fa-video-camera:before {
  content: "\f03d";
}
.fa-photo:before,
.fa-image:before,
.fa-picture-o:before {
  content: "\f03e";
}
.fa-pencil:before {
  content: "\f040";
}
.fa-map-marker:before {
  content: "\f041";
}
.fa-adjust:before {
  content: "\f042";
}
.fa-tint:before {
  content: "\f043";
}
.fa-edit:before,
.fa-pencil-square-o:before {
  content: "\f044";
}
.fa-share-square-o:before {
  content: "\f045";
}
.fa-check-square-o:before {
  content: "\f046";
}
.fa-arrows:before {
  content: "\f047";
}
.fa-step-backward:before {
  content: "\f048";
}
.fa-fast-backward:before {
  content: "\f049";
}
.fa-backward:before {
  content: "\f04a";
}
.fa-play:before {
  content: "\f04b";
}
.fa-pause:before {
  content: "\f04c";
}
.fa-stop:before {
  content: "\f04d";
}
.fa-forward:before {
  content: "\f04e";
}
.fa-fast-forward:before {
  content: "\f050";
}
.fa-step-forward:before {
  content: "\f051";
}
.fa-eject:before {
  content: "\f052";
}
.fa-chevron-left:before {
  content: "\f053";
}
.fa-chevron-right:before {
  content: "\f054";
}
.fa-plus-circle:before {
  content: "\f055";
}
.fa-minus-circle:before {
  content: "\f056";
}
.fa-times-circle:before {
  content: "\f057";
}
.fa-check-circle:before {
  content: "\f058";
}
.fa-question-circle:before {
  content: "\f059";
}
.fa-info-circle:before {
  content: "\f05a";
}
.fa-crosshairs:before {
  content: "\f05b";
}
.fa-times-circle-o:before {
  content: "\f05c";
}
.fa-check-circle-o:before {
  content: "\f05d";
}
.fa-ban:before {
  content: "\f05e";
}
.fa-arrow-left:before {
  content: "\f060";
}
.fa-arrow-right:before {
  content: "\f061";
}
.fa-arrow-up:before {
  content: "\f062";
}
.fa-arrow-down:before {
  content: "\f063";
}
.fa-mail-forward:before,
.fa-share:before {
  content: "\f064";
}
.fa-expand:before {
  content: "\f065";
}
.fa-compress:before {
  content: "\f066";
}
.fa-plus:before {
  content: "\f067";
}
.fa-minus:before {
  content: "\f068";
}
.fa-asterisk:before {
  content: "\f069";
}
.fa-exclamation-circle:before {
  content: "\f06a";
}
.fa-gift:before {
  content: "\f06b";
}
.fa-leaf:before {
  content: "\f06c";
}
.fa-fire:before {
  content: "\f06d";
}
.fa-eye:before {
  content: "\f06e";
}
.fa-eye-slash:before {
  content: "\f070";
}
.fa-warning:before,
.fa-exclamation-triangle:before {
  content: "\f071";
}
.fa-plane:before {
  content: "\f072";
}
.fa-calendar:before {
  content: "\f073";
}
.fa-random:before {
  content: "\f074";
}
.fa-comment:before {
  content: "\f075";
}
.fa-magnet:before {
  content: "\f076";
}
.fa-chevron-up:before {
  content: "\f077";
}
.fa-chevron-down:before {
  content: "\f078";
}
.fa-retweet:before {
  content: "\f079";
}
.fa-shopping-cart:before {
  content: "\f07a";
}
.fa-folder:before {
  content: "\f07b";
}
.fa-folder-open:before {
  content: "\f07c";
}
.fa-arrows-v:before {
  content: "\f07d";
}
.fa-arrows-h:before {
  content: "\f07e";
}
.fa-bar-chart-o:before,
.fa-bar-chart:before {
  content: "\f080";
}
.fa-twitter-square:before {
  content: "\f081";
}
.fa-facebook-square:before {
  content: "\f082";
}
.fa-camera-retro:before {
  content: "\f083";
}
.fa-key:before {
  content: "\f084";
}
.fa-gears:before,
.fa-cogs:before {
  content: "\f085";
}
.fa-comments:before {
  content: "\f086";
}
.fa-thumbs-o-up:before {
  content: "\f087";
}
.fa-thumbs-o-down:before {
  content: "\f088";
}
.fa-star-half:before {
  content: "\f089";
}
.fa-heart-o:before {
  content: "\f08a";
}
.fa-sign-out:before {
  content: "\f08b";
}
.fa-linkedin-square:before {
  content: "\f08c";
}
.fa-thumb-tack:before {
  content: "\f08d";
}
.fa-external-link:before {
  content: "\f08e";
}
.fa-sign-in:before {
  content: "\f090";
}
.fa-trophy:before {
  content: "\f091";
}
.fa-github-square:before {
  content: "\f092";
}
.fa-upload:before {
  content: "\f093";
}
.fa-lemon-o:before {
  content: "\f094";
}
.fa-phone:before {
  content: "\f095";
}
.fa-square-o:before {
  content: "\f096";
}
.fa-bookmark-o:before {
  content: "\f097";
}
.fa-phone-square:before {
  content: "\f098";
}
.fa-twitter:before {
  content: "\f099";
}
.fa-facebook:before {
  content: "\f09a";
}
.fa-github:before {
  content: "\f09b";
}
.fa-unlock:before {
  content: "\f09c";
}
.fa-credit-card:before {
  content: "\f09d";
}
.fa-rss:before {
  content: "\f09e";
}
.fa-hdd-o:before {
  content: "\f0a0";
}
.fa-bullhorn:before {
  content: "\f0a1";
}
.fa-bell:before {
  content: "\f0f3";
}
.fa-certificate:before {
  content: "\f0a3";
}
.fa-hand-o-right:before {
  content: "\f0a4";
}
.fa-hand-o-left:before {
  content: "\f0a5";
}
.fa-hand-o-up:before {
  content: "\f0a6";
}
.fa-hand-o-down:before {
  content: "\f0a7";
}
.fa-arrow-circle-left:before {
  content: "\f0a8";
}
.fa-arrow-circle-right:before {
  content: "\f0a9";
}
.fa-arrow-circle-up:before {
  content: "\f0aa";
}
.fa-arrow-circle-down:before {
  content: "\f0ab";
}
.fa-globe:before {
  content: "\f0ac";
}
.fa-wrench:before {
  content: "\f0ad";
}
.fa-tasks:before {
  content: "\f0ae";
}
.fa-filter:before {
  content: "\f0b0";
}
.fa-briefcase:before {
  content: "\f0b1";
}
.fa-arrows-alt:before {
  content: "\f0b2";
}
.fa-group:before,
.fa-users:before {
  content: "\f0c0";
}
.fa-chain:before,
.fa-link:before {
  content: "\f0c1";
}
.fa-cloud:before {
  content: "\f0c2";
}
.fa-flask:before {
  content: "\f0c3";
}
.fa-cut:before,
.fa-scissors:before {
  content: "\f0c4";
}
.fa-copy:before,
.fa-files-o:before {
  content: "\f0c5";
}
.fa-paperclip:before {
  content: "\f0c6";
}
.fa-save:before,
.fa-floppy-o:before {
  content: "\f0c7";
}
.fa-square:before {
  content: "\f0c8";
}
.fa-navicon:before,
.fa-reorder:before,
.fa-bars:before {
  content: "\f0c9";
}
.fa-list-ul:before {
  content: "\f0ca";
}
.fa-list-ol:before {
  content: "\f0cb";
}
.fa-strikethrough:before {
  content: "\f0cc";
}
.fa-underline:before {
  content: "\f0cd";
}
.fa-table:before {
  content: "\f0ce";
}
.fa-magic:before {
  content: "\f0d0";
}
.fa-truck:before {
  content: "\f0d1";
}
.fa-pinterest:before {
  content: "\f0d2";
}
.fa-pinterest-square:before {
  content: "\f0d3";
}
.fa-google-plus-square:before {
  content: "\f0d4";
}
.fa-google-plus:before {
  content: "\f0d5";
}
.fa-money:before {
  content: "\f0d6";
}
.fa-caret-down:before {
  content: "\f0d7";
}
.fa-caret-up:before {
  content: "\f0d8";
}
.fa-caret-left:before {
  content: "\f0d9";
}
.fa-caret-right:before {
  content: "\f0da";
}
.fa-columns:before {
  content: "\f0db";
}
.fa-unsorted:before,
.fa-sort:before {
  content: "\f0dc";
}
.fa-sort-down:before,
.fa-sort-desc:before {
  content: "\f0dd";
}
.fa-sort-up:before,
.fa-sort-asc:before {
  content: "\f0de";
}
.fa-envelope:before {
  content: "\f0e0";
}
.fa-linkedin:before {
  content: "\f0e1";
}
.fa-rotate-left:before,
.fa-undo:before {
  content: "\f0e2";
}
.fa-legal:before,
.fa-gavel:before {
  content: "\f0e3";
}
.fa-dashboard:before,
.fa-tachometer:before {
  content: "\f0e4";
}
.fa-comment-o:before {
  content: "\f0e5";
}
.fa-comments-o:before {
  content: "\f0e6";
}
.fa-flash:before,
.fa-bolt:before {
  content: "\f0e7";
}
.fa-sitemap:before {
  content: "\f0e8";
}
.fa-umbrella:before {
  content: "\f0e9";
}
.fa-paste:before,
.fa-clipboard:before {
  content: "\f0ea";
}
.fa-lightbulb-o:before {
  content: "\f0eb";
}
.fa-exchange:before {
  content: "\f0ec";
}
.fa-cloud-download:before {
  content: "\f0ed";
}
.fa-cloud-upload:before {
  content: "\f0ee";
}
.fa-user-md:before {
  content: "\f0f0";
}
.fa-stethoscope:before {
  content: "\f0f1";
}
.fa-suitcase:before {
  content: "\f0f2";
}
.fa-bell-o:before {
  content: "\f0a2";
}
.fa-coffee:before {
  content: "\f0f4";
}
.fa-cutlery:before {
  content: "\f0f5";
}
.fa-file-text-o:before {
  content: "\f0f6";
}
.fa-building-o:before {
  content: "\f0f7";
}
.fa-hospital-o:before {
  content: "\f0f8";
}
.fa-ambulance:before {
  content: "\f0f9";
}
.fa-medkit:before {
  content: "\f0fa";
}
.fa-fighter-jet:before {
  content: "\f0fb";
}
.fa-beer:before {
  content: "\f0fc";
}
.fa-h-square:before {
  content: "\f0fd";
}
.fa-plus-square:before {
  content: "\f0fe";
}
.fa-angle-double-left:before {
  content: "\f100";
}
.fa-angle-double-right:before {
  content: "\f101";
}
.fa-angle-double-up:before {
  content: "\f102";
}
.fa-angle-double-down:before {
  content: "\f103";
}
.fa-angle-left:before {
  content: "\f104";
}
.fa-angle-right:before {
  content: "\f105";
}
.fa-angle-up:before {
  content: "\f106";
}
.fa-angle-down:before {
  content: "\f107";
}
.fa-desktop:before {
  content: "\f108";
}
.fa-laptop:before {
  content: "\f109";
}
.fa-tablet:before {
  content: "\f10a";
}
.fa-mobile-phone:before,
.fa-mobile:before {
  content: "\f10b";
}
.fa-circle-o:before {
  content: "\f10c";
}
.fa-quote-left:before {
  content: "\f10d";
}
.fa-quote-right:before {
  content: "\f10e";
}
.fa-spinner:before {
  content: "\f110";
}
.fa-circle:before {
  content: "\f111";
}
.fa-mail-reply:before,
.fa-reply:before {
  content: "\f112";
}
.fa-github-alt:before {
  content: "\f113";
}
.fa-folder-o:before {
  content: "\f114";
}
.fa-folder-open-o:before {
  content: "\f115";
}
.fa-smile-o:before {
  content: "\f118";
}
.fa-frown-o:before {
  content: "\f119";
}
.fa-meh-o:before {
  content: "\f11a";
}
.fa-gamepad:before {
  content: "\f11b";
}
.fa-keyboard-o:before {
  content: "\f11c";
}
.fa-flag-o:before {
  content: "\f11d";
}
.fa-flag-checkered:before {
  content: "\f11e";
}
.fa-terminal:before {
  content: "\f120";
}
.fa-code:before {
  content: "\f121";
}
.fa-mail-reply-all:before,
.fa-reply-all:before {
  content: "\f122";
}
.fa-star-half-empty:before,
.fa-star-half-full:before,
.fa-star-half-o:before {
  content: "\f123";
}
.fa-location-arrow:before {
  content: "\f124";
}
.fa-crop:before {
  content: "\f125";
}
.fa-code-fork:before {
  content: "\f126";
}
.fa-unlink:before,
.fa-chain-broken:before {
  content: "\f127";
}
.fa-question:before {
  content: "\f128";
}
.fa-info:before {
  content: "\f129";
}
.fa-exclamation:before {
  content: "\f12a";
}
.fa-superscript:before {
  content: "\f12b";
}
.fa-subscript:before {
  content: "\f12c";
}
.fa-eraser:before {
  content: "\f12d";
}
.fa-puzzle-piece:before {
  content: "\f12e";
}
.fa-microphone:before {
  content: "\f130";
}
.fa-microphone-slash:before {
  content: "\f131";
}
.fa-shield:before {
  content: "\f132";
}
.fa-calendar-o:before {
  content: "\f133";
}
.fa-fire-extinguisher:before {
  content: "\f134";
}
.fa-rocket:before {
  content: "\f135";
}
.fa-maxcdn:before {
  content: "\f136";
}
.fa-chevron-circle-left:before {
  content: "\f137";
}
.fa-chevron-circle-right:before {
  content: "\f138";
}
.fa-chevron-circle-up:before {
  content: "\f139";
}
.fa-chevron-circle-down:before {
  content: "\f13a";
}
.fa-html5:before {
  content: "\f13b";
}
.fa-css3:before {
  content: "\f13c";
}
.fa-anchor:before {
  content: "\f13d";
}
.fa-unlock-alt:before {
  content: "\f13e";
}
.fa-bullseye:before {
  content: "\f140";
}
.fa-ellipsis-h:before {
  content: "\f141";
}
.fa-ellipsis-v:before {
  content: "\f142";
}
.fa-rss-square:before {
  content: "\f143";
}
.fa-play-circle:before {
  content: "\f144";
}
.fa-ticket:before {
  content: "\f145";
}
.fa-minus-square:before {
  content: "\f146";
}
.fa-minus-square-o:before {
  content: "\f147";
}
.fa-level-up:before {
  content: "\f148";
}
.fa-level-down:before {
  content: "\f149";
}
.fa-check-square:before {
  content: "\f14a";
}
.fa-pencil-square:before {
  content: "\f14b";
}
.fa-external-link-square:before {
  content: "\f14c";
}
.fa-share-square:before {
  content: "\f14d";
}
.fa-compass:before {
  content: "\f14e";
}
.fa-toggle-down:before,
.fa-caret-square-o-down:before {
  content: "\f150";
}
.fa-toggle-up:before,
.fa-caret-square-o-up:before {
  content: "\f151";
}
.fa-toggle-right:before,
.fa-caret-square-o-right:before {
  content: "\f152";
}
.fa-euro:before,
.fa-eur:before {
  content: "\f153";
}
.fa-gbp:before {
  content: "\f154";
}
.fa-dollar:before,
.fa-usd:before {
  content: "\f155";
}
.fa-rupee:before,
.fa-inr:before {
  content: "\f156";
}
.fa-cny:before,
.fa-rmb:before,
.fa-yen:before,
.fa-jpy:before {
  content: "\f157";
}
.fa-ruble:before,
.fa-rouble:before,
.fa-rub:before {
  content: "\f158";
}
.fa-won:before,
.fa-krw:before {
  content: "\f159";
}
.fa-bitcoin:before,
.fa-btc:before {
  content: "\f15a";
}
.fa-file:before {
  content: "\f15b";
}
.fa-file-text:before {
  content: "\f15c";
}
.fa-sort-alpha-asc:before {
  content: "\f15d";
}
.fa-sort-alpha-desc:before {
  content: "\f15e";
}
.fa-sort-amount-asc:before {
  content: "\f160";
}
.fa-sort-amount-desc:before {
  content: "\f161";
}
.fa-sort-numeric-asc:before {
  content: "\f162";
}
.fa-sort-numeric-desc:before {
  content: "\f163";
}
.fa-thumbs-up:before {
  content: "\f164";
}
.fa-thumbs-down:before {
  content: "\f165";
}
.fa-youtube-square:before {
  content: "\f166";
}
.fa-youtube:before {
  content: "\f167";
}
.fa-xing:before {
  content: "\f168";
}
.fa-xing-square:before {
  content: "\f169";
}
.fa-youtube-play:before {
  content: "\f16a";
}
.fa-dropbox:before {
  content: "\f16b";
}
.fa-stack-overflow:before {
  content: "\f16c";
}
.fa-instagram:before {
  content: "\f16d";
}
.fa-flickr:before {
  content: "\f16e";
}
.fa-adn:before {
  content: "\f170";
}
.fa-bitbucket:before {
  content: "\f171";
}
.fa-bitbucket-square:before {
  content: "\f172";
}
.fa-tumblr:before {
  content: "\f173";
}
.fa-tumblr-square:before {
  content: "\f174";
}
.fa-long-arrow-down:before {
  content: "\f175";
}
.fa-long-arrow-up:before {
  content: "\f176";
}
.fa-long-arrow-left:before {
  content: "\f177";
}
.fa-long-arrow-right:before {
  content: "\f178";
}
.fa-apple:before {
  content: "\f179";
}
.fa-windows:before {
  content: "\f17a";
}
.fa-android:before {
  content: "\f17b";
}
.fa-linux:before {
  content: "\f17c";
}
.fa-dribbble:before {
  content: "\f17d";
}
.fa-skype:before {
  content: "\f17e";
}
.fa-foursquare:before {
  content: "\f180";
}
.fa-trello:before {
  content: "\f181";
}
.fa-female:before {
  content: "\f182";
}
.fa-male:before {
  content: "\f183";
}
.fa-gittip:before {
  content: "\f184";
}
.fa-sun-o:before {
  content: "\f185";
}
.fa-moon-o:before {
  content: "\f186";
}
.fa-archive:before {
  content: "\f187";
}
.fa-bug:before {
  content: "\f188";
}
.fa-vk:before {
  content: "\f189";
}
.fa-weibo:before {
  content: "\f18a";
}
.fa-renren:before {
  content: "\f18b";
}
.fa-pagelines:before {
  content: "\f18c";
}
.fa-stack-exchange:before {
  content: "\f18d";
}
.fa-arrow-circle-o-right:before {
  content: "\f18e";
}
.fa-arrow-circle-o-left:before {
  content: "\f190";
}
.fa-toggle-left:before,
.fa-caret-square-o-left:before {
  content: "\f191";
}
.fa-dot-circle-o:before {
  content: "\f192";
}
.fa-wheelchair:before {
  content: "\f193";
}
.fa-vimeo-square:before {
  content: "\f194";
}
.fa-turkish-lira:before,
.fa-try:before {
  content: "\f195";
}
.fa-plus-square-o:before {
  content: "\f196";
}
.fa-space-shuttle:before {
  content: "\f197";
}
.fa-slack:before {
  content: "\f198";
}
.fa-envelope-square:before {
  content: "\f199";
}
.fa-wordpress:before {
  content: "\f19a";
}
.fa-openid:before {
  content: "\f19b";
}
.fa-institution:before,
.fa-bank:before,
.fa-university:before {
  content: "\f19c";
}
.fa-mortar-board:before,
.fa-graduation-cap:before {
  content: "\f19d";
}
.fa-yahoo:before {
  content: "\f19e";
}
.fa-google:before {
  content: "\f1a0";
}
.fa-reddit:before {
  content: "\f1a1";
}
.fa-reddit-square:before {
  content: "\f1a2";
}
.fa-stumbleupon-circle:before {
  content: "\f1a3";
}
.fa-stumbleupon:before {
  content: "\f1a4";
}
.fa-delicious:before {
  content: "\f1a5";
}
.fa-digg:before {
  content: "\f1a6";
}
.fa-pied-piper:before {
  content: "\f1a7";
}
.fa-pied-piper-alt:before {
  content: "\f1a8";
}
.fa-drupal:before {
  content: "\f1a9";
}
.fa-joomla:before {
  content: "\f1aa";
}
.fa-language:before {
  content: "\f1ab";
}
.fa-fax:before {
  content: "\f1ac";
}
.fa-building:before {
  content: "\f1ad";
}
.fa-child:before {
  content: "\f1ae";
}
.fa-paw:before {
  content: "\f1b0";
}
.fa-spoon:before {
  content: "\f1b1";
}
.fa-cube:before {
  content: "\f1b2";
}
.fa-cubes:before {
  content: "\f1b3";
}
.fa-behance:before {
  content: "\f1b4";
}
.fa-behance-square:before {
  content: "\f1b5";
}
.fa-steam:before {
  content: "\f1b6";
}
.fa-steam-square:before {
  content: "\f1b7";
}
.fa-recycle:before {
  content: "\f1b8";
}
.fa-automobile:before,
.fa-car:before {
  content: "\f1b9";
}
.fa-cab:before,
.fa-taxi:before {
  content: "\f1ba";
}
.fa-tree:before {
  content: "\f1bb";
}
.fa-spotify:before {
  content: "\f1bc";
}
.fa-deviantart:before {
  content: "\f1bd";
}
.fa-soundcloud:before {
  content: "\f1be";
}
.fa-database:before {
  content: "\f1c0";
}
.fa-file-pdf-o:before {
  content: "\f1c1";
}
.fa-file-word-o:before {
  content: "\f1c2";
}
.fa-file-excel-o:before {
  content: "\f1c3";
}
.fa-file-powerpoint-o:before {
  content: "\f1c4";
}
.fa-file-photo-o:before,
.fa-file-picture-o:before,
.fa-file-image-o:before {
  content: "\f1c5";
}
.fa-file-zip-o:before,
.fa-file-archive-o:before {
  content: "\f1c6";
}
.fa-file-sound-o:before,
.fa-file-audio-o:before {
  content: "\f1c7";
}
.fa-file-movie-o:before,
.fa-file-video-o:before {
  content: "\f1c8";
}
.fa-file-code-o:before {
  content: "\f1c9";
}
.fa-vine:before {
  content: "\f1ca";
}
.fa-codepen:before {
  content: "\f1cb";
}
.fa-jsfiddle:before {
  content: "\f1cc";
}
.fa-life-bouy:before,
.fa-life-buoy:before,
.fa-life-saver:before,
.fa-support:before,
.fa-life-ring:before {
  content: "\f1cd";
}
.fa-circle-o-notch:before {
  content: "\f1ce";
}
.fa-ra:before,
.fa-rebel:before {
  content: "\f1d0";
}
.fa-ge:before,
.fa-empire:before {
  content: "\f1d1";
}
.fa-git-square:before {
  content: "\f1d2";
}
.fa-git:before {
  content: "\f1d3";
}
.fa-hacker-news:before {
  content: "\f1d4";
}
.fa-tencent-weibo:before {
  content: "\f1d5";
}
.fa-qq:before {
  content: "\f1d6";
}
.fa-wechat:before,
.fa-weixin:before {
  content: "\f1d7";
}
.fa-send:before,
.fa-paper-plane:before {
  content: "\f1d8";
}
.fa-send-o:before,
.fa-paper-plane-o:before {
  content: "\f1d9";
}
.fa-history:before {
  content: "\f1da";
}
.fa-circle-thin:before {
  content: "\f1db";
}
.fa-header:before {
  content: "\f1dc";
}
.fa-paragraph:before {
  content: "\f1dd";
}
.fa-sliders:before {
  content: "\f1de";
}
.fa-share-alt:before {
  content: "\f1e0";
}
.fa-share-alt-square:before {
  content: "\f1e1";
}
.fa-bomb:before {
  content: "\f1e2";
}
.fa-soccer-ball-o:before,
.fa-futbol-o:before {
  content: "\f1e3";
}
.fa-tty:before {
  content: "\f1e4";
}
.fa-binoculars:before {
  content: "\f1e5";
}
.fa-plug:before {
  content: "\f1e6";
}
.fa-slideshare:before {
  content: "\f1e7";
}
.fa-twitch:before {
  content: "\f1e8";
}
.fa-yelp:before {
  content: "\f1e9";
}
.fa-newspaper-o:before {
  content: "\f1ea";
}
.fa-wifi:before {
  content: "\f1eb";
}
.fa-calculator:before {
  content: "\f1ec";
}
.fa-paypal:before {
  content: "\f1ed";
}
.fa-google-wallet:before {
  content: "\f1ee";
}
.fa-cc-visa:before {
  content: "\f1f0";
}
.fa-cc-mastercard:before {
  content: "\f1f1";
}
.fa-cc-discover:before {
  content: "\f1f2";
}
.fa-cc-amex:before {
  content: "\f1f3";
}
.fa-cc-paypal:before {
  content: "\f1f4";
}
.fa-cc-stripe:before {
  content: "\f1f5";
}
.fa-bell-slash:before {
  content: "\f1f6";
}
.fa-bell-slash-o:before {
  content: "\f1f7";
}
.fa-trash:before {
  content: "\f1f8";
}
.fa-copyright:before {
  content: "\f1f9";
}
.fa-at:before {
  content: "\f1fa";
}
.fa-eyedropper:before {
  content: "\f1fb";
}
.fa-paint-brush:before {
  content: "\f1fc";
}
.fa-birthday-cake:before {
  content: "\f1fd";
}
.fa-area-chart:before {
  content: "\f1fe";
}
.fa-pie-chart:before {
  content: "\f200";
}
.fa-line-chart:before {
  content: "\f201";
}
.fa-lastfm:before {
  content: "\f202";
}
.fa-lastfm-square:before {
  content: "\f203";
}
.fa-toggle-off:before {
  content: "\f204";
}
.fa-toggle-on:before {
  content: "\f205";
}
.fa-bicycle:before {
  content: "\f206";
}
.fa-bus:before {
  content: "\f207";
}
.fa-ioxhost:before {
  content: "\f208";
}
.fa-angellist:before {
  content: "\f209";
}
.fa-cc:before {
  content: "\f20a";
}
.fa-shekel:before,
.fa-sheqel:before,
.fa-ils:before {
  content: "\f20b";
}
.fa-meanpath:before {
  content: "\f20c";
}
/*!
*
* IPython base
*
*/
.modal.fade .modal-dialog {
  -webkit-transform: translate(0, 0);
  -ms-transform: translate(0, 0);
  -o-transform: translate(0, 0);
  transform: translate(0, 0);
}
code {
  color: #000;
}
pre {
  font-size: inherit;
  line-height: inherit;
}
label {
  font-weight: normal;
}
/* Make the page background atleast 100% the height of the view port */
/* Make the page itself atleast 70% the height of the view port */
.border-box-sizing {
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
}
.corner-all {
  border-radius: 2px;
}
.no-padding {
  padding: 0px;
}
/* Flexible box model classes */
/* Taken from Alex Russell http://infrequently.org/2009/08/css-3-progress/ */
/* This file is a compatability layer.  It allows the usage of flexible box 
model layouts accross multiple browsers, including older browsers.  The newest,
universal implementation of the flexible box model is used when available (see
`Modern browsers` comments below).  Browsers that are known to implement this 
new spec completely include:

    Firefox 28.0+
    Chrome 29.0+
    Internet Explorer 11+ 
    Opera 17.0+

Browsers not listed, including Safari, are supported via the styling under the
`Old browsers` comments below.
*/
.hbox {
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: horizontal;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: horizontal;
  -moz-box-align: stretch;
  display: box;
  box-orient: horizontal;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: row;
  align-items: stretch;
}
.hbox > * {
  /* Old browsers */
  -webkit-box-flex: 0;
  -moz-box-flex: 0;
  box-flex: 0;
  /* Modern browsers */
  flex: none;
}
.vbox {
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: vertical;
  -moz-box-align: stretch;
  display: box;
  box-orient: vertical;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: column;
  align-items: stretch;
}
.vbox > * {
  /* Old browsers */
  -webkit-box-flex: 0;
  -moz-box-flex: 0;
  box-flex: 0;
  /* Modern browsers */
  flex: none;
}
.hbox.reverse,
.vbox.reverse,
.reverse {
  /* Old browsers */
  -webkit-box-direction: reverse;
  -moz-box-direction: reverse;
  box-direction: reverse;
  /* Modern browsers */
  flex-direction: row-reverse;
}
.hbox.box-flex0,
.vbox.box-flex0,
.box-flex0 {
  /* Old browsers */
  -webkit-box-flex: 0;
  -moz-box-flex: 0;
  box-flex: 0;
  /* Modern browsers */
  flex: none;
  width: auto;
}
.hbox.box-flex1,
.vbox.box-flex1,
.box-flex1 {
  /* Old browsers */
  -webkit-box-flex: 1;
  -moz-box-flex: 1;
  box-flex: 1;
  /* Modern browsers */
  flex: 1;
}
.hbox.box-flex,
.vbox.box-flex,
.box-flex {
  /* Old browsers */
  /* Old browsers */
  -webkit-box-flex: 1;
  -moz-box-flex: 1;
  box-flex: 1;
  /* Modern browsers */
  flex: 1;
}
.hbox.box-flex2,
.vbox.box-flex2,
.box-flex2 {
  /* Old browsers */
  -webkit-box-flex: 2;
  -moz-box-flex: 2;
  box-flex: 2;
  /* Modern browsers */
  flex: 2;
}
.box-group1 {
  /*  Deprecated */
  -webkit-box-flex-group: 1;
  -moz-box-flex-group: 1;
  box-flex-group: 1;
}
.box-group2 {
  /* Deprecated */
  -webkit-box-flex-group: 2;
  -moz-box-flex-group: 2;
  box-flex-group: 2;
}
.hbox.start,
.vbox.start,
.start {
  /* Old browsers */
  -webkit-box-pack: start;
  -moz-box-pack: start;
  box-pack: start;
  /* Modern browsers */
  justify-content: flex-start;
}
.hbox.end,
.vbox.end,
.end {
  /* Old browsers */
  -webkit-box-pack: end;
  -moz-box-pack: end;
  box-pack: end;
  /* Modern browsers */
  justify-content: flex-end;
}
.hbox.center,
.vbox.center,
.center {
  /* Old browsers */
  -webkit-box-pack: center;
  -moz-box-pack: center;
  box-pack: center;
  /* Modern browsers */
  justify-content: center;
}
.hbox.baseline,
.vbox.baseline,
.baseline {
  /* Old browsers */
  -webkit-box-pack: baseline;
  -moz-box-pack: baseline;
  box-pack: baseline;
  /* Modern browsers */
  justify-content: baseline;
}
.hbox.stretch,
.vbox.stretch,
.stretch {
  /* Old browsers */
  -webkit-box-pack: stretch;
  -moz-box-pack: stretch;
  box-pack: stretch;
  /* Modern browsers */
  justify-content: stretch;
}
.hbox.align-start,
.vbox.align-start,
.align-start {
  /* Old browsers */
  -webkit-box-align: start;
  -moz-box-align: start;
  box-align: start;
  /* Modern browsers */
  align-items: flex-start;
}
.hbox.align-end,
.vbox.align-end,
.align-end {
  /* Old browsers */
  -webkit-box-align: end;
  -moz-box-align: end;
  box-align: end;
  /* Modern browsers */
  align-items: flex-end;
}
.hbox.align-center,
.vbox.align-center,
.align-center {
  /* Old browsers */
  -webkit-box-align: center;
  -moz-box-align: center;
  box-align: center;
  /* Modern browsers */
  align-items: center;
}
.hbox.align-baseline,
.vbox.align-baseline,
.align-baseline {
  /* Old browsers */
  -webkit-box-align: baseline;
  -moz-box-align: baseline;
  box-align: baseline;
  /* Modern browsers */
  align-items: baseline;
}
.hbox.align-stretch,
.vbox.align-stretch,
.align-stretch {
  /* Old browsers */
  -webkit-box-align: stretch;
  -moz-box-align: stretch;
  box-align: stretch;
  /* Modern browsers */
  align-items: stretch;
}
div.error {
  margin: 2em;
  text-align: center;
}
div.error > h1 {
  font-size: 500%;
  line-height: normal;
}
div.error > p {
  font-size: 200%;
  line-height: normal;
}
div.traceback-wrapper {
  text-align: left;
  max-width: 800px;
  margin: auto;
}
/**
 * Primary styles
 *
 * Author: Jupyter Development Team
 */
body {
  background-color: #fff;
  /* This makes sure that the body covers the entire window and needs to
       be in a different element than the display: box in wrapper below */
  position: absolute;
  left: 0px;
  right: 0px;
  top: 0px;
  bottom: 0px;
  overflow: visible;
}
body > #header {
  /* Initially hidden to prevent FLOUC */
  display: none;
  background-color: #fff;
  /* Display over codemirror */
  position: relative;
  z-index: 100;
}
body > #header #header-container {
  padding-bottom: 5px;
  padding-top: 5px;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
}
body > #header .header-bar {
  width: 100%;
  height: 1px;
  background: #e7e7e7;
  margin-bottom: -1px;
}
@media print {
  body > #header {
    display: none !important;
  }
}
#header-spacer {
  width: 100%;
  visibility: hidden;
}
@media print {
  #header-spacer {
    display: none;
  }
}
#ipython_notebook {
  padding-left: 0px;
  padding-top: 1px;
  padding-bottom: 1px;
}
@media (max-width: 991px) {
  #ipython_notebook {
    margin-left: 10px;
  }
}
[dir="rtl"] #ipython_notebook {
  float: right !important;
}
#noscript {
  width: auto;
  padding-top: 16px;
  padding-bottom: 16px;
  text-align: center;
  font-size: 22px;
  color: red;
  font-weight: bold;
}
#ipython_notebook img {
  height: 28px;
}
#site {
  width: 100%;
  display: none;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  overflow: auto;
}
@media print {
  #site {
    height: auto !important;
  }
}
/* Smaller buttons */
.ui-button .ui-button-text {
  padding: 0.2em 0.8em;
  font-size: 77%;
}
input.ui-button {
  padding: 0.3em 0.9em;
}
span#login_widget {
  float: right;
}
span#login_widget > .button,
#logout {
  color: #333;
  background-color: #fff;
  border-color: #ccc;
}
span#login_widget > .button:focus,
#logout:focus,
span#login_widget > .button.focus,
#logout.focus {
  color: #333;
  background-color: #e6e6e6;
  border-color: #8c8c8c;
}
span#login_widget > .button:hover,
#logout:hover {
  color: #333;
  background-color: #e6e6e6;
  border-color: #adadad;
}
span#login_widget > .button:active,
#logout:active,
span#login_widget > .button.active,
#logout.active,
.open > .dropdown-togglespan#login_widget > .button,
.open > .dropdown-toggle#logout {
  color: #333;
  background-color: #e6e6e6;
  border-color: #adadad;
}
span#login_widget > .button:active:hover,
#logout:active:hover,
span#login_widget > .button.active:hover,
#logout.active:hover,
.open > .dropdown-togglespan#login_widget > .button:hover,
.open > .dropdown-toggle#logout:hover,
span#login_widget > .button:active:focus,
#logout:active:focus,
span#login_widget > .button.active:focus,
#logout.active:focus,
.open > .dropdown-togglespan#login_widget > .button:focus,
.open > .dropdown-toggle#logout:focus,
span#login_widget > .button:active.focus,
#logout:active.focus,
span#login_widget > .button.active.focus,
#logout.active.focus,
.open > .dropdown-togglespan#login_widget > .button.focus,
.open > .dropdown-toggle#logout.focus {
  color: #333;
  background-color: #d4d4d4;
  border-color: #8c8c8c;
}
span#login_widget > .button:active,
#logout:active,
span#login_widget > .button.active,
#logout.active,
.open > .dropdown-togglespan#login_widget > .button,
.open > .dropdown-toggle#logout {
  background-image: none;
}
span#login_widget > .button.disabled:hover,
#logout.disabled:hover,
span#login_widget > .button[disabled]:hover,
#logout[disabled]:hover,
fieldset[disabled] span#login_widget > .button:hover,
fieldset[disabled] #logout:hover,
span#login_widget > .button.disabled:focus,
#logout.disabled:focus,
span#login_widget > .button[disabled]:focus,
#logout[disabled]:focus,
fieldset[disabled] span#login_widget > .button:focus,
fieldset[disabled] #logout:focus,
span#login_widget > .button.disabled.focus,
#logout.disabled.focus,
span#login_widget > .button[disabled].focus,
#logout[disabled].focus,
fieldset[disabled] span#login_widget > .button.focus,
fieldset[disabled] #logout.focus {
  background-color: #fff;
  border-color: #ccc;
}
span#login_widget > .button .badge,
#logout .badge {
  color: #fff;
  background-color: #333;
}
.nav-header {
  text-transform: none;
}
#header > span {
  margin-top: 10px;
}
.modal_stretch .modal-dialog {
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: vertical;
  -moz-box-align: stretch;
  display: box;
  box-orient: vertical;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: column;
  align-items: stretch;
  min-height: 80vh;
}
.modal_stretch .modal-dialog .modal-body {
  max-height: calc(100vh - 200px);
  overflow: auto;
  flex: 1;
}
@media (min-width: 768px) {
  .modal .modal-dialog {
    width: 700px;
  }
}
@media (min-width: 768px) {
  select.form-control {
    margin-left: 12px;
    margin-right: 12px;
  }
}
/*!
*
* IPython auth
*
*/
.center-nav {
  display: inline-block;
  margin-bottom: -4px;
}
/*!
*
* IPython tree view
*
*/
/* We need an invisible input field on top of the sentense*/
/* "Drag file onto the list ..." */
.alternate_upload {
  background-color: none;
  display: inline;
}
.alternate_upload.form {
  padding: 0;
  margin: 0;
}
.alternate_upload input.fileinput {
  text-align: center;
  vertical-align: middle;
  display: inline;
  opacity: 0;
  z-index: 2;
  width: 12ex;
  margin-right: -12ex;
}
.alternate_upload .btn-upload {
  height: 22px;
}
/**
 * Primary styles
 *
 * Author: Jupyter Development Team
 */
[dir="rtl"] #tabs li {
  float: right;
}
ul#tabs {
  margin-bottom: 4px;
}
[dir="rtl"] ul#tabs {
  margin-right: 0px;
}
ul#tabs a {
  padding-top: 6px;
  padding-bottom: 4px;
}
ul.breadcrumb a:focus,
ul.breadcrumb a:hover {
  text-decoration: none;
}
ul.breadcrumb i.icon-home {
  font-size: 16px;
  margin-right: 4px;
}
ul.breadcrumb span {
  color: #5e5e5e;
}
.list_toolbar {
  padding: 4px 0 4px 0;
  vertical-align: middle;
}
.list_toolbar .tree-buttons {
  padding-top: 1px;
}
[dir="rtl"] .list_toolbar .tree-buttons {
  float: left !important;
}
[dir="rtl"] .list_toolbar .pull-right {
  padding-top: 1px;
  float: left !important;
}
[dir="rtl"] .list_toolbar .pull-left {
  float: right !important;
}
.dynamic-buttons {
  padding-top: 3px;
  display: inline-block;
}
.list_toolbar [class*="span"] {
  min-height: 24px;
}
.list_header {
  font-weight: bold;
  background-color: #EEE;
}
.list_placeholder {
  font-weight: bold;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 7px;
  padding-right: 7px;
}
.list_container {
  margin-top: 4px;
  margin-bottom: 20px;
  border: 1px solid #ddd;
  border-radius: 2px;
}
.list_container > div {
  border-bottom: 1px solid #ddd;
}
.list_container > div:hover .list-item {
  background-color: red;
}
.list_container > div:last-child {
  border: none;
}
.list_item:hover .list_item {
  background-color: #ddd;
}
.list_item a {
  text-decoration: none;
}
.list_item:hover {
  background-color: #fafafa;
}
.list_header > div,
.list_item > div {
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 7px;
  padding-right: 7px;
  line-height: 22px;
}
.list_header > div input,
.list_item > div input {
  margin-right: 7px;
  margin-left: 14px;
  vertical-align: baseline;
  line-height: 22px;
  position: relative;
  top: -1px;
}
.list_header > div .item_link,
.list_item > div .item_link {
  margin-left: -1px;
  vertical-align: baseline;
  line-height: 22px;
}
.new-file input[type=checkbox] {
  visibility: hidden;
}
.item_name {
  line-height: 22px;
  height: 24px;
}
.item_icon {
  font-size: 14px;
  color: #5e5e5e;
  margin-right: 7px;
  margin-left: 7px;
  line-height: 22px;
  vertical-align: baseline;
}
.item_buttons {
  line-height: 1em;
  margin-left: -5px;
}
.item_buttons .btn,
.item_buttons .btn-group,
.item_buttons .input-group {
  float: left;
}
.item_buttons > .btn,
.item_buttons > .btn-group,
.item_buttons > .input-group {
  margin-left: 5px;
}
.item_buttons .btn {
  min-width: 13ex;
}
.item_buttons .running-indicator {
  padding-top: 4px;
  color: #5cb85c;
}
.item_buttons .kernel-name {
  padding-top: 4px;
  color: #5bc0de;
  margin-right: 7px;
  float: left;
}
.toolbar_info {
  height: 24px;
  line-height: 24px;
}
.list_item input:not([type=checkbox]) {
  padding-top: 3px;
  padding-bottom: 3px;
  height: 22px;
  line-height: 14px;
  margin: 0px;
}
.highlight_text {
  color: blue;
}
#project_name {
  display: inline-block;
  padding-left: 7px;
  margin-left: -2px;
}
#project_name > .breadcrumb {
  padding: 0px;
  margin-bottom: 0px;
  background-color: transparent;
  font-weight: bold;
}
#tree-selector {
  padding-right: 0px;
}
[dir="rtl"] #tree-selector a {
  float: right;
}
#button-select-all {
  min-width: 50px;
}
#select-all {
  margin-left: 7px;
  margin-right: 2px;
}
.menu_icon {
  margin-right: 2px;
}
.tab-content .row {
  margin-left: 0px;
  margin-right: 0px;
}
.folder_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f114";
}
.folder_icon:before.pull-left {
  margin-right: .3em;
}
.folder_icon:before.pull-right {
  margin-left: .3em;
}
.notebook_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f02d";
  position: relative;
  top: -1px;
}
.notebook_icon:before.pull-left {
  margin-right: .3em;
}
.notebook_icon:before.pull-right {
  margin-left: .3em;
}
.running_notebook_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f02d";
  position: relative;
  top: -1px;
  color: #5cb85c;
}
.running_notebook_icon:before.pull-left {
  margin-right: .3em;
}
.running_notebook_icon:before.pull-right {
  margin-left: .3em;
}
.file_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f016";
  position: relative;
  top: -2px;
}
.file_icon:before.pull-left {
  margin-right: .3em;
}
.file_icon:before.pull-right {
  margin-left: .3em;
}
#notebook_toolbar .pull-right {
  padding-top: 0px;
  margin-right: -1px;
}
ul#new-menu {
  left: auto;
  right: 0;
}
[dir="rtl"] #new-menu {
  text-align: right;
}
.kernel-menu-icon {
  padding-right: 12px;
  width: 24px;
  content: "\f096";
}
.kernel-menu-icon:before {
  content: "\f096";
}
.kernel-menu-icon-current:before {
  content: "\f00c";
}
#tab_content {
  padding-top: 20px;
}
#running .panel-group .panel {
  margin-top: 3px;
  margin-bottom: 1em;
}
#running .panel-group .panel .panel-heading {
  background-color: #EEE;
  padding-top: 4px;
  padding-bottom: 4px;
  padding-left: 7px;
  padding-right: 7px;
  line-height: 22px;
}
#running .panel-group .panel .panel-heading a:focus,
#running .panel-group .panel .panel-heading a:hover {
  text-decoration: none;
}
#running .panel-group .panel .panel-body {
  padding: 0px;
}
#running .panel-group .panel .panel-body .list_container {
  margin-top: 0px;
  margin-bottom: 0px;
  border: 0px;
  border-radius: 0px;
}
#running .panel-group .panel .panel-body .list_container .list_item {
  border-bottom: 1px solid #ddd;
}
#running .panel-group .panel .panel-body .list_container .list_item:last-child {
  border-bottom: 0px;
}
[dir="rtl"] #running .col-sm-8 {
  float: right !important;
}
.delete-button {
  display: none;
}
.duplicate-button {
  display: none;
}
.rename-button {
  display: none;
}
.shutdown-button {
  display: none;
}
.dynamic-instructions {
  display: inline-block;
  padding-top: 4px;
}
/*!
*
* IPython text editor webapp
*
*/
.selected-keymap i.fa {
  padding: 0px 5px;
}
.selected-keymap i.fa:before {
  content: "\f00c";
}
#mode-menu {
  overflow: auto;
  max-height: 20em;
}
.edit_app #header {
  -webkit-box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
  box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
}
.edit_app #menubar .navbar {
  /* Use a negative 1 bottom margin, so the border overlaps the border of the
    header */
  margin-bottom: -1px;
}
.dirty-indicator {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  width: 20px;
}
.dirty-indicator.pull-left {
  margin-right: .3em;
}
.dirty-indicator.pull-right {
  margin-left: .3em;
}
.dirty-indicator-dirty {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  width: 20px;
}
.dirty-indicator-dirty.pull-left {
  margin-right: .3em;
}
.dirty-indicator-dirty.pull-right {
  margin-left: .3em;
}
.dirty-indicator-clean {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  width: 20px;
}
.dirty-indicator-clean.pull-left {
  margin-right: .3em;
}
.dirty-indicator-clean.pull-right {
  margin-left: .3em;
}
.dirty-indicator-clean:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f00c";
}
.dirty-indicator-clean:before.pull-left {
  margin-right: .3em;
}
.dirty-indicator-clean:before.pull-right {
  margin-left: .3em;
}
#filename {
  font-size: 16pt;
  display: table;
  padding: 0px 5px;
}
#current-mode {
  padding-left: 5px;
  padding-right: 5px;
}
#texteditor-backdrop {
  padding-top: 20px;
  padding-bottom: 20px;
}
@media not print {
  #texteditor-backdrop {
    background-color: #EEE;
  }
}
@media print {
  #texteditor-backdrop #texteditor-container .CodeMirror-gutter,
  #texteditor-backdrop #texteditor-container .CodeMirror-gutters {
    background-color: #fff;
  }
}
@media not print {
  #texteditor-backdrop #texteditor-container .CodeMirror-gutter,
  #texteditor-backdrop #texteditor-container .CodeMirror-gutters {
    background-color: #fff;
  }
}
@media not print {
  #texteditor-backdrop #texteditor-container {
    padding: 0px;
    background-color: #fff;
    -webkit-box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
    box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
  }
}
/*!
*
* IPython notebook
*
*/
/* CSS font colors for translated ANSI colors. */
.ansibold {
  font-weight: bold;
}
/* use dark versions for foreground, to improve visibility */
.ansiblack {
  color: black;
}
.ansired {
  color: darkred;
}
.ansigreen {
  color: darkgreen;
}
.ansiyellow {
  color: #c4a000;
}
.ansiblue {
  color: darkblue;
}
.ansipurple {
  color: darkviolet;
}
.ansicyan {
  color: steelblue;
}
.ansigray {
  color: gray;
}
/* and light for background, for the same reason */
.ansibgblack {
  background-color: black;
}
.ansibgred {
  background-color: red;
}
.ansibggreen {
  background-color: green;
}
.ansibgyellow {
  background-color: yellow;
}
.ansibgblue {
  background-color: blue;
}
.ansibgpurple {
  background-color: magenta;
}
.ansibgcyan {
  background-color: cyan;
}
.ansibggray {
  background-color: gray;
}
div.cell {
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: vertical;
  -moz-box-align: stretch;
  display: box;
  box-orient: vertical;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: column;
  align-items: stretch;
  border-radius: 2px;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  border-width: 1px;
  border-style: solid;
  border-color: transparent;
  width: 100%;
  padding: 5px;
  /* This acts as a spacer between cells, that is outside the border */
  margin: 0px;
  outline: none;
  border-left-width: 1px;
  padding-left: 5px;
  background: linear-gradient(to right, transparent -40px, transparent 1px, transparent 1px, transparent 100%);
}
div.cell.jupyter-soft-selected {
  border-left-color: #90CAF9;
  border-left-color: #E3F2FD;
  border-left-width: 1px;
  padding-left: 5px;
  border-right-color: #E3F2FD;
  border-right-width: 1px;
  background: #E3F2FD;
}
@media print {
  div.cell.jupyter-soft-selected {
    border-color: transparent;
  }
}
div.cell.selected {
  border-color: #ababab;
  border-left-width: 0px;
  padding-left: 6px;
  background: linear-gradient(to right, #42A5F5 -40px, #42A5F5 5px, transparent 5px, transparent 100%);
}
@media print {
  div.cell.selected {
    border-color: transparent;
  }
}
div.cell.selected.jupyter-soft-selected {
  border-left-width: 0;
  padding-left: 6px;
  background: linear-gradient(to right, #42A5F5 -40px, #42A5F5 7px, #E3F2FD 7px, #E3F2FD 100%);
}
.edit_mode div.cell.selected {
  border-color: #66BB6A;
  border-left-width: 0px;
  padding-left: 6px;
  background: linear-gradient(to right, #66BB6A -40px, #66BB6A 5px, transparent 5px, transparent 100%);
}
@media print {
  .edit_mode div.cell.selected {
    border-color: transparent;
  }
}
.prompt {
  /* This needs to be wide enough for 3 digit prompt numbers: In[100]: */
  min-width: 14ex;
  /* This padding is tuned to match the padding on the CodeMirror editor. */
  padding: 0.4em;
  margin: 0px;
  font-family: monospace;
  text-align: right;
  /* This has to match that of the the CodeMirror class line-height below */
  line-height: 1.21429em;
  /* Don't highlight prompt number selection */
  -webkit-touch-callout: none;
  -webkit-user-select: none;
  -khtml-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
  /* Use default cursor */
  cursor: default;
}
@media (max-width: 540px) {
  .prompt {
    text-align: left;
  }
}
div.inner_cell {
  min-width: 0;
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: vertical;
  -moz-box-align: stretch;
  display: box;
  box-orient: vertical;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: column;
  align-items: stretch;
  /* Old browsers */
  -webkit-box-flex: 1;
  -moz-box-flex: 1;
  box-flex: 1;
  /* Modern browsers */
  flex: 1;
}
/* input_area and input_prompt must match in top border and margin for alignment */
div.input_area {
  border: 1px solid #cfcfcf;
  border-radius: 2px;
  background: #f7f7f7;
  line-height: 1.21429em;
}
/* This is needed so that empty prompt areas can collapse to zero height when there
   is no content in the output_subarea and the prompt. The main purpose of this is
   to make sure that empty JavaScript output_subareas have no height. */
div.prompt:empty {
  padding-top: 0;
  padding-bottom: 0;
}
div.unrecognized_cell {
  padding: 5px 5px 5px 0px;
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: horizontal;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: horizontal;
  -moz-box-align: stretch;
  display: box;
  box-orient: horizontal;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: row;
  align-items: stretch;
}
div.unrecognized_cell .inner_cell {
  border-radius: 2px;
  padding: 5px;
  font-weight: bold;
  color: red;
  border: 1px solid #cfcfcf;
  background: #eaeaea;
}
div.unrecognized_cell .inner_cell a {
  color: inherit;
  text-decoration: none;
}
div.unrecognized_cell .inner_cell a:hover {
  color: inherit;
  text-decoration: none;
}
@media (max-width: 540px) {
  div.unrecognized_cell > div.prompt {
    display: none;
  }
}
div.code_cell {
  /* avoid page breaking on code cells when printing */
}
@media print {
  div.code_cell {
    page-break-inside: avoid;
  }
}
/* any special styling for code cells that are currently running goes here */
div.input {
  page-break-inside: avoid;
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: horizontal;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: horizontal;
  -moz-box-align: stretch;
  display: box;
  box-orient: horizontal;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: row;
  align-items: stretch;
}
@media (max-width: 540px) {
  div.input {
    /* Old browsers */
    display: -webkit-box;
    -webkit-box-orient: vertical;
    -webkit-box-align: stretch;
    display: -moz-box;
    -moz-box-orient: vertical;
    -moz-box-align: stretch;
    display: box;
    box-orient: vertical;
    box-align: stretch;
    /* Modern browsers */
    display: flex;
    flex-direction: column;
    align-items: stretch;
  }
}
/* input_area and input_prompt must match in top border and margin for alignment */
div.input_prompt {
  color: #303F9F;
  border-top: 1px solid transparent;
}
div.input_area > div.highlight {
  margin: 0.4em;
  border: none;
  padding: 0px;
  background-color: transparent;
}
div.input_area > div.highlight > pre {
  margin: 0px;
  border: none;
  padding: 0px;
  background-color: transparent;
}
/* The following gets added to the <head> if it is detected that the user has a
 * monospace font with inconsistent normal/bold/italic height.  See
 * notebookmain.js.  Such fonts will have keywords vertically offset with
 * respect to the rest of the text.  The user should select a better font.
 * See: https://github.com/ipython/ipython/issues/1503
 *
 * .CodeMirror span {
 *      vertical-align: bottom;
 * }
 */
.CodeMirror {
  line-height: 1.21429em;
  /* Changed from 1em to our global default */
  font-size: 14px;
  height: auto;
  /* Changed to auto to autogrow */
  background: none;
  /* Changed from white to allow our bg to show through */
}
.CodeMirror-scroll {
  /*  The CodeMirror docs are a bit fuzzy on if overflow-y should be hidden or visible.*/
  /*  We have found that if it is visible, vertical scrollbars appear with font size changes.*/
  overflow-y: hidden;
  overflow-x: auto;
}
.CodeMirror-lines {
  /* In CM2, this used to be 0.4em, but in CM3 it went to 4px. We need the em value because */
  /* we have set a different line-height and want this to scale with that. */
  padding: 0.4em;
}
.CodeMirror-linenumber {
  padding: 0 8px 0 4px;
}
.CodeMirror-gutters {
  border-bottom-left-radius: 2px;
  border-top-left-radius: 2px;
}
.CodeMirror pre {
  /* In CM3 this went to 4px from 0 in CM2. We need the 0 value because of how we size */
  /* .CodeMirror-lines */
  padding: 0;
  border: 0;
  border-radius: 0;
}
/*

Original style from softwaremaniacs.org (c) Ivan Sagalaev <Maniac@SoftwareManiacs.Org>
Adapted from GitHub theme

*/
.highlight-base {
  color: #000;
}
.highlight-variable {
  color: #000;
}
.highlight-variable-2 {
  color: #1a1a1a;
}
.highlight-variable-3 {
  color: #333333;
}
.highlight-string {
  color: #BA2121;
}
.highlight-comment {
  color: #408080;
  font-style: italic;
}
.highlight-number {
  color: #080;
}
.highlight-atom {
  color: #88F;
}
.highlight-keyword {
  color: #008000;
  font-weight: bold;
}
.highlight-builtin {
  color: #008000;
}
.highlight-error {
  color: #f00;
}
.highlight-operator {
  color: #AA22FF;
  font-weight: bold;
}
.highlight-meta {
  color: #AA22FF;
}
/* previously not defined, copying from default codemirror */
.highlight-def {
  color: #00f;
}
.highlight-string-2 {
  color: #f50;
}
.highlight-qualifier {
  color: #555;
}
.highlight-bracket {
  color: #997;
}
.highlight-tag {
  color: #170;
}
.highlight-attribute {
  color: #00c;
}
.highlight-header {
  color: blue;
}
.highlight-quote {
  color: #090;
}
.highlight-link {
  color: #00c;
}
/* apply the same style to codemirror */
.cm-s-ipython span.cm-keyword {
  color: #008000;
  font-weight: bold;
}
.cm-s-ipython span.cm-atom {
  color: #88F;
}
.cm-s-ipython span.cm-number {
  color: #080;
}
.cm-s-ipython span.cm-def {
  color: #00f;
}
.cm-s-ipython span.cm-variable {
  color: #000;
}
.cm-s-ipython span.cm-operator {
  color: #AA22FF;
  font-weight: bold;
}
.cm-s-ipython span.cm-variable-2 {
  color: #1a1a1a;
}
.cm-s-ipython span.cm-variable-3 {
  color: #333333;
}
.cm-s-ipython span.cm-comment {
  color: #408080;
  font-style: italic;
}
.cm-s-ipython span.cm-string {
  color: #BA2121;
}
.cm-s-ipython span.cm-string-2 {
  color: #f50;
}
.cm-s-ipython span.cm-meta {
  color: #AA22FF;
}
.cm-s-ipython span.cm-qualifier {
  color: #555;
}
.cm-s-ipython span.cm-builtin {
  color: #008000;
}
.cm-s-ipython span.cm-bracket {
  color: #997;
}
.cm-s-ipython span.cm-tag {
  color: #170;
}
.cm-s-ipython span.cm-attribute {
  color: #00c;
}
.cm-s-ipython span.cm-header {
  color: blue;
}
.cm-s-ipython span.cm-quote {
  color: #090;
}
.cm-s-ipython span.cm-link {
  color: #00c;
}
.cm-s-ipython span.cm-error {
  color: #f00;
}
.cm-s-ipython span.cm-tab {
  background: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADAAAAAMCAYAAAAkuj5RAAAAAXNSR0IArs4c6QAAAGFJREFUSMft1LsRQFAQheHPowAKoACx3IgEKtaEHujDjORSgWTH/ZOdnZOcM/sgk/kFFWY0qV8foQwS4MKBCS3qR6ixBJvElOobYAtivseIE120FaowJPN75GMu8j/LfMwNjh4HUpwg4LUAAAAASUVORK5CYII=);
  background-position: right;
  background-repeat: no-repeat;
}
div.output_wrapper {
  /* this position must be relative to enable descendents to be absolute within it */
  position: relative;
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: vertical;
  -moz-box-align: stretch;
  display: box;
  box-orient: vertical;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: column;
  align-items: stretch;
  z-index: 1;
}
/* class for the output area when it should be height-limited */
div.output_scroll {
  /* ideally, this would be max-height, but FF barfs all over that */
  height: 24em;
  /* FF needs this *and the wrapper* to specify full width, or it will shrinkwrap */
  width: 100%;
  overflow: auto;
  border-radius: 2px;
  -webkit-box-shadow: inset 0 2px 8px rgba(0, 0, 0, 0.8);
  box-shadow: inset 0 2px 8px rgba(0, 0, 0, 0.8);
  display: block;
}
/* output div while it is collapsed */
div.output_collapsed {
  margin: 0px;
  padding: 0px;
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: vertical;
  -moz-box-align: stretch;
  display: box;
  box-orient: vertical;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: column;
  align-items: stretch;
}
div.out_prompt_overlay {
  height: 100%;
  padding: 0px 0.4em;
  position: absolute;
  border-radius: 2px;
}
div.out_prompt_overlay:hover {
  /* use inner shadow to get border that is computed the same on WebKit/FF */
  -webkit-box-shadow: inset 0 0 1px #000;
  box-shadow: inset 0 0 1px #000;
  background: rgba(240, 240, 240, 0.5);
}
div.output_prompt {
  color: #D84315;
}
/* This class is the outer container of all output sections. */
div.output_area {
  padding: 0px;
  page-break-inside: avoid;
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: horizontal;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: horizontal;
  -moz-box-align: stretch;
  display: box;
  box-orient: horizontal;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: row;
  align-items: stretch;
}
div.output_area .MathJax_Display {
  text-align: left !important;
}
div.output_area .rendered_html table {
  margin-left: 0;
  margin-right: 0;
}
div.output_area .rendered_html img {
  margin-left: 0;
  margin-right: 0;
}
div.output_area img,
div.output_area svg {
  max-width: 100%;
  height: auto;
}
div.output_area img.unconfined,
div.output_area svg.unconfined {
  max-width: none;
}
/* This is needed to protect the pre formating from global settings such
   as that of bootstrap */
.output {
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: vertical;
  -moz-box-align: stretch;
  display: box;
  box-orient: vertical;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: column;
  align-items: stretch;
}
@media (max-width: 540px) {
  div.output_area {
    /* Old browsers */
    display: -webkit-box;
    -webkit-box-orient: vertical;
    -webkit-box-align: stretch;
    display: -moz-box;
    -moz-box-orient: vertical;
    -moz-box-align: stretch;
    display: box;
    box-orient: vertical;
    box-align: stretch;
    /* Modern browsers */
    display: flex;
    flex-direction: column;
    align-items: stretch;
  }
}
div.output_area pre {
  margin: 0;
  padding: 0;
  border: 0;
  vertical-align: baseline;
  color: black;
  background-color: transparent;
  border-radius: 0;
}
/* This class is for the output subarea inside the output_area and after
   the prompt div. */
div.output_subarea {
  overflow-x: auto;
  padding: 0.4em;
  /* Old browsers */
  -webkit-box-flex: 1;
  -moz-box-flex: 1;
  box-flex: 1;
  /* Modern browsers */
  flex: 1;
  max-width: calc(100% - 14ex);
}
div.output_scroll div.output_subarea {
  overflow-x: visible;
}
/* The rest of the output_* classes are for special styling of the different
   output types */
/* all text output has this class: */
div.output_text {
  text-align: left;
  color: #000;
  /* This has to match that of the the CodeMirror class line-height below */
  line-height: 1.21429em;
}
/* stdout/stderr are 'text' as well as 'stream', but execute_result/error are *not* streams */
div.output_stderr {
  background: #fdd;
  /* very light red background for stderr */
}
div.output_latex {
  text-align: left;
}
/* Empty output_javascript divs should have no height */
div.output_javascript:empty {
  padding: 0;
}
.js-error {
  color: darkred;
}
/* raw_input styles */
div.raw_input_container {
  line-height: 1.21429em;
  padding-top: 5px;
}
pre.raw_input_prompt {
  /* nothing needed here. */
}
input.raw_input {
  font-family: monospace;
  font-size: inherit;
  color: inherit;
  width: auto;
  /* make sure input baseline aligns with prompt */
  vertical-align: baseline;
  /* padding + margin = 0.5em between prompt and cursor */
  padding: 0em 0.25em;
  margin: 0em 0.25em;
}
input.raw_input:focus {
  box-shadow: none;
}
p.p-space {
  margin-bottom: 10px;
}
div.output_unrecognized {
  padding: 5px;
  font-weight: bold;
  color: red;
}
div.output_unrecognized a {
  color: inherit;
  text-decoration: none;
}
div.output_unrecognized a:hover {
  color: inherit;
  text-decoration: none;
}
.rendered_html {
  color: #000;
  /* any extras will just be numbers: */
}
.rendered_html em {
  font-style: italic;
}
.rendered_html strong {
  font-weight: bold;
}
.rendered_html u {
  text-decoration: underline;
}
.rendered_html :link {
  text-decoration: underline;
}
.rendered_html :visited {
  text-decoration: underline;
}
.rendered_html h1 {
  font-size: 185.7%;
  margin: 1.08em 0 0 0;
  font-weight: bold;
  line-height: 1.0;
}
.rendered_html h2 {
  font-size: 157.1%;
  margin: 1.27em 0 0 0;
  font-weight: bold;
  line-height: 1.0;
}
.rendered_html h3 {
  font-size: 128.6%;
  margin: 1.55em 0 0 0;
  font-weight: bold;
  line-height: 1.0;
}
.rendered_html h4 {
  font-size: 100%;
  margin: 2em 0 0 0;
  font-weight: bold;
  line-height: 1.0;
}
.rendered_html h5 {
  font-size: 100%;
  margin: 2em 0 0 0;
  font-weight: bold;
  line-height: 1.0;
  font-style: italic;
}
.rendered_html h6 {
  font-size: 100%;
  margin: 2em 0 0 0;
  font-weight: bold;
  line-height: 1.0;
  font-style: italic;
}
.rendered_html h1:first-child {
  margin-top: 0.538em;
}
.rendered_html h2:first-child {
  margin-top: 0.636em;
}
.rendered_html h3:first-child {
  margin-top: 0.777em;
}
.rendered_html h4:first-child {
  margin-top: 1em;
}
.rendered_html h5:first-child {
  margin-top: 1em;
}
.rendered_html h6:first-child {
  margin-top: 1em;
}
.rendered_html ul {
  list-style: disc;
  margin: 0em 2em;
  padding-left: 0px;
}
.rendered_html ul ul {
  list-style: square;
  margin: 0em 2em;
}
.rendered_html ul ul ul {
  list-style: circle;
  margin: 0em 2em;
}
.rendered_html ol {
  list-style: decimal;
  margin: 0em 2em;
  padding-left: 0px;
}
.rendered_html ol ol {
  list-style: upper-alpha;
  margin: 0em 2em;
}
.rendered_html ol ol ol {
  list-style: lower-alpha;
  margin: 0em 2em;
}
.rendered_html ol ol ol ol {
  list-style: lower-roman;
  margin: 0em 2em;
}
.rendered_html ol ol ol ol ol {
  list-style: decimal;
  margin: 0em 2em;
}
.rendered_html * + ul {
  margin-top: 1em;
}
.rendered_html * + ol {
  margin-top: 1em;
}
.rendered_html hr {
  color: black;
  background-color: black;
}
.rendered_html pre {
  margin: 1em 2em;
}
.rendered_html pre,
.rendered_html code {
  border: 0;
  background-color: #fff;
  color: #000;
  font-size: 100%;
  padding: 0px;
}
.rendered_html blockquote {
  margin: 1em 2em;
}
.rendered_html table {
  margin-left: auto;
  margin-right: auto;
  border: 1px solid black;
  border-collapse: collapse;
}
.rendered_html tr,
.rendered_html th,
.rendered_html td {
  border: 1px solid black;
  border-collapse: collapse;
  margin: 1em 2em;
}
.rendered_html td,
.rendered_html th {
  text-align: left;
  vertical-align: middle;
  padding: 4px;
}
.rendered_html th {
  font-weight: bold;
}
.rendered_html * + table {
  margin-top: 1em;
}
.rendered_html p {
  text-align: left;
}
.rendered_html * + p {
  margin-top: 1em;
}
.rendered_html img {
  display: block;
  margin-left: auto;
  margin-right: auto;
}
.rendered_html * + img {
  margin-top: 1em;
}
.rendered_html img,
.rendered_html svg {
  max-width: 100%;
  height: auto;
}
.rendered_html img.unconfined,
.rendered_html svg.unconfined {
  max-width: none;
}
div.text_cell {
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: horizontal;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: horizontal;
  -moz-box-align: stretch;
  display: box;
  box-orient: horizontal;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: row;
  align-items: stretch;
}
@media (max-width: 540px) {
  div.text_cell > div.prompt {
    display: none;
  }
}
div.text_cell_render {
  /*font-family: "Helvetica Neue", Arial, Helvetica, Geneva, sans-serif;*/
  outline: none;
  resize: none;
  width: inherit;
  border-style: none;
  padding: 0.5em 0.5em 0.5em 0.4em;
  color: #000;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
}
a.anchor-link:link {
  text-decoration: none;
  padding: 0px 20px;
  visibility: hidden;
}
h1:hover .anchor-link,
h2:hover .anchor-link,
h3:hover .anchor-link,
h4:hover .anchor-link,
h5:hover .anchor-link,
h6:hover .anchor-link {
  visibility: visible;
}
.text_cell.rendered .input_area {
  display: none;
}
.text_cell.rendered .rendered_html {
  overflow-x: auto;
  overflow-y: hidden;
}
.text_cell.unrendered .text_cell_render {
  display: none;
}
.cm-header-1,
.cm-header-2,
.cm-header-3,
.cm-header-4,
.cm-header-5,
.cm-header-6 {
  font-weight: bold;
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
}
.cm-header-1 {
  font-size: 185.7%;
}
.cm-header-2 {
  font-size: 157.1%;
}
.cm-header-3 {
  font-size: 128.6%;
}
.cm-header-4 {
  font-size: 110%;
}
.cm-header-5 {
  font-size: 100%;
  font-style: italic;
}
.cm-header-6 {
  font-size: 100%;
  font-style: italic;
}
/*!
*
* IPython notebook webapp
*
*/
@media (max-width: 767px) {
  .notebook_app {
    padding-left: 0px;
    padding-right: 0px;
  }
}
#ipython-main-app {
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  height: 100%;
}
div#notebook_panel {
  margin: 0px;
  padding: 0px;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  height: 100%;
}
div#notebook {
  font-size: 14px;
  line-height: 20px;
  overflow-y: hidden;
  overflow-x: auto;
  width: 100%;
  /* This spaces the page away from the edge of the notebook area */
  padding-top: 20px;
  margin: 0px;
  outline: none;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  min-height: 100%;
}
@media not print {
  #notebook-container {
    padding: 15px;
    background-color: #fff;
    min-height: 0;
    -webkit-box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
    box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
  }
}
@media print {
  #notebook-container {
    width: 100%;
  }
}
div.ui-widget-content {
  border: 1px solid #ababab;
  outline: none;
}
pre.dialog {
  background-color: #f7f7f7;
  border: 1px solid #ddd;
  border-radius: 2px;
  padding: 0.4em;
  padding-left: 2em;
}
p.dialog {
  padding: 0.2em;
}
/* Word-wrap output correctly.  This is the CSS3 spelling, though Firefox seems
   to not honor it correctly.  Webkit browsers (Chrome, rekonq, Safari) do.
 */
pre,
code,
kbd,
samp {
  white-space: pre-wrap;
}
#fonttest {
  font-family: monospace;
}
p {
  margin-bottom: 0;
}
.end_space {
  min-height: 100px;
  transition: height .2s ease;
}
.notebook_app > #header {
  -webkit-box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
  box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
}
@media not print {
  .notebook_app {
    background-color: #EEE;
  }
}
kbd {
  border-style: solid;
  border-width: 1px;
  box-shadow: none;
  margin: 2px;
  padding-left: 2px;
  padding-right: 2px;
  padding-top: 1px;
  padding-bottom: 1px;
}
/* CSS for the cell toolbar */
.celltoolbar {
  border: thin solid #CFCFCF;
  border-bottom: none;
  background: #EEE;
  border-radius: 2px 2px 0px 0px;
  width: 100%;
  height: 29px;
  padding-right: 4px;
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: horizontal;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: horizontal;
  -moz-box-align: stretch;
  display: box;
  box-orient: horizontal;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: row;
  align-items: stretch;
  /* Old browsers */
  -webkit-box-pack: end;
  -moz-box-pack: end;
  box-pack: end;
  /* Modern browsers */
  justify-content: flex-end;
  display: -webkit-flex;
}
@media print {
  .celltoolbar {
    display: none;
  }
}
.ctb_hideshow {
  display: none;
  vertical-align: bottom;
}
/* ctb_show is added to the ctb_hideshow div to show the cell toolbar.
   Cell toolbars are only shown when the ctb_global_show class is also set.
*/
.ctb_global_show .ctb_show.ctb_hideshow {
  display: block;
}
.ctb_global_show .ctb_show + .input_area,
.ctb_global_show .ctb_show + div.text_cell_input,
.ctb_global_show .ctb_show ~ div.text_cell_render {
  border-top-right-radius: 0px;
  border-top-left-radius: 0px;
}
.ctb_global_show .ctb_show ~ div.text_cell_render {
  border: 1px solid #cfcfcf;
}
.celltoolbar {
  font-size: 87%;
  padding-top: 3px;
}
.celltoolbar select {
  display: block;
  width: 100%;
  height: 32px;
  padding: 6px 12px;
  font-size: 13px;
  line-height: 1.42857143;
  color: #555555;
  background-color: #fff;
  background-image: none;
  border: 1px solid #ccc;
  border-radius: 2px;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075);
  -webkit-transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
  -o-transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
  transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
  height: 30px;
  padding: 5px 10px;
  font-size: 12px;
  line-height: 1.5;
  border-radius: 1px;
  width: inherit;
  font-size: inherit;
  height: 22px;
  padding: 0px;
  display: inline-block;
}
.celltoolbar select:focus {
  border-color: #66afe9;
  outline: 0;
  -webkit-box-shadow: inset 0 1px 1px rgba(0,0,0,.075), 0 0 8px rgba(102, 175, 233, 0.6);
  box-shadow: inset 0 1px 1px rgba(0,0,0,.075), 0 0 8px rgba(102, 175, 233, 0.6);
}
.celltoolbar select::-moz-placeholder {
  color: #999;
  opacity: 1;
}
.celltoolbar select:-ms-input-placeholder {
  color: #999;
}
.celltoolbar select::-webkit-input-placeholder {
  color: #999;
}
.celltoolbar select::-ms-expand {
  border: 0;
  background-color: transparent;
}
.celltoolbar select[disabled],
.celltoolbar select[readonly],
fieldset[disabled] .celltoolbar select {
  background-color: #eeeeee;
  opacity: 1;
}
.celltoolbar select[disabled],
fieldset[disabled] .celltoolbar select {
  cursor: not-allowed;
}
textarea.celltoolbar select {
  height: auto;
}
select.celltoolbar select {
  height: 30px;
  line-height: 30px;
}
textarea.celltoolbar select,
select[multiple].celltoolbar select {
  height: auto;
}
.celltoolbar label {
  margin-left: 5px;
  margin-right: 5px;
}
.completions {
  position: absolute;
  z-index: 110;
  overflow: hidden;
  border: 1px solid #ababab;
  border-radius: 2px;
  -webkit-box-shadow: 0px 6px 10px -1px #adadad;
  box-shadow: 0px 6px 10px -1px #adadad;
  line-height: 1;
}
.completions select {
  background: white;
  outline: none;
  border: none;
  padding: 0px;
  margin: 0px;
  overflow: auto;
  font-family: monospace;
  font-size: 110%;
  color: #000;
  width: auto;
}
.completions select option.context {
  color: #286090;
}
#kernel_logo_widget {
  float: right !important;
  float: right;
}
#kernel_logo_widget .current_kernel_logo {
  display: none;
  margin-top: -1px;
  margin-bottom: -1px;
  width: 32px;
  height: 32px;
}
#menubar {
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  margin-top: 1px;
}
#menubar .navbar {
  border-top: 1px;
  border-radius: 0px 0px 2px 2px;
  margin-bottom: 0px;
}
#menubar .navbar-toggle {
  float: left;
  padding-top: 7px;
  padding-bottom: 7px;
  border: none;
}
#menubar .navbar-collapse {
  clear: left;
}
.nav-wrapper {
  border-bottom: 1px solid #e7e7e7;
}
i.menu-icon {
  padding-top: 4px;
}
ul#help_menu li a {
  overflow: hidden;
  padding-right: 2.2em;
}
ul#help_menu li a i {
  margin-right: -1.2em;
}
.dropdown-submenu {
  position: relative;
}
.dropdown-submenu > .dropdown-menu {
  top: 0;
  left: 100%;
  margin-top: -6px;
  margin-left: -1px;
}
.dropdown-submenu:hover > .dropdown-menu {
  display: block;
}
.dropdown-submenu > a:after {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  display: block;
  content: "\f0da";
  float: right;
  color: #333333;
  margin-top: 2px;
  margin-right: -10px;
}
.dropdown-submenu > a:after.pull-left {
  margin-right: .3em;
}
.dropdown-submenu > a:after.pull-right {
  margin-left: .3em;
}
.dropdown-submenu:hover > a:after {
  color: #262626;
}
.dropdown-submenu.pull-left {
  float: none;
}
.dropdown-submenu.pull-left > .dropdown-menu {
  left: -100%;
  margin-left: 10px;
}
#notification_area {
  float: right !important;
  float: right;
  z-index: 10;
}
.indicator_area {
  float: right !important;
  float: right;
  color: #777;
  margin-left: 5px;
  margin-right: 5px;
  width: 11px;
  z-index: 10;
  text-align: center;
  width: auto;
}
#kernel_indicator {
  float: right !important;
  float: right;
  color: #777;
  margin-left: 5px;
  margin-right: 5px;
  width: 11px;
  z-index: 10;
  text-align: center;
  width: auto;
  border-left: 1px solid;
}
#kernel_indicator .kernel_indicator_name {
  padding-left: 5px;
  padding-right: 5px;
}
#modal_indicator {
  float: right !important;
  float: right;
  color: #777;
  margin-left: 5px;
  margin-right: 5px;
  width: 11px;
  z-index: 10;
  text-align: center;
  width: auto;
}
#readonly-indicator {
  float: right !important;
  float: right;
  color: #777;
  margin-left: 5px;
  margin-right: 5px;
  width: 11px;
  z-index: 10;
  text-align: center;
  width: auto;
  margin-top: 2px;
  margin-bottom: 0px;
  margin-left: 0px;
  margin-right: 0px;
  display: none;
}
.modal_indicator:before {
  width: 1.28571429em;
  text-align: center;
}
.edit_mode .modal_indicator:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f040";
}
.edit_mode .modal_indicator:before.pull-left {
  margin-right: .3em;
}
.edit_mode .modal_indicator:before.pull-right {
  margin-left: .3em;
}
.command_mode .modal_indicator:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: ' ';
}
.command_mode .modal_indicator:before.pull-left {
  margin-right: .3em;
}
.command_mode .modal_indicator:before.pull-right {
  margin-left: .3em;
}
.kernel_idle_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f10c";
}
.kernel_idle_icon:before.pull-left {
  margin-right: .3em;
}
.kernel_idle_icon:before.pull-right {
  margin-left: .3em;
}
.kernel_busy_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f111";
}
.kernel_busy_icon:before.pull-left {
  margin-right: .3em;
}
.kernel_busy_icon:before.pull-right {
  margin-left: .3em;
}
.kernel_dead_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f1e2";
}
.kernel_dead_icon:before.pull-left {
  margin-right: .3em;
}
.kernel_dead_icon:before.pull-right {
  margin-left: .3em;
}
.kernel_disconnected_icon:before {
  display: inline-block;
  font: normal normal normal 14px/1 FontAwesome;
  font-size: inherit;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  content: "\f127";
}
.kernel_disconnected_icon:before.pull-left {
  margin-right: .3em;
}
.kernel_disconnected_icon:before.pull-right {
  margin-left: .3em;
}
.notification_widget {
  color: #777;
  z-index: 10;
  background: rgba(240, 240, 240, 0.5);
  margin-right: 4px;
  color: #333;
  background-color: #fff;
  border-color: #ccc;
}
.notification_widget:focus,
.notification_widget.focus {
  color: #333;
  background-color: #e6e6e6;
  border-color: #8c8c8c;
}
.notification_widget:hover {
  color: #333;
  background-color: #e6e6e6;
  border-color: #adadad;
}
.notification_widget:active,
.notification_widget.active,
.open > .dropdown-toggle.notification_widget {
  color: #333;
  background-color: #e6e6e6;
  border-color: #adadad;
}
.notification_widget:active:hover,
.notification_widget.active:hover,
.open > .dropdown-toggle.notification_widget:hover,
.notification_widget:active:focus,
.notification_widget.active:focus,
.open > .dropdown-toggle.notification_widget:focus,
.notification_widget:active.focus,
.notification_widget.active.focus,
.open > .dropdown-toggle.notification_widget.focus {
  color: #333;
  background-color: #d4d4d4;
  border-color: #8c8c8c;
}
.notification_widget:active,
.notification_widget.active,
.open > .dropdown-toggle.notification_widget {
  background-image: none;
}
.notification_widget.disabled:hover,
.notification_widget[disabled]:hover,
fieldset[disabled] .notification_widget:hover,
.notification_widget.disabled:focus,
.notification_widget[disabled]:focus,
fieldset[disabled] .notification_widget:focus,
.notification_widget.disabled.focus,
.notification_widget[disabled].focus,
fieldset[disabled] .notification_widget.focus {
  background-color: #fff;
  border-color: #ccc;
}
.notification_widget .badge {
  color: #fff;
  background-color: #333;
}
.notification_widget.warning {
  color: #fff;
  background-color: #f0ad4e;
  border-color: #eea236;
}
.notification_widget.warning:focus,
.notification_widget.warning.focus {
  color: #fff;
  background-color: #ec971f;
  border-color: #985f0d;
}
.notification_widget.warning:hover {
  color: #fff;
  background-color: #ec971f;
  border-color: #d58512;
}
.notification_widget.warning:active,
.notification_widget.warning.active,
.open > .dropdown-toggle.notification_widget.warning {
  color: #fff;
  background-color: #ec971f;
  border-color: #d58512;
}
.notification_widget.warning:active:hover,
.notification_widget.warning.active:hover,
.open > .dropdown-toggle.notification_widget.warning:hover,
.notification_widget.warning:active:focus,
.notification_widget.warning.active:focus,
.open > .dropdown-toggle.notification_widget.warning:focus,
.notification_widget.warning:active.focus,
.notification_widget.warning.active.focus,
.open > .dropdown-toggle.notification_widget.warning.focus {
  color: #fff;
  background-color: #d58512;
  border-color: #985f0d;
}
.notification_widget.warning:active,
.notification_widget.warning.active,
.open > .dropdown-toggle.notification_widget.warning {
  background-image: none;
}
.notification_widget.warning.disabled:hover,
.notification_widget.warning[disabled]:hover,
fieldset[disabled] .notification_widget.warning:hover,
.notification_widget.warning.disabled:focus,
.notification_widget.warning[disabled]:focus,
fieldset[disabled] .notification_widget.warning:focus,
.notification_widget.warning.disabled.focus,
.notification_widget.warning[disabled].focus,
fieldset[disabled] .notification_widget.warning.focus {
  background-color: #f0ad4e;
  border-color: #eea236;
}
.notification_widget.warning .badge {
  color: #f0ad4e;
  background-color: #fff;
}
.notification_widget.success {
  color: #fff;
  background-color: #5cb85c;
  border-color: #4cae4c;
}
.notification_widget.success:focus,
.notification_widget.success.focus {
  color: #fff;
  background-color: #449d44;
  border-color: #255625;
}
.notification_widget.success:hover {
  color: #fff;
  background-color: #449d44;
  border-color: #398439;
}
.notification_widget.success:active,
.notification_widget.success.active,
.open > .dropdown-toggle.notification_widget.success {
  color: #fff;
  background-color: #449d44;
  border-color: #398439;
}
.notification_widget.success:active:hover,
.notification_widget.success.active:hover,
.open > .dropdown-toggle.notification_widget.success:hover,
.notification_widget.success:active:focus,
.notification_widget.success.active:focus,
.open > .dropdown-toggle.notification_widget.success:focus,
.notification_widget.success:active.focus,
.notification_widget.success.active.focus,
.open > .dropdown-toggle.notification_widget.success.focus {
  color: #fff;
  background-color: #398439;
  border-color: #255625;
}
.notification_widget.success:active,
.notification_widget.success.active,
.open > .dropdown-toggle.notification_widget.success {
  background-image: none;
}
.notification_widget.success.disabled:hover,
.notification_widget.success[disabled]:hover,
fieldset[disabled] .notification_widget.success:hover,
.notification_widget.success.disabled:focus,
.notification_widget.success[disabled]:focus,
fieldset[disabled] .notification_widget.success:focus,
.notification_widget.success.disabled.focus,
.notification_widget.success[disabled].focus,
fieldset[disabled] .notification_widget.success.focus {
  background-color: #5cb85c;
  border-color: #4cae4c;
}
.notification_widget.success .badge {
  color: #5cb85c;
  background-color: #fff;
}
.notification_widget.info {
  color: #fff;
  background-color: #5bc0de;
  border-color: #46b8da;
}
.notification_widget.info:focus,
.notification_widget.info.focus {
  color: #fff;
  background-color: #31b0d5;
  border-color: #1b6d85;
}
.notification_widget.info:hover {
  color: #fff;
  background-color: #31b0d5;
  border-color: #269abc;
}
.notification_widget.info:active,
.notification_widget.info.active,
.open > .dropdown-toggle.notification_widget.info {
  color: #fff;
  background-color: #31b0d5;
  border-color: #269abc;
}
.notification_widget.info:active:hover,
.notification_widget.info.active:hover,
.open > .dropdown-toggle.notification_widget.info:hover,
.notification_widget.info:active:focus,
.notification_widget.info.active:focus,
.open > .dropdown-toggle.notification_widget.info:focus,
.notification_widget.info:active.focus,
.notification_widget.info.active.focus,
.open > .dropdown-toggle.notification_widget.info.focus {
  color: #fff;
  background-color: #269abc;
  border-color: #1b6d85;
}
.notification_widget.info:active,
.notification_widget.info.active,
.open > .dropdown-toggle.notification_widget.info {
  background-image: none;
}
.notification_widget.info.disabled:hover,
.notification_widget.info[disabled]:hover,
fieldset[disabled] .notification_widget.info:hover,
.notification_widget.info.disabled:focus,
.notification_widget.info[disabled]:focus,
fieldset[disabled] .notification_widget.info:focus,
.notification_widget.info.disabled.focus,
.notification_widget.info[disabled].focus,
fieldset[disabled] .notification_widget.info.focus {
  background-color: #5bc0de;
  border-color: #46b8da;
}
.notification_widget.info .badge {
  color: #5bc0de;
  background-color: #fff;
}
.notification_widget.danger {
  color: #fff;
  background-color: #d9534f;
  border-color: #d43f3a;
}
.notification_widget.danger:focus,
.notification_widget.danger.focus {
  color: #fff;
  background-color: #c9302c;
  border-color: #761c19;
}
.notification_widget.danger:hover {
  color: #fff;
  background-color: #c9302c;
  border-color: #ac2925;
}
.notification_widget.danger:active,
.notification_widget.danger.active,
.open > .dropdown-toggle.notification_widget.danger {
  color: #fff;
  background-color: #c9302c;
  border-color: #ac2925;
}
.notification_widget.danger:active:hover,
.notification_widget.danger.active:hover,
.open > .dropdown-toggle.notification_widget.danger:hover,
.notification_widget.danger:active:focus,
.notification_widget.danger.active:focus,
.open > .dropdown-toggle.notification_widget.danger:focus,
.notification_widget.danger:active.focus,
.notification_widget.danger.active.focus,
.open > .dropdown-toggle.notification_widget.danger.focus {
  color: #fff;
  background-color: #ac2925;
  border-color: #761c19;
}
.notification_widget.danger:active,
.notification_widget.danger.active,
.open > .dropdown-toggle.notification_widget.danger {
  background-image: none;
}
.notification_widget.danger.disabled:hover,
.notification_widget.danger[disabled]:hover,
fieldset[disabled] .notification_widget.danger:hover,
.notification_widget.danger.disabled:focus,
.notification_widget.danger[disabled]:focus,
fieldset[disabled] .notification_widget.danger:focus,
.notification_widget.danger.disabled.focus,
.notification_widget.danger[disabled].focus,
fieldset[disabled] .notification_widget.danger.focus {
  background-color: #d9534f;
  border-color: #d43f3a;
}
.notification_widget.danger .badge {
  color: #d9534f;
  background-color: #fff;
}
div#pager {
  background-color: #fff;
  font-size: 14px;
  line-height: 20px;
  overflow: hidden;
  display: none;
  position: fixed;
  bottom: 0px;
  width: 100%;
  max-height: 50%;
  padding-top: 8px;
  -webkit-box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
  box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
  /* Display over codemirror */
  z-index: 100;
  /* Hack which prevents jquery ui resizable from changing top. */
  top: auto !important;
}
div#pager pre {
  line-height: 1.21429em;
  color: #000;
  background-color: #f7f7f7;
  padding: 0.4em;
}
div#pager #pager-button-area {
  position: absolute;
  top: 8px;
  right: 20px;
}
div#pager #pager-contents {
  position: relative;
  overflow: auto;
  width: 100%;
  height: 100%;
}
div#pager #pager-contents #pager-container {
  position: relative;
  padding: 15px 0px;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
}
div#pager .ui-resizable-handle {
  top: 0px;
  height: 8px;
  background: #f7f7f7;
  border-top: 1px solid #cfcfcf;
  border-bottom: 1px solid #cfcfcf;
  /* This injects handle bars (a short, wide = symbol) for 
        the resize handle. */
}
div#pager .ui-resizable-handle::after {
  content: '';
  top: 2px;
  left: 50%;
  height: 3px;
  width: 30px;
  margin-left: -15px;
  position: absolute;
  border-top: 1px solid #cfcfcf;
}
.quickhelp {
  /* Old browsers */
  display: -webkit-box;
  -webkit-box-orient: horizontal;
  -webkit-box-align: stretch;
  display: -moz-box;
  -moz-box-orient: horizontal;
  -moz-box-align: stretch;
  display: box;
  box-orient: horizontal;
  box-align: stretch;
  /* Modern browsers */
  display: flex;
  flex-direction: row;
  align-items: stretch;
  line-height: 1.8em;
}
.shortcut_key {
  display: inline-block;
  width: 21ex;
  text-align: right;
  font-family: monospace;
}
.shortcut_descr {
  display: inline-block;
  /* Old browsers */
  -webkit-box-flex: 1;
  -moz-box-flex: 1;
  box-flex: 1;
  /* Modern browsers */
  flex: 1;
}
span.save_widget {
  margin-top: 6px;
}
span.save_widget span.filename {
  height: 1em;
  line-height: 1em;
  padding: 3px;
  margin-left: 16px;
  border: none;
  font-size: 146.5%;
  border-radius: 2px;
}
span.save_widget span.filename:hover {
  background-color: #e6e6e6;
}
span.checkpoint_status,
span.autosave_status {
  font-size: small;
}
@media (max-width: 767px) {
  span.save_widget {
    font-size: small;
  }
  span.checkpoint_status,
  span.autosave_status {
    display: none;
  }
}
@media (min-width: 768px) and (max-width: 991px) {
  span.checkpoint_status {
    display: none;
  }
  span.autosave_status {
    font-size: x-small;
  }
}
.toolbar {
  padding: 0px;
  margin-left: -5px;
  margin-top: 2px;
  margin-bottom: 5px;
  box-sizing: border-box;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
}
.toolbar select,
.toolbar label {
  width: auto;
  vertical-align: middle;
  margin-right: 2px;
  margin-bottom: 0px;
  display: inline;
  font-size: 92%;
  margin-left: 0.3em;
  margin-right: 0.3em;
  padding: 0px;
  padding-top: 3px;
}
.toolbar .btn {
  padding: 2px 8px;
}
.toolbar .btn-group {
  margin-top: 0px;
  margin-left: 5px;
}
#maintoolbar {
  margin-bottom: -3px;
  margin-top: -8px;
  border: 0px;
  min-height: 27px;
  margin-left: 0px;
  padding-top: 11px;
  padding-bottom: 3px;
}
#maintoolbar .navbar-text {
  float: none;
  vertical-align: middle;
  text-align: right;
  margin-left: 5px;
  margin-right: 0px;
  margin-top: 0px;
}
.select-xs {
  height: 24px;
}
.pulse,
.dropdown-menu > li > a.pulse,
li.pulse > a.dropdown-toggle,
li.pulse.open > a.dropdown-toggle {
  background-color: #F37626;
  color: white;
}
/**
 * Primary styles
 *
 * Author: Jupyter Development Team
 */
/** WARNING IF YOU ARE EDITTING THIS FILE, if this is a .css file, It has a lot
 * of chance of beeing generated from the ../less/[samename].less file, you can
 * try to get back the less file by reverting somme commit in history
 **/
/*
 * We'll try to get something pretty, so we
 * have some strange css to have the scroll bar on
 * the left with fix button on the top right of the tooltip
 */
@-moz-keyframes fadeOut {
  from {
    opacity: 1;
  }
  to {
    opacity: 0;
  }
}
@-webkit-keyframes fadeOut {
  from {
    opacity: 1;
  }
  to {
    opacity: 0;
  }
}
@-moz-keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
@-webkit-keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
/*properties of tooltip after "expand"*/
.bigtooltip {
  overflow: auto;
  height: 200px;
  -webkit-transition-property: height;
  -webkit-transition-duration: 500ms;
  -moz-transition-property: height;
  -moz-transition-duration: 500ms;
  transition-property: height;
  transition-duration: 500ms;
}
/*properties of tooltip before "expand"*/
.smalltooltip {
  -webkit-transition-property: height;
  -webkit-transition-duration: 500ms;
  -moz-transition-property: height;
  -moz-transition-duration: 500ms;
  transition-property: height;
  transition-duration: 500ms;
  text-overflow: ellipsis;
  overflow: hidden;
  height: 80px;
}
.tooltipbuttons {
  position: absolute;
  padding-right: 15px;
  top: 0px;
  right: 0px;
}
.tooltiptext {
  /*avoid the button to overlap on some docstring*/
  padding-right: 30px;
}
.ipython_tooltip {
  max-width: 700px;
  /*fade-in animation when inserted*/
  -webkit-animation: fadeOut 400ms;
  -moz-animation: fadeOut 400ms;
  animation: fadeOut 400ms;
  -webkit-animation: fadeIn 400ms;
  -moz-animation: fadeIn 400ms;
  animation: fadeIn 400ms;
  vertical-align: middle;
  background-color: #f7f7f7;
  overflow: visible;
  border: #ababab 1px solid;
  outline: none;
  padding: 3px;
  margin: 0px;
  padding-left: 7px;
  font-family: monospace;
  min-height: 50px;
  -moz-box-shadow: 0px 6px 10px -1px #adadad;
  -webkit-box-shadow: 0px 6px 10px -1px #adadad;
  box-shadow: 0px 6px 10px -1px #adadad;
  border-radius: 2px;
  position: absolute;
  z-index: 1000;
}
.ipython_tooltip a {
  float: right;
}
.ipython_tooltip .tooltiptext pre {
  border: 0;
  border-radius: 0;
  font-size: 100%;
  background-color: #f7f7f7;
}
.pretooltiparrow {
  left: 0px;
  margin: 0px;
  top: -16px;
  width: 40px;
  height: 16px;
  overflow: hidden;
  position: absolute;
}
.pretooltiparrow:before {
  background-color: #f7f7f7;
  border: 1px #ababab solid;
  z-index: 11;
  content: "";
  position: absolute;
  left: 15px;
  top: 10px;
  width: 25px;
  height: 25px;
  -webkit-transform: rotate(45deg);
  -moz-transform: rotate(45deg);
  -ms-transform: rotate(45deg);
  -o-transform: rotate(45deg);
}
ul.typeahead-list i {
  margin-left: -10px;
  width: 18px;
}
ul.typeahead-list {
  max-height: 80vh;
  overflow: auto;
}
ul.typeahead-list > li > a {
  /** Firefox bug **/
  /* see https://github.com/jupyter/notebook/issues/559 */
  white-space: normal;
}
.cmd-palette .modal-body {
  padding: 7px;
}
.cmd-palette form {
  background: white;
}
.cmd-palette input {
  outline: none;
}
.no-shortcut {
  display: none;
}
.command-shortcut:before {
  content: "(command)";
  padding-right: 3px;
  color: #777777;
}
.edit-shortcut:before {
  content: "(edit)";
  padding-right: 3px;
  color: #777777;
}
#find-and-replace #replace-preview .match,
#find-and-replace #replace-preview .insert {
  background-color: #BBDEFB;
  border-color: #90CAF9;
  border-style: solid;
  border-width: 1px;
  border-radius: 0px;
}
#find-and-replace #replace-preview .replace .match {
  background-color: #FFCDD2;
  border-color: #EF9A9A;
  border-radius: 0px;
}
#find-and-replace #replace-preview .replace .insert {
  background-color: #C8E6C9;
  border-color: #A5D6A7;
  border-radius: 0px;
}
#find-and-replace #replace-preview {
  max-height: 60vh;
  overflow: auto;
}
#find-and-replace #replace-preview pre {
  padding: 5px 10px;
}
.terminal-app {
  background: #EEE;
}
.terminal-app #header {
  background: #fff;
  -webkit-box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
  box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.2);
}
.terminal-app .terminal {
  width: 100%;
  float: left;
  font-family: monospace;
  color: white;
  background: black;
  padding: 0.4em;
  border-radius: 2px;
  -webkit-box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.4);
  box-shadow: 0px 0px 12px 1px rgba(87, 87, 87, 0.4);
}
.terminal-app .terminal,
.terminal-app .terminal dummy-screen {
  line-height: 1em;
  font-size: 14px;
}
.terminal-app .terminal .xterm-rows {
  padding: 10px;
}
.terminal-app .terminal-cursor {
  color: black;
  background: white;
}
.terminal-app #terminado-container {
  margin-top: 20px;
}
/*# sourceMappingURL=style.min.css.map */
    </style>
<style type="text/css">
    .highlight .hll { background-color: #ffffcc }
.highlight  { background: #f8f8f8; }
.highlight .c { color: #408080; font-style: italic } /* Comment */
.highlight .err { border: 1px solid #FF0000 } /* Error */
.highlight .k { color: #008000; font-weight: bold } /* Keyword */
.highlight .o { color: #666666 } /* Operator */
.highlight .ch { color: #408080; font-style: italic } /* Comment.Hashbang */
.highlight .cm { color: #408080; font-style: italic } /* Comment.Multiline */
.highlight .cp { color: #BC7A00 } /* Comment.Preproc */
.highlight .cpf { color: #408080; font-style: italic } /* Comment.PreprocFile */
.highlight .c1 { color: #408080; font-style: italic } /* Comment.Single */
.highlight .cs { color: #408080; font-style: italic } /* Comment.Special */
.highlight .gd { color: #A00000 } /* Generic.Deleted */
.highlight .ge { font-style: italic } /* Generic.Emph */
.highlight .gr { color: #FF0000 } /* Generic.Error */
.highlight .gh { color: #000080; font-weight: bold } /* Generic.Heading */
.highlight .gi { color: #00A000 } /* Generic.Inserted */
.highlight .go { color: #888888 } /* Generic.Output */
.highlight .gp { color: #000080; font-weight: bold } /* Generic.Prompt */
.highlight .gs { font-weight: bold } /* Generic.Strong */
.highlight .gu { color: #800080; font-weight: bold } /* Generic.Subheading */
.highlight .gt { color: #0044DD } /* Generic.Traceback */
.highlight .kc { color: #008000; font-weight: bold } /* Keyword.Constant */
.highlight .kd { color: #008000; font-weight: bold } /* Keyword.Declaration */
.highlight .kn { color: #008000; font-weight: bold } /* Keyword.Namespace */
.highlight .kp { color: #008000 } /* Keyword.Pseudo */
.highlight .kr { color: #008000; font-weight: bold } /* Keyword.Reserved */
.highlight .kt { color: #B00040 } /* Keyword.Type */
.highlight .m { color: #666666 } /* Literal.Number */
.highlight .s { color: #BA2121 } /* Literal.String */
.highlight .na { color: #7D9029 } /* Name.Attribute */
.highlight .nb { color: #008000 } /* Name.Builtin */
.highlight .nc { color: #0000FF; font-weight: bold } /* Name.Class */
.highlight .no { color: #880000 } /* Name.Constant */
.highlight .nd { color: #AA22FF } /* Name.Decorator */
.highlight .ni { color: #999999; font-weight: bold } /* Name.Entity */
.highlight .ne { color: #D2413A; font-weight: bold } /* Name.Exception */
.highlight .nf { color: #0000FF } /* Name.Function */
.highlight .nl { color: #A0A000 } /* Name.Label */
.highlight .nn { color: #0000FF; font-weight: bold } /* Name.Namespace */
.highlight .nt { color: #008000; font-weight: bold } /* Name.Tag */
.highlight .nv { color: #19177C } /* Name.Variable */
.highlight .ow { color: #AA22FF; font-weight: bold } /* Operator.Word */
.highlight .w { color: #bbbbbb } /* Text.Whitespace */
.highlight .mb { color: #666666 } /* Literal.Number.Bin */
.highlight .mf { color: #666666 } /* Literal.Number.Float */
.highlight .mh { color: #666666 } /* Literal.Number.Hex */
.highlight .mi { color: #666666 } /* Literal.Number.Integer */
.highlight .mo { color: #666666 } /* Literal.Number.Oct */
.highlight .sa { color: #BA2121 } /* Literal.String.Affix */
.highlight .sb { color: #BA2121 } /* Literal.String.Backtick */
.highlight .sc { color: #BA2121 } /* Literal.String.Char */
.highlight .dl { color: #BA2121 } /* Literal.String.Delimiter */
.highlight .sd { color: #BA2121; font-style: italic } /* Literal.String.Doc */
.highlight .s2 { color: #BA2121 } /* Literal.String.Double */
.highlight .se { color: #BB6622; font-weight: bold } /* Literal.String.Escape */
.highlight .sh { color: #BA2121 } /* Literal.String.Heredoc */
.highlight .si { color: #BB6688; font-weight: bold } /* Literal.String.Interpol */
.highlight .sx { color: #008000 } /* Literal.String.Other */
.highlight .sr { color: #BB6688 } /* Literal.String.Regex */
.highlight .s1 { color: #BA2121 } /* Literal.String.Single */
.highlight .ss { color: #19177C } /* Literal.String.Symbol */
.highlight .bp { color: #008000 } /* Name.Builtin.Pseudo */
.highlight .fm { color: #0000FF } /* Name.Function.Magic */
.highlight .vc { color: #19177C } /* Name.Variable.Class */
.highlight .vg { color: #19177C } /* Name.Variable.Global */
.highlight .vi { color: #19177C } /* Name.Variable.Instance */
.highlight .vm { color: #19177C } /* Name.Variable.Magic */
.highlight .il { color: #666666 } /* Literal.Number.Integer.Long */
    </style>
<style type="text/css">
    
/* Temporary definitions which will become obsolete with Notebook release 5.0 */
.ansi-black-fg { color: #3E424D; }
.ansi-black-bg { background-color: #3E424D; }
.ansi-black-intense-fg { color: #282C36; }
.ansi-black-intense-bg { background-color: #282C36; }
.ansi-red-fg { color: #E75C58; }
.ansi-red-bg { background-color: #E75C58; }
.ansi-red-intense-fg { color: #B22B31; }
.ansi-red-intense-bg { background-color: #B22B31; }
.ansi-green-fg { color: #00A250; }
.ansi-green-bg { background-color: #00A250; }
.ansi-green-intense-fg { color: #007427; }
.ansi-green-intense-bg { background-color: #007427; }
.ansi-yellow-fg { color: #DDB62B; }
.ansi-yellow-bg { background-color: #DDB62B; }
.ansi-yellow-intense-fg { color: #B27D12; }
.ansi-yellow-intense-bg { background-color: #B27D12; }
.ansi-blue-fg { color: #208FFB; }
.ansi-blue-bg { background-color: #208FFB; }
.ansi-blue-intense-fg { color: #0065CA; }
.ansi-blue-intense-bg { background-color: #0065CA; }
.ansi-magenta-fg { color: #D160C4; }
.ansi-magenta-bg { background-color: #D160C4; }
.ansi-magenta-intense-fg { color: #A03196; }
.ansi-magenta-intense-bg { background-color: #A03196; }
.ansi-cyan-fg { color: #60C6C8; }
.ansi-cyan-bg { background-color: #60C6C8; }
.ansi-cyan-intense-fg { color: #258F8F; }
.ansi-cyan-intense-bg { background-color: #258F8F; }
.ansi-white-fg { color: #C5C1B4; }
.ansi-white-bg { background-color: #C5C1B4; }
.ansi-white-intense-fg { color: #A1A6B2; }
.ansi-white-intense-bg { background-color: #A1A6B2; }

.ansi-bold { font-weight: bold; }

    </style>


<style type="text/css">
/* Overrides of notebook CSS for static HTML export */
body {
  overflow: visible;
  padding: 8px;
}

div#notebook {
  overflow: visible;
  border-top: none;
}@media print {
  div.cell {
    display: block;
    page-break-inside: avoid;
  } 
  div.output_wrapper { 
    display: block;
    page-break-inside: avoid; 
  }
  div.output { 
    display: block;
    page-break-inside: avoid; 
  }
}
</style>

<!-- Custom stylesheet, it must be in the same directory as the html file -->
<!-- <link rel="stylesheet" href="custom.css"> -->

<!-- Loading mathjax macro -->
<!-- Load mathjax -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.1/MathJax.js?config=TeX-AMS_HTML"></script>
    <!-- MathJax configuration -->
    <script type="text/x-mathjax-config">
    MathJax.Hub.Config({
        tex2jax: {
            inlineMath: [ ['$','$'], ["\\(","\\)"] ],
            displayMath: [ ['$$','$$'], ["\\[","\\]"] ],
            processEscapes: true,
            processEnvironments: true
        },
        // Center justify equations in code and markdown cells. Elsewhere
        // we use CSS to left justify single line equations in code cells.
        displayAlign: 'center',
        "HTML-CSS": {
            styles: {'.MathJax_Display': {"margin": 0}},
            linebreaks: { automatic: true }
        }
    });
    </script>
    <!-- End of mathjax configuration --></head>
<body>
  <div tabindex="-1" id="notebook" class="border-box-sizing">
    <div class="container" id="notebook-container">

<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="PySPPL:-Introduction">PySPPL: Introduction<a class="anchor-link" href="#PySPPL:-Introduction">&#182;</a></h1><p>Python SPPL is a probabilistic programming language that is built for enabling one to perform inference in probabilistic programs that require gradient based inference algorithms. As <code>if-else</code> statements within probabilistic programs that use gradient based inference, take on two different forms. On one hand hand <code>if-else</code> have the usual programmer interpretation, but on the other, when random variables are placed inside of the predicate, or the body of an <code>if-else</code> expression, then we must treat those variables with care as discontinuities arise at point of indecision. We must ensure that at this indecision boundary the discontinuity, with respect to space it is in and the measure imposed on it, has a measure of zero.</p>
<p>Our framework was built to ensure that certain criteria in the compiled output of a directed acyclic graphical model are met. The language is extensible enough for one to add their own custom built potentials; which could be either log joint densities or loss functions, within the framework. There is a higher layer inference framework that takes advantage of PySPPL called <a href="https://github.com/bradleygramhansen/pyfo">pyfo</a>, we are actively developing this. The corresponding paper is called <a href="https://arxiv.org/abs/1804.03523">Discontinuous Hamiltonian Monte Carlo for Probabilistic Programs</a>.</p>
<p>In this walk-through we shall go through the basics of how to write a model and how to compile the model. In the following walk-through we shall show how to use custom density functions, how add other distributions within the framework and how to take advantage of the translation rules that are embedded within the language.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="PySPPL-imports">PySPPL imports<a class="anchor-link" href="#PySPPL-imports">&#182;</a></h2>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[3]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="o">%</span><span class="k">matplotlib</span> inline
<span class="kn">from</span> <span class="nn">pyppl</span> <span class="k">import</span> <span class="n">compile_model</span> 
<span class="kn">from</span> <span class="nn">pyppl.utils.core</span> <span class="k">import</span> <span class="n">create_network_graph</span><span class="p">,</span> <span class="n">display_graph</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="A-statistical-model-with-basic-control-flow">A statistical model with basic control-flow<a class="anchor-link" href="#A-statistical-model-with-basic-control-flow">&#182;</a></h2><p>For fun, let us add some contextual data: Whether or not Alice decides to go to space is highly dependent upon the number of points Alice collects, which is dependent upon a draw from a centered normal distribution, $x_1$. If she draws a number greater than 0, then we observe that Alice gets 1.5 points and the likelihood she goes to space, given the 1.5 points, is distributed by $\mathcal{N}(1.5~|~x_1,1)$. However, if she draws a number less than or equal to 0, then her likelihood is quite different. She gains 1 point, but the likelihood that the distribution is centered around 1, is dependent upon a random draw from a categorical distribution that returns a 0 with probability 0.1, 1 with probability 0.2, and 2 with probability 0.7. If we find that the value of the $x_1$ after the inference is greater than zero, then Alice goes to space, else she stays on Earth :-(</p>
<p>$$ x_1 \sim \mathcal{N}(0,1) $$
$$ x_2 \sim \mathcal{Cat}(0.1, 0.2, 0.7) $$
we observe our data ("points")
$$y_1 = 1.5 $$
$$y_2 = 1 $$</p>
<p>likelihood terms
$$ y_1 = 1.5~|~x_1 = \mathcal{N}(y_1~|~x_1,~1) $$
$$ y_2 = 1~|~x_2 = \mathcal{N}(y_2~|~x_2,~1) $$</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[34]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">model_if_clojure</span><span class="o">=</span><span class="s2">&quot;&quot;&quot;</span>
<span class="s2">(let [x1 (sample (normal 0 1))</span>
<span class="s2">      x2 (sample (categorical [0.1 0.2 0.7]))</span>
<span class="s2">      y1 1.5</span>
<span class="s2">      y2 1]</span>
<span class="s2">  (if (&gt; x1 0)</span>
<span class="s2">    (observe (normal x1 1) y1)</span>
<span class="s2">    (observe (normal x2 1) y2))</span>
<span class="s2">  [x1 x2])</span>
<span class="s2">&quot;&quot;&quot;</span>


<span class="n">compiled_clojure</span> <span class="o">=</span> <span class="n">compile_model</span><span class="p">(</span><span class="n">model_if_clojure</span><span class="p">,</span> <span class="n">language</span><span class="o">=</span><span class="s1">&#39;clojure&#39;</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>The compiler takes the above code and transforms it into a model class, from which the user can manipulate the program and interface with an inference engine.</p>
<p>As can be seen above, the language consists of some special syntax, one being 
<font color='red'>sample</font><code>(&lt;distribution_name&gt;(param1, param2m, ...))</code></p>
<p>which generates the <code>priors</code> for the variables of interest, and the second being 
<font color='blue'>observe</font><code>(&lt;distribution name&gt;(param1, param2, ...), &lt;observation/data&gt;)</code></p>
<p>which generates the likelihood given the observed data. The definitions given here are for when writing models in <code>python</code>, but examples of what the statements look like in <code>clojure</code> is given in the example above.</p>
<p>Finally, <code>if</code>-expressions, whilst on the surface look like usual <code>if</code>-statements, are interpreted in a special way in <code>PySPPL</code>. If the predicate, in the example above this is <code>(&gt; x1 0)</code>, contains any <font color='red'>sampled</font> variables, then within <code>PySPPL</code> a specific key-value pair is generated for that <code>if</code>-statement, so that those variables can be controlled in a special way.</p>
<p>This is especially important when using gradient based inference algorithms, as the conditions within the predicates can create <strong>measure zero</strong> discontinuities. When using algorithms such as Hamiltonian Monte Carlo (HMC) for performing inference in models that are of a low dimensionality with a suitably low number of discontinuities, one may not notice a difference in the outcome of the inference result. If they have the ground truth available. However, using HMC on such models is completely and utterly statistically wrong. But the HMC algorithm for such a model would run without hindrance.</p>
<p>This is dangerous for two reasons. One, If probabilistic programming languages and systems are supposed to deal with these subtleties whilst letting the modeller focus on modelling, then we are letting down a large group of the target users, who may not truly understand these subtleties. Two, the use of gradient based inference with control flow is poorly understood. Whilst point two, is re-iterating point one to some extent, it is important to understand, that a lack of understanding about a particular inference technique is detrimental to the setup of the probabilistic programming language and system. This is one of the reasons behind <code>PySPPL</code>, a simple language with inbuilt constraints to avoid these issue, yet is flexible enough to be integrated into other probabilistic programming systems.</p>
<p>Here is a print out of the model class for the above model:</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[3]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="nb">print</span><span class="p">(</span><span class="n">compiled_clojure</span><span class="o">.</span><span class="n">code</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre># 2018-06-18 09:42:24.644173
import torch
import torch.distributions as dist


class Model():

	def __init__(self, vertices: set, arcs: set, data: set, conditionals: set):
		super().__init__()
		self.vertices = vertices
		self.arcs = arcs
		self.data = data
		self.conditionals = conditionals
	
	def __repr__(self):
		V = &#39;\n&#39;.join(sorted([repr(v) for v in self.vertices]))
		A = &#39;, &#39;.join([&#39;({}, {})&#39;.format(u.name, v.name) for (u, v) in self.arcs]) if len(self.arcs) &gt; 0 else &#39;  -&#39;
		C = &#39;\n&#39;.join(sorted([repr(v) for v in self.conditionals])) if len(self.conditionals) &gt; 0 else &#39;  -&#39;
		D = &#39;\n&#39;.join([repr(u) for u in self.data]) if len(self.data) &gt; 0 else &#39;  -&#39;
		graph = &#39;Vertices V:\n{V}\nArcs A:\n  {A}\n\nConditions C:\n{C}\n\nData D:\n{D}\n&#39;.format(V=V, A=A, C=C, D=D)
		graph = &#39;#Vertices: {}, #Arcs: {}\n&#39;.format(len(self.vertices), len(self.arcs)) + graph
		return graph
	
	def gen_cond_bit_vector(self, state):
		result = 0
		for cond in self.conditionals:
			result = cond.update_bit_vector(state, result)
		return result

	def gen_cond_vars(self):
		return [c.name for c in self.conditionals]

	def gen_cont_vars(self):
		return [v.name for v in self.vertices if v.is_continuous and not v.is_conditional and v.is_sampled]

	def gen_disc_vars(self):
		return [v.name for v in self.vertices if v.is_discrete and v.is_sampled]

	def gen_if_vars(self):
		return [v.name for v in self.vertices if v.is_conditional and v.is_sampled and v.is_continuous]

	def gen_log_pdf(self, state):
		log_pdf = 0
		dst_ = dist.Normal(loc=0, scale=1)
		log_pdf = log_pdf + dst_.log_pdf(state[&#39;x30001&#39;])
		dst_ = dist.Categorical(probs=[0.1, 0.2, 0.7])
		log_pdf = log_pdf + dst_.log_pdf(state[&#39;x30002&#39;])
		state[&#39;cond_30003&#39;] = (state[&#39;x30001&#39;] &gt; 0)
		dst_ = dist.Normal(loc=state[&#39;x30001&#39;], scale=1)
		if state[&#39;cond_30003&#39;]:
			log_pdf = log_pdf + dst_.log_pdf(state[&#39;y30004&#39;])
		dst_ = dist.Normal(loc=state[&#39;x30002&#39;], scale=1)
		if not state[&#39;cond_30003&#39;]:
			log_pdf = log_pdf + dst_.log_pdf(state[&#39;y30005&#39;])
		return log_pdf

	def gen_prior_samples(self):
		state = {}
		dst_ = dist.Normal(loc=0, scale=1)
		state[&#39;x30001&#39;] = dst_.sample()
		dst_ = dist.Categorical(probs=[0.1, 0.2, 0.7])
		state[&#39;x30002&#39;] = dst_.sample()
		state[&#39;cond_30003&#39;] = (state[&#39;x30001&#39;] &gt; 0)
		dst_ = dist.Normal(loc=state[&#39;x30001&#39;], scale=1)
		state[&#39;y30004&#39;] = 1.5
		dst_ = dist.Normal(loc=state[&#39;x30002&#39;], scale=1)
		state[&#39;y30005&#39;] = 1
		return state

	def get_arcs(self):
		return self.arcs

	def get_arcs_names(self):
		return [(u.name, v.name) for (u, v) in self.arcs]

	def get_conditions(self):
		return self.conditionals

	def get_vars(self):
		return [v.name for v in self.vertices if v.is_sampled]

	def get_vertices(self):
		return self.vertices

	def get_vertices_names(self):
		return [v.name for v in self.vertices]

	def is_torch_imported(self):
		import sys 
		print(&#39;torch&#39; in sys.modules) 
		print(torch.__version__) 
		print(type(torch.tensor)) 
		import inspect 
		print(inspect.getfile(torch))

</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>We can change the models imported by changing the arguments in the <code>compile_model</code> function. By specification to our current application the compiler automatically imports <code>pytorch</code>. This can be easily removed by going into <code>ppl_graph_codegen.py</code> file and then removing the <code>if not has_dist</code> block.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[38]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">compile_clojure</span> <span class="o">=</span> <span class="n">compile_model</span><span class="p">(</span><span class="n">model_if_clojure</span><span class="p">,</span> <span class="n">language</span><span class="o">=</span><span class="s1">&#39;clojure&#39;</span><span class="p">,</span><span class="n">imports</span><span class="o">=</span><span class="s1">&#39;import matplotlib as mpl </span><span class="se">\n</span><span class="s1">import numpy as np &#39;</span><span class="p">)</span>
<span class="nb">print</span><span class="p">(</span><span class="n">compile_clojure</span><span class="o">.</span><span class="n">code</span><span class="p">[:</span><span class="mi">121</span><span class="p">])</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre># 2018-06-18 09:55:22.261447
import torch
import torch.distributions as dist
import matplotlib as mpl 
import numpy as np
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="Printing-the-Graph-G(V,E)-of-the-statistical-model.">Printing the Graph G(V,E) of the statistical model.<a class="anchor-link" href="#Printing-the-Graph-G(V,E)-of-the-statistical-model.">&#182;</a></h2><p>Each vertex of the graph is an object, with a set of attributes. These attributes describe the relationships between the vertex and other vertices. In addition to this, the attributes contain information about the observables and latent variables at each vertex.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[48]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="nb">print</span><span class="p">(</span><span class="n">compile_clojure</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>#Vertices: 4, #Arcs: 2
Vertices V:
Vertex x30001 [Sample]
  Name:           x30001
  Ancestors:      
  Cond-Ancs.:     
  Dist-Args:      {&#39;loc&#39;: &#39;0&#39;, &#39;scale&#39;: &#39;1&#39;}
  Dist-Code:      dist.Normal(0, 1)
  Dist-Name:      Normal
  Dist-Type:      DistributionType.CONTINUOUS
  Sample-Size:    1
Vertex x30002 [Sample]
  Name:           x30002
  Ancestors:      
  Cond-Ancs.:     
  Dist-Args:      {&#39;probs&#39;: &#39;[0.1, 0.2, 0.7]&#39;}
  Dist-Code:      dist.Categorical([0.1, 0.2, 0.7])
  Dist-Name:      Categorical
  Dist-Type:      DistributionType.DISCRETE
  Sample-Size:    1
Vertex y30004 [Observe]
  Name:           y30004
  Ancestors:      x30001
  Conditions:     cond_30003=True
  Cond-Ancs.:     x30001
  Cond-Nodes:     cond_30003
  Dist-Args:      {&#39;loc&#39;: &#34;state[&#39;x30001&#39;]&#34;, &#39;scale&#39;: &#39;1&#39;}
  Dist-Code:      dist.Normal(state[&#39;x30001&#39;], 1)
  Dist-Name:      Normal
  Dist-Type:      DistributionType.CONTINUOUS
  Sample-Size:    1
  Observation:    1.5
Vertex y30005 [Observe]
  Name:           y30005
  Ancestors:      x30002
  Conditions:     cond_30003=False
  Cond-Ancs.:     x30001
  Cond-Nodes:     cond_30003
  Dist-Args:      {&#39;loc&#39;: &#34;state[&#39;x30002&#39;]&#34;, &#39;scale&#39;: &#39;1&#39;}
  Dist-Code:      dist.Normal(state[&#39;x30002&#39;], 1)
  Dist-Name:      Normal
  Dist-Type:      DistributionType.CONTINUOUS
  Sample-Size:    1
  Observation:    1
Arcs A:
  (x30001, y30004), (x30002, y30005)

Conditions C:
Condition
  Name:         cond_30003
  Ancestors:    x30001
  Condition:    (state[&#39;x30001&#39;] &gt; 0)
  Function:     state[&#39;x30001&#39;]
  Op:           &gt;

Data D:
  -

</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>We can see from the graph that $x_2$ is only dependent on the observation $y_2$, whereas $x_1$ can be affected by both observations.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="An-example-of-an-independent-Categorical-model">An example of an independent Categorical model<a class="anchor-link" href="#An-example-of-an-independent-Categorical-model">&#182;</a></h2>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[40]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">model_categorical</span> <span class="o">=</span> <span class="s2">&quot;&quot;&quot;</span>
<span class="s2">(let[z (sample (categorical [0.7 0.15 0.15]))</span>
<span class="s2">    z1 (sample (categorical [0.1 0.5 0.4]))</span>
<span class="s2">    z2 (sample (categorical [0.2 0.2 0.6]))]</span>
<span class="s2">    z z1 z2)&quot;&quot;&quot;</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[49]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">compiled_clojure</span> <span class="o">=</span> <span class="n">compile_model</span><span class="p">(</span><span class="n">model_categorical</span><span class="p">,</span> <span class="n">language</span><span class="o">=</span><span class="s1">&#39;clojure&#39;</span><span class="p">)</span>
<span class="c1"># print(compiled_clojure.code)</span>
<span class="n">vertices</span> <span class="o">=</span> <span class="n">compiled_clojure</span><span class="o">.</span><span class="n">vertices</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="Plotting-the-depndence-graph">Plotting the depndence graph<a class="anchor-link" href="#Plotting-the-depndence-graph">&#182;</a></h3>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[50]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">create_network_graph</span><span class="p">(</span><span class="n">vertices</span><span class="o">=</span><span class="n">vertices</span><span class="p">)</span>
<span class="n">display_graph</span><span class="p">(</span><span class="n">vertices</span><span class="o">=</span><span class="n">vertices</span><span class="p">);</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>




<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>As you can see, in this model there are no dependencies between the different latent variables.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="A-Hidden-Markov-Model">A Hidden Markov Model<a class="anchor-link" href="#A-Hidden-Markov-Model">&#182;</a></h2><p>In a HMM the goal is to infer the hidden states. In doing so we aim to explain how our observations are produced, as the underlying assumption is that the hidden state directly affects the observation produced. This is a very short description, of a very powerful tool. See <a href="http://mlg.eng.cam.ac.uk/zoubin/papers/ijprai.pdf">here</a> for more details on HMMs.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[51]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">model_hmm_clojure</span><span class="o">=</span><span class="s2">&quot;&quot;&quot;</span>
<span class="s2">(defn data [n]</span>
<span class="s2">  (let [points (vector 0.9 0.8 0.7 0.0 -0.025</span>
<span class="s2">                       5.0 2.0 0.1 0.0 0.13</span>
<span class="s2">                       0.45 6.0 0.2 0.3 -1.0 -1.0)]</span>
<span class="s2">    (get points n)))</span>

<span class="s2">;; Define the init, transition, and observation distributions</span>
<span class="s2">(defn get-init-params []</span>
<span class="s2">  (vector (/ 1. 3.) (/ 1. 3.) (/ 1. 3.)))</span>

<span class="s2">(defn get-trans-params [k]</span>
<span class="s2">  (nth (vector (vector 0.1  0.5  0.4 )</span>
<span class="s2">               (vector 0.2  0.2  0.6 )</span>
<span class="s2">               (vector 0.7 0.15 0.15 )) k))</span>

<span class="s2">(defn get-obs-dist [k]</span>
<span class="s2">  (nth (vector (normal -1. 1.)</span>
<span class="s2">               (normal  1. 1.)</span>
<span class="s2">               (normal  0. 1.)) k))</span>

<span class="s2">;; Function to step through HMM and sample latent state</span>
<span class="s2">(defn hmm-step [n states]</span>
<span class="s2">  (let [next-state (sample (categorical (get-trans-params (last states))))]</span>
<span class="s2">    (observe (get-obs-dist next-state) (data n))</span>
<span class="s2">    (conj states next-state)))</span>

<span class="s2">;; Loop through the data</span>
<span class="s2">(let [init-state (sample (categorical (get-init-params)))]</span>
<span class="s2">  (loop 16 (vector init-state) hmm-step))</span>

<span class="s2">&quot;&quot;&quot;</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="Plotting-the-graphical-model">Plotting the graphical model<a class="anchor-link" href="#Plotting-the-graphical-model">&#182;</a></h3>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[52]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">compiled_clojure</span> <span class="o">=</span> <span class="n">compile_model</span><span class="p">(</span><span class="n">model_hmm_clojure</span><span class="p">,</span> <span class="n">language</span><span class="o">=</span><span class="s1">&#39;clojure&#39;</span><span class="p">)</span>
<span class="n">vertices</span> <span class="o">=</span> <span class="n">compiled_clojure</span><span class="o">.</span><span class="n">vertices</span>
<span class="n">create_network_graph</span><span class="p">(</span><span class="n">vertices</span><span class="o">=</span><span class="n">vertices</span><span class="p">)</span>
<span class="n">display_graph</span><span class="p">(</span><span class="n">vertices</span><span class="o">=</span><span class="n">vertices</span><span class="p">);</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>




<div class="output_png output_subarea ">
<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAX8AAAD8CAYAAACfF6SlAAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAALEgAACxIB0t1+/AAAADl0RVh0U29mdHdhcmUAbWF0cGxvdGxpYiB2ZXJzaW9uIDIuMi4yLCBodHRwOi8vbWF0cGxvdGxpYi5vcmcvhp/UCwAAIABJREFUeJzsnXl4U1X6xz/nZmvapnuhlH2HUnYFREBAUBTBDfgpijqKOqDiqIjOoo6jzrjPiAgq6oy4gaCoKC4gIiCCIGtZlK2A2ELplnTJes/vj3ND05UWCljJ93nyJE1yzz23Sb7nPe/yfYWUkjDCCCOMMM4uaGd6AmGEEUYYYZx+hMk/jDDCCOMsRJj8wwgjjDDOQoTJP4wwwgjjLESY/MMII4wwzkKEyT+MMMII4yxEmPzDCCOMMM5ChMk/jDDCCOMsRJj8wwgjjDDOQoTJP4wwwgjjLESY/MMII4wwzkKEyT+MMMII4yxEmPzDCCOMMM5ChMk/jDDCCOMshPlMT6Au+PHHHxuZzebXgHTCC1cYoAMZfr9/Yu/evY+c6cmEEUZDQoMif7PZ/FpKSkrn5OTkfE3Two0IznLoui5ycnLSsrOzXwNGn+n5hBFGQ0JDs57Tk5OTnWHiDwNA0zSZnJxciNoJhhFGGHVAg7L8AS1M/GGEwvg+/DaMGCE0IA71u/IDBUipn9lJhRFG1Who5B9GGHWGEFQiZSmpH1IWIhLoCQwEWhvnkIAAAgixF1gJbEDK0no5Zxhh1AN+GxbTiSIpqTtC9K63W1JS9+Od8oEHHkhp165dlw4dOqR16tQpbdmyZVGn8hL79OnTccWKFZG1ff+nn37qGDJkSLvQ51wulxYXF9cjLy+v3Oc9bNiwtrNnz46v7diZmZmWESNGtKnr+YNo2rRp16ysrNNicAhBpBCcLwQPArOAZ4B/GvcvC8GDxuv2EzyBCSEuBJ4HbgGaAEeAg8Avxv1h4/lbgH8jxIUIYTrJSwueX0OIBIRoZNw37N9yGKcdDdvyz82t3/kfZ7ylS5dGffnll3Fbt27dbrfbZVZWltnj8Yh6ncMpgMPh0AcOHFj4zjvvxN911125ALm5uaYff/wxeuHChftqM4bP56NVq1a+L774Yu+pne3JQQhMwGBgLGAFXChSDoS8zUQZKU8QgvnAcinLvaemk8QCk4FOwK+Ap5p3BoB842YDbgD6IMRMpCys04Wp84Z3GWHUG8LWQh1w6NAhS0JCgt9ut0uAJk2a+Fu1auUDmDp1apP09PTO7du373Lttde21HXlVejTp0/HW265pXl6enrnNm3adPn2228jL7roorYtW7ZMnzJlSirATz/9ZG3dunWX0aNHt27Tpk2XESNGtHG5XJU+mw8//DCmR48endLS0jpfcsklbQoLCzWABQsWxLRu3bpLWlpa5wULFsRVNfdrr702b/78+QnBv9955524gQMHOh0Oh/7NN99E9ujRo1Pnzp3Tevbs2Wnz5s02gOnTpycOHTq0Xb9+/Tr079+/408//WRt3759l+Cce/fu3TEtLa1zWlpa5yVLlhzbAblcLtPgwYPbtWrVKn38+PEtAoHKnDpz5syErl27du7UqVPa+PHjW/r9fvx+P1dffXWr9u3bd+nQoUPao48+2qgun48QxALTUCSbDxww7itOIFDh9RuAacbxxztJLPAginz3UT3xV4THeH9r4EFjnNrhTO8ywvhdIkz+dcAVV1zh/PXXX62tWrVKv/7661t89tln0cHX7r///iMZGRk7du3ata20tFSbO3fusR+31WrVMzIydvzhD3/IGTt2bLvZs2cf2Llz57Z58+YlZWdnmwAyMzMj7rzzziN79+7d5nA49GeeeSY59NxZWVnmf/7zn01WrFjx8/bt23f06tWr5LHHHmtcUlIi7rzzzlaffPLJ7oyMjB1HjhyxVDX3q666yrlt27bI4Pnmz5+fcO211+YBdO/e3b1u3bqdO3bs2P7II48cmjZtWrPgcdu2bYv8+OOP96xbt+6n0PFSU1P9K1eu/Hn79u075s2bt/eee+5pEXxt69atUTNnzjywe/fujMzMTNucOXPKuZY2bNgQsWDBgoR169bv3Lp1509CmMXMma8krV79fWRWVpZl165d237++eftd9xxR25tPxuDuE+alGtcABSZTgYSURb/ieBX4/jJtSJntUic8IJWp0UmjLMKYfKvA2JjY/WMjIztM2bM2J+cnOy/8cYb206fPj0R4PPPP3d069atU4cOHdJWr17tyMjIOOZLvvLKKwsAunfvXtquXbvSli1b+ux2u2zevLln7969VoCUlBTvRRddVAwwYcKE3NWrV0eHnnv58uVRe/bsiejTp0+nTp06pc2dOzfxwIED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
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="PySPPL-for-python-based-models">PySPPL for python based models<a class="anchor-link" href="#PySPPL-for-python-based-models">&#182;</a></h1><p>PySPPLs design allows one to use it with many different languages, we so far have built an interface for both <code>python</code> and <code>clojure</code> code. 
It is also important to note that the number of distributions one can add to <code>PySPPL</code> is boundless, as we will show in future walk-throughs.</p>
<h2 id="Bayesian-linear-regression-model">Bayesian linear regression model<a class="anchor-link" href="#Bayesian-linear-regression-model">&#182;</a></h2><p>The aim of inference in this model is to infer the equation of the line $ x = y*s + b$ (this is written to match the notation below. In general one would see his written as $y = mx +c$).</p>
<p>$$slope \sim \mathcal{N}(0, 10) $$
$$bias \sim \mathcal{N}(0, 10) $$</p>
<p>Observations
$$y = [(1.,2.), (2.1,3.9), (3.,5.3)] $$
Constructing the equation of the predicted curve
$$x_n = slope \times y[0,:] + bias$$
The likelihood
$$y = y[1,:]~|~x_n = \mathcal{N}(y[1,:]~|~x_n,~\mathbf{I}) $$</p>
<h2 id="The-Python-SPPL-code">The Python SPPL code<a class="anchor-link" href="#The-Python-SPPL-code">&#182;</a></h2>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[53]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">model_lr_python</span> <span class="o">=</span> <span class="s2">&quot;&quot;&quot;import torch</span>
<span class="s2">slope = sample(normal(torch.tensor(0.0), torch.tensor(10.0)))</span>
<span class="s2">bias  = sample(normal(torch.tensor(0.0), torch.tensor(10.0)))</span>
<span class="s2">y  = torch.tensor([[1.0, 2.1], [2.0, 3.9], [3.0, 5.3]])</span>
<span class="s2">xn = slope*data[:,0] + bias # y  = mx + c</span>
<span class="s2">observe(normal(xn, torch.ones(len(xn))),data[:,1])</span>

<span class="s2">[slope, bias]</span>
<span class="s2">&quot;&quot;&quot;</span>

<span class="n">compiled_python</span> <span class="o">=</span> <span class="n">compile_model</span><span class="p">(</span><span class="n">model_lr_python</span><span class="p">,</span> <span class="n">language</span><span class="o">=</span><span class="s1">&#39;python&#39;</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="The-Graph">The Graph<a class="anchor-link" href="#The-Graph">&#182;</a></h2>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[54]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="nb">print</span><span class="p">(</span><span class="n">compiled_python</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>#Vertices: 3, #Arcs: 2
Vertices V:
Vertex x30001 [Sample]
  Name:           x30001
  Ancestors:      
  Cond-Ancs.:     
  Dist-Args:      {&#39;loc&#39;: &#39;torch.tensor(0.0)&#39;, &#39;scale&#39;: &#39;torch.tensor(10.0)&#39;}
  Dist-Code:      dist.Normal(torch.tensor(0.0), torch.tensor(10.0))
  Dist-Name:      Normal
  Dist-Type:      DistributionType.CONTINUOUS
  Sample-Size:    1
  Orig. Name:     slope
Vertex x30002 [Sample]
  Name:           x30002
  Ancestors:      
  Cond-Ancs.:     
  Dist-Args:      {&#39;loc&#39;: &#39;torch.tensor(0.0)&#39;, &#39;scale&#39;: &#39;torch.tensor(10.0)&#39;}
  Dist-Code:      dist.Normal(torch.tensor(0.0), torch.tensor(10.0))
  Dist-Name:      Normal
  Dist-Type:      DistributionType.CONTINUOUS
  Sample-Size:    1
  Orig. Name:     bias
Vertex y30003 [Observe]
  Name:           y30003
  Ancestors:      x30002, x30001
  Conditions:     
  Cond-Ancs.:     
  Cond-Nodes:     
  Dist-Args:      {&#39;loc&#39;: &#34;((state[&#39;x30001&#39;] * state[&#39;data&#39;][:,0]) + state[&#39;x30002&#39;])&#34;, &#39;scale&#39;: &#34;torch.ones(len(((state[&#39;x30001&#39;] * state[&#39;data&#39;][:,0]) + state[&#39;x30002&#39;])))&#34;}
  Dist-Code:      dist.Normal(((state[&#39;x30001&#39;] * state[&#39;data&#39;][:,0]) + state[&#39;x30002&#39;]), torch.ones(len(((state[&#39;x30001&#39;] * state[&#39;data&#39;][:,0]) + state[&#39;x30002&#39;]))))
  Dist-Name:      Normal
  Dist-Type:      DistributionType.CONTINUOUS
  Sample-Size:    1
  Observation:    state[&#39;data&#39;][:,1]
Arcs A:
  (x30002, y30003), (x30001, y30003)

Conditions C:
  -

Data D:
  -

</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="The-dependency-graph">The dependency graph<a class="anchor-link" href="#The-dependency-graph">&#182;</a></h2><p>With <code>python</code> models we can plot the user defined label names.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[55]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">vertices</span> <span class="o">=</span> <span class="n">compiled_python</span><span class="o">.</span><span class="n">vertices</span>
<span class="n">create_network_graph</span><span class="p">(</span><span class="n">vertices</span><span class="o">=</span><span class="n">vertices</span><span class="p">)</span>
<span class="n">display_graph</span><span class="p">(</span><span class="n">vertices</span><span class="o">=</span><span class="n">vertices</span><span class="p">);</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>




<div class="output_png output_subarea ">
<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAYYAAAD8CAYAAABzTgP2AAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAALEgAACxIB0t1+/AAAADl0RVh0U29mdHdhcmUAbWF0cGxvdGxpYiB2ZXJzaW9uIDIuMi4yLCBodHRwOi8vbWF0cGxvdGxpYi5vcmcvhp/UCwAAIABJREFUeJzt3Xl4leWd//H39yQkJBCWsBjCDiFkk6BUXCkUFFEWgYijuNVKx0od27rPtJ3O1LGtVX/tUEu1OK224yUM++ZSFzaLWpBFkkDYBJVFkEDCGkhy//64TzgEA4SQ5GT5vK6LC0jOeZ5vDno+537u5/7e5pxDRESkTCDcBYiISN2iYBARkXIUDCIiUo6CQUREylEwiIhIOQoGEREpR8EgIiLlKBhERKQcBYOIiJSjYBARkXIUDCIiUo6CQUREylEwiIhIOQoGEREpJzLcBYjIhfn444/bR0ZGvgRkoA97AqVAdnFx8YR+/frtqcoBFAwi9VxkZORLCQkJqe3atdsfCAS0wUojV1paanv37k3bvXv3S8CoqhxDny7OxSyAWTxm7YO/6zWTuiajXbt2hQoFAQgEAq5du3YF+BFklWjEUBGzWOASYADQHf86OcCAEsy2AsuAVTh3NGx1ingBhYKcKvjfQ5U/xCoYTmUWAQwCxgFRwEFgD1ByyqMigA7AvcCdmE0HFuNcCSIiDYAui5Qxawk8BtwF7Ac+C/5++ht+yWnfvwt4LPh8kfBr2zYTs37V9qtt28xznfLxxx9PSEpKSk9OTk5LSUlJe++995rV5I/Yv3//3kuXLo2t7OMXLFgQ961vfSvp1K8dPHgw0KpVq775+fnl3gevvfbanlOmTGld2WNv27atybBhw3qc7/nLdOzY8eJdu3bVqQ/pCgYoC4Un8JeNPgWKKvnMouDjuwNPKBykTti3r3rfZM5xvHfeeafZW2+91WrdunW5GzduzF20aNHGHj16HK/WGmpAXFxc6YABAwpeffXVkyGwb9++iI8//rj5rbfeWlCZY5w4cYJu3bqdePPNN7fWXKW1T8HgLx9NBNoAO6t4lJ3B508MHk+k0dixY0eT+Pj44piYGAfQoUOH4m7dup0AeOSRRzpkZGSk9urVK/22227rWlpaCvhP/Pfee2/njIyM1B49eqQvWbIkdujQoT27du2a8eCDDyYC5OXlRXXv3j191KhR3Xv06JE+bNiwHgcPHvzae9asWbNa9O3bNyUtLS31hhtu6FFQUBAAmDFjRovu3bunp6Wlpc6YMaNVRbXfdttt+dOnT48v+/urr77aasCAAYVxcXGlixYtiu3bt29Kampq2iWXXJKydu3aaIBJkya1GTx4cNIVV1yRfNVVV/XOy8uL6tWrV3pZzf369eudlpaWmpaWlvr222+fHDkdPHgwYtCgQUndunXLGD9+fJeSkq9ffZ48eXL8xRdfnJqSkpI2fvz4rsXFxRQXF5OVldWtV69e6cnJyWn/+Z//2b6q/1aVpWDwcwopVD0UyuwMHmfQBR5HpF4ZPXp04c6dO6O6deuWcccdd3RZuHBh87LvPfroo3uys7PXb9q0Kefo0aOBqVOnnhxVR0VFlWZnZ6+/55579o4bNy5pypQpn23YsCFn2rRpbXfv3h0BsG3btqYPPPDAnq1bt+bExcWVPvPMM+1OPfeuXbsif/GLX3RYunTpxtzc3PWXXnrpkSeffPKiI0eO2AMPPNBt3rx5m7Ozs9fv2bOnSUW1jx07tjAnJye27HzTp0+Pv+222/IBMjMzj61YsWLD+vXrc3/2s5/teOyxxzqVPS8nJyd27ty5W1asWJF36vESExOLly1btjE3N3f9tGnTtv7oRz/qUva9devWNZs8efJnmzdvzt62bVv0X/7yl3KXq1atWtV0xowZ8StXrtywYcOG3EAg4F544YU2H3zwQeyuXbuabNq0KWfjxo253//+9/dV5d/pfDTuYPB3H43jwkOhzE5gHGYx1XQ8kTqvZcuWpdnZ2bnPP//89nbt2hXffffdPSdNmtQG4I033ojr06dPSnJyctry5cvjsrOzT/6/MWbMmAMAmZmZR5OSko527dr1RExMjOvcuXPR1q1bowASEhKODx069DDAnXfeuW/58uXNTz334sWLm23ZsqVp//79U1JSUtKmTp3a5rPPPotas2ZN006dOhVdfPHFRYFAgNtvv73CN9OmTZu666677sBf//rX1rt27YrMzc2NHTt2bCFAfn5+xI033tizV69e6Y899ljnjRs3Ni173oABAwovuuiir33kP378uI0fP75bcnJy2rhx43pu2bLl5HMuvvjiw2lpaccjIyO55ZZb8pctW1buZ3nzzTfjsrOzYzMzM1NTUlLS3n///RZb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SExMvLis5URhYWEgISGhT1FRkeXk5EQPGDCgV3p6emq/fv16r169uinAhg0bovr27ZuSnJycVtba+3R33nnn/vfee69l2WgnLy8vas+ePU2uv/76QwUFBYErr7wyOS0tLTU5OTntf//3f1uVPaZbt24ZY8aM6ZacnJy+ZcuWqFM337n22mt7pqenpyYlJaU/++yz5Vpr3HvvvZ2TkpLSr7zyyuSdO3d+LYDP9Fr813/9V/uePXumJycnp40YMeKsmwRVhYIBwLkC4FeENt2p7JxDNKHNfX4VPM55ntp94Zz7nXNuEJAMvAd8F3+5aZaZ3W7aAEjqsHXr1sVkZmYeOfVr8fHxpR06dDiem5sbDfDJJ580mzdv3uacnJycefPmxS9dujR21qxZLRISEk7k5eXlbtq0KWfs2LGFRUVF9uCDD3aZO3fulpycnPV33333V4888sjJkcfx48ctOzt7/XPPPbcrNTX1yOuvvx4HMG3atJYDBw4siI6OdhMmTOg6efLkz3JyctY/88wzX9x///1dACZOnNhlwoQJezdu3JjboUOHCoccF110UUlmZubhGTNmtAR45ZVX4keOHLk/EAgQGxtbunDhws25ubnrlyxZsvHf/u3fOpXtL/HZZ59FP/DAA3s3b96ck5ycXG6ToldffXVbTk7O+jVr1uS++OKLF5W1+D569GjgG9/4xuHNmzfnXH311QefeOKJcmF1ttdi0qRJCdnZ2bkbN27Mffnll7df0D9gBTQJWsa5Asx+TWjP52h836NCvr7nc4vgryLgL1TTns/OuT34ieo/mm/ZMQq4FfiDmS3D39001zlX4/3YRarTNddcU5iQkFACMHz48P2LFy9uPnr06IIf//jHne+///6ON910U8GwYcMOrVixoummTZtiBg8enAz+0ky7du1OvomX7ZUAMG7cuP2vvfZa65EjRx78v//7v/iJEyfuLSgoCKxevbr5uHHjepY9rqyH0qpVq5q/8cYbWwDuu+++fU8++eTJ/RVOdcstt+RPmzat9R133HFg1qxZ8VOmTNkWrMV++MMfdvrwww+bBwIB9uzZE/XFF19EAnTo0OH4kCFDKuwF9fTTT1+0cOHCVgC7d+9ukpOT0zQhIeFwIBBgwoQJ+QDf+c539o0dO7bc1p+ffPJJ9Jlei969ex8dM2ZM91GjRh24/fbbq33NlILh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
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="Models-in-pure-python">Models in pure python<a class="anchor-link" href="#Models-in-pure-python">&#182;</a></h1><p>We don't need to import <code>torch</code>, we can actually write models in pure python, for example:</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[56]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">model_purepython</span><span class="o">=</span><span class="s2">&quot;&quot;&quot;mean = sample(poisson(3))</span>
<span class="s2">x= sample(gamma(mean,1))</span>
<span class="s2">y= 10</span>
<span class="s2">observe(normal(x,5), y)</span>
<span class="s2">&quot;&quot;&quot;</span>
<span class="n">compiled_python</span> <span class="o">=</span> <span class="n">compile_model</span><span class="p">(</span><span class="n">model_purepython</span><span class="p">,</span> <span class="n">language</span><span class="o">=</span><span class="s1">&#39;python&#39;</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="An-Example-of-the-Graph-G(V,E)">An Example of the Graph G(V,E)<a class="anchor-link" href="#An-Example-of-the-Graph-G(V,E)">&#182;</a></h2>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[57]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="nb">print</span><span class="p">(</span><span class="n">compiled_python</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre>#Vertices: 3, #Arcs: 2
Vertices V:
Vertex x30001 [Sample]
  Name:           x30001
  Ancestors:      
  Cond-Ancs.:     
  Dist-Args:      {&#39;lam&#39;: &#39;3&#39;}
  Dist-Code:      dist.Poisson(3)
  Dist-Name:      Poisson
  Dist-Type:      DistributionType.DISCRETE
  Sample-Size:    1
  Orig. Name:     mean
Vertex x30002 [Sample]
  Name:           x30002
  Ancestors:      x30001
  Cond-Ancs.:     
  Dist-Args:      {&#39;alpha&#39;: &#34;state[&#39;x30001&#39;]&#34;, &#39;beta&#39;: &#39;1&#39;}
  Dist-Code:      dist.Gamma(state[&#39;x30001&#39;], 1)
  Dist-Name:      Gamma
  Dist-Type:      DistributionType.CONTINUOUS
  Sample-Size:    1
  Orig. Name:     x
Vertex y30003 [Observe]
  Name:           y30003
  Ancestors:      x30002
  Conditions:     
  Cond-Ancs.:     
  Cond-Nodes:     
  Dist-Args:      {&#39;loc&#39;: &#34;state[&#39;x30002&#39;]&#34;, &#39;scale&#39;: &#39;5&#39;}
  Dist-Code:      dist.Normal(state[&#39;x30002&#39;], 5)
  Dist-Name:      Normal
  Dist-Type:      DistributionType.CONTINUOUS
  Sample-Size:    1
  Observation:    10
Arcs A:
  (x30001, x30002), (x30002, y30003)

Conditions C:
  -

Data D:
  -

</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[58]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">vertices</span> <span class="o">=</span> <span class="n">compiled_python</span><span class="o">.</span><span class="n">vertices</span>
<span class="n">create_network_graph</span><span class="p">(</span><span class="n">vertices</span><span class="o">=</span><span class="n">vertices</span><span class="p">)</span>
<span class="n">display_graph</span><span class="p">(</span><span class="n">vertices</span><span class="o">=</span><span class="n">vertices</span><span class="p">);</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>




<div class="output_png output_subarea ">
<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAYYAAAD8CAYAAABzTgP2AAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAALEgAACxIB0t1+/AAAADl0RVh0U29mdHdhcmUAbWF0cGxvdGxpYiB2ZXJzaW9uIDIuMi4yLCBodHRwOi8vbWF0cGxvdGxpYi5vcmcvhp/UCwAAIABJREFUeJzt3Xl81dWd//HX5yYkJBCBsIctQEggCQREcSkogiJWQJASFVFrZcaROrZWrT6my3TqONa209/vZyvVYuvU1lF2EREtLijWpbJKEgMIgsoiaxK2AEnO749zw02QJYSb3CT3/Xw8eNSG5HtPIt4X57ucY845REREKgUiPQAREWlYFAYREalGYRARkWoUBhERqUZhEBGRahQGERGpRmEQEZFqFAYREalGYRARkWoUBhERqUZhEBGRahQGERGpRmEQEZFqYiM9gAbPLAC0xv+syoAinKuI7KBEROqOwnAyZonAIGAY0BP/c3KAAeWYbQKWAStx7nDExikCrFixokNsbOzTQDY6CyBQAeSVlZVNHTx48M7aHMC0H0MVZjHAcGASEAfsB0qA8iqfFQOcByQBR4HZwFKcK0ckAtasWfNSp06d+rVv374kEAjoP+goV1FRYbt27Wq1Y8eOgpycnHG1OYZmDJXMWgHTgL7ANuDIKT6zHNgX/BUP3AoMwWw6zhXXx1BFTpDdvn37fYqCAAQCAde+ffviHTt2ZNf6GOEcUKPlo/AQ/rTRZ5w6Cic6Evz8nsBDweOI1LeAoiBVBf881Pr9XWHwp4+mAW3xM4Xa2Bb8+mnB44mINFoKg7+mUHn66FxsCx5n+DkeR+TctGuXg9ngsP1q1y7nTC/54IMPdkpLS8tKT0/P7Nu3b+abb77Zoi6/xSFDhmS88847iTX9/JdffjnpiiuuSKv6sf379wdat249cO/evdXeB6+88sreM2bMaFPTY2/evLnZ6NGje53t61fq0qVL/+3btzeo0/rRHQZ/99Ekzj0KlbYBkzBLCNPxRM7enj3hfZM5w/Fef/31Fq+99lrrtWvXFqxfv77grbfeWt+rV6+jYR1DHUhKSqoYNmxY8XPPPXc8Anv27IlZsWJFyxtvvLFG1wuPHTtGamrqsVdffXVT3Y20/kV3GPwtqXHU/JrCmRzBX5AeFKbjiTR4W7dubZacnFyWkJDgADp37lyWmpp6DOD+++/vnJ2d3a9Pnz5ZN910U4+KCv8I0JAhQzLuuOOObtnZ2f169eqV9fbbbyeOGjWqd48ePbLvueeeFIB169bF9ezZM2vcuHE9e/XqlTV69Ohe+/fv/9p71rx5884bOHBg38zMzH7XXHNNr+Li4gDAnDlzzuvZs2dWZmZmvzlz5rQ+2dhvuummvbNnz06u/P/PPfdc62HDhpUkJSVVvPXWW4kDBw7s269fv8xBgwb1XbNmTTzA448/3nbEiBFpF198cfqll16asW7durg+ffpkVY558ODBGZmZmf0yMzP7LVmy5PjMaf/+/THDhw9PS01NzZ48eXL38vKv38g4ffr05P79+/fr27dv5uTJk3uUlZVRVlbGxIkTU/v06ZOVnp6e+R//8R8davvvqqaiPQzD8LekhlNJ8LgiUWH8+PEl27Zti0tNTc2eMmVK90WLFrWs/L0HHnhgZ15e3icbNmzIP3z4cOCFF144foNGXFxcRV5e3ie33377rkmTJqXNmDHj88LCwvyZM2e227FjRwzA5s2bm9999907N23alJ+UlFTxq1/9qn3V196+fXvsf/3Xf3V+55131hcUFHxy/vnnH3r44Yc7Hjp0yO6+++7Ul1566dO8vLxPdu7c2exkY7/++utL8vPzEytfb/bs2ck33XTTXoCcnJzSjz76qPCTTz4p+Pd///etP/zhD7tWfl1+fn7iggULNn700Ufrqh4vJSWlbNmyZesLCgo+mTlz5qZ77723e+XvrV27tsX06dM///TTT/M2b94c/+yzz1Y7XbVy5crmc+bMSV6+fHlhYWFhQSAQcE8++WTb999/P3H79u3NNmzYkL9+/fqC7373u3tq8+/pbDSo81r1Kdbs9nJ4dAjkr4G02+DN16D/bmgzA55fAt1nwzcA/gne+A2sug8G/h5GHYNmPeHLRTB7N8RdCt/LgcIN0L0z7PkYXks0C+gJaYkGrVq1qsjLyyt49dVXk954442k2267rfdPf/rTL++55549ixcvTvrNb37TqbS0NFBUVBSbmZl5GCgGmDBhQhFATk7O4bS0tMM9evQ4BtCtW7cjmzZtimvbtm15p06djo4aNeogwC233LLn8ccf7wB8VfnaS5cubbFx48bmQ4YM6Qtw7NgxGzx48IHVq1c379q165H+/fsfAbj55pv3PP300+05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+Hmjyr0SACZNmrTv+eefbzN27Nj9s2bNSp42bdqu4uLiwKpVq1pOmjSpd+XnHT161ABWrlzZcvHixRsB7rzzzj0PP/zwSU/L5ubm7p05c2abKVOmFM2bNy95xowZm4Njse9///tdP/jgg5aBQICdO3fGffnll7EAnTt3Pjpy5MiTrgX12GOPdVy0aFFrgB07djTLz89v3qlTp4OBQICpU6fuBfjOd76z5/rrr6+29efHH38cf6qfRUZGxuEJEyb0HDduXNHNN99cdOJrniuFoRFzzh0BXgZeNrPmwNX4SDxqZiuAmcB859yu0xxG5JxkZ2cffvHFF6tdLN27d29g+/btcZmZmUc+/PDDxJMtOT1gwIAjK1euLJg7d26rn/zkJ11ef/31ktzc3KK0tLTDq1evLjzZayUlJR2frd90001FDz/8cJevvvoqJi8vL3Hs2LElJSUlgaSkpLLCwsKCk319IBA44+JwkydPLvrRj37U7d13300sLS0NDBs27BDAU089lbxnz57YtWvXfhIfH++6dOnS//DhwwE49TLcL7/8ctLbb7+dtHz58sKkpKSKIUOGZFR+zYlOtgz3qX4Wb7311obFixcnLViwoNWvf/3rzuvWrctv1uykexHViq4xNBHOuVLn3ALn3M34axK/A64ANpjZ38xsqpm1jewopSkaN27c/tLS0sDvfve7tgBlZWVMmzat26RJk3ZXvpG/++6753311VcxBw4csFdeeaX15ZdffmDz5s3NkpKSKqZNm7b3Bz/4wY7Vq1cnDhgwoHTv3r2xlUttHzlyxJYvX978ZK/bqlWrigEDBhy88847u48cObI4NjaW5OTkiq5dux7905/+1Ab837Lff//9BIDzzz//wIwZM5IBZsyYccr/Flq1alVxySWX7J86dWrqhAkTjs9QiouLY9q1a3csPj7eLVy4MGnbtm1xZ/rZFBUVxbRq1ao8KSmpYtWqVc3XrFlzfKvPiooKKu8++p//+Z+2Q4YMqbYM96l+FuXl5WzcuDFu7Nix+5944omtBw4ciCkuLg7r6SSFoQlyzh12zs13zt2Ef8biD8AoYJOZvWpm3zGziN4OJ3WnbdvwLvl+puMFAgFefPHFT+fNm9emR48e2T179syOj4+vePzxx49vODNgwICD48aN652VlZU1duzYfZdddtmhFStWJAwcOLBf3759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
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="Gaussian-Mixture-model">Gaussian Mixture model<a class="anchor-link" href="#Gaussian-Mixture-model">&#182;</a></h2><p>In this model the goal of the inference procedure is to infer the unknown means that describe the observations. Gaussian mixtures assume that the data can be modelled by a collection of Gaussian distributions (of course this is by no means always true).</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[59]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">model_gmm2</span> <span class="o">=</span> <span class="s2">&quot;&quot;&quot;</span>
<span class="s2">import torch</span>

<span class="s2">means  = 2</span>
<span class="s2">samples  = 10</span>
<span class="s2">y = [-2.0, -2.5, -1.7, -1.9, -2.2, 1.5, 2.2, 3.0, 1.2, 2.8,</span>
<span class="s2">      -1.7, -1.3,  3.2,  0.8, -0.9, 0.3, 1.4, 2.1, 0.8, 1.9] </span>
<span class="s2">ys = torch.tensor([y])</span>
<span class="s2">pi = torch.tensor(0.5*torch.ones(samples,means))</span>
<span class="s2">mus = sample(normal(torch.zeros(means,1), 2*torch.ones(means,1)))</span>

<span class="s2">zn = sample(categorical(pi), sample_size=2)</span>

<span class="s2">for i in range(samples):</span>
<span class="s2">    index = (zn == i).nonzero()</span>
<span class="s2">    observe(normal(mus[i]*torch.ones(len(index),1), 2*torch.ones(len(index),1)), ys[index])</span>
<span class="s2">&quot;&quot;&quot;</span>

<span class="n">compiled_python</span> <span class="o">=</span> <span class="n">compile_model</span><span class="p">(</span><span class="n">model_gmm2</span><span class="p">,</span> <span class="n">language</span><span class="o">=</span><span class="s1">&#39;python&#39;</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="The-code-output">The code output<a class="anchor-link" href="#The-code-output">&#182;</a></h2>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[36]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="nb">print</span><span class="p">(</span><span class="n">compiled_python</span><span class="o">.</span><span class="n">code</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>


<div class="output_subarea output_stream output_stdout output_text">
<pre># 2018-06-15 08:40:37.239078
import torch
import torch.distributions as dist
import torch

class Model():

	def __init__(self, vertices: set, arcs: set, data: set, conditionals: set):
		super().__init__()
		self.vertices = vertices
		self.arcs = arcs
		self.data = data
		self.conditionals = conditionals
	
	def __repr__(self):
		V = &#39;\n&#39;.join(sorted([repr(v) for v in self.vertices]))
		A = &#39;, &#39;.join([&#39;({}, {})&#39;.format(u.name, v.name) for (u, v) in self.arcs]) if len(self.arcs) &gt; 0 else &#39;  -&#39;
		C = &#39;\n&#39;.join(sorted([repr(v) for v in self.conditionals])) if len(self.conditionals) &gt; 0 else &#39;  -&#39;
		D = &#39;\n&#39;.join([repr(u) for u in self.data]) if len(self.data) &gt; 0 else &#39;  -&#39;
		graph = &#39;Vertices V:\n{V}\nArcs A:\n  {A}\n\nConditions C:\n{C}\n\nData D:\n{D}\n&#39;.format(V=V, A=A, C=C, D=D)
		graph = &#39;#Vertices: {}, #Arcs: {}\n&#39;.format(len(self.vertices), len(self.arcs)) + graph
		return graph
	
	def gen_cond_bit_vector(self, state):
		result = 0
		for cond in self.conditionals:
			result = cond.update_bit_vector(state, result)
		return result

	def gen_cond_vars(self):
		return [c.name for c in self.conditionals]

	def gen_cont_vars(self):
		return [v.name for v in self.vertices if v.is_continuous and not v.is_conditional and v.is_sampled]

	def gen_disc_vars(self):
		return [v.name for v in self.vertices if v.is_discrete and v.is_sampled]

	def gen_if_vars(self):
		return [v.name for v in self.vertices if v.is_conditional and v.is_sampled and v.is_continuous]

	def gen_log_pdf(self, state):
		log_pdf = 0
		dst_ = dist.Normal(loc=torch.zeros(2, 1), scale=(2 * torch.ones(2, 1)))
		log_pdf = log_pdf + dst_.log_pdf(state[&#39;x30001&#39;])
		dst_ = dist.Categorical(probs=torch.tensor((0.5 * torch.ones(10, 2))))
		log_pdf = log_pdf + dst_.log_pdf(state[&#39;x30002&#39;])
		dst_ = dist.Normal(loc=(state[&#39;x30001&#39;][0] * torch.ones(len((state[&#39;x30002&#39;] == 0).nonzero()), 1)), scale=(2 * torch.ones(len((state[&#39;x30002&#39;] == 0).nonzero()), 1)))
		log_pdf = log_pdf + dst_.log_pdf(state[&#39;y30004&#39;])
		dst_ = dist.Normal(loc=(state[&#39;x30001&#39;][1] * torch.ones(len((state[&#39;x30002&#39;] == 1).nonzero()), 1)), scale=(2 * torch.ones(len((state[&#39;x30002&#39;] == 1).nonzero()), 1)))
		log_pdf = log_pdf + dst_.log_pdf(state[&#39;y30005&#39;])
		dst_ = dist.Normal(loc=(state[&#39;x30001&#39;][2] * torch.ones(len((state[&#39;x30002&#39;] == 2).nonzero()), 1)), scale=(2 * torch.ones(len((state[&#39;x30002&#39;] == 2).nonzero()), 1)))
		log_pdf = log_pdf + dst_.log_pdf(state[&#39;y30006&#39;])
		dst_ = dist.Normal(loc=(state[&#39;x30001&#39;][3] * torch.ones(len((state[&#39;x30002&#39;] == 3).nonzero()), 1)), scale=(2 * torch.ones(len((state[&#39;x30002&#39;] == 3).nonzero()), 1)))
		log_pdf = log_pdf + dst_.log_pdf(state[&#39;y30007&#39;])
		dst_ = dist.Normal(loc=(state[&#39;x30001&#39;][4] * torch.ones(len((state[&#39;x30002&#39;] == 4).nonzero()), 1)), scale=(2 * torch.ones(len((state[&#39;x30002&#39;] == 4).nonzero()), 1)))
		log_pdf = log_pdf + dst_.log_pdf(state[&#39;y30008&#39;])
		dst_ = dist.Normal(loc=(state[&#39;x30001&#39;][5] * torch.ones(len((state[&#39;x30002&#39;] == 5).nonzero()), 1)), scale=(2 * torch.ones(len((state[&#39;x30002&#39;] == 5).nonzero()), 1)))
		log_pdf = log_pdf + dst_.log_pdf(state[&#39;y30009&#39;])
		dst_ = dist.Normal(loc=(state[&#39;x30001&#39;][6] * torch.ones(len((state[&#39;x30002&#39;] == 6).nonzero()), 1)), scale=(2 * torch.ones(len((state[&#39;x30002&#39;] == 6).nonzero()), 1)))
		log_pdf = log_pdf + dst_.log_pdf(state[&#39;y30010&#39;])
		dst_ = dist.Normal(loc=(state[&#39;x30001&#39;][7] * torch.ones(len((state[&#39;x30002&#39;] == 7).nonzero()), 1)), scale=(2 * torch.ones(len((state[&#39;x30002&#39;] == 7).nonzero()), 1)))
		log_pdf = log_pdf + dst_.log_pdf(state[&#39;y30011&#39;])
		dst_ = dist.Normal(loc=(state[&#39;x30001&#39;][8] * torch.ones(len((state[&#39;x30002&#39;] == 8).nonzero()), 1)), scale=(2 * torch.ones(len((state[&#39;x30002&#39;] == 8).nonzero()), 1)))
		log_pdf = log_pdf + dst_.log_pdf(state[&#39;y30012&#39;])
		dst_ = dist.Normal(loc=(state[&#39;x30001&#39;][9] * torch.ones(len((state[&#39;x30002&#39;] == 9).nonzero()), 1)), scale=(2 * torch.ones(len((state[&#39;x30002&#39;] == 9).nonzero()), 1)))
		log_pdf = log_pdf + dst_.log_pdf(state[&#39;y30013&#39;])
		return log_pdf

	def gen_log_pdf_transformed(self, state):
		log_pdf = 0
		dst_ = dist.Normal(loc=torch.zeros(2, 1), scale=(2 * torch.ones(2, 1)), transformed=True)
		log_pdf = log_pdf + dst_.log_pdf(state[&#39;x30001&#39;])
		dst_ = dist.Categorical(probs=torch.tensor((0.5 * torch.ones(10, 2))), transformed=True)
		log_pdf = log_pdf + dst_.log_pdf(state[&#39;x30002&#39;])
		dst_ = dist.Normal(loc=(state[&#39;x30001&#39;][0] * torch.ones(len((state[&#39;x30002&#39;] == 0).nonzero()), 1)), scale=(2 * torch.ones(len((state[&#39;x30002&#39;] == 0).nonzero()), 1)), transformed=True)
		log_pdf = log_pdf + dst_.log_pdf(state[&#39;y30004&#39;])
		dst_ = dist.Normal(loc=(state[&#39;x30001&#39;][1] * torch.ones(len((state[&#39;x30002&#39;] == 1).nonzero()), 1)), scale=(2 * torch.ones(len((state[&#39;x30002&#39;] == 1).nonzero()), 1)), transformed=True)
		log_pdf = log_pdf + dst_.log_pdf(state[&#39;y30005&#39;])
		dst_ = dist.Normal(loc=(state[&#39;x30001&#39;][2] * torch.ones(len((state[&#39;x30002&#39;] == 2).nonzero()), 1)), scale=(2 * torch.ones(len((state[&#39;x30002&#39;] == 2).nonzero()), 1)), transformed=True)
		log_pdf = log_pdf + dst_.log_pdf(state[&#39;y30006&#39;])
		dst_ = dist.Normal(loc=(state[&#39;x30001&#39;][3] * torch.ones(len((state[&#39;x30002&#39;] == 3).nonzero()), 1)), scale=(2 * torch.ones(len((state[&#39;x30002&#39;] == 3).nonzero()), 1)), transformed=True)
		log_pdf = log_pdf + dst_.log_pdf(state[&#39;y30007&#39;])
		dst_ = dist.Normal(loc=(state[&#39;x30001&#39;][4] * torch.ones(len((state[&#39;x30002&#39;] == 4).nonzero()), 1)), scale=(2 * torch.ones(len((state[&#39;x30002&#39;] == 4).nonzero()), 1)), transformed=True)
		log_pdf = log_pdf + dst_.log_pdf(state[&#39;y30008&#39;])
		dst_ = dist.Normal(loc=(state[&#39;x30001&#39;][5] * torch.ones(len((state[&#39;x30002&#39;] == 5).nonzero()), 1)), scale=(2 * torch.ones(len((state[&#39;x30002&#39;] == 5).nonzero()), 1)), transformed=True)
		log_pdf = log_pdf + dst_.log_pdf(state[&#39;y30009&#39;])
		dst_ = dist.Normal(loc=(state[&#39;x30001&#39;][6] * torch.ones(len((state[&#39;x30002&#39;] == 6).nonzero()), 1)), scale=(2 * torch.ones(len((state[&#39;x30002&#39;] == 6).nonzero()), 1)), transformed=True)
		log_pdf = log_pdf + dst_.log_pdf(state[&#39;y30010&#39;])
		dst_ = dist.Normal(loc=(state[&#39;x30001&#39;][7] * torch.ones(len((state[&#39;x30002&#39;] == 7).nonzero()), 1)), scale=(2 * torch.ones(len((state[&#39;x30002&#39;] == 7).nonzero()), 1)), transformed=True)
		log_pdf = log_pdf + dst_.log_pdf(state[&#39;y30011&#39;])
		dst_ = dist.Normal(loc=(state[&#39;x30001&#39;][8] * torch.ones(len((state[&#39;x30002&#39;] == 8).nonzero()), 1)), scale=(2 * torch.ones(len((state[&#39;x30002&#39;] == 8).nonzero()), 1)), transformed=True)
		log_pdf = log_pdf + dst_.log_pdf(state[&#39;y30012&#39;])
		dst_ = dist.Normal(loc=(state[&#39;x30001&#39;][9] * torch.ones(len((state[&#39;x30002&#39;] == 9).nonzero()), 1)), scale=(2 * torch.ones(len((state[&#39;x30002&#39;] == 9).nonzero()), 1)), transformed=True)
		log_pdf = log_pdf + dst_.log_pdf(state[&#39;y30013&#39;])
		return log_pdf.sum()

	def gen_prior_samples(self):
		state = {}
		dst_ = dist.Normal(loc=torch.zeros(2, 1), scale=(2 * torch.ones(2, 1)))
		state[&#39;x30001&#39;] = dst_.sample()
		dst_ = dist.Categorical(probs=torch.tensor((0.5 * torch.ones(10, 2))))
		state[&#39;x30002&#39;] = dst_.sample(sample_size=2)
		state[&#39;data_30003&#39;] = [-2.0, -2.5, -1.7, -1.9, -2.2, 1.5, 2.2, 3.0, 1.2, 2.8, -1.7, -1.3, 3.2, 0.8, -0.9, 0.3, 1.4, 2.1, 0.8, 1.9]
		dst_ = dist.Normal(loc=(state[&#39;x30001&#39;][0] * torch.ones(len((state[&#39;x30002&#39;] == 0).nonzero()), 1)), scale=(2 * torch.ones(len((state[&#39;x30002&#39;] == 0).nonzero()), 1)))
		state[&#39;y30004&#39;] = torch.tensor([state[&#39;data_30003&#39;]])[(state[&#39;x30002&#39;] == 0).nonzero()]
		dst_ = dist.Normal(loc=(state[&#39;x30001&#39;][1] * torch.ones(len((state[&#39;x30002&#39;] == 1).nonzero()), 1)), scale=(2 * torch.ones(len((state[&#39;x30002&#39;] == 1).nonzero()), 1)))
		state[&#39;y30005&#39;] = torch.tensor([state[&#39;data_30003&#39;]])[(state[&#39;x30002&#39;] == 1).nonzero()]
		dst_ = dist.Normal(loc=(state[&#39;x30001&#39;][2] * torch.ones(len((state[&#39;x30002&#39;] == 2).nonzero()), 1)), scale=(2 * torch.ones(len((state[&#39;x30002&#39;] == 2).nonzero()), 1)))
		state[&#39;y30006&#39;] = torch.tensor([state[&#39;data_30003&#39;]])[(state[&#39;x30002&#39;] == 2).nonzero()]
		dst_ = dist.Normal(loc=(state[&#39;x30001&#39;][3] * torch.ones(len((state[&#39;x30002&#39;] == 3).nonzero()), 1)), scale=(2 * torch.ones(len((state[&#39;x30002&#39;] == 3).nonzero()), 1)))
		state[&#39;y30007&#39;] = torch.tensor([state[&#39;data_30003&#39;]])[(state[&#39;x30002&#39;] == 3).nonzero()]
		dst_ = dist.Normal(loc=(state[&#39;x30001&#39;][4] * torch.ones(len((state[&#39;x30002&#39;] == 4).nonzero()), 1)), scale=(2 * torch.ones(len((state[&#39;x30002&#39;] == 4).nonzero()), 1)))
		state[&#39;y30008&#39;] = torch.tensor([state[&#39;data_30003&#39;]])[(state[&#39;x30002&#39;] == 4).nonzero()]
		dst_ = dist.Normal(loc=(state[&#39;x30001&#39;][5] * torch.ones(len((state[&#39;x30002&#39;] == 5).nonzero()), 1)), scale=(2 * torch.ones(len((state[&#39;x30002&#39;] == 5).nonzero()), 1)))
		state[&#39;y30009&#39;] = torch.tensor([state[&#39;data_30003&#39;]])[(state[&#39;x30002&#39;] == 5).nonzero()]
		dst_ = dist.Normal(loc=(state[&#39;x30001&#39;][6] * torch.ones(len((state[&#39;x30002&#39;] == 6).nonzero()), 1)), scale=(2 * torch.ones(len((state[&#39;x30002&#39;] == 6).nonzero()), 1)))
		state[&#39;y30010&#39;] = torch.tensor([state[&#39;data_30003&#39;]])[(state[&#39;x30002&#39;] == 6).nonzero()]
		dst_ = dist.Normal(loc=(state[&#39;x30001&#39;][7] * torch.ones(len((state[&#39;x30002&#39;] == 7).nonzero()), 1)), scale=(2 * torch.ones(len((state[&#39;x30002&#39;] == 7).nonzero()), 1)))
		state[&#39;y30011&#39;] = torch.tensor([state[&#39;data_30003&#39;]])[(state[&#39;x30002&#39;] == 7).nonzero()]
		dst_ = dist.Normal(loc=(state[&#39;x30001&#39;][8] * torch.ones(len((state[&#39;x30002&#39;] == 8).nonzero()), 1)), scale=(2 * torch.ones(len((state[&#39;x30002&#39;] == 8).nonzero()), 1)))
		state[&#39;y30012&#39;] = torch.tensor([state[&#39;data_30003&#39;]])[(state[&#39;x30002&#39;] == 8).nonzero()]
		dst_ = dist.Normal(loc=(state[&#39;x30001&#39;][9] * torch.ones(len((state[&#39;x30002&#39;] == 9).nonzero()), 1)), scale=(2 * torch.ones(len((state[&#39;x30002&#39;] == 9).nonzero()), 1)))
		state[&#39;y30013&#39;] = torch.tensor([state[&#39;data_30003&#39;]])[(state[&#39;x30002&#39;] == 9).nonzero()]
		return state

	def get_arcs(self):
		return self.arcs

	def get_arcs_names(self):
		return [(u.name, v.name) for (u, v) in self.arcs]

	def get_conditions(self):
		return self.conditionals

	def get_vars(self):
		return [v.name for v in self.vertices if v.is_sampled]

	def get_vertices(self):
		return self.vertices

	def get_vertices_names(self):
		return [v.name for v in self.vertices]

	def is_torch_imported(self):
		import sys 
		print(&#39;torch&#39; in sys.modules) 
		print(torch.__version__) 
		print(type(torch.tensor)) 
		import inspect 
		print(inspect.getfile(torch))

</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="The-dependency-graph">The dependency graph<a class="anchor-link" href="#The-dependency-graph">&#182;</a></h2>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[60]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">vertices</span> <span class="o">=</span> <span class="n">compiled_python</span><span class="o">.</span><span class="n">vertices</span>
<span class="n">create_network_graph</span><span class="p">(</span><span class="n">vertices</span><span class="o">=</span><span class="n">vertices</span><span class="p">)</span>
<span class="n">display_graph</span><span class="p">(</span><span class="n">vertices</span><span class="o">=</span><span class="n">vertices</span><span class="p">);</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>




<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="Coal-Mining-model">Coal Mining model<a class="anchor-link" href="#Coal-Mining-model">&#182;</a></h2><p>This model is popular change point detection model in the statistics community. The goal of the model is to infer, whether or not improvements in technology and safety had an impact on reducing the number of coal mining related deaths. See <a href="https://www.google.com/url?sa=t&amp;rct=j&amp;q=&amp;esrc=s&amp;source=web&amp;cd=7&amp;ved=0ahUKEwibzpmXxeTbAhVIPhQKHRxGCVEQFghFMAY&amp;url=https%3A%2F%2Fwiki.helsinki.fi%2Fdownload%2Fattachments%2F48865343%2FWB.pdf&amp;usg=AOvVaw0Vx-U9LuQU4j9W-dnLpZgr">here</a> for more details.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[4]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">model_coal_mining</span><span class="o">=</span><span class="s2">&quot;&quot;&quot;</span>
<span class="s2">e = sample(exponential(1))</span>
<span class="s2">l = sample(exponential(1))</span>
<span class="s2">T = 112</span>
<span class="s2">s = sample(uniform(0,10))</span>
<span class="s2">y = [4,5,4,1,0,4,3,4,0,6,3,3,4,0,2,6,3,3,5,4,5,3,1,4,4,1,5,5,</span>
<span class="s2">      3,4,2,5,2,2,3,4,2,1,3,2,1,1,1,1,1,3,0,0,1,0,1,1,0,0,3,1,</span>
<span class="s2">      0,3,2,2,0,1,1,1,0,1,0,1,0,0,0,2,1,0,0,0,1,1,0,2,2,3,1,1,</span>
<span class="s2">      2,1,1,1,1,2,4,2,0,0,0,1,4,0,0,0,1,0,0,0,0,0,1,0,0,1,0,0]</span>
<span class="s2">for i in range(T-1):</span>
<span class="s2">    if i+1 &lt; s:</span>
<span class="s2">        observe(exponential(e), y[i])</span>
<span class="s2">    else:</span>
<span class="s2">        observe(exponential(1), y[i])</span>
<span class="s2">[e,l,s]</span>
<span class="s2">&quot;&quot;&quot;</span>
<span class="n">compiled_python</span> <span class="o">=</span> <span class="n">compile_model</span><span class="p">(</span><span class="n">model_coal_mining</span><span class="p">,</span> <span class="n">language</span><span class="o">=</span><span class="s1">&#39;python&#39;</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h2 id="The-dependency-graph">The dependency graph<a class="anchor-link" href="#The-dependency-graph">&#182;</a></h2>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[5]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">vertices</span> <span class="o">=</span> <span class="n">compiled_python</span><span class="o">.</span><span class="n">vertices</span>
<span class="n">create_network_graph</span><span class="p">(</span><span class="n">vertices</span><span class="o">=</span><span class="n">vertices</span><span class="p">)</span>
<span class="n">display_graph</span><span class="p">(</span><span class="n">vertices</span><span class="o">=</span><span class="n">vertices</span><span class="p">);</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area">

<div class="prompt"></div>




<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
"
>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered"><div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>I would like to thank <a href="http://www.cs.ox.ac.uk/people/andrea.patane/">Andrea Patanè</a>, <a href="http://ori.ox.ac.uk/mrg_people/sasha-salter/">Sasha Salter</a> and Saeid Naderiparizi for proof reading the post.</p>

</div>
</div>
</div>
    </div>
  </div>
</body>

 


</html>
