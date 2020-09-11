# Adding PrimeNG Components to Your Angular Project

<details><summary style="font-size:1.5em">Prologue</summary>
<p>Now that we have a basic understanding of <a href="angular-key-concepts.html">Angular Key Concepts</a>, let's add some components to our project. We don't have to start from scratch, we can use one of the fine UI libraries available for Angular, such as Google's <a href="https://material.angular.io/">Angular Material</a>, Teradata's <a href="https://teradata.github.io/covalent/#/">Covalent</a> or PrimeFaces' <a href="https://www.primefaces.org/primeng/#/">PrimeNG</a>.
</p>

<p>In this post, I will focus on adding PrimeNG components to the project we created in <a href="getting-started-with-angular.html">Getting Started with Angular</a>.</p>

<p>PrimeNG's official <a href="https://www.primefaces.org/primeng/#/setup"> Getting Started</a> is great, but this post distills it and combines information from other parts of the documentation so all you need to get started with all that PrimeNG offers is in one spot.
</p>
</details>

## TL;DR
This post walks you through installing packages you need to incorporate PrimeNG components (and dependencies) into your Angular project and editing the files `app.module.ts`, `angular.json` and `index.html` to link them all up.

## 1. Installing NPM Packages


> If following along from where we left off in a previous post, consider creating a new source branch to be able to come back later to this point.

Go to your terminal and install the packages as follows:

```bash
npm install primeng --save      # Required
npm install primeicons --save   # Mostly required
npm install @angular/animations --save # For animations
npm install primeflex --save # Optional, for FlexGrid
npm install chart.js --save # Optional, for Charts
npm install quill --save # Optional, for Editor component
npm install fullcalendar@4.0.0-alpha.2 --save # Optional, for use FullCalendar (available on PrimeNG v7+)
npm install prismjs --save # Optional, For code-highlighting
```

## 2. Importing the Components you will Use

PrimeNG components and directives can be individually imported based on your need, instead of importing the whole library. This saves on the size of your app. 

Keep in mind:
1. Some functionality requires multiple imports, where they're used. For example, for menu components, the module (e.g. `MenuModule`) should be imported in `app.module.ts` and the type `MenuItem`  should be imported in the file the menu model is defined. Another example is for tree components (e.g. `TreeModule` and `TreeNode`).
2. Some components require scripts and/or styles to be incorporated.
3. FlexGrid uses PrimeFlex and has no imports.

I've made a list of every import available on PrimeNG as of writing for convenience. You can copy the whole thing into your app and comment out any lines you won't need. 

In your `app.module.ts`, modules need to be first imported then declared in the `imports` array of the `NgModule` decoration of your AppModule.

