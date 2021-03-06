---
title: Layout Manager Directive
_description: Only Ignite UI for Angular Layout Manager directive provides various styles of responsive and fluid user interfaces.
_keywords: Ignite UI for Angular, UI controls, Angular widgets, web widgets, UI widgets, Angular, Native Angular Components Suite, Native Angular Controls, Native Angular Components Library, Angular Layout Manager component, Angular Layout Manager controls
---

##Layout Manager
<p class="highlight">The Ignite UI for Angular Layout Directive allows developers to specify a layout direction for any children of the container it is applied to. Layout can flow vertically or horizontally, with controls for wrapping, justification, and alignment.</p>
<div class="divider"></div>

### Layout Demo
<div class="sample-container loading" style="height: 2460px">
    <iframe id="layout-sample-iframe" src='{environment:demosBaseUrl}/layouts/layout' width="100%" height="100%" seamless frameBorder="0" onload="onSampleIframeContentLoaded(this);"></iframe>
</div>
<div>
    <button data-localize="stackblitz" disabled class="stackblitz-btn" data-iframe-id="layout-sample-iframe" data-demos-base-url="{environment:demosBaseUrl}">view on stackblitz</button>
</div>
<div class="divider--half"></div>

###Usage
Use the [**igxLayout**]({environment:angularApiUrl}/classes/igxlayoutdirective.html) directive on a container element to specify the layout
direction for its children: horizontally with [`igxLayoutDir`]({environment:angularApiUrl}/classes/igxlayoutdirective.html#dir)`="row"` or vertically with
[`igxLayoutDir`]({environment:angularApiUrl}/classes/igxlayoutdirective.html#dir)`="column"`.

**Note**: the [`igxLayout`]({environment:angularApiUrl}/classes/igxlayoutdirective.html) directive affects the flow directions for that
container's **immediate** children.
<div class="divider--half"></div>

### Nesting
Use the [`igxFlex`]({environment:angularApiUrl}/classes/igxflexdirective.html) directive for elements inside an [`igxLayout`]({environment:angularApiUrl}/classes/igxlayoutdirective.html) parent to control specific flexbox properties.
<div class="divider--half"></div>


### API References
<div class="divider--half"></div>

* [IgxLayoutDirective]({environment:angularApiUrl}/classes/igxlayoutdirective.html)
* [IgxFlexDirective]({environment:angularApiUrl}/classes/igxflexdirective.html)