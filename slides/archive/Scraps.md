
<!-- Page 11 - Web Sites (SPAs) - Architecture -->

<!-- _class: details invert -->

### Web Sites (SPAs)

![height:250px](./images/website-spas-high-level.drawio.svg)

<div class="detail-summary">

- The server/cloud stack is the focus, turning data into pages and layouts
- Complex page layouts are generally built on top of templating frameworks
- SPAs may modify a page layout, but the initial layout comes from the server
- Result: web devs expect fat data pipes in the server/cloud stack so they can get large data payloads (object graphs) all at once and choose what to filter

</div>

---

<!-- Page 12 - Web Sites (SPAs) - Summary -->

<!-- _class: details invert -->

### Web Sites (SPAs)

<div class="two-columns">

<div>

#### <i>Browser (Client)</i>

- Requests: Browse, Submit
- State Management: Cookies
- Data Mapping: None
- Caching: Local, Session, Cookies
- Resiliency: Browser
- Development Focus: Interactivity, Data Updates
- Data Goal: Fat Data Pipes (to Site)

</div>

<div>

#### <i>Site (Server/Cloud)</i>

- Responses: Page Layouts (Whole)
- State Management: Server/Cloud
- Data Mapping: Source to Site
- Caching: Server/Cloud
- Resiliency: Server/Cloud, Services
- Development Focus: Layouts, State, Services
- Data Goal: Fat Data Pipes (inside Site)

<span class="break" />

</div>

</div>

---

/*
@font-face {
  font-family: Martel_Sans_Regular;
  src: url('../fonts/Google Fonts/Martel_Sans/MartelSans-Regular.ttf');
  font-weight: regular;
}
*/

/*
h3 {
  font-size: 60px;
}
*/

/*
li {
  font-family: Martel_Sans_Bold;
}
*/

<!--
/*
section.section_title ul li {
  font-size: 64px;
  line-height: 2ex;
}
*/


/*
@font-face {
  font-family: Permanent_Marker;
  src: url('../fonts/Google Fonts/Permanent_Marker/PermanentMarker-Regular.ttf');
  font-weight: regular;
}
*/
-->

/*
section.summary ul li,
section.title ul li {
  line-height: 1.75em;
}
*/

/*
section.title h2 {
  font-weight: 900;
}
*/

/*
section.title ul {
  list-style-type: none;
}
*/

/*
section.title ul li h3,
section.title ul li h4 {
  font-family: Pangolin, cursive;
  font-size: 48px;
  font-size: 48px;
  text-align: center;
}
*/

<!--
<div class="detail-summary" style="padding: 20px 0px 0px;">

(*) Single-page application (SPAs) request pages (HTML/JS/CSS) like traditional sites and update their content via API calls but still rely on the browser infrastructure

</div>
-->

<!-- ########## Page 5 - Web Sites (Traditional / SPAs) - Summary ########## -->

<!-- _class: details -->

### Web Sites (Traditional and SPAs)

<div class="two-columns">

<div>

#### <i>Browser (Client)</i>

- Requests: Browse, Submit, API Calls (SPAs)
- State Mgmt: Page (SPAs)
- Data Map: API to Layout (SPAs)
- Caching: Browser
- Resiliency: Browser
- Development: Interactivity, Data Updates, Layout Updates (SPAs)
- Data Goal: Fat Data Pipes

<span class="break" />

###### Focus: Single-page Applications

</div>

<div>

#### <i>Site (Server/Cloud)</i>

- Responses: Layout (Whole/Partial), Data (JSON/XML)
- State Mgmt: Server/Cloud
- Data Map: Source to Site
- Caching: Server/Cloud
- Resiliency: Server/Cloud, Services
- Development: Layouts, Services, State (Traditional)
- Data Goal: Fat Data Pipes

<span class="break" />

###### Focus: Traditional Sites

</div>

</div>

<!--
<div class="detail-summary" style="padding: 20px 0px 0px;">

(*) Single-page application (SPAs) request pages (HTML/JS/CSS) like traditional sites and update their content via API calls but still rely on the browser infrastructure

</div>
-->

<!-- ################## Page 10 - Web vs Mobile - Summary ################## -->

<!-- _class: details -->

## Web vs Mobile - Different Focuses

<div class="two-columns">

<div>

##### <i>Web Site</i>