```typescript
// Angular imports - as needed
import { BrowserModule } from '@angular/platform-browser';
import { BrowserAnimationsModule } from '@angular/platform-browser/animations';
import { NgModule } from '@angular/core';
import { FormsModule } from '@angular/forms';
import { HttpClientModule } from '@angular/common/http';

// PrimeNG imports - as needed
import { AccordionModule } from 'primeng/accordion'; // <p-accordion><p-accordionTab>
import { AutoCompleteModule } from 'primeng/autocomplete'; // <p-autoComplete>
import { BlockUIModule } from 'primeng/blockui'; // <p-blockUI>
import { BreadcrumbModule } from 'primeng/breadcrumb'; // <p-breadcrumb>
import { ButtonModule } from 'primeng/button'; // <button pButton (click)=""> or <p-button (onClick)="">
import { CalendarModule } from 'primeng/calendar';  // <p-calendar>
import { CaptchaModule } from 'primeng/captcha'; //  <p-captcha> // Needs script
import { CardModule } from 'primeng/card'; // <p-card><p-header/><p-footer/>
import { CarouselModule } from 'primeng/carousel'; // <p-carousel>
import { ChartModule } from 'primeng/chart'; // <p-chart type="">
import { CheckboxModule } from 'primeng/checkbox'; // <p-checkbox>
import { ChipsModule } from 'primeng/chips'; // <p-chips>
import { CodeHighlighterModule } from 'primeng/codehighlighter'; // <pre><code class="" pCode>
import { ColorPickerModule } from 'primeng/colorpicker'; // <p-colorPicker>
import { ConfirmDialogModule } from 'primeng/confirmdialog'; // <p-confirmDialog>
import { ContextMenuModule } from 'primeng/contextmenu'; // <p-contextMenu>
import { DataScrollerModule } from 'primeng/datascroller'; // <p-dataScroller>
import { DataViewModule } from 'primeng/dataview'; // <p-dataView>
import { DeferModule } from 'primeng/defer'; // <div pDefer><ng-template>
import { DialogModule } from 'primeng/dialog'; // <p-dialog>
import { DragDropModule } from 'primeng/dragdrop'; // <div pDraggable="" dragHandle="">
import { DropdownModule } from 'primeng/dropdown'; // <p-drowdown>
import { EditorModule } from 'primeng/editor'; // <p-editor> Based on Quill
import { FieldsetModule } from 'primeng/fieldset'; // <p-fieldset>
import { FileUploadModule } from 'primeng/fileupload'; // <p-fileUpload>
// FlexGrid: Uses PrimeFlex
import { FullCalendarModule } from 'primeng/fullcalendar'; // <p-fullCalendar> Needs dependency. v7+
import { GalleriaModule } from 'primeng/galleria'; // <p-galleria>
import { GMapModule } from 'primeng/gmap'; // <p-gmap>
import { GrowlModule } from 'primeng/growl'; // <p-growl>
import { InplaceModule } from 'primeng/inplace'; // <p-inplace>
import { InputMaskModule } from 'primeng/inputmask'; // <p-inputMask>
import { InputSwitchModule } from 'primeng/inputswitch'; // <p-inputSwitch>
import { InputTextareaModule } from 'primeng/inputtextarea'; // <textarea pInputTextarea>
import { InputTextModule } from 'primeng/inputtext'; // <input type="text" pInputText />
import { KeyFilterModule } from 'primeng/keyfilter'; // <input pKeyFilter="">
import { LightboxModule } from 'primeng/lightbox'; // <p-lightbox>
import { ListboxModule } from 'primeng/listbox'; // <p-listbox>
import { MegaMenuModule } from 'primeng/megamenu'; // <p-megaMenu>
import { MenubarModule } from 'primeng/menubar'; // <p-menubar>
import { MenuModule } from 'primeng/menu'; // <p-menu>
import { MessageModule } from 'primeng/message'; // <p-message>
import { MessagesModule } from 'primeng/messages'; // <p-messages>
import { MultiSelectModule } from 'primeng/multiselect'; // <p-multiSelect>
import { OrderListModule } from 'primeng/orderlist'; // <p-orderList>
import { OrganizationChartModule } from 'primeng/organizationchart'; // <p-organizationChart>
import { OverlayPanelModule } from 'primeng/overlaypanel'; // <p-overlayPanel>
import { PaginatorModule } from 'primeng/paginator'; // <p-paginator>
import { PanelMenuModule } from 'primeng/panelmenu'; // <p-panelMenu>
import { PanelModule } from 'primeng/panel'; // <p-panel>
import { PasswordModule } from 'primeng/password'; // <input type="password" pPassword/>
import { PickListModule } from 'primeng/picklist'; // <p-pickList>
import { ProgressSpinnerModule } from 'primeng/progressspinner'; // <p-progressSpinner>
import { RadioButtonModule } from 'primeng/radiobutton'; // <p-radioButton>
import { RatingModule } from 'primeng/rating'; // <p-rating>
import { ScrollPanelModule } from 'primeng/scrollpanel'; // <p-scrollPanel>
import { SidebarModule } from 'primeng/sidebar'; // <p-sidebar>
import { SlideMenuModule } from 'primeng/slidemenu';
import { SliderModule } from 'primeng/slider'; // <p-slider>
import { SpinnerModule } from 'primeng/spinner'; // <p-spinner>
import { SplitButtonModule } from 'primeng/splitbutton'; // <p-splitButton>
import { StepsModule } from 'primeng/steps'; // <p-steps>
import { TableModule } from 'primeng/table'; // <p-table>
import { TabMenuModule } from 'primeng/tabmenu'; // <p-tabMenu>
import { TabViewModule } from 'primeng/tabview'; // <p-tabView><p-tabPanel>
import { TerminalModule } from 'primeng/terminal'; // <p-terminal>
import { TieredMenuModule } from 'primeng/tieredmenu'; // <p-tieredMenu>
import { ToastModule } from 'primeng/toast'; // <p-toast>
import { ToggleButtonModule } from 'primeng/togglebutton'; // <p-toggleButton>
import { ToolbarModule } from 'primeng/toolbar'; // <p-toolbar><div class="ui-toolbar-group-left">
import { TooltipModule } from 'primeng/tooltip'; // <input type="text" pTooltip="">
import { TreeModule } from 'primeng/tree'; // <p-tree>
import { TreeTableModule } from 'primeng/treetable'; // <p-treeTable>
import { TriStateCheckboxModule } from 'primeng/tristatecheckbox'; // <p-triStateCheckbox>

// For reference, include these lines where the types are used:

// import { ConfirmationService } from 'primeng/api'; // used with ConfirmDialog
// import { MenuItem } from 'primeng/api'; // used with breadcrumb, contextMenu, menu, menubar, panelMenu, slideMenu, tieredMenu
// import { Message } from 'primeng/api'; // used with the MessageService
// import { MessageService } from 'primeng/api'; // alternative to the component approach
// import { TreeNode } from 'primeng/api'; // used with tree coponents

import { AppComponent } from './app.component';

@NgModule({
    declarations: [
        AppComponent
    ],
    imports: [
        // Angular modules
        BrowserModule,
        BrowserAnimationsModule,
        FormsModule,
        HttpClientModule,

        // PrimeNG modules
        AccordionModule,
        AutoCompleteModule,
        BlockUIModule,
        BreadcrumbModule,
        ButtonModule,
        CalendarModule,
        CaptchaModule,
        CardModule,
        CarouselModule,
        ChartModule,
        CheckboxModule,
        ChipsModule,
        CodeHighlighterModule,
        ColorPickerModule,
        ConfirmDialogModule,
        ContextMenuModule,
        DataScrollerModule,
        DataViewModule,
        DeferModule,
        DialogModule,
        DragDropModule,
        DropdownModule,
        EditorModule,
        FieldsetModule,
        FileUploadModule,
        FullCalendarModule,
        GalleriaModule,
        GMapModule,
        GrowlModule,
        InplaceModule,
        InputMaskModule,
        InputSwitchModule,
        InputTextareaModule,
        InputTextModule,
        KeyFilterModule,
        LightboxModule,
        ListboxModule,
        MegaMenuModule,
        MenubarModule,
        MenuModule,
        MessageModule,
        MessagesModule,
        MultiSelectModule,
        OrderListModule,
        OrganizationChartModule,
        OverlayPanelModule,
        PaginatorModule,
        PanelMenuModule,
        PanelModule,
        PasswordModule,
        PickListModule,
        ProgressSpinnerModule,
        RadioButtonModule,
        RatingModule,
        ScrollPanelModule,
        SidebarModule,
        SlideMenuModule,
        SliderModule,
        SpinnerModule,
        SplitButtonModule,
        StepsModule,
        TableModule,
        TabMenuModule,
        TabViewModule,
        TerminalModule,
        TieredMenuModule,
        ToastModule,
        ToggleButtonModule,
        ToolbarModule,
        TooltipModule,
        TreeModule,
        TreeTableModule,
        TriStateCheckboxModule
    ],
    providers: [],
    bootstrap: [AppComponent]
})
export class AppModule { }
```


