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

1. <!DOCTYPE html>: This tells the browser that the document is an HTML5 document.

2. <html lang="en">: This starts the HTML document and specifies that the primary language used is English.

3. <head>...</head>: This section contains metadata about the document, like character encoding and viewport settings. It also includes the title of the webpage.

4. <meta charset="UTF-8">: This specifies the character encoding of the document to be UTF-8, which supports a wide range of characters.

5. <meta name="viewport" content="width=device-width, initial-scale=1.0">: This sets the viewport width to the width of the device and sets the initial zoom level to 1.0, ensuring proper scaling on mobile devices.

6. <title>Power BI Embedded Example</title>: This sets the title of the webpage displayed in the browser tab.

7. <script src="..."></script>: These lines include JavaScript libraries needed for embedding Power BI content. You may need to replace the URLs with the actual URLs of the JavaScript libraries you're using.

8. <body>...</body>: This section contains the content of the webpage that users see. In this example, it includes a container with the ID "embedContainer" where the Power BI content will be embedded, and a script tag to include the application logic from an external JavaScript file (app.js).

**To customize this code for your application, you'll typically replace the following features:**

- Replace the <title> tag content with your desired webpage title.
- Replace the <script> tags' src attribute URLs with the URLs of the JavaScript libraries you're using for Power BI embedding.
- Customize the content within the <body> tag according to your application's needs, and replace "embedContainer" with the ID of the container where you want to embed the Power BI content.
