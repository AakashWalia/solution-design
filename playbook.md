# Purpose Of The Playbook

The purpose of this is to:
- Provide instructions to configure Adobe Launch if you are onboarding a new product.
- Provide information on how to configure rules, extensions, and data elements in Adobe Launch.
- Provide step-by-step instructions on how to track new events.

## Adobe Launch Configuration

### Creating an Adobe Launch Property
A property is a container house with extensions, rules, data elements, and libraries as you deploy tags to your site. A property can be any grouping of one or more domains and subdomains. You can manage and track these assets similarly.

Follow the steps below to see how you can set up a new Launch property.

1. Go to the Data Collection from your home screen of Adobe Experience Cloud. You should now see the Tags Properties screen.
(./pics/Screenshot 2024-10-17 at 11.22.51 AM.png)
3. To create a property, click the New Property button.
4. Name your property (e.g., TAL New Website).
5. As the domain, enter `tal.com.au` since this is the domain where the tal site is hosted. Although the “Domain” field is required, the tag property will work on any domain where it’s implemented. The main purpose of this field is to pre-populate menu options in the Rule builder.
6. Click the Save button.

**Note**: This is a one-time step. If you already have a property setup, you don't need to set up a new property. However, if you are onboarding a new product with a different domain, it is recommended to create a separate property.

### Implement asynchronous embed code

The embed code is a `<script>` tag that you put on your webpages to load and execute the logic you build in tags. If you load the library asynchronously, the browser continues to load the page, retrieves the tag library, and executes it in parallel. In this case, there is only one embed code, which you put in the `<head>`.

1. From the property Overview screen, click Environments in the left navigation to go to the environments page. Note that Development, Staging, and Production environments have been pre-created for you. In the Development row, click the Install icon to open the modal.
2. Note that tags will default to the asynchronous embed codes.
3. Click the Copy icon to copy the embed code to your clipboard.
4. Click Close to close the modal.

- Copy the code to be pasted in the head tag.
- Implement the embed code in the `<head>` of the HTML Page.
- The copied script must be implemented on all pages in the development environment. The script must be embedded in the `<head>` tag of all pages. Repeat the same process for the Staging environment and Production environment.

### Adobe Launch Script Q&A

Open the developer console and navigate to the “Console” tab.

- Type the command, `_satellite.property.name` and if the script has been implemented correctly then this command should return ‘TAL New Website’ as the value. Please refer to an example screenshot below.

After the Launch script has been validated, your Launch property is ready and you can start creating rules, data elements, extensions, and libraries. Before you start implementing rules in Launch, it is suggested to set up report suites in Adobe Analytics.

**Note**: When you are adding new steps of the form or adding a new page, you need to follow the steps in this section and add the embedded code in the `<head>` tag of the new page.

In the next section, we will go through configuring extensions, creating eVars, elements and rules.

## Extensions

An extension is essentially an add-on that provides extra features or functionalities to an existing program. Think of it like adding new tools to your toolbox. Extensions unlock a whole new level of tracking capabilities, data elements, and event actions.

### Finding extensions:

- **Installed**: See all the extensions currently active in your Launch toolbox.
- **Catalogue**: Explore a library of additional extensions you can add to expand your toolbox.
- **Updates**: Check for improvements or bug fixes for your existing extensions.

### Adding and configuring extensions:

- **Browse the catalogue**: Find the extension that fits your needs, like one for reading dataLayer pushes or integrating with a specific marketing platform.
- **Activate and configure**: Simply add the chosen extension to your Launch toolbox and adjust its settings if needed (not all extensions require configuration).

#### Example:

We are using a dataLayer Manager extension that reads the dataLayer pushes that we have implemented on the website.
- **Configuration**: The extension is easy to configure and requires a dataLayer object be named so it can read the specific object on the website.
- **Use**: After configuration, the extension can be used in rules to trigger specific actions.
  - Click on Add Rule > Click on Add on events.
  - Choose the dataLayer extension.
  - Select Event Type as dataLayer push and give the appropriate event type name to the rules corresponding to your dataLayer push.
  - Save the rule. Your rule will now trigger actions whenever there is a **'interaction'** dataLayer object on the website.

#### Remember:

- Changes only take effect after you publish them.
- Adobe provides some core extensions, but there are many more from other vendors available in the catalogue.
- You can even build custom extensions with the Core extension as a starting point, giving you control over your tracking setup.

### Steps to create eVars and Events

1. Click Analytics > Admin > Report Suites.
2. Select the report suite for which you want to create an eVar or event and click on edit settings.
3. Select Conversion Variables if you want to create eVars or Success Events if you want to create events.

## Rules/Tags Configuration

### Rules Definition And Structure

Adobe Launch uses rules to control when and how tags (marketing pixels, tracking scripts) fire on your website or app. These rules act like conditional statements, determining which tags are deployed based on specific criteria.

#### Structure of a Launch Rule:

