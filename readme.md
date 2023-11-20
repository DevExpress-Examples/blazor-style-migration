<!-- default badges list -->
[![](https://img.shields.io/badge/Open_in_DevExpress_Support_Center-FF7200?style=flat-square&logo=DevExpress&logoColor=white)](https://supportcenter.devexpress.com/ticket/details/T1130491)
[![](https://img.shields.io/badge/📖_How_to_use_DevExpress_Examples-e9f6fc?style=flat-square)](https://docs.devexpress.com/GeneralInformation/403183)
<!-- default badges end -->

# DevExpress Blazor Components - How to Update CSS Styles

This document summarizes the most common scenarios in which you should use our private CSS selectors to apply a style to an element.
 
You can also press `Ctrl+F` and search for a private CSS selector that you used in a previous version. This helps you find a selector used in v22.2 or prior, and copy the new equivalent of this selector.

If you do not manage to find your scenario in this topic, you can inspect a component render and create a new CSS selector as described in the following articles: 

* [View and Change CSS](https://developer.chrome.com/docs/devtools/css/)<br/>
* [How to Implement CSS-related Solutions for DevExpress Components](https://supportcenter.devexpress.com/ticket/details/T632424)

Feel free to write to our [Support Center](http://devexpress.com/support/center). We are ready to research your specific case.

<a name="thetableofcontents"></a>
## Table of Contents

- [Restoring Changes Made after our v22.2 Release](#restoring-changes-made-after-our-v222-release)
  - [DxGrid](#dxgrid)
    - [Align header captions](#align-header-captions)
    - [Color alternate rows](#color-alternate-rows)
    - [Change the default "No data to display" text](#change-the-default-no-data-to-display-text)
    - [Change the header cells' background color](#change-the-header-cells-background-color)
    - [Change selected row background color](#change-selected-row-background-color)
    - [Focus an editor inside the edit form](#focus-an-editor-inside-the-edit-form)
    - [Hide the expand/collapse button for detail rows](#hide-the-expandcollapse-button-for-detail-rows)
    - [Hide the skeleton element](#hide-the-skeleton-element)
    - [Hide "No data to display" message](#hide-no-data-to-display-message)
    - [Hide vertical lines](#hide-vertical-lines)
    - [Hide the header row](#hide-the-header-row)
    - [Highlight a row on hover](#highlight-a-row-on-hover)
    - [Place a scrollable DxGrid into DxPopup](#place-a-scrollable-dxgrid-into-dxpopup)
    - [Prevent caption wrapping](#prevent-caption-wrapping)
    - [Remove paddings for a detail grid](#remove-paddings-for-a-detail-grid)
  - [DxFormLayout](#dxformlayout)
    - [Change the location and style of a Form Layout item](#change-the-location-and-style-of-a-form-layout-item)
    - [Change item captions](#change-item-captions)
  - [DxToolbar](#dxtoolbar)
    - [Change title text color](#change-title-text-color)
    - [Center toolbar item content](#center-toolbar-item-content)
  - [DxTabs](#dxtabs)
    - [Create rounded tabs](#create-rounded-tabs)
  - [DxScheduler](#dxscheduler)
    - [Change edit form width](#change-edit-form-width)
  - [DxEditors](#dxeditors)
    - [Modify the Clear button](#modify-the-clear-button)
    - [Blazor Editors inside the "input-group" container](#blazor-editors-inside-the-input-group-container)
    - [DxTextBox](#dxtextbox)
      - [Change the input's text style](#change-the-inputs-text-style)
      - [Customize the Clear button's icon](#customize-the-clear-buttons-icon)
      - [Display an icon inside the input element](#display-an-icon-inside-the-input-element)
    - [DxTagBox](#dxtagbox)
      - [Always force tags to start at a new line](#always-force-tags-to-start-at-a-new-line)
    - [DxComboBox](#dxcombobox)
      - [Change the height of a drop-down list](#change-the-height-of-a-drop-down-list)
      - [Change drop-down text font size](#change-drop-down-text-font-size)
      - [Modify "No data to display" message](#modify-no-data-to-display-message)
      - [Hide column headers](#hide-column-headers)
    - [DxDateEdit](#dxdateedit)
      - [Highlight a week on mouse hover](#highlight-a-week-on-mouse-hover)
      - [Hide the drop down button](#hide-the-drop-down-button)
      - [Localize the Time section scroll picker's text](#localize-the-time-section-scroll-pickers-text)
    - [DxCalendar](#dxcalendar)
      - [Change font color of weekends](#change-font-color-of-weekends)
      - [Hide week numbers](#hide-week-numbers)
      - [Hide the footer](#hide-the-footer)
      - [Hide the footer's Today button](#hide-the-footers-today-button)
  - [DxPopup](#dxpopup)
    - [Adjust popup size and position on the page](#adjust-popup-size-and-position-on-the-page)
    - [Customize popup size and position](#customize-popup-size-and-position)
    - [Customize the Close header's button icon](#customize-the-close-headers-button-icon)
    - [Hide the modal background](#hide-the-modal-background)
- [Restoring Changes Made after our v23.1 Release](#restoring-changes-made-after-our-v231-release)
  - [Navigation TreeView customizations in projects created with DevExpress Templates](#navigation-treeview-customizations-in-projects-created-with-devexpress-templates)
  - [DxAccordion](#dxaccordion)
    - [Modify background color of a selected item](#modify-background-color-of-a-selected-item)
    - [Change font weight in root items](#change-font-weight-in-root-items)
    - [Change font size in nested items](#change-font-size-in-nested-items)
    - [Remove item borders](#remove-item-borders)
  - [DxContextMenu](#dxcontextmenu)
    - [Add a Scroll Bar](#add-a-scroll-bar)
  - [DxGrid](#dxgrid-1)
    - [Align column headers](#align-column-headers)
  - [DxGridLayout](#dxgridlayout)
    - [Specify a gap between items](#specify-a-gap-between-items)
  - [DxMenu](#dxmenu)
    - [Alter item paddings](#alter-item-paddings)
    - [Place an icon above item text](#place-an-icon-above-item-text)
    - [Specify item width](#specify-item-width)
    - [Specify drop-down item's width](#specify-drop-down-items-width)
    - [Change item font size](#change-item-font-size)
    - [Wrap and center item text](#wrap-and-center-item-text)
    - [Change item text color](#change-i-text-colcr)
    - [Change item background color](#ciangebitem-backgcound-color)
    - [Make a drop-down item overflow container boundaries](#make-a-drop-down-item-overflow-container-boundaries)
    - [Add a scroll bar to a drop-down item](#add-a-scroll-bar-to-a-drop-down-item)
    - [Remove background for selected and hovered drop-down items](#remove-background-for-selected-and-hovered-drop-down-items)
    - [Reduce Menu size](#reduce-menu-size)
    - [Remove the left padding of a drop-down toggle](#remove-the-left-padding-of-a-drop-down-toggle)
    - [Add custom content to title container](#add-custom-content-to-title-container)
  - [DxTabs](#dxtabs-1)
    - [Create rounded tabs](#create-rounded-tabs-1)
    - [Change background color of a tab header](#change-background-color-of-a-tab-header)
    - [Change the font of a tab header](#change-the-font-of-a-tab-header)
  - [DxTreeView](#dxtreeview)
    - [Display filter panel at the bottom of the bomponent](#display-filter-panel-at-the-bottom-of-the-component)
    - [Apply custom highlighting to filter results](#apply-custom-highlighting-to-filter-results)
    - [Customize badge appearance](#customize-badge-appearance)
    - [Achieve NavLinkMatch.All behavior](#achieve-navlinkmatchall-behavior)
    - [Customize item container's indents](#customize-item-containers-indents)
    - [Remove left margin of child nodes](#remove-left-margin-of-child-nodes)
    - [Display Context Menu for a node](#display-context-menu-for-a-node)
    - [Place an icon above node text](#place-an-icon-above-node-text)
- [Restoring Changes Made after our v23.2 Release](#restoring-changes-made-after-our-v232-release)
  - [DxToolbar](dxtoolbar-1)
    - [Change item border color](#change-item-border-color)

## Restoring Changes Made after our v22.2 Release

### DxGrid

#### Align Header Captions

In both v22.1 and v22.2, use the same razor code:

```cs
<DxGrid Data="@forecasts"
        CssClass="myGrid">
    <Columns>
        <DxGridDataColumn Caption="Date" FieldName="Date" />
        <DxGridDataColumn Caption="Temperature" FieldName="TemperatureF" />
    </Columns>
</DxGrid>


@code {
    private WeatherForecast[]? forecasts;

    protected override async Task OnInitializedAsync() {
        forecasts = await ForecastService.GetForecastAsync(DateTime.Now);
    }
}
```

In v22.1, use the following CSS rules:

```css
.myGrid .dxbs-grid-header-content {
    justify-content: right;
}
```
In v22.2, use the following CSS rules:
```css
.myGrid .dxbl-grid-header-content {
    justify-content: right;
}
```

[Return to the table of contents.](#thetableofcontents)

#### Color Alternate Rows

To color alternate rows (using the universal technique), handle the CustomizeElement event:

```cs
<style>
    .highlighted-item > td {
        background-color: rgba(245, 198, 203, 0.5);
    }
</style>

<DxGrid Data="@forecasts" CssClass="my-grid" CustomizeElement="Grid_CustomizeElement">
    <Columns>
        <DxGridDataColumn Caption="Date" FieldName="Date" />
        <DxGridDataColumn Caption="Temperature" FieldName="TemperatureF" />
    </Columns>
</DxGrid>


@code {
    private WeatherForecast[] forecasts;
    protected override async Task OnInitializedAsync() {
        forecasts = await ForecastService.GetForecastAsync(DateTime.Now);
    }
    void Grid_CustomizeElement(GridCustomizeElementEventArgs e) {
        if (e.ElementType == GridElementType.DataRow) {
            e.CssClass = e.VisibleIndex % 2 == 0 ? "highlighted-item" : null;
        }

    }
}
```

If your DxGrid does not display master-detail relationships and does not use the Grid’s grouping capabilities, use the following v22.2 CSS rule:

```cs
<style>
    .my-grid .dxbl-grid-table > tbody > tr:nth-child(2n+1) {
        background-color: lightgray;
    }
</style>

<DxGrid Data="@forecasts" CssClass="my-grid">
    <Columns>
        <DxGridDataColumn Caption="Date" FieldName="Date" />
        <DxGridDataColumn Caption="Temperature" FieldName="TemperatureF" />
    </Columns>
</DxGrid>
```

[Return to the table of contents.](#thetableofcontents)


#### Change the Default "No data to display" Text

In v22.1, use the following CSS rules:

```css
.dxbs-grid .dxbs-grid-empty-data > span {
    display: none;
}

.dxbs-grid .dxbs-grid-empty-data::after {
    content: 'my test content'
}
```
In v22.2, use the following CSS rules:

```css
.dxbl-grid .dxbl-grid-empty-data > span {
    display: none;
}

.dxbl-grid .dxbl-grid-empty-data::after {
    content: 'my test content'
}
```
[Return to the table of contents.](#thetableofcontents)


#### Change the Header Cell Background Color

In v22.1, use the following CSS rules:

```css
.dxbs-grid-header:nth-child(1){
    background-color: aqua !important
}
```

In v22.2, use the new CustomizeElement event to change the header cell color instead of adding a custom CSS style:

```cs
void Grid_CustomizeElement(GridCustomizeElementEventArgs e) {
    if(e.ElementType == GridElementType.HeaderRow) {
    e.Style = "background-color: aqua;";
}
```
[Return to the table of contents.](#thetableofcontents)

### Change Selected Row Background Color

In v22.1, use the following CSS rules:

```css
.dxbs-grid-table {
    --dx-grid-selection-color: blue;
}
```
In v22.2, use the following CSS rules:

```css
.dxbl-grid {
    --dxbl-grid-selection-bg: red;
}
```
[Return to the table of contents.](#thetableofcontents)

#### Focus an Editor Inside the Edit Form

To focus an editor inside the grid edit form in v22.1 and earlier, use the JavaScript input.focus method:

```js
function focusFirstEditor() {
    setTimeout(function myfunction() {
        var inputElement = document.querySelectorAll(".my-grid .dxbs-grid-edit-form input")[1];
        inputElement.focus();
    }, 1000);
}
```

In v22.2, the DxGrid automatically focuses the first editor. If you wish to focus a different editor, wrap it in the CasadingValue component and set the CascadingValue.Name property to "FocusOnEditStart":

```cs
@page "/grid"
@using System.Globalization

@using DxBlazorApplication1.Data
@inject WeatherForecastService ForecastService

<h2>DevExpress Grid</h2>


<DxGrid Data="@forecasts" CssClass="my-grid" EditMode="GridEditMode.EditForm">
    <EditFormTemplate Context="EditFormContext">
        @{
            var employee = (WeatherForecast)EditFormContext.EditModel;
        }
        <DxFormLayout CssClass="w-100">
            <DxFormLayoutItem Caption="First Name:">
                <DxTextBox @bind-Text="@employee.Name1" />
            </DxFormLayoutItem>
            <DxFormLayoutItem Caption="Last Name:">
                <CascadingValue Value="true" Name="FocusOnEditStart" IsFixed="true">
                    <DxTextBox @bind-Text="@employee.Name2" />
                </CascadingValue>
            </DxFormLayoutItem>
        </DxFormLayout>
    </EditFormTemplate>
    <Columns>
        <DxGridCommandColumn Width="120px" />
        <DxGridDataColumn Caption="Name1" FieldName="Name1" />
        <DxGridDataColumn Caption="Name2" FieldName="Name2" />
    </Columns>
</DxGrid>

@code {    
    private WeatherForecast[] forecasts;
    protected override async Task OnInitializedAsync() {
        forecasts = await ForecastService.GetForecastAsync(DateTime.Now);
    }

}
```
[Return to the table of contents.](#thetableofcontents)

#### Hide the Expand/Collapse Button for Detail Rows

In both v22.1 and v22.2, use the same razor code:

```cs
<DxGrid @ref="masterGrid" Data="MasterGridData" ShowAllRows="true" CustomizeElement="OnCustomizeElement">
    <Columns>
        <DxGridDataColumn FieldName="CustomerId" />
        <DxGridDataColumn FieldName="CustomerName" />
    </Columns>
    <DetailRowTemplate>
        <DetailGrid Customer="(Customer)context.DataItem" />
    </DetailRowTemplate>
</DxGrid>

void OnCustomizeElement(GridCustomizeElementEventArgs args)
{
    if (args.ElementType == GridElementType.DataRow)
    {
        var masterRowKey = args.Grid.GetRowValue(args.VisibleIndex, args.Grid.KeyFieldName);
        if (true /* your logic here to check if there are detail rows for a current master row (masterRowKey)*/)
        {
            args.CssClass = "hideDetailButton";
        }
    }
}
```

In v22.1, use the following CSS rules:

```css
.hideDetailButton .dxbs-grid-expand-button-cell button {
    visibility: hidden;
}
```

In v22.2, use the following CSS rules:

```css
.hideDetailButton .dxbl-grid-expand-button-cell .dxbl-grid-expand-button {
    visibility: hidden;
}
```


[Return to the table of contents.](#thetableofcontents)

#### Hide the Skeleton Element

In both v22.1 and v22.2, use the same razor code:

  ```cs
@inject HttpClient client
@inject IJSRuntime JS

<DxGrid Data="@productsDatasource" @ref="grid">
    <Columns>
        <DxGridDataColumn FieldName="ProductName" Width="200px" SortIndex="0" />
        <DxGridDataColumn Caption="Price" FieldName="UnitPrice" />
    </Columns>
</DxGrid>

@code {
    private GridDevExtremeDataSource<Product>? productsDatasource { get; set; }
    private DxGrid? grid;

    protected override void OnInitialized() {
        var uri = new Uri("https://demos.devexpress.com/blazor/api/nwind/getproducts");
        productsDatasource = new GridDevExtremeDataSource<Product>(client, uri);
    }
}
  ```
  
In v22.1, use the following CSS rules:

```css
.dxbs-grid-skeleton-content {
    visibility: hidden;
}
```

In v22.2, use the following CSS rules:

```css
.dxbl-grid-skeleton-content {
    visibility: hidden;
}
```

[Return to the table of contents.](#thetableofcontents)

#### Hide "No data to display" Message

In v22.1, use the following CSS rules:

```css
.dxbs-grid-empty-data{
    visibility:hidden;
}

```

In v22.2, use the following CSS rules:

```css
.dxbl-grid-empty-data{
    visibility:hidden;
}

```

[Return to the table of contents.](#thetableofcontents)

#### Hide Vertical Lines

In both v22.1 and v22.2, use the same razor code:

  ```cs
<DxGrid Data="@forecasts" CssClass="my-grid">
    <Columns>
        <DxGridDataColumn Caption="Date" FieldName="Date" />
        <DxGridDataColumn Caption="Temperature" FieldName="TemperatureF" />
    </Columns>
</DxGrid>
  ```
  
In v22.1, use the following CSS rules:

```css
.my-grid .table-bordered td {
    border-width: 0;
}
.my-grid > .card {
    border-left: 0px;
    border-right: 0px;
}
    .my-grid > .card .dxbs-grid-header {
        border-left: 0px;
    }
```

In v22.2, use the following CSS rules:

```css
.my-grid {
    border-left: 0px;
    border-right: 0px;
}

    .my-grid.dxbl-grid .dxbl-grid-table > tbody > tr > td {
        border-left-width: 0px;
    }

    .my-grid.dxbl-grid .dxbl-grid-table > thead > tr > th {
        border-left-width: 0px;
    }

```

[Return to the table of contents.](#thetableofcontents)

#### Hide the Header Row

To hide the header row (universal technique), handle the CustomizeElement event:

```cs
<style>
    .hiddenHeader {
        display :none;
    }
</style>

<DxCheckBox @bind-Checked="ShowHeader">Show Header</DxCheckBox>

<DxGrid Data="@forecasts" 
        CustomizeElement="OnCustomizeElement">
    <Columns>
        <DxGridDataColumn Caption="Date" FieldName="Date" Width="200px" SortIndex="0" />
        <DxGridDataColumn Caption="Summary" FieldName="Summary" />
        <DxGridDataColumn Caption="Temperature (C)" FieldName="TemperatureC" Width="150px" />
        <DxGridDataColumn Caption="Temperature (F)" FieldName="TemperatureF" Width="150px" />
    </Columns>
</DxGrid>

@code {
    private WeatherForecast[] forecasts;

    public bool ShowHeader = true;

    protected override async Task OnInitializedAsync() {
        forecasts = await ForecastService.GetForecastAsync(DateTime.Now);
    }
    void OnCustomizeElement (GridCustomizeElementEventArgs args) {
        if (args.ElementType == GridElementType.HeaderRow) {
            args.CssClass = ShowHeader ? "" : "hiddenHeader";
        }
    }
}
```

You can achieve the same result with CSS rules. In both v22.1 and v22.2, use the same razor code:

```cs
<DxCheckBox @bind-Checked="ShowHeader">Show Header</DxCheckBox>

<DxGrid Data="@forecasts" CssClass="@(ShowHeader ? "" : "hiddenHeader")">
    <Columns>
        <DxGridDataColumn Caption="Date" FieldName="Date" Width="200px" SortIndex="0" />
        <DxGridDataColumn Caption="Summary" FieldName="Summary" />
        <DxGridDataColumn Caption="Temperature (C)" FieldName="TemperatureC" Width="150px" />
        <DxGridDataColumn Caption="Temperature (F)" FieldName="TemperatureF" Width="150px" />
    </Columns>
</DxGrid>

@code {
    private WeatherForecast[] forecasts;

    public bool ShowHeader = true;

    protected override async Task OnInitializedAsync() {
        forecasts = await ForecastService.GetForecastAsync(DateTime.Now);
    }
}
```

In v22.1, use the following CSS rules:

```css
.hiddenHeader .dxbs-grid-header-content {
    display: none;
}

.hiddenHeader .dxbs-grid-header {
    padding: 0px 0px 0px 0px !important;
    border-bottom: none !important;
}
```

In v22.2, use the following CSS rules:

```css
.hiddenHeader .dxbl-grid-header-content {
    display: none;
}

.hiddenHeader .dxbl-grid-header {
    padding: 0px 0px 0px 0px !important;
    border-bottom: none !important;
}
```

[Return to the table of contents.](#thetableofcontents)


#### Highlight a Row on Hover

To highlight a row on hover in v22.2, handle the CustomizeElement event:

```cs
<style>
    .highlighted-item:hover, .highlighted-item:hover > td {
        background-color: yellow;
    }
</style>

@if (forecasts == null) {
    <p><em>Loading...</em></p>
}
else {
    <DxGrid Data="@forecasts" CssClass="mw-1100" CustomizeElement="OnCustomizeElement">
        <Columns>
            <DxGridDataColumn Caption="Date" FieldName="Date" />
            <DxGridDataColumn Caption="Temperature" FieldName="TemperatureF" />
        </Columns>
    </DxGrid>
}

@code {
    private WeatherForecast[]? forecasts;

    protected override async Task OnInitializedAsync() {
        forecasts = await ForecastService.GetForecastAsync(DateTime.Now);
    }

    void OnCustomizeElement(GridCustomizeElementEventArgs e) {
        if(e.ElementType == GridElementType.DataRow)
            e.CssClass = "highlighted-item";
    }
}
```

[Return to the table of contents.](#thetableofcontents)


#### Place a Scrollable DxGrid into DxPopup

In v22.2, use the following code:

```css
<style type="text/css">
    .mop-data-grid {
        height: 100%;
        width:100%
    }

    .popupContent {
        height: 800px;
    }
</style>


<DxPopup HeaderText="Adresse" BodyCssClass="popupContent" @bind-Visible="@isVisible">        
        <DxGrid Data="@forecasts" PageSize="@PageSize"
                CssClass="mop-data-grid">
            <Columns>
                <DxGridDataColumn Caption="Date" FieldName="Date" />
                <DxGridDataColumn Caption="Temperature" FieldName="TemperatureF" />
            </Columns>
        </DxGrid>    
</DxPopup>


@code {
    private WeatherForecast[]? forecasts;
    bool isVisible = true;

    public int PageSize { get; set; }

    protected override async Task OnInitializedAsync() {
        forecasts = await ForecastService.GetForecastAsync(DateTime.Now);
        PageSize = forecasts.Count();
    }
}
```

[Return to the table of contents.](#thetableofcontents)

#### Prevent Caption Wrapping

To prevent caption wrapping (using the universal technique), handle the CustomizeElement event:

```cs
<style>
    .custom-header-cell {
        white-space: nowrap;
    }
</style>

@if (forecasts == null) {
    <p><em>Loading...</em></p>
}
else {
    <DxGrid Data="@forecasts"
        CssClass="myGrid" ColumnResizeMode="GridColumnResizeMode.NextColumn"
        CustomizeElement="OnCustomizeElement">
        <Columns>
            <DxGridDataColumn Caption="Date" FieldName="Date" />
            <DxGridDataColumn Caption="Temperature Long Caption" FieldName="TemperatureF" />
        </Columns>
    </DxGrid>
}

@code {
    private WeatherForecast[]? forecasts;

    void OnCustomizeElement(GridCustomizeElementEventArgs args) {
        if (args.ElementType == GridElementType.HeaderCell) {
            args.CssClass = "custom-header-cell";
        }
    }
    protected override async Task OnInitializedAsync() {
        forecasts = await ForecastService.GetForecastAsync(DateTime.Now);
    }
}
```

You can achieve the same result with the following CSS rules.

In v22.1, use the following CSS rules:

```css
.myGrid .dxbs-grid-header-content {
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
}
```

In v22.2, use the following CSS rules:

```css
.myGrid .dxbl-grid-header-content {
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
}
```

[Return to the table of contents.](#thetableofcontents)


#### Remove Paddings for a Detail Grid

In v22.1, use the following CSS rules:

```css
.dxbs-grid .dxbs-grid-detail-cell {
    padding-top: 0px;
    padding-bottom: 0px;
}
```

In v22.2, use the following CSS rules:

```css
.dxbl-grid .dxbl-grid-table .dxbl-grid-detail-cell {
    padding-top: 0px;
    padding-bottom: 0px;
}
```

[Return to the table of contents.](#thetableofcontents)


### DxFormLayout

#### Change the Location and Style of a Form Layout Item

In old versions, it was necessary to both use a custom label and to hide the built-in label:

```cs
<style>
.isRequired {
    font-weight: bold !important;
}
</style>

<DxFormLayoutItem Caption="" ColSpanMd="6">
    <label class="col-form-label dxbs-fl-cpt isRequired">Company Name: *</label>
    <DxTextBox @bind-Text="@Name" />
</DxFormLayoutItem>
```

In v22.1 and v22.2, use the CaptionCssClass and CaptionPosition properties instead (available for Form Layout items):

```cs
<style>
.isRequired {
    font-weight: bold !important;
}
</style>

<DxFormLayoutItem Caption="Company Name: *" CaptionPosition="CaptionPosition.Vertical" CaptionCssClass="isRequired" ColSpanMd="6">
    <DxTextBox @bind-Text="@Name" />
</DxFormLayoutItem>
```

[Return to the table of contents.](#thetableofcontents)


#### Change Item Captions

In v22.1, use the following CSS rules:

```css
.dxbs-fl-cpt {
    text-align: right;
}
```

In v22.2, use the following CSS rules:

```css
.dxbl-fl-cpt {
    text-align: right;
}
```

[Return to the table of contents.](#thetableofcontents)

### DxToolbar

#### Change Title Text Color

In both v22.1 and v22.2, use the same razor code:

```cs
<DxToolbar  CssClass="myClass" Title="Test">
...
</DxToolbar>
```

In v22.1, use the following CSS rules:

```css
.myClass .dxbs-ta-title{
    color:red!important;
}
```

In v22.2, use the following CSS rules:

```css
.myClass .dxbl-toolbar-title{
    color:red!important;
}
```

[Return to the table of contents.](#thetableofcontents)


#### Center Toolbar Item Content

In both v20.1 and v22.2, use the same razor code:

```cs
<DxToolbar ItemRenderStyleMode="ToolbarRenderStyleMode.Contained">
    <Items>
        <DxToolbarItem Name="Add" IconCssClass="fa fa-plus" Text="Add New Program" Tooltip="Add New Program" />
        <DxToolbarItem CssClass="mycss" Name="ShowAllSwitch" BeginGroup="true" GroupName="MyTestGroup" RenderStyleMode="ToolbarItemRenderStyleMode.Plain">
            <Template>
                <div>
                    <DxCheckBox Checked="@ShowAll" CheckType="CheckType.Switch">Show All Programs</DxCheckBox>
                </div>
            </Template>
        </DxToolbarItem>
        <DxToolbarItem Name="SearchBox" Alignment="@ToolbarItemAlignment.Right" BeginGroup="true" RenderStyleMode="ToolbarItemRenderStyleMode.Contained">
            <Template>
                <DxTextBox @bind-Text="@SearchString"
                           ClearButtonDisplayMode="@DataEditorClearButtonDisplayMode.Auto"
                           NullText="Search Programs...">
                </DxTextBox>
            </Template>
        </DxToolbarItem>
    </Items>
</DxToolbar>

@code {
    public bool ShowAll { get; set; } = true;
    public string SearchString { get; set; } = "";
}
```
  
In v20.1, use the following CSS rules:

```css
.btn-group.dxbs-toolbar-group:nth-child(2),
.btn-group.dxbs-toolbar-group:nth-child(2) > div {
    width: 100%;
}

.btn-group.dxbs-toolbar-group:nth-child(2) .dx-checkbox {
    display: flex;
    align-items: center;
    justify-content: center;
}
```

In v22.2, use the following CSS rules:

```css
.dxbl-btn-group.dxbl-toolbar-group:nth-child(2) {
    width: 100%;
    display: flex;
    justify-content: center;
}
```

[Return to the table of contents.](#thetableofcontents)

### DxTabs

#### Create Rounded Tabs

In both v22.1 and v22.2, use the same razor code:

```cs
<DxTabs CssClass="MyTabsCss">
    <DxTab Text="Home" CssClass="MyTabCss"></DxTab>
    <DxTab Text="Products" CssClass="MyTabCss"></DxTab>
    <DxTab Text="Support" CssClass="MyTabCss"></DxTab>
</DxTabs>
```

In v22.1, use the following CSS rules:

```css
.MyTabsCss > ul {
    border-bottom-width: 0px;
}
.MyTabCss > a {
    border-radius: 20px !important;
    border: 1px solid white !important;
}
.MyTabCss > a:hover {
    border-color: #e9ecef !important;
}
.MyTabCss > a.active {
    border-color: dodgerblue !important;
    background-color: dodgerblue !important;
}
```

In v22.2, use the following CSS rules:

```css
.MyTabsCss {
    border-bottom-width:0px;
}
.MyTabCss  {
    border-radius: 20px !important;
    border: 1px solid white !important;
}
.MyTabCss:hover {
    border-color: #e9ecef !important;
}

.MyTabCss.dxbl-active {
    border-color: dodgerblue !important;
    background-color: dodgerblue !important;
}
.MyTabCss.dxbl-active:after {
    background-color:transparent!important;
}
```

[Return to the table of contents.](#thetableofcontents)

### DxScheduler

#### Change Edit Form Width

In v22.1, use the following CSS rules:

```css
.dxbs-appointment-edit-dialog {
    width: 800px!important;
    max-width: 800px!important;
}
```

In v22.2, use the following CSS rules:

```css
.dxbs-apt-edit-dialog {
    width: 800px!important;
    max-width: 800px!important;
}
```

[Return to the table of contents.](#thetableofcontents)

### DxEditors

#### Modify the Clear Button

In v22.1, use the following code:

```cs
<style type="text/css">
    .my-textbox .dxbs-editor-clear-btn {
        color: red;
    }
</style>
<DxTextBox 
    Text="123"
    CssClass="my-textbox"
    ClearButtonDisplayMode="DataEditorClearButtonDisplayMode.Auto"></DxTextBox>
```

In v22.2, use the following code:

```cs
<style type="text/css">
    .my-textbox .dxbl-edit-btn-clear {
        color: red;
    }
</style>
<DxTextBox 
    Text="123"
    CssClass="my-textbox"
    ClearButtonDisplayMode="DataEditorClearButtonDisplayMode.Auto"></DxTextBox>
```

[Return to the table of contents.](#thetableofcontents)

#### Blazor Editors inside the "input-group" Container

In v22.1, editors occupy 100% of the container width in the following markup:

```cs
<div class="input-group">
    <DxTextBox ... />
    <DxMemo ... />
    <DxSpinEdit ... />
    <DxComboBox ... />
    <DxTagBox ... />
    <DxDateEdit ... />
</div>
```

In v22.2, it's necessary to set the width of each editor to 100%:

```cs
<style>
    .editor-width {
        width: 100%;
    }
</style>

<div class="input-group">
    <DxTextBox CssClass="editor-width" ... />
    <DxMemo CssClass="editor-width" ... />
    <DxSpinEdit CssClass="editor-width" ... />
    <DxComboBox CssClass="editor-width" ... />
    <DxTagBox CssClass="editor-width" ... />
    <DxDateEdit CssClass="editor-width" ... />
</div>
```

[Return to the table of contents.](#thetableofcontents)

#### DxTextBox 

##### Change the Input's Text Style

In both v22.1 and v22.2, use the same razor code:

```cs
<DxTextBox CssClass=@(EditMode ? "title-editor" : "title-editor-readonly")  ReadOnly=@(EditMode ? false : true)
           Text="Projekt ZUM 4.0 - Installtion new server">
</DxTextBox>
```

In v22.1, use the following CSS rules:

```css
.title-editor .dxbs-editor-input-container > input {
    color: #000000;
    font-size: 2rem;
    font-weight: 600;
}

.title-editor-readonly .dxbs-editor-input-container > input {
    color: #000000;
    background-color: transparent;
    font-size: 2rem;
    font-weight: 600;
}
```

In v22.2, use the following CSS rules:

```css
dxbl-input-editor.title-editor > input {
    color: #000000;
    font-size: 2rem;
    font-weight: 600;
}

dxbl-input-editor.title-editor-readonly > input {
    color: #000000;
    background-color: transparent;
    font-size: 2rem;
    font-weight: 600;
}
```


[Return to the table of contents.](#thetableofcontents)

##### Customize the Clear Button's Icon

In both v22.1 and v22.2, use the same razor code:

```cs
<DxTextBox @bind-Text="@TextValue" ClearButtonDisplayMode="DataEditorClearButtonDisplayMode.Auto"></DxTextBox>
@code {
    string TextValue { get; set; }
}
```

In v22.1, use the following CSS rules:

```css
.dxbs-editor-clear-btn > svg {
    display:none;
}
.dxbs-editor-clear-btn::after {
    content: " ";
    width:16px;
    height:16px;
    background-image:url('/images/facebook_icon.svg');
}
```

In v22.2, use the following CSS rules:

```css
.dxbl-edit-btn-clear > svg {
    display:none;
}
.dxbl-edit-btn-clear::after {
    content: " ";
    width:16px;
    height:16px;
    background-image:url('/images/facebook_icon.svg');
}
```

[Return to the table of contents.](#thetableofcontents)

##### Display an Icon inside the Input Element

In v22.1, use the following CSS rules:

```cs
<style>
    .glyphicon .form-control {
        padding-left: 3em;
    }
</style>

<div style="position: relative;">
    <DxTextBox CssClass="glyphicon" NullText="Type something here"></DxTextBox>
    <div style="position: absolute; width: 100%; height: 100%; top: 0; pointer-events: none;">
        <svg class="dxbs-button-icon" role="img" style="position: static; height: 100%; width: calc(1em + 18px); padding-left: 1em;">
            <use href="#dxbs-calendar-icon" />
        </svg>
    </div>
</div>
<div style="display: none;">
    <svg version="1.1" id="_x31_" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px"
         viewBox="0 0 18 18" style="enable-background:new 0 0 18 18;" xml:space="preserve">
    <symbol id="dxbs-calendar-icon" viewBox="0 0 18 18">
    <style type="text/css">

        .st0 {
            fill-rule: evenodd;
            clip-rule: evenodd;
            fill: #3F3F3F;
        }
</style>
    <path id="_x32_" d="M6,8v2H4V8H6 M10,8v2H8V8H10 M14,8v2h-2V8H14 M16,1c1.1,0,2,0.9,2,2v13c0,1.1-0.9,2-2,2H2c-1.1,0-2-0.9-2-2V3
            c0-1.1,0.9-2,2-2h1V0h2v1h8V0h2v1H16 M16,16V5H2v11H16 M6,12v2H4v-2H6 M10,12v2H8v-2H10 M14,12v2h-2v-2H14z" />
            </symbol>
            </svg>
</div>
```

In v22.2, use the following CSS rules:

```cs
<style>
    .glyphicon input {
        padding-left: 3em;
    }
</style>

<div style="position: relative;">
    <DxTextBox CssClass="glyphicon" NullText="Type something here"></DxTextBox>
    <div style="position: absolute; width: 100%; height: 100%; top: 0; pointer-events: none;">
        <div style="position: static; height: 100%; width: calc(1em + 18px); padding-left: 1em;padding-top:0.2em;">
            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-calendar" viewBox="0 0 16 16"> <path d="M3.5 0a.5.5 0 0 1 .5.5V1h8V.5a.5.5 0 0 1 1 0V1h1a2 2 0 0 1 2 2v11a2 2 0 0 1-2 2H2a2 2 0 0 1-2-2V3a2 2 0 0 1 2-2h1V.5a.5.5 0 0 1 .5-.5zM1 4v10a1 1 0 0 0 1 1h12a1 1 0 0 0 1-1V4H1z" /> </svg>
        </div>
    </div>
</div>
```

[Return to the table of contents.](#thetableofcontents)

#### DxTagBox 

##### Always Force Tags to Start at a New Line

In v22.1, use the following code:

```css
.dxbs-tag,
.dxbs-tag-text {
   width: 100%;
}
```

In v22.2, use the following code:

```css
.dxbl-tag,
.dxbl-tag-text {
   width: 100%;
}
```

[Return to the table of contents.](#thetableofcontents)


#### DxComboBox 

##### Change the Height of a Drop-Down List

In both v22.1 and v22.2, use the same razor code:

```cs
<DxComboBox Data="@dataSource" @bind-Value="@Value" TextFieldName="Name" ValueFieldName="ID" DropDownCssClass="combo-dropdown">
</DxComboBox>
```

In v22.1 use the following code:

```css
.combo-dropdown {
    max-height: 500px !important;
}
    .combo-dropdown .dxbs-listbox {
        max-height: 500px !important;
    }
```

In v22.2, use the following code:

```css
.combo-dropdown {
    max-height: 500px !important;
}
    .combo-dropdown .dxbl-listbox {
        max-height: 500px !important;
    }
```

[Return to the table of contents.](#thetableofcontents)

##### Change Drop-Down Text Font Size

In v22.1, use the following code:

```css
 ul.dxbs-dropdown-area li {
       font-size: smaller;
}
```

In v22.2, use the following code:

```css
 .dxbl-edit-dropdown li {
       font-size: smaller;
}
```

[Return to the table of contents.](#thetableofcontents)

##### Modify "No data to display" Message

In v19.2, use the following code:

```cs
<style>
    .MyComboBox .dxbs-empty-data-row {
        color: transparent;
        width: 300px;
        user-select:none;
    }
.MyComboBox .dxbs-empty-data-row:before {
      position: absolute;
      content: 'This is my looooong text';
      color: #212529;
      font: inherit;
      width: 100%;
      left: 0;
}
</style>
<DxComboBox Data="@MyList" CssClass="MyComboBox"   FilteringMode="@DataGridFilteringMode.Contains"   AllowUserInput="true">
</DxComboBox>
```

In v22.2, use the following code:

```cs
.myComboBox .dxbl-listbox-empty-data-item {
      color: transparent;
      width: 300px;
      user-select:none;
}

.myComboBox .dxbl-listbox-empty-data-item:before {
      position: absolute;
      content: 'Custom text';
      color: #212529;
      font: inherit;
      width: 100%;
      left: 0;
  }

<DxComboBox Data="@MyList"   DropDownCssClass="myComboBox" >
</DxComboBox>
```

[Return to the table of contents.](#thetableofcontents)

##### Hide Column Headers

In both v22.1 and v22.2, use the same razor code:

```cs
<DxComboBox Data="@forecasts" @bind-Value="@test"
            DropDownCssClass="SecondComboBoxDropDown">
    <DxListEditorColumn FieldName="@nameof(WeatherForecast.Date)"
                        Caption="Date" />
    <DxListEditorColumn FieldName="@nameof(WeatherForecast.TemperatureF)"
                        Caption="Temperature F" />
</DxComboBox>


@code {
    private WeatherForecast[]? forecasts;
    WeatherForecast test;

    protected override async Task OnInitializedAsync() {
        forecasts = await ForecastService.GetForecastAsync(DateTime.Now);
    }
}
```

In v22.1, use the following code:

```css
.SecondComboBoxDropDown .dxbs-listbox .dxbs-gridview > .card > .dxgvHSDC {
    display: none !important;
}

```

In v22.2, use the following code:

```css
.SecondComboBoxDropDown .dxgvHSDC {
    display: none !important;
}
```

[Return to the table of contents.](#thetableofcontents)

#### DxDateEdit 

Internally, we use DxCalendar in the DxDateEdit popup. As such, when you need to apply a style to DxCalendar in the DxDateEdit popup, you can write selectors for DxCalendar itself. To write a selector for a specific DxDateEdit, assign the DxDateEdit.DropDownCssClass property.

[Return to the table of contents.](#thetableofcontents)

##### Highlight a Week on Mouse Hover

In both v22.1 and v22.2, use the same razor code:

```cs
<DxDateEdit @bind-Date="@DateStart" DropDownCssClass="customDateEdit">
</DxDateEdit>

@code {
    public DateTime DateStart { get; set; } = DateTime.Now;    
}
```

In v22.1, use the following CSS rule:

```css
.customDateEdit .dxbs-calendar-table tr:hover {
    background-color: lightgray;
}
```

In v22.2, use the following CSS rule:

```css
.customDateEdit .dxbl-calendar-week-row:hover {
    background-color: lightgray;
}
```

[Return to the table of contents.](#thetableofcontents)


##### Hide the Drop-Down Button

In both v22.1 and v22.2, use the same razor code:

```cs
<DxDateEdit @bind-Date="@DateTimeValue" CssClass="my-date-edit" />
```

In v22.1, use the following CSS rule:

```css
.my-date-edit .dxbs-editor-dropdown-button {
    display: none;
}
```

In v22.2, use the following CSS rule:

```css
.my-date-edit .dxbl-edit-btn-dropdown {
    display: none;
}

```

[Return to the table of contents.](#thetableofcontents)

##### Localize the Time Section Scroll Picker's Text

In both v22.1 and v22.2, use the same razor code:

```cs
<DxDateEdit @bind-Date="@DateTimeValue"
            TimeSectionVisible="true" DropDownBodyCssClass="my-drop-down-body"   DropDownVisibleChanged="OnDropDownVisibleChanged"
            CssClass="cw-320" />

@code {
    DateTime DateTimeValue { get; set; } = DateTime.Now.AddHours(-7);
    void OnDropDownVisibleChanged(bool isVisible)
    {
        if (isVisible)
            JSRuntime.InvokeVoidAsync("updateRoller", "heure", "m", "seconde");
    }
}
```

In v22.1, use the following script:

```js
var dropDownBody, localizedHour, localizedMinute,localizedSecond;
function updateRoller(hour, minute, second) {
    localizedHour = hour;
    localizedMinute = minute;
    localizedSecond = second;
    setTimeout(function() {
        dropDownBody = document.querySelector(".my-drop-down-body");
        var tabHeader = dropDownBody.querySelector(".dxbs-date-time-edit-dropdown-tabs-time");
        tabHeader.onclick  = function() {
            setTimeout(function() {
                var captions = dropDownBody.querySelectorAll(".roller-title");
                captions[0].innerText = hour;
                captions[1].innerText = minute;
                captions[2].innerText = second;
            }, 300);
        }
    }, 700);
}
```

In v22.2, use the following script:

```js
var dropDownBody, localizedHour, localizedMinute,localizedSecond;
function updateRoller(hour, minute, second) {
    localizedHour = hour;
    localizedMinute = minute;
    localizedSecond = second;
    setTimeout(function() {
        dropDownBody = document.querySelector(".my-drop-down-body");
        var tabHeader = dropDownBody.querySelector(".dxbl-date-time-edit-tabs");
        tabHeader.onclick  = function() {
            setTimeout(function() {
                var captions = dropDownBody.querySelectorAll(".dxbl-roller-title");
                captions[0].innerText = hour;
                captions[1].innerText = minute;
                captions[2].innerText = second;
            }, 300);
        }
    }, 700);
}
```

[Return to the table of contents.](#thetableofcontents)


#### DxCalendar

##### Change Font Color of Weekends

In both v22.1 and v22.2, use the same razor code:

```cs
<DxCalendar SelectedDate="@DateStart"  CssClass="myCalendarCss"></DxCalendar>

@code {
    public DateTime DateStart { get; set; } = DateTime.Now;
}

```

In v22.1, use the following CSS rule:

```css
.myCalendarCss .dxbs-weekend {
    color: black!important;
}

```

In v22.2, use the following CSS rule:

```css
.myCalendarCss .dxbl-calendar-day.dxbl-calendar-weekend {
    color: black;
}
```

[Return to the table of contents.](#thetableofcontents)

##### Hide Week Numbers

In both v22.1 and v22.2, use the same razor code:

```cs
<DxCalendar CssClass="myClass" SelectedDate="@DateStart"></DxCalendar>

@code {
    public DateTime DateStart { get; set; } = DateTime.Now;
}
```

In v19.2, use the following CSS rule:

```css
.myClass .dxbs-calendar td:not(.dxbs-day) {
    display: none;
}
```

In v22.2, use the following CSS rule:

```css
.myClass .dxbl-calendar-week-number,
.myClass .dxbl-calendar-days-of-week th:first-child {
    display: none;
}
```

[Return to the table of contents.](#thetableofcontents)

##### Hide the footer

In both v22.1 and v22.2, use the same razor code:
```cs
<DxCalendar SelectedDate="@DateStart" CssClass="customCalendar"></DxCalendar>

@code {
    public DateTime DateStart { get; set; } = DateTime.Now;
}
```

In v22.1, use the following CSS rule:

```css
.customCalendar .dxbs-calendar-footer {
    display: none;
}


```

In v22.2, use the following CSS rule:

```css
.customCalendar .dxbl-calendar-footer {
    display: none;
}
```

[Return to the table of contents.](#thetableofcontents)

##### Hide the Footer's Today Button

In both v22.1 and v22.2, use the same razor code:

```cs
<DxCalendar SelectedDate="@DateStart" CssClass="customCalendar"></DxCalendar>

@code {
    public DateTime DateStart { get; set; } = DateTime.Now;
}
```

In v22.1, use the following CSS rule:

```css
.customCalendar .dxbs-calendar-footer > button:first-child {
    display: none;
}
```

In v22.2, use the following CSS rule:

```css
.customCalendar .dxbl-calendar-footer > button:first-child {
    display: none;
}
```

[Return to the table of contents.](#thetableofcontents)

### DxPopup

#### Adjust Popup Size and Position on the Page

In both v22.1 and v22.2, use the same razor code:

```cs
<DxPopup @bind-Visible="@SummaryGeneratedFlag" ShowCloseButton="true" CssClass="DashboardModal" HeaderText="Work Control Summary">
    <Content>
        <p>Content</p>
    </Content>
</DxPopup>
```

In v22.1, use the following CSS rules:

```css
.DashboardModal.modal-dialog.dxbs-popup {
    position: fixed !important;
    left: auto !important;
    right: 0 !important;
    box-sizing: border-box !important;
    max-width: 100% !important;
    width: 30% !important;
    margin: 0rem !important;
    top: 0 !important;
    height: 100% !important;
}
```

In v22.2, use the following CSS rules:

```css
.DashboardModal.modal-dialog.dxbs-popup {
    position: fixed !important;
    left: auto !important;
    right: 0 !important;
    box-sizing: border-box !important;
    max-width: 100% !important;
    width: 30% !important;
    margin: 0rem !important;
    top: 0 !important;
    height: 100% !important;
}
```

[Return to the table of contents.](#thetableofcontents)

#### Customize Popup Size and Position

In both v22.1 and v22.2, use the same razor code:

```cs
<DxPopup @bind-Visible="@SummaryGeneratedFlag" ShowCloseButton="true" CssClass="DashboardModal" HeaderText="Work Control Summary">
    <Content>
        <p>Content</p>
    </Content>
</DxPopup>
```

In v22.1, use the following CSS rules:

```css
.DashboardModal.modal-dialog.dxbs-popup {
    position: fixed !important;
    left: auto !important;
    right: 0 !important;
    box-sizing: border-box !important;
    max-width: 100% !important;
    width: 30% !important;
    margin: 0rem !important;
    top: 0 !important;
    height: 100% !important;
}
```

In v22.2, use the following CSS rules:

```css
.DashboardModal.modal-dialog.dxbs-popup {
    position: fixed !important;
    left: auto !important;
    right: 0 !important;
    box-sizing: border-box !important;
    max-width: 100% !important;
    width: 30% !important;
    margin: 0rem !important;
    top: 0 !important;
    height: 100% !important;
}
```

[Return to the table of contents.](#thetableofcontents)

#### Customize the Close Header's Button Icon

In both v22.1 and v22.2, use the same razor code:

```cs
<DxPopup HeaderText="Header" @bind-Visible="@PopupVisible" CssClass="customPopup">
    <Content>
       ...
    </Content>
</DxPopup>
```

In v22.1, use the following CSS rules:

```css
.customPopup .dxbs-popup-header-button{
    content: "icn";
    color: transparent;
    display: inline-block;
    background-image: url("/images/facebook_icon.svg");
    background-repeat: no-repeat;
    background-size: contain;
}
.customPopup .dxbs-popup-header-button svg {
    display: none;
}
```

In v22.2, use the following CSS rules:

```css
.customPopup .dxbl-popup-header-button .dxbl-image {
    content: "icn";
    color: transparent;
    display: inline-block;
    background-image: url("/images/facebook_icon.svg");
    background-repeat: no-repeat;
    background-size: contain;
}
```

[Return to the table of contents.](#thetableofcontents)

#### Hide the Modal Background

In both v22.1 and v22.2, use the same razor code:

```cs
<div class="target-container" @onclick="@(() => PopupVisible = true)">
    <p class="target-caption">CLICK TO SHOW A POP-UP WINDOW</p>
</div>
<DxPopup HeaderText="Header"
         @bind-Visible="@PopupVisible"
         BodyText="Test content">
</DxPopup>

@code {
    bool PopupVisible { get; set; } = false;
}
```

In v22.1, use the following CSS rules:

```css
.modal-backdrop.dxbs-modal-back {
    display: none!important;
}
```

In v22.2, use the following CSS rules:

```css
.dxbl-modal-back {
    display: none!important;
}
```

[Return to the table of contents.](#thetableofcontents)

## Restoring Changes Made after our v23.1 Release

### Navigation TreeView Customizations in Projects Created with DevExpress Templates

DevExpress templates generate projects that contain a left-side navbar with a TreeView. For the TreeView, we specified custom styles and changed its default appearance. In v23.1, these styles cannot be applied. In v23.1, do the following to restore appearance:

1. Use Project Converter to update styles automatically.

2. Update styles manually.
2.1 Assign a CSS class for all nodes in the *NavMenu.razor* file:

```Razor
<DxTreeView>
     <DxTreeViewNode Text="Node1" CssClass="my-item" />
     <DxTreeViewNode Text="Node2" CssClass="my-item" />
     @* ... *@
</DxTreeView>
```

2.2  In the *NavMenu.razor.css* file, remove the following code:
```css
::deep .app-sidebar > .nav-pills > .nav-item:first-of-type {
    padding-top: 1rem;
}

::deep .app-sidebar > .nav-pills > .nav-item:last-of-type {
    padding-bottom: 1rem;
}

::deep .app-sidebar .nav-pills > .nav-item a {
    border-radius: 0px;
    display: flex;
    align-items: center;
}

::deep .app-sidebar > .nav-pills > .nav-item > a {
    font-size: 1rem !important;
    font-weight: 600 !important;
    padding: .25rem 1rem .25rem .125rem;
}
::deep .app-sidebar,
::deep .app-sidebar > .nav-pills,
::deep .app-sidebar > .nav-pills > .nav-item,
::deep .app-sidebar > .nav-pills > .nav-item > a:not(.active) {
    background-color: inherit;
}

@media (max-width: 1199.98px) {
    ::deep .app-sidebar > .nav-pills > .nav-item:last-of-type {
        padding-bottom: 0;
    }
}
```

2.3 In the same file, add the following code:
```css
::deep .app-sidebar {
    --dxbl-treeview-spacing-x: 0.5rem;
    --dxbl-treeview-spacing-y: 1rem;
}

::deep .app-sidebar .my-item > :first-child {
    --dxbl-treeview-font-weight: 600;
}

/* Use this rule for TreeViews without nested nodes */
::deep .app-sidebar .my-item > :only-child:not(.dxbl-treeview-tmpl) > button {
    display: none;
}

@media (max-width: 1199.98px) {
    ::deep .app-sidebar {
        padding-bottom: 0;
    }
}
```

[Return to the table of contents.](#thetableofcontents)

### DxAccordion

#### Modify Background Color of a Selected Item

In v22.2, use the following CSS rules:

```css
.dxbl-accordion-item-content.active {
    background-color: lightcyan;
}
.dxbl-accordion-group {
    --dxbl-accordion-group-header-selected-bg: lightcyan;
}
```

In v23.1, use the following CSS rules:

```css
.dxbl-accordion-group {
    --dxbl-accordion-group-header-selected-bg: lightcyan;
    --dxbl-accordion-group-item-selection-bg: lightcyan;
}
```

[Return to the table of contents.](#thetableofcontents)

#### Change Font Weight in Root Items

In v22.2, use the following CSS rules:

```css
.dxbl-accordion-group-header {
    font-weight: 600;
}
```

In v23.1, use the following CSS rules:

```css
.dxbl-accordion-group-header {
    --dxbl-group-header-font-weight: 600;
}
```

[Return to the table of contents.](#thetableofcontents)

#### Change Font Size in Nested Items

In v22.2, use the following CSS rules:

```css
.dxbl-accordion-group .dxbl-accordion-item-content>.dxbl-accordion-item-text-container>.dxbl-text {
    font-size: 12px;
}
```

In v23.1, use the following CSS rules:

```css
.dxbl-accordion-group .dxbl-accordion-item-content>.dxbl-accordion-item-text-container>.dxbl-text {
    --dxbl-text-font-size: 12px;
}
```

[Return to the table of contents.](#thetableofcontents)

#### Remove Item Borders

In v22.2, use the following CSS rules:

```css
.dxbl-group-header {
    border: 0;
}
```

In v23.1, use the following CSS rules:

```css
.dxbl-group-header {
    --dxbl-accordion-group-border-width: 0;
}
```

[Return to the table of contents.](#thetableofcontents)

### DxContextMenu

#### Add a Scroll Bar

In v20.2, use the following code:

```cs
<style>
    .myScrollMenu.dx-blazor-context-menu.dropdown-menu, .dx-blazor-context-menu-submenu.dropdown-menu {
        max-height: 180px;
        overflow-y: auto;
    }
</style>

<DxContextMenu @ref="@ContextMenu" CssClass="myScrollMenu">
```

In v23.1, use the following code:

```cs
<style>
    .myScrollMenu.dxbl-context-menu-dropdown {
        max-height: 180px;
        overflow-y: auto;
    }
</style>

<DxContextMenu @ref="@ContextMenu" CssClass="myScrollMenu"> ... </DxContextMenu>
```

[Return to the table of contents.](#thetableofcontents)

### DxGrid

#### Align Column Headers

In v22.2, use the following CSS rules:

```css
.dxbl-grid-header-content {
    justify-content: center !important;
    text-align: center !important;
}
```

In v23.1, use the following CSS rule:

```css
.dxbl-grid-header-content > span {
    width:100%;
}
.dxbl-grid-header-content {
    justify-content: center !important;
    text-align: center !important;
}
```

### DxGridLayout

#### Specify a Gap Between Items

In v21.1, use the following CSS rules:

```css
.gap-3 > .dx-gridlayout-root {
    gap: inherit !important;
}
```

In v23.1, use the [ItemContainerCssClass](https://docs.devexpress.com/Blazor/DevExpress.Blazor.DxGridLayout.ItemContainerCssClass) property as follows:

```cs
<style>
    .item-container {
        gap: 10px !important;
    }
</style>

<DxGridLayout style="height:500px" ItemContainerCssClass="item-container">...</DxGridLayout>
```

### DxMenu

#### Alter Item Paddings

In v21.1-v22.2, use the following CSS rules:

```cs
<style>
    .my-menu .dx-menu-horizontal-item {
        padding: 0;
    }
</style>

<DxMenu CssClass="my-menu">...</DxMenu>
```

In v23.1, use the following CSS rules:

```cs
<style>
    .my-menu {
        --dxbl-menu-item-padding-x: 0;
        --dxbl-menu-item-padding-y: 0;
    }
</style>

<DxMenu CssClass="my-menu">...</DxMenu>
```

[Return to the table of contents.](#thetableofcontents)

#### Place an Icon Above Item Text

In v21.2, use the following code:

```cs
<style>
    .iconVertAlign .dx-menu-horizontal-item {
        flex-direction: column;
        align-items: center;
        justify-content: center;
    }
    .iconVertAlign .dx-menu-item-text-container {
        padding-left: 0 !important;
    }
</style>

<DxMenu>
    <Items>
        <DxMenuItem Text="My item" CssClass="iconVertAlign" />
    </Items>
</DxMenu>
```

In v23.1, use the following code:

```cs
<style>
    .dxbl-menu-item > .dxbl-btn {
        flex-direction: column;
        align-items: center;
    }

    .dxbl-menu.dxbl-menu-horizontal .dxbl-menu-item > .dxbl-btn {
        --dxbl-btn-image-spacing: 0 !important;
    }
</style>

<DxMenu>
    <Items>
        <DxMenuItem Text="My item" CssClass="iconVertAlign" />
    </Items>
</DxMenu>
```

[Return to the table of contents.](#thetableofcontents)

#### Specify Item Width

In v21.2, use the following code:

```cs
<style>
    .menuItemLg .dx-menu-horizontal-item.nav-link.item-position-start {
        width: 65px;
    }
</style>

<DxMenu>
    <Items>
        <DxMenuItem Text="My item" CssClass="menuItemLg" />
    </Items>
</DxMenu>
```

In v23.1, use the following code:

```cs
<style>
    .dxbl-menu-item > .dxbl-btn {
        width: 65px;
    }
</style>

<DxMenu>
    <Items>
        <DxMenuItem Text="My item" />
    </Items>
</DxMenu>
```

[Return to the table of contents.](#thetableofcontents)

#### Specify Drop-Down Item's Width

In v21.2, use the following code:

```cs
<style>
    .myMenu .dropdown-menu {
        width: 250px !important;
    }
</style>

<DxMenu ItemsPosition="ItemPosition.Start" CssClass="myMenu">
    @* ... *@
</DxMenu>
```

In v23.1, use the `SubMenuCssClass` property as follows:

```cs
<style>
    .myMenu {
        width: 250px;
    }
</style>

<DxMenu ItemsPosition="ItemPosition.Start" SubMenuCssClass="myMenu">
    @* ... *@
</DxMenu>
```

[Return to the table of contents.](#thetableofcontents)

#### Change Item Font Size

In v21.2, use the following code:

```cs
<style>
    .menuItemLg {
        font-size: 11px;
    }
</style>

<DxMenu>
    <Items>
        <DxMenuItem Text="My item" CssClass="menuItemLg" />
    </Items>
</DxMenu>
```

In v23.1, use the following code:

```cs
<style>
    .menuItemLg {
        --dxbl-menu-item-font-size: 11px;
    }
</style>

<DxMenu>
    <Items>
        <DxMenuItem Text="My item" CssClass="menuItemLg" />
    </Items>
</DxMenu>
```

[Return to the table of contents.](#thetableofcontents)

#### Wrap and Center Item Text

In v21.2, use the following code:

```cs
<style>
    .wrapText .dx-menu-item-text {
        white-space: normal !important;
    }
    .wrapText .dx-menu-item-text-container {
        text-align: center;
    }
</style>

<DxMenu>
    <Items>
        <DxMenuItem Text="My item" CssClass="wrapText" />
    </Items>
</DxMenu>
```

In v23.1, use the following code:

```cs
<style>
    .wrapText .dxbl-menu-item-text {
        white-space: normal !important;
    }
    .wrapText .dxbl-menu-item-text-container {
        text-align: center;
    }
</style>

<DxMenu>
    <Items>
        <DxMenuItem Text="My item" CssClass="menuItemLg" />
    </Items>
</DxMenu>
```

[Return to the table of contents.](#thetableofcontents)

#### Change Item Text Color

In v21.2, use the following CSS rules:

```css
.menu-container .dx-menu-item {
    color: white !important;
}
```

In v23.1, use the following code:

```cs
<style>
    .my-menu {
        color: white;
    }
</style>

 <DxMenu CssClass="my-menu">...</DxMenu>
```

[Return to the table of contents.](#thetableofcontents)

#### Change Item Background Color

In v22.1, use the following CSS rules:

```css
.my-menu dxbl-menu-item {
    background-color: yellow; 
}
```

In v23.1, use the following CSS rules:

```css
.my-menu .dxbl-menu-item {
    background-color: yellow;
}
```

[Return to the table of contents.](#thetableofcontents)

#### Make a Drop-Down Item Overflow Container Boundaries

In v20.2, use the following code:

```cs
<style>
    .menu-style .nav-item.dropdown.dx-menu-item {
        position: inherit !important;
    }
</style>

<DxMenu DropDownActionMode="MenuDropDownActionMode.Click" CssClass="customMenu">
    <Items>
        @* ... *@
    </Items>
</DxMenu>
```

In v21.2, use the following code:

```cs
<style>
    .customMenu .dropdown-menu {
        position: fixed;
    }
</style>

<DxMenu DropDownActionMode="MenuDropDownActionMode.Click" CssClass="customMenu">
    <Items>
        @* ... *@
    </Items>
</DxMenu>
```

In v23.1, you can remove these rules. This functionality is available out-of-the-box.

[Return to the table of contents.](#thetableofcontents)

#### Add a Scroll Bar to a Drop-Down Item

In v22.1, use one of the following CSS rules:

```css
.menu-item .dropdown-menu {
    height: 100px;
    overflow: auto !important;
}

.my-menu .dropdown-menu > ul {
    max-height:600px;
    overflow-y: auto;
}
```

In v23.1, use the `SubMenuCssClass` property as follows:

```cs
<style>
    .myMenu {
        height: 100px;
        overflow: auto !important;
    }
</style>

<DxMenu SubMenuCssClass="myMenu">
    @* ... *@
</DxMenu>
```

[Return to the table of contents.](#thetableofcontents)

#### Remove Background for Selected and Hovered Drop-Down Items

In v21.2, use the following CSS rules:

```css
.nav-link.item-position-start:hover {
    background-color: #FFF;
    transform: none!important;
}
.nav-link.item-position-start.selected {
    background-color: #FFF;
    transform: none !important;
}
```

In v23.1, use the following CSS rules:

```css
.dxbl-menu-item .dxbl-active {
    background-color: #FFF;
    transform: none !important;
}

.dxbl-menu-dropdown-item {
    background-color: #FFF;
    transform: none !important;
}
```

[Return to the table of contents.](#thetableofcontents)

#### Reduce Menu Size

In v21.2, use the following rules:

```css
.nav-link, .dropdown-item {
    padding: 0.1rem 0.5rem;
}

.menuitem {
    font-size: 0.8rem;
}
```

In v23.1, set the [SizeMode](https://docs.devexpress.com/Blazor/DevExpress.Blazor.DxMenu.SizeMode) property value to `Small`:

```cs
<DxMenu Title="DevExpress" SizeMode="SizeMode.Large">...</DxMenu>
```

[Return to the table of contents.](#thetableofcontents)

#### Remove the Left Padding of a Drop-Down Toggle

In v21.2, use the following CSS rules:

```css
.my-menu .dropdown-toggle {
    padding-left: unset;
}
```

In v23.1, use the following CSS rules:

```css
.dxbl-menu-dropdown-toggle {
    --dxbl-btn-image-spacing: 0;
}
```

[Return to the table of contents.](#thetableofcontents)

#### Add Custom Content to Title Container

In v20.2, use the following CSS selectors:

```css
.my-menu .dx-menu-title::before{
    <!-- Custom content -->
}
.my-menu .dx-menu-title::after {
    <!-- Custom content -->
}
```

In v23.1, use the [TitleTemplate](https://docs.devexpress.com/Blazor/DevExpress.Blazor.DxMenu.TitleTemplate) property.

[Return to the table of contents.](#thetableofcontents)

### DxTabs

#### Create Rounded Tabs

In v22.1, v22.2, and v23.1, use the same razor code:

```cs
<DxTabs CssClass="MyTabsCss">
    <DxTab Text="Home" CssClass="MyTabCss"></DxTab>
    <DxTab Text="Products" CssClass="MyTabCss"></DxTab>
    <DxTab Text="Support" CssClass="MyTabCss"></DxTab>
</DxTabs>
```

In v22.1, use the following CSS rules:

```css
.MyTabsCss > ul {
    border-bottom-width: 0px;
}
.MyTabCss > a {
    border-radius: 20px !important;
    border: 1px solid white !important;
}
.MyTabCss > a:hover {
    border-color: #e9ecef !important;
}
.MyTabCss > a.active {
    border-color: dodgerblue !important;
    background-color: dodgerblue !important;
}
```

In v22.2, use the following CSS rules:

```css
.MyTabsCss {
    border-bottom-width:0px;
}
.MyTabCss  {
    border-radius: 20px !important;
    border: 1px solid white !important;
}
.MyTabCss:hover {
    border-color: #e9ecef !important;
}

.MyTabCss.dxbl-active {
    border-color: dodgerblue !important;
    background-color: dodgerblue !important;
}
.MyTabCss.dxbl-active:after {
    background-color:transparent!important;
}
```

In v23.1, use the following CSS rules:

```css
.MyTabsCss nav {
    border-bottom-width: 0px !important; 
}
.MyTabCss  {
    border-radius: 20px !important;
    border: 1px solid white !important;
}
.MyTabCss:hover {
    border-color: #e9ecef !important;
}

.MyTabCss.dxbl-active {
    border-color: dodgerblue !important;
    background-color: dodgerblue !important;
}
.MyTabCss.dxbl-active:after {
    background-color:transparent!important;
}
```

[Return to the table of contents.](#thetableofcontents)

#### Change Background Color of a Tab Header

In v22.2 and v23.1, use the same razor code:

```cs
<DxTabs CssClass="MyTabsCss">
    <DxTab Text="Home" CssClass="MyTabCss"></DxTab>
    <DxTab Text="Products" CssClass="MyTabCss"></DxTab>
    <DxTab Text="Support" CssClass="MyTabCss"></DxTab>
</DxTabs>
```

In v22.1, use the following CSS rule:

```css
.MyTabsCss {
    background-color: #e6eaf4 !important;
}
```

In v23.1, use the following CSS rule:

```css
.MyTabsCss nav {
    background-color: #e6eaf4 !important;
}
```

[Return to the table of contents.](#thetableofcontents)

#### Change the Font of a Tab Header

In v22.2 and v23.1, use the same razor code:

```cs
<DxTabs CssClass="MyTabsCss">
    <DxTab Text="Home" CssClass="MyTabCss"></DxTab>
    <DxTab Text="Products" CssClass="MyTabCss"></DxTab>
    <DxTab Text="Support" CssClass="MyTabCss"></DxTab>
</DxTabs>
```

In v22.1, use the following CSS rule:

```css
.MyTabsCss {
       font-size: 13px !important;
       font-weight: 600 !important;
}
```

In v23.1, use the following CSS rule:

```css
.MyTabsCss nav {
    font-size: 13px !important;
    font-weight: 600 !important;
}
```

[Return to the table of contents.](#thetableofcontents)

### DxTreeView

#### Display Filter Panel at the Bottom of the Component

In v22.2, use the following code:

```cs
<style>
    .treeview {
        display: flex;
        flex-flow: column;
    }

    .treeview ul.nav-pills {
        order: 1;
    }

    .treeview .dxbl-navigation-filter {
        order: 2;
    }
</style>

<DxTreeView ShowFilterPanel="true" CssClass="treeview">...</DxTreeView>
```

In v23.1, use the following code:

```cs
<style>
    .treeview .dxbl-navigation-filter {
        order: 1;
    }
</style>

<DxTreeView ShowFilterPanel="true" CssClass="treeview">...</DxTreeView>
```

[Return to the table of contents.](#thetableofcontents)

#### Apply Custom Highlighting to Filter Results

In v22.1, use the following code:

```cs
<DxTreeView>
    <NodeTextTemplate>
        <span>
            @{
                var text = context.Text;
                if (!context.FilterInfo.IsApplied) {
                    @text
                } else {
                    var filterValue = context.FilterInfo.Value;
                    var res = Regex.Replace(text, filterValue, $"<mark>$&</mark>", RegexOptions.IgnoreCase);
                    @((MarkupString)res)
                }
            }
        </span>
    </NodeTextTemplate>
</DxTreeView>
```


In v23.1, use the following code:

```cs
<style>
    mark {
        padding-top: 0;
        padding-bottom: 0;
    }
</style>

<DxTreeView>
    <NodeTextTemplate>
        <span>
            @{
                var text = context.Text;
                if (!context.FilterInfo.IsApplied) {
                    @text
                } else {
                    var filterValue = context.FilterInfo.Value;
                    var res = Regex.Replace(text, filterValue, $"<mark>$&</mark>", RegexOptions.IgnoreCase);
                    @((MarkupString)res)
                }
            }
        </span>
    </NodeTextTemplate>
</DxTreeView>
```

[Return to the table of contents.](#thetableofcontents)

#### Customize Badge Appearance

In v21.2, use the `badge` class:

```css
.my-node a .badge {
    background-color: blue !important;
}
```

In v23.1, use the `dxbl-badge` class:

```css
.my-node .dxbl-badge {
    background-color: blue !important;
}
```

[Return to the table of contents.](#thetableofcontents)

#### Achieve NavLinkMatch.All Behavior

In v20.2, use the following code:

```cs
<NodeTemplate>
    <NavLink Match="@(string.IsNullOrEmpty(context.NavigateUrl) ? NavLinkMatch.All : NavLinkMatch.Prefix)" class="nav-link" href="@context.NavigateUrl">@context.Text</NavLink>
</NodeTemplate>
```

In v23.1, you can remove the `NodeTemplate` and set the [DxTreeView.UrlMatchMode](https://docs.devexpress.com/Blazor/DevExpress.Blazor.DxTreeView.UrlMatchMode) or [DxTreeViewNode.UrlMatchMode](https://docs.devexpress.com/Blazor/DevExpress.Blazor.DxTreeViewNode.UrlMatchMode) property to `Exact`.

```cs
<DxTreeView AllowSelectNodes="true" UrlMatchMode="NavigationUrlMatchMode.Exact">
    <Nodes>
        <DxTreeViewNode NavigateUrl="./" Text="Overview" UrlMatchMode="NavigationUrlMatchMode.Exact"></DxTreeViewNode>
        <DxTreeViewNode NavigateUrl="grid" Text="Grid"></DxTreeViewNode>
    </Nodes>
</DxTreeView>
```

[Return to the table of contents.](#thetableofcontents)

#### Customize Item Container Indents

In v21.2, use the following CSS rules:

```css
.my-custom-treeview div.dxbs-tree-tmpl + ul.nav {
    margin: 0.2em 0px 0.2em 40px !important;
}
```

In v23.1, use the following CSS rules:

```css
.my-custom-treeview .dxbl-treeview-items-container {
    margin: 0.2em 0px 0.2em 40px !important;
}
```

[Return to the table of contents.](#thetableofcontents)

#### Remove Left Margin of Child Nodes

In v21.1, use the following CSS rules:

```css
.treeview > ul.nav ul.nav {
    margin-left: unset;
}
```

In v23.1, use the following CSS rules:

```css
.treeview {
    --dxbl-treeview-item-content-indent: unset;
}
```

#### Display Context Menu for a Node

In v21.2, use the following CSS rules to display a Context Menu above the `NodeTextTemplate`:

```css
.custom-list-class .nav-link {
    transform: none!important;
}
.custom-list-class .nav-link:hover {
    z-index: 1;
}
```

In v23.1, you can remove these classes as we redesigned the layout of our Context Menu. These classes are no longer required.

[Return to the table of contents.](#thetableofcontents)

#### Place an Icon Above Node Text

In v22.2, use the following code:

```cs
<style>
    .menuButton a {
        flex-direction: column;
    }
</style>

<DxTreeView>
    <DxTreeViewNode IconCssClass="my-icon" 
                    CssClass="menuButton" />
    @* ... *@
</DxTreeView>
```

In v23.1, use the following code:

```cs
<style>
    .menuButton .dxbl-treeview-item-container {
            flex-direction: column;
    }
</style>

<DxTreeView>
    <DxTreeViewNode IconCssClass="my-icon" 
                    CssClass="menuButton" />
    @* ... *@
</DxTreeView>
```

[Return to the table of contents.](#thetableofcontents)

## Restoring Changes Made after our v23.2 Release

### DxToolbar

#### Change Item Border Color

In v23.1, use the following style:

```css
.my-toolbar .dxbl-toolbar-group > .dxbl-btn { border: 1px red solid; }
```

In v23.2, use the following style:

```css
.my-toolbar .dxbl-toolbar-group > .dxbl-toolbar-item > .dxbl-btn { border: 1px red solid; } 
```

[Return to the table of contents.](#thetableofcontents)
