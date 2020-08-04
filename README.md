# Product Comparison

VTEX Product Comparison app is responsible for collecting products (with selected SKU) and give comparison view to compare features and specifications of the product, so user can get better understanding about their needs.

The app therefore exports few store blocks expected to configure full functionality, such as `sku selector`, `comparison drawer` and `comparison list` views.

![Comparison drawer](https://user-images.githubusercontent.com/2637457/89266842-0a805180-d654-11ea-9a80-d34cc9f91c1b.PNG)
![Comparison page](https://user-images.githubusercontent.com/2637457/89266856-0f450580-d654-11ea-998d-bcd7c46378fa.PNG)

# Features and Blocks
This application has few blocks that we can use to configure full feature.

Block | Description
------------ | -------------
`comparison-context-wrapper` | This block contains `product comparison context` which will hold comparison item information
`product-comparison` | This is the main component of comparison page which wraps `comparison-context-wrapper` 
`product-comparison-block` | This is the generic child component which will extend to develop other feature blocks
`product-comparison-block.selector` | This is the product selector checkbox which we can use inside product summary
`product-comparison-block.drawer` | This is product comparison bucket which is placed bottom of the page
`product-comparison-block.list` | This is product comparison page content, this block allows `product-summary` block and `product-comparison-block`
`product-comparison-block.grid` | This is comparison comparison fields as grid (you will be able to show and hide fields)

# Configuration

### 1. Add `Product Comparison` app to store theme

```
"dependencies": {
  ...
  "vtex.product-comparison": "0.x"
  ...
}
```

### 2. Extend required interfaces to add new functionality

Add product comparison to search results page we need to do some configurations on existing blocks in `store-theme` applications. Therefore we need to extend few exising interfaces.

  * #### Interfaces needds to extend
    We need to extend `store.search`,  `product-summary.shelf` and `search-result-layout.desktop` blocks in `store-theme`
    
      1. Add `interfaces.json` file if not exist in `store-theme`
      2. Add this configurations inside `interfaces.json`
       
         ```
          "store.search.product-comparison": {
            "around": ["comparison-context-wrapper"]
          },
          "product-summary.shelf.product-comparison": {
            "allowed": ["product-comparison-block"]
          },
          "search-result-layout.desktop.product-comparison": {
            "allowed": ["product-comparison-block"]
          }
          ```
  * #### Replace old blocks with new extended blocks
    Replace all the places we have used old blocks with new extended blocks like below.

  1. Replace `store.search`
    
        ```diff
        {
          ...
        - "store.search": {
        + "store.search.product-comparison": {
            ...
          },
        - "store.search#brand": {
        + "store.search.product-comparison#brand": {
            ...
          },
        - "store.search#department": {
        + "store.search.product-comparison#department": {
            ...
          }
          ...
          etc.
        ```
      
   2. Continue same thing with other tow blocks (`product-summary.shelf` and `search-result-layout.desktop`)
    

### 3. Add product comparison selector and comparison drawer to search result page

  1. Add comparison drawer
    `product-comparison-block.drawer` block needs to be added inside extended `search-result-layout.desktop.product-comparison` to display comparison drawer
    
      ```diff
        "search-result-layout.desktop.product-comparison#search": {
          "children": [
            "flex-layout.row#searchbread",
            "flex-layout.row#searchtitle",
            "flex-layout.row#result"
      +     "product-comparison-block.drawer"
          ],
          ...
        },
      ```
  2. Add product selector checkbox
  3. Add product comparison page
  
