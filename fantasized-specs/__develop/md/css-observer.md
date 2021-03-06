# CSS Observer Module level 1

## Fantasized Draft, ${LastUpdate}

<dl>
<dt>This version:</dt>
<dd><a href="https://hiroyau.ga/fantasized-specs/css-observer.html">https://hiroyau.ga/fantasized-specs/css-observer.html</a></dd>
<dt>Editors:</dt>
<dd><a href="https://github.com/]">Hiroya Uga</a></dd>
<dt>Issue Tracking:</dt>
<dd><a href="https://github.com/hiroya-uga/hiroya-uga.github.io/blob/master/fantasized-specs/css-observer.html">GitHub Issues</a></dd>
</dl>


## Abstract

This module introduces the ability to  observe the status of elements, with new css properties and pseudo classes. For example, entering and leaving of elements the screen view area by scroll, and changing the `display` property of elements. The define of these are approach to enable  interaction implementation without JavaScript.

[TOC]


## 1. Introduction

Sometimes in web pages, elements are required a change style when enters the screen by scroll. For example, elements is observed by such as the [Intersection Observer API](https://w3c.github.io/IntersectionObserver/), and change style by manipulating the attributes of the elements entered on the screen is adopted. In that case, may be used CSS Transitions, CSS Animations, and requestAnimationFrame often.

This module realizes such an expression only with CSS, without processing of start and end of observer by JavaScript.


## 2. Observers

### 2.1. The `observe-type` property

<div class="propdef">
<table>
<tbody>
<tr>
<th>Name:</th>
<td><dfn>observe-type</dfn></td>
</tr>

<tr>
<th>value:</th>
<td>none | [view | view-in | view-out | view-top | view-right | view-bottom | view-left | [ view-top-in || view-right-in || view-bottom-in || view-left-in || view-top-out || view-right-out || view-bottom-out || view-left-out ] ] || display</td>
</tr>

<tr>
<th>Initial:</th>
<td>none</td>
</tr>

<tr>
<th>Applies to:</th>
<td>See below</td>
</tr>

<tr>
<th>Inherited:</th>
<td>no</td>
</tr>

<tr>
<th>Percentages:</th>
<td>n/a</td>
</tr>

<tr>
<th>Computed value:</th>
<td>specified keyword(s)</td>
</tr>

<tr>
<th>Animation type:</th>
<td>not animatable</td>
</tr>
</tbody>
</table>
</div>

<dl>
<dt><dfn>none</dfn></dt>
<dd>The user agent do not observe element.</dd>

<dt><dfn>view</dfn></dt>
<dd>The user agent observe entry and exit of elements in all directions.</dd>

<dt><dfn>view-in</dfn></dt>
<dd>The user agent observe entry of elements in all directions.</dd>

<dt><dfn>view-out</dfn></dt>
<dd>The user agent observe exit of elements in all directions.</dd>

<dt><dfn>view-*</dfn></dt>
<dd>This asterisk of notation replaced the move keyword(ex. in, out). This The user agent observe entry or exit elements in all directions.</dd>

<dt><dfn>view-*-in</dfn></dt>
<dd>This asterisk of notation replaced the direction keyword(ex. top, right, bottom, left). This The user agent observe entry of elements in instructed directions.</dd>

<dt><dfn>view-*-out</dfn></dt>
<dd>This asterisk of notation replaced the direction keyword(ex. top, right, bottom, left). The user agent observe exit of elements in instructed directions.</dd>

<dt><dfn>display</dfn></dt>
<dd>The user agent observe css display property of elements. Communicate the CSSOM of change after  ​​to the user agent, before properties change from none to the values ​​that form <a href="https://www.w3.org/TR/CSS22/box.html">box models</a>. This spec is to support CSS transition animation work without requestAnimationFrame, even if display property changes from none to block at same time.</dd>
<dd class="example">

```javascript
function sample () {
  target.style.display = 'none';
  target.style.height = 0;

  button.addEventListener('click', function () {
    target.style.display = 'block';

    // requestAnimationFrame(() => {
    target.style.height = '100px';
    // });
  });
}
```

</dd>
<dd class="example">

```css
a div {
  display: none;
  height: 0;
  transition: .2s height ease-out;
  observe: display; /* The user agent is observing change of display property. */
}

a:hover div,
a:focus div {
  display: block;
  height: 100px; /* CSS Transitions work because the user agent is known that height of this element is 0. */
}
```

</dd>
</dl>

### 2.3. The `observe-disconect` property

<div class="propdef">
<table>
<tbody>
<tr>
<th>Name:</th>
<td><dfn>observe-conect</dfn></td>
</tr>

<tr>
<th>value:</th>
<td>once | infinite</td>
</tr>

<tr>
<th>Initial:</th>
<td>once</td>
</tr>

<tr>
<th>Applies to:</th>
<td>See below</td>
</tr>

<tr>
<th>Inherited:</th>
<td>no</td>
</tr>

<tr>
<th>Percentages:</th>
<td>n/a</td>
</tr>

<tr>
<th>Computed value:</th>
<td>specified keyword(s)</td>
</tr>

<tr>
<th>Animation type:</th>
<td>not animatable</td>
</tr>
</tbody>
</table>
</div>


## 3. Selectors

### 3.1. Pseudo-classes


## 4. Usege

<div class="example">

```css
div {
   observe: view-top once;
   transition: .2s opacity ease-out;
   opacity: 1; /* For not support browsers */
}

div:view-in {
   opacity: 1;  /* In the screen */
}

div:view-out {
  opacity: 0;   /* Out of screen */
}
```

</div>