- **Events (If)**: This defines the trigger for the rule. It can be one or more events (user actions like page loads or clicks) or data elements (dynamic values extracted from your site). You can also specify exceptions (conditions that prevent the rule from firing).
- **Actions (Then)**: This defines what happens when the event(s) in the "If" section occur. This typically involves firing one or more tags configured within Launch.

#### Example:

Imagine tracking form completions for TAL users. You'd set up a rule with these conditions:
- **Event**: Form completion
- **Data Elements**: Gender, Page Name, Email, Click Text

If all these conditions are met, the rule would trigger the firing of the relevant form completion tracking tag.

#### Key Points:

- Multiple events within a rule are joined by OR (any event triggers the rule).
- Multiple conditions within a rule are joined by AND (all conditions must be met).
- Rules can have an order assigned, controlling the execution sequence for rules sharing an event.
- Rule components (events, conditions, actions) can be processed sequentially or in parallel depending on a property setting.

## Data Elements

A data element is a variable that stores a specific piece of information from your website. You can use data elements throughout your rules to build a dictionary of commonly used data. This dictionary makes your tracking more efficient because you define the data once and use it everywhere. All the parameters/variables from your Analytics SDR tab will have corresponding data elements.

### Benefits of Data Elements:

- **Organisation**: Group all your website data in one place for easy reference.
- **Efficiency**: Define data once and use it in multiple rules, saving time and effort.
- **Flexibility**: Easily update data sources without modifying multiple rules.

### Examples of Data Elements:

- **Gender**: Captures the gender the user inputted in the form.
- **Page Name**: Extract the name of the current page from the URL.
- **Email**: Captures emails of the users.
- **Click Text**: Tracks the name of the button click so you can report on a specific button.

### How to Create a Data Element:

1. Go to the "Data Elements" tab in your Launch property.
2. Click "Create New Data Element."
3. Give it a clear name (e.g., "Email").
4. Choose the extension that provides the data (e.g., dataLayer manager).
5. Select the specific data type (e.g., "Context Aware").
6. Configure the data source (e.g., specify the dataLayer path. Make sure it matches the name of the parameter in your dataLayer object).
7. Save the data element.

### Using Data Elements in Rules:

Once you have data elements, you can use them in your tracking rules in set variables:
- **Example**: Create a rule to track form completions.
- Use another data element for "Asset Type" to identify what asset the users submitted the form for.

#### Key Points:

- Data elements are crucial for organising and using website data in Launch.
- They improve efficiency and flexibility in your tracking setup.
- Different extensions may provide different data element types.

By using data elements effectively, you can build a more organised and efficient tracking system for your website.

# Step-by-Step Guide: Creating Rules for Form Complete

## 1. Configure Data Elements

- **Email**:
  - Go to **Data Elements** in Adobe Launch.
  - Click **Create New Data Element**.
  - Name it `DLM - Email`.
  - Choose the **dataLayer Manager** extension.
  - Set the data element path to the email field in your dataLayer **user.email** .
  - Save the data element.

- **Gender**:
  - Repeat the above steps, naming it `Gender` and setting the correct path **form.gender**.

- **Page Name**:
  - Repeat the above steps, naming it `Page Name` and setting the correct path **pageInfo.pageName**.

- **Click Text**:
  - Repeat the above steps, naming it `Click Text` and setting the correct path **clickText**.

## 2. Create the Rule

- Go to **Rules** in Adobe Launch.
- Click **Create New Rule**.
- Name the rule `Form Complete`.

## 3. Set the Trigger

- Click **Add Event**.
- Select the **dataLayer Manager** extension.
- Choose **Event Type** as `dataLayer Push`.
- Set the **Event Name** to `interaction`.
- Save the event.

## 4. Set the condition

- Add a condition to ensure the rule only fires when (for example)`Form Name` is `quote`:
  - Go to **Conditions** in the rule setup.
  - Click **Add Condition**.
  - Select **Core** as the extension.
  - Choose **Value Comparison**.
  - Set the **Value** to `Form Name` (the data element you created).
  - Choose **Equals** as the operator.
  - Set the comparison value to `quote`.

## 5. Configure Actions

- Click **Add Action**.
- Select **Adobe Analytics** as the extension.
- Choose **Set Variables**.

- **Map eVars**:
  - Map `Email` to the corresponding eVar (check this in your report suite).
  - Map `Gender` to the corresponding eVar (check this in your report suite).
  - Map `Page Name` to the corresponding eVar (check this in your report suite).
  - Map `Click Text` to the corresponding eVar (check this in your report suite).
  - Map `event` to the corresponding event number (check this in your report suite).

- Click **Add Action**.
- Select **Adobe Analytics** as the extension.
- Choose **Send Beacon** and give the event a name.

- Click **Add Action**.
- Select **Adobe Analytics** as the extension.
- Choose **Clear Variables*

- Click **Keep Changes**.

- Build and deploy the library to the development environment.
- Test using the browser console and debugging tools like Omnibug to ensure the rule fires correctly.