## 3. Importing Dependency Styles

You can import dependency styles a few ways;
1. Directly in `<head>` in `index.html` as in `<link rel="stylesheet" type="text/css" href="dependency.min.css">`,
2. Import the css in `src/styles.less` as in  `@import '../node_modules/fullcalendar/dist/dependency.min.css';` - Note: use relative paths
3. Put a reference to the `styles` array under `projects.architect.build.options` in `angular.json`. Example:

```json
[
    "node_modules/primeflex/primeflex.scss",                   // If using FlexGrid
    "node_modules/fullcalendar/dist/fullcalendar.min.css",     // If using FullCalendar component
    "node_modules/quill/dist/quill.core.css",                  // If using editor component
    "node_modules/quill/dist/quill.snow.css",                  // If using editor component
    "node_modules/primeng/resources/themes/omega/theme.scss",  // Based on your theme
    "node_modules/primeng/resources/primeng.min.css",
    "node_modules/primeicons/primeicons.css",
    "src/styles.less"
]
```


## 4. Importing Dependency Scripts

You can import dependency scripts in a couple of ways:
### 1. Include a `<script>` tag directly in your `index.html`.
```HTML
<!-- For Captcha component -->
<script src="https://www.google.com/recaptcha/api.js" async defer></script>

<!-- For GMaps component (replace GOOGLE_MAPS_API_KEY value with your own -->
<script type="text/javascript" src="https://maps.google.com/maps/api/js?key=GOOGLE_MAPS_API_KEY" async defer></script>
```

### 2. Include a referece in the `scripts` array under `projects.architect.build.options` in `angular.json`.

For example:
```json
[
    "node_modules/chart.js/dist/Chart.js",                      // If using chart components
    "node_modules/fullcalendar/dist/fullcalendar.min.js",       // If using FullCalendar component
    "node_modules/quill/dist/quill.js"                          // If using editor component
]
```

At this point, if you do an `ng serve` and go to `http://localhost:4200`, you should be able to see the app like before. If the page is broken in any way, including nothing beind displayed, check out the Developer Tools console to check out any error messages. Otherwise, you're good to go to use PrimeNG components in your own components.