- Synchronous Browse, Submit
- Site Response: Page (HTML/JS)
- State Mgmt: Server, Page
- ORM: Data Source to Server/Cloud
- Client Caching: Browser
- Focus: Heavy Server/Cloud Services
- Resiliency: Server/Cloud
- Data Goal: Fat Data Pipes

</div>

<div>

##### <i>Mobile App</i>

- Asynchronous REST  (GET, POST, etc.)
- API Response: JSON/XML (DTO)
- State Mgmt: App, Cache (OS, DB)
- ORM: Data Source to API, API to App
- Client Caching: App (Custom or OS)
- Focus: Light API Consumption
- Resiliency: API Calls, Server/Cloud
- Data Goal: Smart Data Pipes

</div>

</div>

---

---

<!-- Page 20 - Mobile Architecture - More Detail -->

<!-- _class: details -->

## Mobile Architecture - More Detail

<div class="mermaid">
%%{init: {'theme': 'neutral',
    'themeVariables': {'labelBackgroundColor': 'transparent'}}}%%
stateDiagram
    direction LR
    [*] --> Page
    Page --> ViewModels : Binding
    ViewModels: ViewModel_1
    ViewModels: ViewModel_2
    ViewModels --> Cache : Cache
    Cache: Platform
    Cache: Local DB
    Cache --> ViewModels : Data?
    ViewModels --> Page : Model
    ViewModels --> API : Request
    API --> ViewModels : JSON
    API: API_1
    API: API_2
</div>

---

<!-- Page 21 - Mobile Architecture - Real World -->

<!-- _class: details -->

## Mobile Architecture - Real-world

<div class="mermaid">
%%{init: {'theme': 'neutral',
    'themeVariables': {'labelBackgroundColor': 'transparent'}}}%%
stateDiagram
    direction LR
    [*] --> Page
    state App_Stack_1 {
        Page --> ViewModels
        ViewModels --> DataService
        ViewModels: ViewModel_1
        ViewModels: ViewModel_2
        DataService --> Cache: Cache
        Cache: Platform
        Cache: Local DB
        Cache --> DataService : Data?
        DataService --> ApiService
        ApiService: ApiService_1
        ApiService: ApiService_2
        ApiService --> DataService : Model
        DataService --> ViewModels : Model
        ViewModels --> Page : Properties
    }
</div>

<div class="mermaid">
%%{init: {'theme': 'neutral',
    'themeVariables': {'labelBackgroundColor': 'transparent'}}}%%
stateDiagram
    direction LR
    state App_Stack_2 {
        direction LR
        ApiTester_1 --> ApiService_1
        ApiService_1 --> ApiTester_1 : Models
        ApiTester_2 --> ApiService_2
        ApiService_2 --> ApiTester_2 : Models
    }
    ApiService_1 --> Api_1
    Api_1 --> ApiService_1
    ApiService_2 --> Api_2
    Api_2 --> ApiService_2
</div>

---

<!-- Page 22 - Mobile Architecture - Real World -->

<!-- _class: details -->

## Mobile Architecture - Real-world

<div class="mermaid">
%%{init: {'theme': 'neutral',
    'themeVariables': {'labelBackgroundColor': 'transparent'}}}%%
stateDiagram
    direction LR
    [*] --> Page
    state App_Stack_1 {
        Page --> ViewModels
        ViewModels --> DataService
        ViewModels: ViewModel_1
        ViewModels: ViewModel_2
        DataService --> Cache: Cache
        Cache: Platform
        Cache: Local DB
        Cache --> DataService : Data?
        DataService --> ApiService
        ApiService: ApiService_1
        ApiService: ApiService_2
        ApiService --> DataService : Model
        DataService --> ViewModels : Model
        ViewModels --> Page : Properties
    }
</div>

<div class="mermaid">
%%{init: {'theme': 'neutral',
    'themeVariables': {'labelBackgroundColor': 'transparent'}}}%%
stateDiagram
    direction LR
    state App_Stack_2 {
        direction LR
        ApiTester_1 --> ApiService_1
        ApiService_1 --> ApiTester_1 : Models
        ApiTester_2 --> ApiService_2
        ApiService_2 --> ApiTester_2 : Models
    }
    ApiService_1 --> Api_1
    Api_1 --> ApiService_1
    ApiService_2 --> Api_2
    Api_2 --> ApiService_2
</div>