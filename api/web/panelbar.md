---
title: kendo.ui.PanelBar
slug: web-kendo.ui.panelbar
tags: api,web
publish: true
---

# kendo.ui.PanelBar

## Description



The **PanelBar** displays hierarchical data as a multi-level, expandable widget that is useful for
constrained areas of a page. Its structure may be defined in HTML or configured dynamically through its API. The
content for items can also be loaded via AJAX by specifying a content URL.


### Getting Started


A **PanelBar** can be created by targeting the root element of a HTML list. A
**PanelBar** will utilize this list to define its structure and content.

#### Create a list of items

    <ul id="panelBar">
        <li>
            Item 1
                <ul>
                    <li>Sub Item 1</li>
                    <li>Sub Item 2</li>
                </ul>
        <li>
        <li>Item 2</li>
    </ul>

Initialization of a **PanelBar** should occur after the DOM is fully loaded. It is recommended
that initialization the **PanelBar** occur within a handler is provided to $(document).ready().

#### Initialize the PanelBar via an ID selector

    $(document).ready(function() {
        $("#panelBar").kendoPanelBar();
    });

**PanelBar** items may contain nested content (including markup) within a **div**
element. Text content located outside nested content will be used as the title of the item.

#### Create a list of items in HTML with nested content

    <ul id="panelBar">
        <li>Item with no content</li>
        <li>Item with content
            <div>This is nested content of a PanelBar item.</div>
        </li>
    </ul>

A **PanelBar** will preserve the content defined within an item.

#### Initialize the PanelBar via an ID selector

    var panelBar = $("#panelbar").kendoPanelBar();

#### Initialize a PanelBar using JSON data object

    $("#panelbar").kendoPanelBar({
        dataSource: [
            {
                text: "Item 1",
                url: "http://www.kendoui.com/"                  // link URL if navigation is needed (optional)
            },
            {
                text: "<b>Item 2</b>",
                encoded: false,                                 // Allows use of HTML for item text
                content: "text"                                 // content within an item
            },
            {
                text: "Item 3",
                contentUrl: "partialContent.html"               // content URL to load within an item
            },
            {
                text: "Item 4",
                imageUrl: "http://www.kendoui.com/test.jpg",    // item image URL, optional
                expanded: true,                                 // item is rendered expanded
                items: [{                                       // Sub item collection.
                    text: "Sub Item 1"
                },
                {
                    text: "Sub Item 2"
                }]
            },
            {
                text: "Item 5",
                // item image sprite CSS class, optional
                spriteCssClass: "imageClass3"
            }
        ]
    });

### Loading Content with AJAX


While any valid technique for loading AJAX content can be used, the **PanelBar** provides built-in
support for asynchronously loading content from URLs. These URLs should return HTML fragments that can be
loaded in the **PanelBar** item content area. Content DIVs should be completely empty for AJAX
loading to work.

#### Create a list of items with a target for dynamic content

    <ul id="panelBar">
        <li>Item 1
            <ul>
                <li>Sub Item 1</li>
            </ul>
        </li>
        <li>Item 2</li>
        <li>
            Item with Dynamic Content
            <div></div>
        </li>
    </ul>

#### Load a PanelBar item content asynchronously via AJAX

    $("#panelBar").kendoPanelBar({
        contentUrls:[
            null,
            null,
            "html-content-snippet.html"
        ]
    });

When the **PanelBar** loads remote content via AJAX, the server response is cached in-memory so
that subsequent expand/collapse actions do not trigger subsequent AJAX requests.


### Customizing PanelBar Animations


By default, a **PanelBar** uses animations to expand and reveal sub-items when an item header is
clicked. These animations can be modified in configuration via the open and close animation properties. A
**PanelBar** can also be configured to only allow one panel to remain open at a time.

#### Changing PanelBar animation and expandMode behavior

    $("#panelBar").kendoPanelBar({
        animation: {
            open : { effects: "fadeIn" }
        },
        expandMode: "single"
    });

