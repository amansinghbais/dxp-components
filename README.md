# DXP Components for Vue applications

## How to use?

# Contribution Guideline

1. Fork the repository and clone it locally from the `main` branch. Before starting your work make sure it's up to date with current `main` branch.
2. Pick an issue from [here](https://github.com/hotwax/dxp-components/issues). Write in the issue comment that you want to pick it, if you can't assign yourself. **Please stay assigned to one issue at a time to not block others**.
3. Create a branch for your edits. Use the following branch naming conventions: **dxp-components/issue-number**.
4. Please add issue number to your commit message.
5. Propose a Pull Request to `main` branch containing issue number and issue title.
6. Use [Pull Request template](https://github.com/hotwax/dxp-components/blob/main/.github/PULL_REQUEST_TEMPLATE.md) (it's automatically added to each PR) and fill as much fields as possible to describe your solution.
7. Reference any relevant issues or other information in your PR.
8. Wait for review and adjust your PR according to it.
9. Congrats! Your PR should now me merged in!

If you can't handle some parts of the issue then please ask for help in the comment. If you have any problems during the implementation of some complex issue, feel free to implement just a part of it.

## Report a bug or request a feature

Always define the type of issue:
* Bug report
* Feature request

While writing issues, please be as specific as possible. All requests regarding support with implementation or application setup should be sent to.

# Join the community on Discord
If you have any questions or ideas feel free to join our <a href="https://discord.gg/SwpJnpdyg3" target="_blank">Discord channel</a>

# The license

DXP Components is completely free and released under the Apache v2.0 License. Check <a href="https://github.com/hotwax/dxp-components/blob/main/LICENSE" target="_blank">LICENSE</a> for more details.


# Components - Overview

## DxpShopifyImg
### Introduction
The 'DxpShopifyImg' component is a component providing a centralized solution for displaying Shopify images with dynamic sizing and image Url.

The component takes an defaultImageUrl from the appContext and initialize the imageUrl with it. The default image path can be used in the 'DxpShopifyImg' component if the 'src' is not provided as a prop or if the provided image URL fails to load.

### Basic Usage
To use the DxpShopifyImg component, integrate it into your Vue 3 application. Provide the image source (src) and an optional size attribute:


      <template>
        <DxpShopifyImg src="path/to/shopify-image.jpg" size="medium" />
      </template>

      <script lang="ts">
      import { DxpShopifyImg } from 'dxpComponents';
      </script>

### Props
<b>"src"</b>
<table>
  <tr>
    <th>Decription</th>
    <td>Path to the Shopfiy image.</td>
  </tr>
  <tr>
    <th>Type</th>
    <td>String</td>
  </tr>
  <tr>
    <th>Required</th>
    <td>False</td>
  </tr>
</table>
<br>

<b>"size"</b>
<table>
  <tr>
    <th>Description</th>
    <td>Desired image size.</td>
  </tr>
  <tr>
    <th>Type</th>
    <td>String</td>
  </tr>
  <tr>
    <th>Required</th>
    <td>False</td>
  </tr>
  <tr>
    <th>Example</th>
    <td>pico, small, icon, thumb, etc</td>
  </tr>
</table>

### Technical Implementation

<b>checkIfImageExists(src: string)</b>

Purpose
* This function serves the purpose of determining whether an image exists at a specified URL.

Usage
* Accepts a single parameter <b>'src'</b> (Type: string), representing the URL of the image to be checked.
* Returns a promise that resolves with <b>'True'</b> if the image exists and rejects with <b>'False'</b> if it does not.

Implementation
* Creates a new <b>Image</b> object and sets event handlers for <b>onload</b> and <b>onerror</b>.
* <b>onload</b> resolves the Promise with true when the image is successfully loaded.
* <b>onerror</b> rejects the Promise with false if there is an error loading the image.
* Sets the source URL for the image from URL given as a argument.

<br>
<b>prepareImgUrl(src: string, size?: string)</b>

Purpose
* It is function to modify the image URL based on the provided size or return the original URL if no size is specified. 

Usage
* Accepts two parameters:
  * "src": (Type - String) Original URL of the image
  * "size": (Type - String, Optional) The size of the image
* Returns as a String a modified URL of the image.

Implementation
* The function first checks if a size parameter is provided. If not, it directly returns the original image URL.
* If a size is provided, the function modifies the image URL based on the specified size. It uses regular expressions to remove any existing size information from the URL and appends the new size.

<br>
<b>setImgUrl()</b>

Purpose
* This is called once the component mounted, responsible for setting the image URL based on certain conditions.

Implementation
* If image URL is given in props as 'src', this calls the prepareImgUrl function with 'src' as a parameter to generate the modified image URL.
* Then this checks if the URL exisis using 'checkIfImageExists' function, and updates the value of imageUrl if the image is found.


## DxpProductIdentifier

### Introduction
Product Identifier typically refers to attributes or properties that uniquely identify and describe a product within a system or database. These identifiers help distinguish one product from another and provide essential information about the product.

DxpProductIdentifer component serves as a user interface for selecting primary and secondary product identifiers. The component is designed to be easily integrated into applications, offering a card-based interface with dropdowns for identifier selection.

### Basic usage
To use the DxpProductIdentifier component, integrate it into your Vue application as follows:

      <template>
        <DxpProductIdentifier />
      </template>

      <script setup lang="ts">
      import { DxpProductIdentifer } from 'dxpComponents';
      </script>

### Technical Implementation

<h4> State Management </h4>
The component relies on a Store ('userProductIdentificationStore') to manage and update the user's product identification preferences.

The following store contains two fields in state:

* <b> productIdentificationPref </b>
  * An object with 'primaryId' and 'secondaryId'
* <b> productIdentificationOptions </b>
  * An array of identification options.

The store also contains some actions and getters for getting and setting productIdentification preference.


<h4> Getters </h4>

The component uses two getters two fetch data form state in userProductIdentificationStore:
* <b> getProductIdentificationOptions: </b> This getter fetches from state an array of product identification options to be displayed in the selection dropdown.

* <b> getProductIdentificationPref: </b> This getter retrieves from state an object containing the product identification preferences from the state.

<h4> getIdentificationPref </h4>

* As soon as component is mounted, the 'getIdentificationPref' action of userProductIdentificationStore gets triggered with current EcomStoreId as a parameter.

* This action retrieves the identification preferences for current EcomStore and updates the state accordingly. If can't fetch preference for this EcomStore it sets primaryId equals 'productId' by default.


<h4> setProductIdentificationPref </h4>

This function is triggered when the selected product identifications are changed, updating the identification preferences in the state.

### Recommendation
The following DxpProductIdentifier component can be used anywhere in any app, with a condition that the app should have dxp-components installed as a dependency in app and the following functions from oms-api should be passed as a parameter at the time of initialization of dxp while creation of app.

* 'getProdcutIdentificationPref' and 'setProductIdentificationPref'