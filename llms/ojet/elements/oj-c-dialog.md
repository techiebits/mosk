Since:

- 18.0.0

Module:

- dialog

## QuickNav

### [Events](#events-section)

- [ojBeforeClose](#event:ojBeforeClose)
- [ojClose](#event:ojClose)
- [ojDragEnd](#event:ojDragEnd)
- [ojDragMove](#event:ojDragMove)
- [ojDragStart](#event:ojDragStart)
- [ojFocus](#event:ojFocus)
- [ojOpen](#event:ojOpen)
- [ojResize](#event:ojResize)
- [ojResizeEnd](#event:ojResizeEnd)
- [ojResizeStart](#event:ojResizeStart)

  

### JET Dialog[](#dialogOverview-section "Bookmarkable Link")

Description: A Dialog is a floating window that typically contains a header, content and footer area. A Dialog is typically modal and centered in viewport. The dialog window can be moved by dragging on the title area, and closed with the 'x' icon (by default). Dialogs can also be resized by dragging on edges or corners of the dialog component.

If the content length exceeds the maximum height, a scrollbar will automatically appear.

```

<oj-c-dialog opened="true">
   <div slot="header">Dialog Header</div>
   <div slot="body">Dialog Body</div>
   <div slot="footer">Dialog Footer</div>
</oj-c-dialog>

Main section content
```

### Focus[](#focus-section "Bookmarkable Link")

Upon opening a dialog, focus is automatically moved to the first item that matches the following:

1. The first `:tabbable` element within the dialog body
2. The first `:tabbable` element within the dialog footer
3. The dialog's close button
4. The dialog itself

The use of the HTML `autofocus` global attribute is discouraged. If specified, the dialog will try to honor it but it may have undesirable implications for accessibility. For more details, see the [Accessibility concerns section](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/autofocus#accessibility_concerns).

While open, the dialog widget ensures that tabbing cycles focus between elements within the dialog itself, not elements outside of it. Modal dialogs additionally prevent mouse users from clicking on elements outside of the dialog.

Upon closing a dialog, focus is automatically returned to the element that had focus when the dialog was opened.

### Keyboard End User Information[](#keyboard-section "Bookmarkable Link")

|Target|Key|Action|
|---|---|---|
|Dialog|Tab or Shift + Tab|Navigate the content of the Dialog.|
|F6|Move focus to the launcher for a Dialog with modeless modality.|
|Esc|Close the Dialog.|
|Dialog Close Icon|Enter or Space|Close the Dialog.|
|Dialog Launcher|F6|Move focus to the first tab stop within the open Dialog. If there is not a tab stop within the content, focus is established on the Dialog.|

### Touch End User Information[](#touch-section "Bookmarkable Link")

|Target|Gesture|Action|
|---|---|---|
|Dialog Close Icon|Tap|Close the Dialog|

### Sizing[](#sizing "Bookmarkable Link")

Dialog dimensions, including `height, width, min-width, max-width, min-height` and `max-height` are defined with attriutes. The default dialog dimensions are the following:

- `height: auto`
- `width: 600px`
- `min-width: 200px`
- `max-width: min(600px, 90vw)`
- `max-height: min(600px, 90vh)`

In most cases, you will want to use the default `height:auto`, since this will automatically adjust the height based on the content. Users can change the dialog dimensions using style attributes:

```

<oj-c-dialog id="wideDialog" title="Wide Dialog" width="400px" min-width="100px" max-width="500px">
   <div slot="body">
      <p> Dialog Text
   </div>
</oj-c-dialog>
```

### Accessibility[](#a11y-section "Bookmarkable Link")

#### role

By default, the role will be set to dialog. This can be observed by inspecting the DOM:

```

 <div class="ojdialog ..." role="dialog">
```

This can be changed using the role attribute. WAI-ARIA recommends that role="dialog" be used if the dialog expects input (such as text input), otherwise, use the role attribute to assign role="alertdialog".

#### aria-labelledby

For simple dialog headers specified using the dialog-title attribute, the dialog component takes care of the `aria-labelledby` attribute and sets it automatically unless explicitly specified by the user. For custom dialog headers specified using the header slot, the user is responsible for setting the `aria-labelledby` attribute and its association with the custom header content.

#### aria-describedby

If the dialog contains additional descriptive text besides the dialog title, this text can be associated with the dialog using the `aria-describedby` attribute. Unlike the `aria-labelledby` association, the `aria-describedby` attribute is never generated and set automatically. It is up to the user to specify the attribute on `oj-dialog` and link it to the element containing the additional description:

```

<oj-c-dialog id="dialog" title="Accessible Title" aria-describedby="desc">
   <div slot="body">
      <p id="desc"> This is a dialog with accessible description.
   </div>
</oj-c-dialog>
```

### Reparenting[](#reparenting-section "Bookmarkable Link")

When dialogs are open, they will be reparented in the document and reparented back when closed. When open, the location of the dialog within the document will be in context of how it's used. Dialogs open from other dialogs will be relocated in the document into the nearest parent dialog's layer. The dialogs layer defines its z-index weight "stacking context". The context of opening is defined by the launcher argument passed to the open method. If not open from another dialog, the dialog will be reparented to a container in the document body. Dialogs of the same type are assigned the same z-index values. The layering between peer popups reflect the opening order.

There are known caveats with this design. However, these scenarios are considered "bad use" based on our JET popup strategy.

1. Events raised within the dialog will not bubble up to the dialog's original ancestors. Instead, listeners for dialog events should be applied to either the dialog's root element, or the document.
2. Likewise, developers should not use CSS descendant selectors, or similar logic, that assumes that the popup will remain a child of its original parent.
3. Dialogs containing iframes are problematic. The iframe elements "may" fire a HTTP GET request for its src attribute each time the iframe is reparented in the document.
4. If an iframe is added to the dialog's content, it must not be the first or last tab stop within the popup or keyboard and VoiceOver navigation will not remain within the dialog.
5. In some browsers, reparenting a dialog that contains elements having overflow, will cause these overflow elements to reset their scrollTop.

### Reading direction[](#rtl-section "Bookmarkable Link")

Setting the reading direction (LTR or RTL) is supported by setting the `"dir"` attribute on the `<html>` element of the page. As with any JET component, in the unusual case that the reading direction is changed post-init, the dialog must be `refresh()`ed, or the page must be reloaded.

### Additional Examples

The following defines a basic dialog, with an ok button in the footer:

```

<oj-c-dialog id="dialogWithFooter" dialog-title="Dialog with Footer" width=400px" min-width="100px" max-widt="500px">
   <div slot="body">
      <p> Dialog Text
   </div>
   <div slot="footer">
      <oj-button id="okButton"> OK </oj-button>
   </div>
</oj-c-dialog>
```

Note that you will need to define your own event handlers for the ok and close buttons (see the demos for examples of this).

A dialog with user-defined header is shown next. Arbitrary header content can be defined using a user-defined header.

```

<oj-c-dialog id="dialog" dialog-title="Dialog Title">
   <div slot="header">
      <span id="dialog-title-id" class="dialog-title"> User Defined Header</span>
   </div>
   <div slot="body">
      <p> Dialog Text
   </div>
</oj-dialog>
```

  

### Usage[](#usage-section "Bookmarkable Link")

##### Signature:

interface CDialogElement

##### Typescript Import Format

```
//To typecheck the element APIs, import as below.import { CDialogElement } from "oj-c/dialog";//For the transpiled javascript to load the element's module, import as belowimport "oj-c/dialog";
```

For additional information visit:

- [Using JET Custom Elements](https://www.oracle.com/webfolder/technetwork/jet/jsdocs/CustomElementOverview.html)
- [Using JET with TypeScript](https://www.oracle.com/webfolder/technetwork/jet/jsdocs/TypescriptOverview.html)
- [JET Module Loading](https://www.oracle.com/webfolder/technetwork/jet/jsdocs/ModuleLoadingOverview.html)

Note: Application logic should not interact with the component's properties or invoke its methods until the [BusyContext](https://www.oracle.com/webfolder/technetwork/jet/jsdocs/oj.BusyContext.html) indicates that the component is ready for interaction.

  

### Slots[](#slots-section "Bookmarkable Link")

JET components that allow child content support slots. Please see the [slots section](https://www.oracle.com/webfolder/technetwork/jet/jsdocs/CustomElementOverview.html#ce-slots-section) of the JET component overview doc for more information on allowed slot content and slot types.

#### body[](#body "Bookmarkable Link")

The content node to be shown within the Dialog body.

The content node to be shown within the Dialog footer.

The content node to be shown within the Dialog header. If a header slot is not specified by the user, the dialog-title attribute will be used instead.

### Attributes[](#members-section "Bookmarkable Link")

#### anchor :(string|[Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)|[oj-c.Dialog.Coords](https://www.oracle.com/webfolder/technetwork/jet/jsdocs/oj-c.Dialog.html#Coords))[](#anchor "Bookmarkable Link")

Specifies Dialog's anchor. Dialog is placed relative to its anchor. If not specified, it is placed relative to window.

##### Names

|Item|Name|
|---|---|
|Property|`anchor`|
|Property change event|`anchorChanged`|
|Property change listener attribute (must be of type function, see [Events and Listeners](https://www.oracle.com/webfolder/technetwork/jet/jsdocs/CustomElementOverview.html#ce-events-section) for additional information.)|`on-anchor-changed`|

#### cancel-behavior :"icon"|"escape"|"none"[](#cancelBehavior "Bookmarkable Link")

Specifies the cancel behavior of the Dialog. Note that the cancelBehavior applies to both automatic and user-defined headers.

##### Supported Values:

|Value|Description|
|---|---|
|`escape`|The dialog will close when it has focus and user presses the escape (ESC) key. A close icon will not be created.|
|`icon`|A close icon will automatically be created. The dialog will close when it has focus and user presses the escape (ESC) key.|
|`none`|A close icon will not be created. No actions will be associated with the escape key.|

Default Value:

- `"none"`

##### Names

|Item|Name|
|---|---|
|Property|`cancelBehavior`|
|Property change event|`cancelBehaviorChanged`|
|Property change listener attribute (must be of type function, see [Events and Listeners](https://www.oracle.com/webfolder/technetwork/jet/jsdocs/CustomElementOverview.html#ce-events-section) for additional information.)|`on-cancel-behavior-changed`|

#### dialog-title :string[](#dialogTitle "Bookmarkable Link")

Specifies title if header slot is not defined (custom header).

##### Names

|Item|Name|
|---|---|
|Property|`dialogTitle`|
|Property change event|`dialogTitleChanged`|
|Property change listener attribute (must be of type function, see [Events and Listeners](https://www.oracle.com/webfolder/technetwork/jet/jsdocs/CustomElementOverview.html#ce-events-section) for additional information.)|`on-dialog-title-changed`|

#### drag-affordance :"none"|"header"[](#dragAffordance "Bookmarkable Link")

Specifies whether the Dialog is draggable.

##### Supported Values:

|Value|Description|
|---|---|
|`header`|The dialog will be draggable by the header.|
|`none`|The dialog will not be draggable.|

Default Value:

- `"none"`

##### Names

|Item|Name|
|---|---|
|Property|`dragAffordance`|
|Property change event|`dragAffordanceChanged`|
|Property change listener attribute (must be of type function, see [Events and Listeners](https://www.oracle.com/webfolder/technetwork/jet/jsdocs/CustomElementOverview.html#ce-events-section) for additional information.)|`on-drag-affordance-changed`|

Specifies whether decorative stripe at the top is present.

##### Supported Values:

|Value|Description|
|---|---|
|`off`|No decoration is rendered.|
|`on`|Renders a textured strip at the top of the dialog header in the Redwood theme.|

Default Value:

- `"on"`

##### Names

|Item|Name|
|---|---|
|Property|`headerDecoration`|
|Property change event|`headerDecorationChanged`|
|Property change listener attribute (must be of type function, see [Events and Listeners](https://www.oracle.com/webfolder/technetwork/jet/jsdocs/CustomElementOverview.html#ce-events-section) for additional information.)|`on-header-decoration-changed`|

#### height :(number|string)[](#height "Bookmarkable Link")

Specifies height of the Dialog.

##### Names

|Item|Name|
|---|---|
|Property|`height`|
|Property change event|`heightChanged`|
|Property change listener attribute (must be of type function, see [Events and Listeners](https://www.oracle.com/webfolder/technetwork/jet/jsdocs/CustomElementOverview.html#ce-events-section) for additional information.)|`on-height-changed`|

#### launcher :(string|[Element](https://developer.mozilla.org/en-US/docs/Web/API/Element))[](#launcher "Bookmarkable Link")

Specifies Dialog's launcher. After Dialog closes, it returns focus to the launcher.

##### Names

|Item|Name|
|---|---|
|Property|`launcher`|
|Property change event|`launcherChanged`|
|Property change listener attribute (must be of type function, see [Events and Listeners](https://www.oracle.com/webfolder/technetwork/jet/jsdocs/CustomElementOverview.html#ce-events-section) for additional information.)|`on-launcher-changed`|

#### max-height :(number|string)[](#maxHeight "Bookmarkable Link")

Specifies maxHeight of the Dialog.

##### Names

|Item|Name|
|---|---|
|Property|`maxHeight`|
|Property change event|`maxHeightChanged`|
|Property change listener attribute (must be of type function, see [Events and Listeners](https://www.oracle.com/webfolder/technetwork/jet/jsdocs/CustomElementOverview.html#ce-events-section) for additional information.)|`on-max-height-changed`|

#### max-width :(number|string)[](#maxWidth "Bookmarkable Link")

Specifies maxWidth of the Dialog.

##### Names

|Item|Name|
|---|---|
|Property|`maxWidth`|
|Property change event|`maxWidthChanged`|
|Property change listener attribute (must be of type function, see [Events and Listeners](https://www.oracle.com/webfolder/technetwork/jet/jsdocs/CustomElementOverview.html#ce-events-section) for additional information.)|`on-max-width-changed`|

#### min-height :(number|string)[](#minHeight "Bookmarkable Link")

Specifies minHeight of the Dialog.

##### Names

|Item|Name|
|---|---|
|Property|`minHeight`|
|Property change event|`minHeightChanged`|
|Property change listener attribute (must be of type function, see [Events and Listeners](https://www.oracle.com/webfolder/technetwork/jet/jsdocs/CustomElementOverview.html#ce-events-section) for additional information.)|`on-min-height-changed`|

#### min-width :(number|string)[](#minWidth "Bookmarkable Link")

Specifies minWidth of the Dialog.

##### Names

|Item|Name|
|---|---|
|Property|`minWidth`|
|Property change event|`minWidthChanged`|
|Property change listener attribute (must be of type function, see [Events and Listeners](https://www.oracle.com/webfolder/technetwork/jet/jsdocs/CustomElementOverview.html#ce-events-section) for additional information.)|`on-min-width-changed`|

#### modality :"modal"|"modeless"[](#modality "Bookmarkable Link")

Specifies modality of the Dialog.

##### Supported Values:

|Value|Description|
|---|---|
|`modal`|The dialog is modal. Interactions with other page elements are disabled. Modal dialogs overlay other page elements.|
|`modeless`|Defines a modeless dialog.|

Default Value:

- `"modal"`

##### Names

|Item|Name|
|---|---|
|Property|`modality`|
|Property change event|`modalityChanged`|
|Property change listener attribute (must be of type function, see [Events and Listeners](https://www.oracle.com/webfolder/technetwork/jet/jsdocs/CustomElementOverview.html#ce-events-section) for additional information.)|`on-modality-changed`|

#### offset :number|{ mainAxis?: number; crossAxis?: number; }[](#offset "Bookmarkable Link")

Specifies displacement of the Dialog from the anchor element placement along the specified axes. The offset object consists of mainAxis and crossAxis properties. The direction in which these propertie are applied depends on the current value of the position property. If a number is used, it represents the main axis. The `mainAxis` property represents the distance between the Popup and the anchor. The `crossAxis` property represents the deviation in the opposite axis to the main axis - the skidding between the Popup and the anchor.

##### Names

|Item|Name|
|---|---|
|Property|`offset`|
|Property change event|`offsetChanged`|
|Property change listener attribute (must be of type function, see [Events and Listeners](https://www.oracle.com/webfolder/technetwork/jet/jsdocs/CustomElementOverview.html#ce-events-section) for additional information.)|`on-offset-changed`|

#### opened* :boolean[](#opened "Bookmarkable Link")

Specifies whether the Dialog is open.

Default Value:

- `false`

Supports writeback:

- `true`

##### Names

|Item|Name|
|---|---|
|Property|`opened`|
|Property change event|`openedChanged`|
|Property change listener attribute (must be of type function, see [Events and Listeners](https://www.oracle.com/webfolder/technetwork/jet/jsdocs/CustomElementOverview.html#ce-events-section) for additional information.)|`on-opened*-changed`|

#### placement :"center"|"end"|"start"|"top"|"bottom"|"top-start"|"top-end"|"start-top"|"start-bottom"|"bottom-start"|"bottom-end"|"end-top"|"end-bottom"[](#placement "Bookmarkable Link")

Specifies the location the dialog will appear relative to another element. If not specified, the default dialog position is "center" on desktop and "bottom-start" on phone.

##### Names

|Item|Name|
|---|---|
|Property|`placement`|
|Property change event|`placementChanged`|
|Property change listener attribute (must be of type function, see [Events and Listeners](https://www.oracle.com/webfolder/technetwork/jet/jsdocs/CustomElementOverview.html#ce-events-section) for additional information.)|`on-placement-changed`|

#### resize-behavior :"none"|"resizable"[](#resizeBehavior "Bookmarkable Link")

Specifies whether the Dialog is resizable.

##### Supported Values:

|Value|Description|
|---|---|
|`none`|The dialog will not be interactively resizable.|
|`resizable`|The dialog will be interactively resizable.|

Default Value:

- `"none"`

##### Names

|Item|Name|
|---|---|
|Property|`resizeBehavior`|
|Property change event|`resizeBehaviorChanged`|
|Property change listener attribute (must be of type function, see [Events and Listeners](https://www.oracle.com/webfolder/technetwork/jet/jsdocs/CustomElementOverview.html#ce-events-section) for additional information.)|`on-resize-behavior-changed`|

#### width :(number|string)[](#width "Bookmarkable Link")

Specifies width of the Dialog.

##### Names

|Item|Name|
|---|---|
|Property|`width`|
|Property change event|`widthChanged`|
|Property change listener attribute (must be of type function, see [Events and Listeners](https://www.oracle.com/webfolder/technetwork/jet/jsdocs/CustomElementOverview.html#ce-events-section) for additional information.)|`on-width-changed`|

### Events[](#events-section "Bookmarkable Link")

#### ojBeforeClose[](#event:ojBeforeClose "Bookmarkable Link")

Triggered immediately before the Dialog closes. Call `event.preventDefault()` in the event listener to veto the event synchronously, which prevents the Dialog from closing. Call `event.detail.accept(Promise.reject());` in the event listener to veto the event asynchronously, which prevents the Dialog from closing.

##### Properties:

All of the event payloads listed below can be found under `event.detail`. See [Events and Listeners](https://www.oracle.com/webfolder/technetwork/jet/jsdocs/CustomElementOverview.html#ce-events-section) for additional information.

|Name|Type|Description|
|---|---|---|
|`accept`|function|This method can be called with an application-created Promise to cancel this event asynchronously. The Promise should be resolved or rejected to accept or cancel the event, respectively.|

#### ojClose[](#event:ojClose "Bookmarkable Link")

#### ojDragEnd[](#event:ojDragEnd "Bookmarkable Link")

Triggered immediately after the Dialog stops moving.

See [Events and Listeners](https://www.oracle.com/webfolder/technetwork/jet/jsdocs/CustomElementOverview.html#ce-events-section) for additional information.

#### ojDragMove[](#event:ojDragMove "Bookmarkable Link")

#### ojDragStart[](#event:ojDragStart "Bookmarkable Link")

#### ojFocus[](#event:ojFocus "Bookmarkable Link")

Triggered immediately after the Dialog receives focus.

See [Events and Listeners](https://www.oracle.com/webfolder/technetwork/jet/jsdocs/CustomElementOverview.html#ce-events-section) for additional information.

#### ojOpen[](#event:ojOpen "Bookmarkable Link")

#### ojResize[](#event:ojResize "Bookmarkable Link")

#### ojResizeEnd[](#event:ojResizeEnd "Bookmarkable Link")

Triggered immediately after the Dialog stops resizing.

See [Events and Listeners](https://www.oracle.com/webfolder/technetwork/jet/jsdocs/CustomElementOverview.html#ce-events-section) for additional information.

#### ojResizeStart[](#event:ojResizeStart "Bookmarkable Link")

Triggered immediately before the Dialog resizes.

See [Events and Listeners](https://www.oracle.com/webfolder/technetwork/jet/jsdocs/CustomElementOverview.html#ce-events-section) for additional information.

### Methods[](#methods-section "Bookmarkable Link")

#### getProperty(property) : {[any](https://www.oracle.com/webfolder/technetwork/jet/jsdocs/CustomElementOverview.html#ce-attrs-any-section)}[](#getProperty "Bookmarkable Link")

Retrieves the value of a property or a subproperty.

##### Parameters:

|Name|Type|Description|
|---|---|---|
|`property`||The property name to get. Supports dot notation for subproperty access.|

##### Returns:

Type

[any](https://www.oracle.com/webfolder/technetwork/jet/jsdocs/CustomElementOverview.html#ce-attrs-any-section)

#### setProperties(properties) : {void}[](#setProperties "Bookmarkable Link")

Performs a batch set of properties.

##### Parameters:

|Name|Type|Description|
|---|---|---|
|`properties`||An object containing the property and value pairs to set.|

##### Returns:

Type

void

#### setProperty(property, value) : {void}[](#setProperty "Bookmarkable Link")

Sets a property or a single subproperty for complex properties and notifies the component of the change, triggering a corresponding event.

##### Parameters:

|Name|Type|Description|
|---|---|---|
|`property`||The property name to set. Supports dot notation for subproperty access.|
|`value`||The new value to set the property to.|

##### Returns:

Type

void

### Type Definitions[](#typedefs-section "Bookmarkable Link")

#### Coords[](#Coords "Bookmarkable Link")

##### Properties:

|Name|Type|Argument|
|---|---|---|
|`contextElement`|[Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)|<optional>|
|`x`|number||
|`y`|number||