### Dynamically Configuring PanelBar Items


The **PanelBar** API provides several methods for dynamically adding or removing Items. To add
items, provide the new item as a JSON object along with a reference item that will be used to determine its
placement in the items hierarchy. Note: The reference item is optional when appending.



A reference item is a target **PanelBar** item HTML element that already exists in the PanelBar.
Any valid selector can be used to obtain a reference to the target item.


Removing an item only requires a reference to the target element that should be removed.

#### Dynamically adding a new root PanelBar item

    var panelBar = $("#panelBar").kendoPanelBar().data("kendoPanelBar");
    
    panelBar.insertAfter(
         { text: "New PanelBar Item" },
         panelBar.element.children("li:last")
    );

### Accessing an Existing PanelBar


You can reference an existing **PanelBar** instance via
[jQuery.data()](http://api.jquery.com/jQuery.data/). Once a reference has been established, you can
use the API to control its behavior.

#### Accessing an existing PanelBar instance

    var panelBar = $("#panelBar").data("kendoPanelBar");

## Configuration

### animation `Object`

A collection of visual animations used when **PanelBar** items are opened or closed through
user interactions. Setting this option to **false** will disable all animations.

#### Example

    $("#panelBar").kendoPanelBar({
        animation: {
            // fade-out closing items over 1000 milliseconds
            close: {
                duration: 1000,
                effects: "fadeOut"
            },
           // fade-in and expand opening items over 500 milliseconds
           open: {
               duration: 500,
               effects: "expandVertical fadeIn"
           }
       }
    });

### animation.close `Object`

The visual animation(s) that will be used when **PanelBar** items are closed.

#### Example

    $("#panelBar").kendoPanelBar({
        animation: {
            close: {
                duration: 200,
                effects: "fadeOut"
            }
        }
    });

### animation.close.duration `Number`*(default: 200)*

The number of milliseconds used for the visual animation when a **PanelBar** item is closed.

#### Example

    $("#panelBar").kendoPanelBar({
        animation: {
            close: {
    
                       duration: 1000
    
                   }
      }
    });

### animation.close.effects `String`

A whitespace-delimited string of animation effects that are utilized when a **PanelBar** item
is closed. Options include **"fadeOut"**.

#### Example

    $("#panelBar").kendoPanelBar({
        animation: {
            close: {
                duration: 1000,
                effects: "fadeOut"
            }
        }
    });

### animation.open `Object`

The visual animation(s) that will be used when opening items.

#### Example

    $("#panelBar").kendoPanelBar({
        animation: {
            open: {
                duration: 200,
                effects: "expandVertical"
            }
        }
    });

### animation.open.duration `Number`*(default: 200)*

The number of milliseconds used for the visual animation when an item is opened.

#### Example

    $("#panelBar").kendoPanelBar({
     animation: {
          open: {
              duration: 1000
          }
       }
    });

### animation.open.effects `String`*(default: "expandVertical")*

A whitespace-delimited string of animation effects that are used when an item is expanded. Options include
**"expandVertical"** and **"fadeIn"**.

### animation.open.show `Boolean`*(default: true)*



### expandMode `String`*(default: "multiple")*

Specifies how the **PanelBar** items are displayed when opened and closed. The following values
are available:


#### *"single"*

Display one item at a time when an item is opened; opening an item will close the previously opened item.

#### *"multiple"*

Display multiple values at one time; opening an item has no visual impact on any other items in the **PanelBar**.

#### Example

    $("#panelBar").kendoPanelBar({
        expandMode: "single"
    });

## Methods

### append

Appends an item to the PanelBar.

#### Example

    var panelBar = $("#panelBar").data("kendoPanelBar");
    panelBar.append(
        [
            {
                text: "Item 1",
                url: "http://www.kendoui.com/"                  // link URL if navigation is needed (optional)
            },
            {
                text: "<b>Item 2</b>",
                encoded: false,                                 // Allows use of HTML for item text
                content: "text"                                 // content within an item
            },
            {
                text: "Item 3",
                contentUrl: "partialContent.html"               // content URL to load within an item
            },
            {
                text: "Item 4",
                imageUrl: "http://www.kendoui.com/test.jpg",    // item image URL, optional
                expanded: true,                                 // item is rendered expanded
                items: [{                                       // Sub item collection.
                    text: "Sub Item 1"
                },
                {
                    text: "Sub Item 2"
                }]
            },
            {
                text: "Item 5",
                // item image sprite CSS class, optional
                spriteCssClass: "imageClass3"
            }
        ],
        referenceItem
    );

#### Parameters

##### item `Selector`

Target item, specified as the JSON representation of an object. You can pass item text, content or
contentUrl here. Can handle an HTML string or array of such strings or JSON.

##### referenceItem `Item`

A reference item to append the new item in

#### Returns

`PanelBar` Returns the PanelBar object to support chaining.

### collapse

Collapses the specified item(s) of a **PanelBar**.

#### Example

    // access an existing PanelBar instance
    var panelBar = $("#panelBar").data("kendoPanelBar");
    // collapse the element with ID, "item1"
    panelBar.collapse($("#item1"));
    // collapse the element with ID, "item2" without visual animations
    panelBar.collapse($("#item2"), false);
    // collapse all list items that start with ID, "item"
    panelBar.collapse($('[id^="item"]'));

#### Parameters

##### element `Selector`

The **PanelBar** item(s) to be collapsed, expressed as a string containing a selector
expression or represented by a [jQuery selector](http://api.jquery.com/category/selectors/).

##### useAnimation `Boolean`

_optional, default: _

Temporarily enables (**true**) or disables (**false**) any visual animation(s)
when collapsing items.

#### Returns

`PanelBar` Returns the PanelBar object to support chaining.

### enable

Enables (**true**) or disables (**false**) the specified item(s) of the
**PanelBar**.

#### Example

    // access an existing PanelBar instance
    var panelBar = $("#panelBar").data("kendoPanelBar");
    // enable the item of the PanelBar with ID, "item1"
    panelBar.enable($("#item1"), true);
    // disable the currently selected item of the PanelBar
    var item = panelBar.select();
    panelBar.enable(item, false);
    // disable all list items that start with ID, "item"
    panelBar.enable($('[id^="item"]'), false);

#### Parameters

##### element `String | Selector`

The **PanelBar** item(s) to be enabled (**true**) or disabled (**false**), expressed as a
string containing a selector expression or represented by a
[jQuery selector](http://api.jquery.com/category/selectors/).

##### enable `Boolean`

The desired state - enabled (**true**) or disabled (**false**) - of the target
element(s).

### expand

Expands the specified item(s) of a **PanelBar**.

#### Example

    // access an existing PanelBar instance
    var panelBar = $("#panelBar").data("kendoPanelBar");
    // expand the element with ID, "item1"
    panelBar.expand($("#item1"));
    // expand the element with ID, "item2" without visual animations
    panelBar.expand($("#item2"), false);
    // expand all list items that start with ID, "item"
    panelBar.expand($('[id^="item"]'));

#### Parameters

##### element `Selector`

The **PanelBar** item(s) to be expanded, expressed as a selector.

##### useAnimation `Boolean`

_optional, default: _

Temporariliy enables (**true**) or disables (**false**) any visual animation(s) when expanding items.

#### Returns

`PanelBar` Returns the PanelBar object to support chaining.

### insertAfter

Inserts a PanelBar item after the specified referenceItem

#### Example

    panelBar.insertAfter(
        [{
            text: "Item 1",
            url: "http://www.kendoui.com"                // Link URL if navigation is needed, optional.
        },
        {
            text: "<b>Item 2</b>",
            encoded: false,                              // Allows use of HTML for item text
            content: "text"                              // Content for the content element
        },
        {
            text: "Item 3",
            contentUrl: "partialContent.html"            // From where to load the item content
        },
        {
            text: "Item 4",
            imageUrl: "http://www.kendoui.com/test.jpg", // Item image URL, optional.
            expanded: true,                              // item is rendered expanded
            items: [{                                    // Sub item collection.
                 text: "Sub Item 1"
            },
            {
                 text: "Sub Item 2"
            }]
        },
        {
            text: "Item 5",
            spriteCssClass: "imageClass3"                // Item image sprite CSS class, optional.
        }],
        referenceItem
    );

#### Parameters

##### item `Selector`

Target item, specified as a JSON object. You can pass item text, content or contentUrl here. Can handle an HTML string or array of such strings or JSON.

##### referenceItem `Item`

A reference item to insert the new item after

### insertBefore

Inserts a PanelBar item before the specified referenceItem

#### Example

    panelBar.insertBefore(
        [{
            text: "Item 1",
            url: "http://www.kendoui.com"                // Link URL if navigation is needed, optional.
        },
        {
            text: "<b>Item 2</b>",
            encoded: false,                              // Allows use of HTML for item text
            content: "text"                              // Content for the content element
        },
        {
            text: "Item 3",
            contentUrl: "partialContent.html"            // From where to load the item content
        },
        {
            text: "Item 4",
            imageUrl: "http://www.kendoui.com/test.jpg", // Item image URL, optional.
            expanded: true,                              // item is rendered expanded
            items: [{                                    // Sub item collection.
                 text: "Sub Item 1"
            },
            {
                 text: "Sub Item 2"
            }]
        },
        {
            text: "Item 5",
            spriteCssClass: "imageClass3"                // Item image sprite CSS class, optional.
        }],
        referenceItem
    );

#### Parameters

##### item `Selector`

Target item, specified as a JSON object. You can pass item text, content or contentUrl here. Can handle an
TML string or array of such strings or JSON.

##### referenceItem `Item`

A reference item to insert the new item before.

#### Returns

`PanelBar` Returns the PanelBar object to support chaining.

### reload

Reloads the content of a **PanelBar** from an AJAX request.

#### Example

    // get a reference to the panel bar
    var panelBar = $("#panelBar").data("kendoPanelBar");
    // reload the panel basr
    panelBar.reload();

#### Parameters

##### element `Selector`

Target element

### remove

Removes the specified PanelBar item(s).

#### Example

    // get a reference to the panel bar
    var panelBar = $("#panelBar").data("kendoPanelBar");
    // remove Item 1
    panelBar.remove("#Item1");

#### Parameters

##### element `Selector`

Target item selector.

### select

Selects the specified item of the **PanelBar**. If this method is invoked without arguments, it
returns the currently selected item.

#### Example

    // access an existing PanelBar instance
    var panelBar = $("#panelBar").data("kendoPanelBar");
    // select the item with ID, "item1"
    panelBar.select("#item1");

#### Parameters

##### element `String | Selector`

The **PanelBar** item to be selected, expressed as a string containing a selector expression or
represented by a [jQuery selector](http://api.jquery.com/category/selectors/).

## Events

### activate

Triggered when an item of a PanelBar is activated.

#### Attach activate event handler during initialization; detach via unbind()

    // event handler for activate
    var onActivate = function(e) {
        // access the activated item via e.item (HTMLElement)
    };
    
    // attach activate event handler during initialization
    var panelBar = $("#panelBar").kendoPanelBar({
        activate: onActivate
    });
    
    // detach activate event handler via unbind()
    panelBar.data("kendoPanelBar").unbind("activate", onActivate);

#### Attach activate event handler via bind(); detach via unbind()

    // event handler for activate
    var onActivate = function(e) {
        // access the activated item via e.item (HTMLElement)
    };
    
    // attach activate event handler via bind()
    $("#panelBar").data("kendoPanelBar").bind("activate", onActivate);
    
    // detach activate event handler via unbind()
    $("#panelBar").data("kendoPanelBar").unbind("activate", onActivate);

#### Event Data

##### e.item `Element`

The activated item of the PanelBar.

### collapse

Triggered when an item of a PanelBar is collapsed.

#### Attach collapse event handler during initialization; detach via unbind()

    // event handler for collapse
    var onCollapse = function(e) {
        // access the collapsed item via e.item (HTMLElement)
    };
    
    // attach collapse event handler during initialization
    var panelBar = $("#panelBar").kendoPanelBar({
        collapse: onCollapse
    });
    
    // detach collapse event handler via unbind()
    panelBar.data("kendoPanelBar").unbind("collapse", onCollapse);

#### Attach collapse event handler via bind(); detach via unbind()

    // event handler for collapse
    var onCollapse = function(e) {
        // access the collapsed item via e.item (HTMLElement)
    };
    
    // attach collapse event handler via bind()
    $("#panelBar").data("kendoPanelBar").bind("collapse", onCollapse);
    
    // detach collapse event handler via unbind()
    $("#panelBar").data("kendoPanelBar").unbind("collapse", onCollapse);

#### Event Data

##### e.item `Element`

The collapsing item of the PanelBar.

### contentLoad

Fires when content is fetched from an AJAX request.

#### Example

    $("#panelBar").kendoPanelBar({
        contentLoad: function(e) {
            // handle event
        }
    });

#### To set after intialization

    // get a reference to the panel bar
    var panelBar = $("#panelBar").data("kendoPanelBar");
    // bind the contentLoad event
    panelBar.bind("contentLoad", function(e) {
        // handle event
    });

#### Event Data

##### e.item `Element`

The selected item

##### e.contentElement `Element`

The loaded content element

### error

Fires when AJAX request results in an error.

#### Example

    $("#panelBar").kendoPanelBar({
        error: function(e) {
            // handle event
        }
    });

#### To set after intialization

    // get a reference to the panel bar
    var panelBar = $("#panelBar").data("kendoPanelBar");
    // bind the error ajax event
    panelBar.bind("error", function(e) {
        // handle event
    });

#### Event Data

##### e.xhr `jqXHR`

The jqXHR object used to load the content

##### e.status `String`

The returned status.

### expand

Triggered when an item of a PanelBar is expanded.

#### Attach expand event handler during initialization; detach via unbind()

    // event handler for expand
    var onExpand = function(e) {
        // access the expanded item via e.item (HTMLElement)
    };
    
    // attach expand event handler during initialization
    var panelBar = $("#panelBar").kendoPanelBar({
        expand: onExpand
    });
    
    // detach expand event handler via unbind()
    panelBar.data("kendoPanelBar").unbind("expand", onExpand);

#### Attach expand event handler via bind(); detach via unbind()

    // event handler for expand
    var onExpand = function(e) {
        // access the expanded item via e.item (HTMLElement)
    };
    
    // attach expand event handler via bind()
    $("#panelBar").data("kendoPanelBar").bind("expand", onExpand);
    
    // detach expand event handler via unbind()
    $("#panelBar").data("kendoPanelBar").unbind("expand", onExpand);

#### Event Data

##### e.item `Element`

The expanding item of the PanelBar.

### select

Triggered when an item of a PanelBar is selected.

#### Attach select event handler during initialization; detach via unbind()

    // event handler for select
    var onSelect = function(e) {
        // access the selected item via e.item (HTMLElement)
    };
    
    // attach select event handler during initialization
    var panelBar = $("#panelBar").kendoPanelBar({
        select: onSelect
    });
    
    // detach select event handler via unbind()
    panelBar.data("kendoPanelBar").unbind("select", onSelect);

#### Attach select event handler via bind(); detach via unbind()

    // event handler for select
    var onSelect = function(e) {
        // access the selected item via e.item (HTMLElement)
    };
    
    // attach select event handler via bind()
    $("#panelBar").data("kendoPanelBar").bind("select", onSelect);
    
    // detach select event handler via unbind()
    $("#panelBar").data("kendoPanelBar").unbind("select", onSelect);

#### Event Data

##### e.item `Element`

The selected item of the PanelBar.