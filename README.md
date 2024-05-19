# Power-BI-Embedded-API-A-Complete-Handbook-for-Power-BI-Integration
Embed Power BI reports/dashboards into your apps seamlessly using Power BI Embedded. This Microsoft service offers APIs enabling developers to integrate Power BI content effortlessly. For instance, integrate sales reports directly into a sales management app interface.

![image](https://github.com/Hagar-zakaria/Power-BI-Embedded-API-A-Complete-Handbook-for-Power-BI-Integration/assets/93611934/a247d5c1-905a-498e-b2b2-3b34c509b8fb)

# Key features of Power BI Embedded API:

1. Embedding Reports and Dashboards: Easily integrate Power BI reports and dashboards into custom apps for seamless user interaction.

2. Integration with Azure: Utilize Azure services to handle processing and rendering of Power BI content, ensuring optimal performance.

3. Customization: Tailor the appearance and behavior of embedded content to match app aesthetics and functionality.

4. Authentication and Security: Implement secure access mechanisms, like Azure Active Directory, to control user permissions and safeguard embedded content.

5. Programmatic Interaction: Enable developers to interact programmatically with embedded Power BI content, facilitating tasks such as data filtering and event handling.

For example, embedding Power BI content in a web app using JavaScript involves steps like including the Power BI JavaScript library and creating a JavaScript file to handle embedding logic. Customization and authentication methods can be implemented as needed for specific app requirements.


# Prerequisites:

1. You need a Power BI account Pro or Premium  and a workspace with the reports or dashboards you want to embed.
2. Obtain an embed token and report/dashboard ID for the content you want to embed.

# Step 1: Incorporate the Power BI JavaScript Library

In your HTML file, include the Power BI JavaScript library using the provided CDN link:   

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Power BI Embedded Example</title>
    <!-- Include Power BI JavaScript library -->
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.2.6/jquery.js"></script>
    <script src="https://microsoft.github.io/PowerBI-JavaScript/demo/node_modules/powerbi-client/dist/powerbi.js"></script>
</head>
<body>
    <!-- Your content goes here -->
    <div id="embedContainer" style="height: 600px;"></div>

    <!-- Include your application logic script -->
    <script src="app.js"></script>
</body>
</html>
```

# **This HTML code sets up a webpage to embed Power BI content into a custom application.**

**Here's a breakdown in simple terms:**

1.  !DOCTYPE html: This tells the browser that the document is an HTML5 document.

2. html lang="en": This starts the HTML document and specifies that the primary language used is English.

3. head>...</head: This section contains metadata about the document, like character encoding and viewport settings. It also includes the title of the webpage.

4. meta charset="UTF-8": This specifies the character encoding of the document to be UTF-8, which supports a wide range of characters.

5. meta name="viewport" content="width=device-width, initial-scale=1.0": This sets the viewport width to the width of the device and sets the initial zoom level to 1.0, ensuring proper scaling on mobile devices.

6. title>Power BI Embedded Example</title: This sets the title of the webpage displayed in the browser tab.

7. script src="..."/script: These lines include JavaScript libraries needed for embedding Power BI content. You may need to replace the URLs with the actual URLs of the JavaScript libraries you're using.

8. body.../body: This section contains the content of the webpage that users see. In this example, it includes a container with the ID "embedContainer" where the Power BI content will be embedded, and a script tag to include the application logic from an external JavaScript file (app.js).

**To customize this code for your application, you'll typically replace the following features:**

- Replace the <title> tag content with your desired webpage title.
- Replace the <script> tags' src attribute URLs with the URLs of the JavaScript libraries you're using for Power BI embedding.
- Customize the content within the <body> tag according to your application's needs, and replace "embedContainer" with the ID of the container where you want to embed the Power BI content.

# Step 2: Develop a JavaScript File (app.js)

Create a JavaScript file named "app.js" to manage the embedding process. This file will house the script responsible for embedding the Power BI content into your application.

<script>
//let loadedResolve, reportLoaded = new Promise((res, rej) => { loadedResolve = res; });
let renderedResolve, reportRendered = new Promise((res, rej) => { renderedResolve = res; });
const reportId = "your_report_id_here";
const groupId = "your_groupId_here";

// Get models. models contains enums that can be used.
models = window['powerbi-client'].models;

// Embed a Power BI report in the given HTML element with the given configurations
// Read more about how to embed a Power BI report in your application here: https://go.microsoft.com/fwlink/?linkid=2153590
function embedPowerBIReport() {
    /*-----------------------------------------------------------------------------------+
    |    Don't change these values here: access token, embed URL and report ID.          | 
    |    To make changes to these values:                                                | 
    |    1. Save any other code changes to a text editor, as these will be lost.         |
    |    2. Select 'Start over' from the ribbon.                                         |
    |    3. Select a report or use an embed token.                                       |
    +-----------------------------------------------------------------------------------*/
    // Read embed application token
    let accessToken = "your_access_token";

    // Read embed URL
    let embedUrl = `https://app.powerbi.com/reportEmbed?reportId=${reportId}&groupId=${groupId}`;

    // Read report Id
    let embedReportId = reportId;

    // Read embed type from radio
    //let tokenType = TOKEN_TYPE;

    // We give All permissions to demonstrate switching between View and Edit mode and saving report.
    let permissions = models.Permissions.All;

    // Create the embed configuration object for the report
    // For more information see https://go.microsoft.com/fwlink/?linkid=2153590
    let config = {
        type: 'report',
        tokenType: models.TokenType.Embed,  // Correct reference
        accessToken: accessToken,
        embedUrl: embedUrl,
        id: embedReportId,
        permissions: permissions,
        viewMode: models.ViewMode.View,
        settings: {
            filterPaneEnabled: false,
            navContentPaneEnabled: true,
            layoutType: models.LayoutType.Custom, // You can experiment with layoutType
            panes: {
                filters: {
                    visible: true
                },
                pageNavigation: {
                    visible: true
                }
            },
            bars: {
                statusBar: {
                    visible: true
                }
            }
        }
    };

    // Get a reference to the embedded report HTML element
    let embedContainer = $('#embedContainer')[0];

    // Embed the report and display it within the div container.
    report = powerbi.embed(embedContainer, config);

    // report.off removes all event handlers for a specific event
    report.off("loaded");

    // report.on will add an event handler
    report.on("loaded", function () {
        loadedResolve();
        report.off("loaded");
    });

    // report.off removes all event handlers for a specific event
    report.off("error");

    report.on("error", function (event) {
        console.log(event.detail);
    });

    // report.off removes all event handlers for a specific event
    report.off("rendered");

    // report.on will add an event handler
    report.on("rendered", function () {
        renderedResolve();
        report.off("rendered");
    });
}

