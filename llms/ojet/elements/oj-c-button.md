Since:

- 13.0.0

Module:

- button

Note: This component supersedes the following component: [\<oj-button>](https://www.oracle.com/webfolder/technetwork/jet/jsdocs/oj.ojButton.html). Migration info available at preceding link.

## QuickNav

  

### JET Button[](#buttonOverview-section "Bookmarkable Link")

Description: Themeable, WAI-ARIA-compliant push buttons, with appropriate styles for hover, active, and disabled.

```
<oj-c-button id="myButton" label="My Button">
</oj-c-button>
<oj-c-button label="start icon">
  <span slot='startIcon' class='myIconClass'></span>
</oj-c-button>
 <oj-c-button label="end icon">
  <span slot='endIcon' class='myIconClass'></span>
</oj-c-button>
```

### Push Buttons[](#pushButtons-section "Bookmarkable Link")

Push buttons are ordinary buttons that do not stay pressed in when clicked. Push buttons are created from `oj-c-button` elements.

### Touch End User Information[](#touch-section "Bookmarkable Link")

|Target|Gesture|Action|
|---|---|---|
|Push Button|Tap|Push the button.|

### Keyboard End User Information[](#keyboard-section "Bookmarkable Link")

|Target|Key|Action|
|---|---|---|
|Push Button|Enter or Space|Push the button.|

### Accessibility[](#a11y-section "Bookmarkable Link")

For accessibility, it is not required to set an aria label on a JET button as it uses the label text to generate an aria label. Therefore the label should be specified even if the button is [icon-only (display=icons)](#display). However, you can override the default behavior by setting `aria-label`. The label can be hidden using the display attribute.

Disabled content: JET supports an accessible luminosity contrast ratio, as specified in [WCAG 2.0 - Section 1.4.3 "Contrast"](http://www.w3.org/TR/WCAG20/#visual-audio-contrast-contrast), in the themes that are accessible. (See the "Theming" chapter of the JET Developer Guide for more information on which themes are accessible.) Note that Section 1.4.3 says that text or images of text that are part of an inactive user interface component have no contrast requirement. Because disabled content may not meet the minimum contrast ratio required of enabled content, it cannot be used to convey meaningful information.

  

### Usage[](#usage-section "Bookmarkable Link")

##### Signature:

interface CButtonElement

##### Typescript Import Format

```
//To typecheck the element APIs, import as below.import { CButtonElement } from "oj-c/button";//For the transpiled javascript to load the element's module, import as belowimport "oj-c/button";
```

For additional information visit:

- [Using JET Custom Elements](https://www.oracle.com/webfolder/technetwork/jet/jsdocs/CustomElementOverview.html)
- [Using JET with TypeScript](https://www.oracle.com/webfolder/technetwork/jet/jsdocs/TypescriptOverview.html)
- [JET Module Loading](https://www.oracle.com/webfolder/technetwork/jet/jsdocs/ModuleLoadingOverview.html)

Note: Application logic should not interact with the component's properties or invoke its methods until the [BusyContext](https://www.oracle.com/webfolder/technetwork/jet/jsdocs/oj.BusyContext.html) indicates that the component is ready for interaction.

  

### Slots[](#slots-section "Bookmarkable Link")

JET components that allow child content support slots. Please see the [slots section](https://www.oracle.com/webfolder/technetwork/jet/jsdocs/CustomElementOverview.html#ce-slots-section) of the JET component overview doc for more information on allowed slot content and slot types.

#### endIcon[](#endIcon "Bookmarkable Link")

The endIcon slot is the button's end icon. The oj-c-button element accepts DOM nodes as children with the endIcon slot.

#### startIcon[](#startIcon "Bookmarkable Link")

The startIcon slot is the button's start icon. The oj-c-button element accepts DOM nodes as children with the startIcon slot.

### Attributes[](#members-section "Bookmarkable Link")

#### chroming :"ghost"|"borderless"|"outlined"|"solid"|"callToAction"|"danger"[](#chroming "Bookmarkable Link")

Indicates in what states the button has variants in background and border.

##### Supported Values:

|Value|Description|
|---|---|
|`borderless`|Borderless buttons are a more prominent variation. Borderless buttons are useful for supplemental actions that require minimal emphasis.|
|`callToAction`|A Call To Action (CTA) button guides the user to take or complete the action that is the main goal of the page or page section. There should only be one CTA button on a page at any given time.|
|`danger`|A Danger button alerts the user to a dangerous situation.|
|`ghost`|Ghost buttons are the least prominent variation. Ghost buttons are useful for performing low-priority tasks, such as manipulating the UI.|
|`outlined`|Outlined buttons are salient, but lighter weight than solid buttons. Outlined buttons are useful for secondary actions.|
|`solid`|Solid buttons stand out, and direct the user's attention to the most important actions in the UI.|

Default Value:

- `"outlined"`

##### Names

|Item|Name|
|---|---|
|Property|`chroming`|
|Property change event|`chromingChanged`|
|Property change listener attribute (must be of type function, see [Events and Listeners](https://www.oracle.com/webfolder/technetwork/jet/jsdocs/CustomElementOverview.html#ce-events-section) for additional information.)|`on-chroming-changed`|

#### disabled :boolean[](#disabled "Bookmarkable Link")

Specifies that the button element should be disabled.

Default Value:

- `false`

##### Names

|Item|Name|
|---|---|
|Property|`disabled`|
|Property change event|`disabledChanged`|
|Property change listener attribute (must be of type function, see [Events and Listeners](https://www.oracle.com/webfolder/technetwork/jet/jsdocs/CustomElementOverview.html#ce-events-section) for additional information.)|`on-disabled-changed`|

#### display :"all"|"icons"|"label"[](#display "Bookmarkable Link")

Display just the label, the icons, or all. Label is used as tooltip and should be set in all cases.

##### Supported Values:

|Value|Description|
|---|---|
|`all`|Display both the label and icons.|
|`icons`|Display only the icons.|
|`label`|Display only the text label.|

Default Value:

- `"all"`

##### Names

|Item|Name|
|---|---|
|Property|`display`|
|Property change event|`displayChanged`|
|Property change listener attribute (must be of type function, see [Events and Listeners](https://www.oracle.com/webfolder/technetwork/jet/jsdocs/CustomElementOverview.html#ce-events-section) for additional information.)|`on-display-changed`|

#### edge :"none"|"bottom"[](#edge "Bookmarkable Link")

Specifies whether the button is attached to an edge. For example setting edge='bottom' can be used to attach a button to the bottom of a card. The button is then stretched to 100% width, and borders adjusted.

##### Supported Values:

|Value|Description|
|---|---|
|`bottom`|Stretch the button to 100% width and adjust borders for usage at bottom of container.|
|`none`|Display a default standalone button.|

Default Value:

- `"none"`

##### Names

|Item|Name|
|---|---|
|Property|`edge`|
|Property change event|`edgeChanged`|
|Property change listener attribute (must be of type function, see [Events and Listeners](https://www.oracle.com/webfolder/technetwork/jet/jsdocs/CustomElementOverview.html#ce-events-section) for additional information.)|`on-edge-changed`|

#### label* :string[](#label "Bookmarkable Link")

Text to show in the button.

##### Names

|Item|Name|
|---|---|
|Property|`label`|
|Property change event|`labelChanged`|
|Property change listener attribute (must be of type function, see [Events and Listeners](https://www.oracle.com/webfolder/technetwork/jet/jsdocs/CustomElementOverview.html#ce-events-section) for additional information.)|`on-label*-changed`|

#### size :"xs"|"sm"|"md"|"lg"[](#size "Bookmarkable Link")

Size of button

##### Supported Values:

|Value|Description|
|---|---|
|`lg`|Display a large button.|
|`md`|Display a default size button.|
|`sm`|Display a small button.|
|`xs`|Display an extra small button. Only supported for component developers with ghost chroming in icon display mode.|

Default Value:

- `"md"`

##### Names

|Item|Name|
|---|---|
|Property|`size`|
|Property change event|`sizeChanged`|
|Property change listener attribute (must be of type function, see [Events and Listeners](https://www.oracle.com/webfolder/technetwork/jet/jsdocs/CustomElementOverview.html#ce-events-section) for additional information.)|`on-size-changed`|

#### tooltip :string[](#tooltip "Bookmarkable Link")

Text to show in the tooltip. This overrides the default tooltip that renders the label when in icon mode.

##### Names

|Item|Name|
|---|---|
|Property|`tooltip`|
|Property change event|`tooltipChanged`|
|Property change listener attribute (must be of type function, see [Events and Listeners](https://www.oracle.com/webfolder/technetwork/jet/jsdocs/CustomElementOverview.html#ce-events-section) for additional information.)|`on-tooltip-changed`|

#### width :(number|string)[](#width "Bookmarkable Link")

Specifies that the button style width

##### Names

|Item|Name|
|---|---|
|Property|`width`|
|Property change event|`widthChanged`|
|Property change listener attribute (must be of type function, see [Events and Listeners](https://www.oracle.com/webfolder/technetwork/jet/jsdocs/CustomElementOverview.html#ce-events-section) for additional information.)|`on-width-changed`|

### Events[](#events-section "Bookmarkable Link")

#### ojAction[](#event:ojAction "Bookmarkable Link")

Triggered when a button is clicked, whether by keyboard, mouse, or touch events. To meet accessibility requirements, the only supported way to react to the click of a button is to listen for this event.

See [Events and Listeners](https://www.oracle.com/webfolder/technetwork/jet/jsdocs/CustomElementOverview.html#ce-events-section) for additional information.

### Methods[](#methods-section "Bookmarkable Link")

#### blur : {void}[](#blur "Bookmarkable Link")

##### Returns:

Type

void

#### click : {void}[](#click "Bookmarkable Link")

##### Returns:

Type

void

#### focus : {void}[](#focus "Bookmarkable Link")

##### Returns:

Type

void

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