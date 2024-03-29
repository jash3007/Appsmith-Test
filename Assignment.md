Building a Product Catalog Manager
Description (optional)

>  ⭐ Level - Beginner  
> ⏱️ Time - 15 minutes

This tutorial guides you through creating a basic product catalog manager on Appsmith. The application connects to a sample API allowing you to read and update product information. You'll learn to:

- Create a new application
- Connect to an API and fetch data
- Display the data in a Table widget
- Build a form in a modal to view product details
- Edit and submit the product details
- Deploy the application

Here's a screenshot of the final result:

![Final View of Product Catalog Manager](https://github.com/jash3007/Appsmith-Test/assets/136789365/56fc947e-27f4-49ce-ba23-3294c8382e7f)
*Final view of Product Catalog Manager*


Let's get started!

# Prerequisites​

You need to have an Appsmith account to get started. Sign up on Appsmith cloud if you don’t have one.

# Create a new application​

1. When you create a new account, Appsmith adds a workspace with an application titled **My first application** on the homepage by default. You need to create a new application for this tutorial. If you are inside an application and need to go to the homepage, click on the Appsmith logo at the top left of the screen to go to the homepage.
2. On the homepage, click the **+ New** button to the right of the screen under the default workspace. You'll land on a new application in the Edit mode.

<img width="1279" class ="center" alt="Product Catalog management" src="https://github.com/jash3007/Appsmith-Test/assets/136789365/b9cb695a-296a-4d58-a98b-47db57f98176">

_Create a new application_

3. Click the ⌵ icon on the top left next to the default application name. Select the Edit Name option. Rename the app to **Product Catalog Management.**
4. On Entity Explorer to the left of the screen, you'll see that Page 1 is the default page on the application. Hover over the page name and click the ︙ icon.
5. Select the **Edit Name** option. Rename the page to Product Information.

<img width="496" class ="center" alt="Edit page name" src="https://github.com/jash3007/Appsmith-Test/assets/136789365/d07a0853-a570-4ab7-9b02-a5147489c55b">

_Edit Page Name_

# Fetch product data


> 📘 Note
> 
> We will use APIs to fetch and update product details in this example. Using Appsmith’s plug-and-play support for many databases, you can also connect to the database of your choice. [Learn more](https://docs.appsmith.com/core-concepts/connecting-to-data-sources)

1. From the Explorer on the left, click the **+** button adjacent to Queries/JS.

<img width="655" alt="Add product api" src="https://github.com/jash3007/Appsmith-Test/assets/136789365/ad49b7d0-cb6c-4f87-9cbc-badc8cc36d3d">

_Creating a new blank API_

2. Select **New blank API.**
3. Next, click the pencil icon next to the default API name on the top left and rename the API to **getProducts.**
4. Select the **HTTP** method as **GET** and enter the API endpoint to fetch the product details.

<img width="1274"  alt="API response" src="https://github.com/jash3007/Appsmith-Test/assets/136789365/131faac0-cb3f-4912-a063-d49a1b09b828">

_Configure API Endpoint to Fetch Product Details_

> 📘 Note 
>
> At this stage, we are explicitly defining the page number in the endpoint, as we have not created a table yet. After creating a table, you need to update the variable in the endpoint.

5. Click on the **Run** button to test the API response. Ensure that you receive the 200 OK response.
6. Navigate to **Settings** and toggle on "Run API on Page load," "Encode query params," and "Smart JSON substitution."

<img width="753" alt="API settings" src="https://github.com/jash3007/Appsmith-Test/assets/136789365/57e05e7c-1f38-4e9d-8fc5-f6c0dfbf5bb4">

_API Settings_


# Display product data on a table

1. Click the **Widgets** tab on the Entity Explorer to the left of the screen.
2. Drag a **Table** widget and drop it to the left of the canvas.
3. A _Property Pane_ appears to the right of the screen containing all the widget properties. On the top of the property pane, click the default name Table1 and rename it to `productTable`.
4. To display the data from the getProducts API, type in the mustache template `{{ }}`. Enter `getProducts.data.products` between the curly braces. This JavaScript expression connects the data from the getProducts API to the Table widget.

<img width="1266" alt="bind api data" src="https://github.com/jash3007/Appsmith-Test/assets/136789365/e1970c86-5c7d-447c-9422-c6d508b65857">

_Bind data from API in Table_


5. Configure the pagination by navigating to the properties of the table widget.
6. Click the **+** button next to **onPageChange** > Select** Execute a query getProducts.run** > **getProducts.run**. Also, toggle on the server-side pagination. This helps fetch product data for the previous and next pages. As mentioned earlier, ensure that you update the variable in the API to enable pagination. Learn more about [Pagination](https://docs.appsmith.com/core-concepts/connecting-to-data-sources/authentication/connect-to-apis#pagination).
7. For column representing images, ensure you set the column type as Image from the image column settings in the property pane (Refer to the gif below).

![Image data type (1)](https://github.com/jash3007/Appsmith-Test/assets/136789365/d2b35c81-445b-4da1-a941-9538f533a0f5)

_Set Image Column type_

8. Similarly, for the Edit column, ensure that you set the column type as **Button** from the column settings in the property pane for the Edit column.

You can re-arrange the columns from the table property panel as per your required sequence. You can also set the visibility for each column.

# Build a modal with form to view and update product details​

To edit the product details, we need a combination of Modal and Form that allows updating product details. Refer to the image below for a better understanding:

<img width="518" alt="Editable modal" src="https://github.com/jash3007/Appsmith-Test/assets/136789365/e77bc2ec-633c-439d-a3cb-74d6cba1d8f9">

_Sample Modal with Form_

To create this, follow the steps below:

1. From the **Widgets** tab, drag and drop a Modal widget on the canvas on top of the Table widget.
2. Select the title of the Modal. On the property pane to the right of the screen, change the title from Modal Title to Product Details in the Text property box.
3. Drag and drop a Form element within the Modal from the **Widgets** tab to view and update the product details.
4. For the product’s category, drag and drop a **Select** element from the Widgets tab inside the Form.
   - On the property pane to the right, click on the default category Select1 and rename it to `categorySelect`
   - In the Text property box, enter `Category`.
   - In the Default Value property box, type `{{productTable.triggeredRow.category}}`. This displays the product’s category for the selected row on the **productTable** Table widget.
5. Drag and drop an **Input** widget inside the Form for the product's name.
   - Rename the widget to `productName`.
   - Select **Single-line text** from the list of options in the Data Type property.
   - In the **Text** property box, enter the `Product Name`.
   - In the **Default Value** property box, type `{{productTable.triggeredRow.productName}}`.
6. For the product’s MRP, drag and drop the **currencyInput** widget in the form.
   - On the property pane to the right, click on the default name **CurrencyInput1** and rename it to `mrpInput`.
   - In the Text property box, enter `MRP`.
   - In the Default Value property box, type `{{productTable.triggeredRow.mrp}}`. This displays the product’s MRP for the selected product on the productTable Table widget.
7. Similarly, drag and drop the **currencyInput** widget again in the form for the product's **Listing price.**
   - On the property pane to the right, click on the default name **CurrencyInput2** and rename it to listingPrice.
   - In the Text property box, enter `Listing Price`.
   - In the Default Value property box, type `{{productTable.triggeredRow.listingPrice}}`. This displays the product’s Listing price for the selected product on the productTable Table widget.
8. You also need to view the product’s availability date. Drop a Datepicker widget inside the Form.
   - Rename the widget to `dateInput`.
   - In the Text property box, enter `Availability Date.`
   - Click the JS button next to the Default Date property to connect the Datepicker widget to the product’s availability date on the table.
   - Type `{{productTable.triggeredRow.availabilityDate}}` in the Default Date property box.

🚩 You've completed binding the data to the widgets on the Form within the Modal. Select the rows on the Table to view the corresponding product details on the Form.

# Update product details​

1. Select the Explorer tab on the Entity Explorer to the screen's left.
2. Click the + icon next to **Queries/JS.**
3. Select **New blank API** from the list of options
4. After the subsequent API screen displays, rename the default API name to `updateProducts`.
5. Set the HTTP method as **PUT** and enter the endpoint of the API that allows you to update the product details.
6. Under the **Body** tab, map your Form elements with respective input fields in the JSON format.

<img width="1273" alt="PUT API" src="https://github.com/jash3007/Appsmith-Test/assets/136789365/2a32b148-4558-441f-80f0-8032433c8b30">

_Configure PUT API to Update Product Details_

7. Navigate back to the form from the **Explorer** tab
8. Select the default **Submit** button on the Form to connect the updateProducts query to a button.
   - On the property pane to the right of the screen, in the Label property box, change the label to `Update`.
   - Click the + icon next to the **onClick** event.
   - In the Action list, select **Execute a query** > Select **updateProducts.run** to run the query on the button click.
   - Click Callbacks right under the action selector.
   - Click the **+** icon next to the onSuccess callback.
   - Select **Execute a query > getProducts.run**.  
     The Update button is now configured to execute the updateProducts query to save any modified product details on the Form and to refresh the Table widget with the updated information.

<img width="918" alt="Update button" src="https://github.com/jash3007/Appsmith-Test/assets/136789365/fa71f134-924f-486c-95e9-e0581c7d3d9e">

_Configure Update Button_

# Deploy the application

1. Click the **Deploy** button on the top right of the screen to deploy the application and test it in the View mode.
2. Select the first row on the Table. Go ahead and modify the product details on the Form and test the **Update** button to see how things work.

Congratulations! You have built a Product Catalog Management app that can display product data from an API and save the updated data on the Form.

In this tutorial, you explored a few widgets and created a simple product catalog manager to view, query, and update product data through APIs. You can use these skills to build your own custom app.
WHAT’S NEXT
Tell your users what they should do after they've finished this page