embedPowerBIReport();
reportLoaded;

// Insert here the code you want to run after the report is loaded

reportRendered;

// Insert here the code you want to run after the report is rendered

</script>


This JavaScript code is designed to embed a Power BI report into a web application. It sets up an embedding function embedPowerBIReport() responsible for configuring and embedding the report using Power BI's client library. Key elements, such as the report and group IDs, and the access token, are placeholders that need to be replaced with actual values corresponding to your Power BI report and authentication credentials. Once the script is embedded into the HTML file, it retrieves the necessary elements and embeds the report into the designated container. Event handlers are set up to handle various states of the embedding process. Users can customize the code by replacing placeholder values and adjusting the configuration settings according to their specific requirements, such as specifying permissions, adjusting layout, or handling error events.


**Here are the features that need to be replaced:**

1. Report ID (reportId): Replace "your_report_id_here" with the ID of your Power BI report.
2. Group ID (groupId): Replace "your_groupId_here" with the ID of the group containing your Power BI report.
3. Access Token (accessToken): Replace "your_access_token" with your Power BI access token.
4. Embed URL (embedUrl): The embed URL is constructed dynamically based on the report and group IDs. No direct replacement needed.
5. Other Configuration Settings: Depending on your requirements, you may want to adjust other settings such as permissions, layout, visibility of panes, and event handling. 6. These adjustments can be made directly within the code as needed.




