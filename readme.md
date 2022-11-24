<!-- default badges list -->
[![](https://img.shields.io/badge/📖_How_to_use_DevExpress_Examples-e9f6fc?style=flat-square)](https://docs.devexpress.com/GeneralInformation/403183)
<!-- default badges end -->
<a name="thetableofcontents"></a>
- [How to update CSS styles to v22.2](#how-to-update-css-styles-to-v222)
- [Most common customizations](#most-common-customizations)
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
    - [Hide header row](#hide-header-row)
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
    - [DxCalender](#dxcalender)
      - [Change font color of weekends](#change-font-color-of-weekends)
      - [Hide week numbers](#hide-week-numbers)
      - [Hide the footer](#hide-the-footer)
      - [Hide the footer's Today button](#hide-the-footers-today-button)
  - [DxPopup](#dxpopup)
    - [Adjust popup size and position on the page](#adjust-popup-size-and-position-on-the-page)
    - [Customize popup size and position](#customize-popup-size-and-position)
    - [Customize the Close header's button icon](#customize-the-close-headers-button-icon)
    - [Hide the modal background](#hide-the-modal-background)

# How to update CSS styles to v22.2

In the [Most common customizations](#most-common-customizations) section of this repository, we summarized the most often cases when our users should use our private CSS selectors to apply a style to an element. 
 
Also, you can press Ctrl+F and search for a private CSS selector that you used in a previous version. This will help you find a selector that you used in v22.1 or prior, and copy the new equivalent of this selector.

If you didn't manage to find your scenario in this document, you can create a new CSS selector by inspecting a component render as described in the following articles: 

[View and change CSS](https://developer.chrome.com/docs/devtools/css/)<br/>
[How to implement CSS-related solutions for DevExpress components](https://supportcenter.devexpress.com/internal/ticket/details/T632424)

Feel free to write to our [Support Center](http://devexpress.com/support/center). We are ready to research your specific case.

[Return to the table of contents.](#thetableofcontents)

# Most common customizations

## DxGrid

### Align header captions

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

### Color alternate rows

To color alternate rows (universal approach), handle the CustomizeElement event:

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


### Change the default "No data to display" text

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


### Change the header cells' background color

In v22.1, use the following CSS rules:

```css
.dxbs-grid-header:nth-child(1){
    background-color: aqua !important
}
```
In v22.2, use the new CustomizeElement event to change the header cells' color instead of adding a custom CSS style:

```cs
void Grid_CustomizeElement(GridCustomizeElementEventArgs e) {
    if(e.ElementType == GridElementType.HeaderRow) {
    e.Style = "background-color: aqua;";
}
```
[Return to the table of contents.](#thetableofcontents)

### Change selected row background color

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

### Focus an editor inside the edit form

To focus an editor inside the grid edit form in v22.1 and earlier, it was necessary to use the JavaScript input.focus method:

```js
function focusFirstEditor() {
    setTimeout(function myfunction() {
        var inputElement = document.querySelectorAll(".my-grid .dxbs-grid-edit-form input")[1];
        inputElement.focus();
    }, 1000);
}
```
In v22.2, we automatically focus the first editor. If you wish to focus a different editor, wrap it into the CasadingValue component and set the CascadingValue.Name property to "FocusOnEditStart"::

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

### Hide the expand/collapse button for detail rows

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

### Hide the skeleton element

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

### Hide "No data to display" message

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

### Hide vertical lines

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

### Hide header row

To hide header row (universal approach), handle the CustomizeElement event:

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

### Place a scrollable DxGrid into DxPopup

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

### Prevent caption wrapping

To prevent caption wrapping (universal approach), handle the CustomizeElement event:

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


### Remove paddings for a detail grid

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


## DxFormLayout

### Change the location and style of a Form Layout item

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


### Change item captions

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

## DxToolbar

### Change title text color

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


### Center toolbar item content

In both v22.1 and v22.2, use the same razor code:

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

## DxTabs

### Create rounded tabs

In both v22.1 and v22.2, use the same razor code:
```cs
<DxTabs CssClass="MyTabsCss">
  <DxTab Text="Home" CssClass="MyTabCss"></DxTab>
  <DxTab Text="Products" CssClass="MyTabCss"></DxTab>
  <DxTab Text="Support" CssClass="MyTabCss"></DxTab>
</DxTabs>
```

In v22.1, use the follwing CSS rules:
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
In v22.2, use the follwing CSS rules:
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

## DxScheduler

### Change edit form width

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

## DxEditors

### Modify the Clear button
In v22.1 use the following code:
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
In v22.2 use the following code:
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

### DxTextBox 

#### Change the input's text style

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

#### Customize the Clear button's icon

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

#### Display an icon inside the input element


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

### DxTagBox 

#### Always force tags to start at a new line

In v22.1 use the following code:

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


### DxComboBox 

#### Change the height of a drop-down list

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

#### Change drop-down text font size

In v22.1 use the following code:

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

#### Modify "No data to display" message

In v19.2 use the following code:

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

#### Hide column headers

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

### DxDateEdit 

Internally, we use DxCalendar in the DxDateEdit popup. As such, when you need to apply a style to DxCalendar in the DxDateEdit popup, you can write selectors for DxCalendar itself. To write a selector for a specific DxDateEdit, assign the DxDateEdit.DropDownCssClass property.

[Return to the table of contents.](#thetableofcontents)

#### Highlight a week on mouse hover

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


#### Hide the drop down button

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

#### Localize the Time section scroll picker's text

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


### DxCalender

#### Change font color of weekends

In both v22.1 and v22.2, use the same razor code:
```cs
<DxCalendar SelectedDate="@DateStart"  CssClass="myCalendarCss"></DxCalendar>

@code {
    public DateTime DateStart { get; set; } = DateTime.Now;
}

```

In 22.1, use the following CSS rule:

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

#### Hide week numbers

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

#### Hide the footer

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

#### Hide the footer's Today button

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

## DxPopup

### Adjust popup size and position on the page

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

### Customize popup size and position

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



### Customize the Close header's button icon

In both v22.1 and v22.2, use the same razor code:

```cs
<DxPopup HeaderText="Header" @bind-Visible="@PopupVisible" CssClass="customPopup">
    <Content>
       ...
    </Content>
</DxPopup>
```

In v22.1, use the following CSS rule:
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

In v22.2, use the following CSS rule:
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

### Hide the modal background

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