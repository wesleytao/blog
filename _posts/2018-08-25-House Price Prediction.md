---
layout: post
title: "House Price Prediction"
date: "2018-08-20 10:49:23 -0400"
---

# Introduction  
The problem involves analyzing housing prices that were sold between May 2014 and May 2015. In this post, we are going to perform two task. 1) exploratory data analysis 2) use machine learning model to predict the sale price fo the houses.


# Dataset Description and its Features  
The dataset contains 21,614 samples and 20 features. The data can be download <a href="file/data.csv">here</a>.
### features
 1. ID — Notation for a house  
 2. Date — Date house was sold  
 3. Price — House price (target variable)  
 4. Bedrooms — Number of bedrooms  
 5. Bathrooms — Number of bathrooms
 6. Sqft_Living — Square footage of the home
 7. Sqft_Lot — Square footage of the lot
 8. Floors — Total floors (levels) in house
 9. Waterfront — House which has a view to a waterfront
 10. View — Has been viewed
 11. Condition — How good the condition is overall
 12. Grade — Overall grade given to the housing unit
 13. Sqft_Above — Square footage of the house apart  from basement
 14. Sqft_Basement — Square footage of the basement
 15. Yr_Built — Built Year
 16. Yr_Renovated — Year when house was renovated
 17. Zipcode — zip
 18. Lat — Latitude coordinate
 19. Long — Longitude coordinate
 20. Sqft_Living15 — Living room area in 2015 (implies some renovations).  This might or might have affected the lotsize area 21) Sqft_lot15 — Lot size area in 2015 (implies some renovations)


# Exploratory Data analysis
<!-- general overview -->
### Sales Record Location and 2018 household density

* most sales are in the **urban area**
* majority of the household are located near **the highway and the river**
* the distribution of the sales is approximately **log-normal**

<div class='tableauPlaceholder' id='viz1535230266344' style='position: relative'><noscript><a href='#'><img alt='overview ' src='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;PR&#47;PRICE_1&#47;overview&#47;1_rss.png' style='border: none' /></a></noscript><object class='tableauViz'  style='display:none;'><param name='host_url' value='https%3A%2F%2Fpublic.tableau.com%2F' /> <param name='embed_code_version' value='3' /> <param name='site_root' value='' /><param name='name' value='PRICE_1&#47;overview' /><param name='tabs' value='no' /><param name='toolbar' value='yes' /><param name='static_image' value='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;PR&#47;PRICE_1&#47;overview&#47;1.png' /> <param name='animate_transition' value='yes' /><param name='display_static_image' value='yes' /><param name='display_spinner' value='yes' /><param name='display_overlay' value='yes' /><param name='display_count' value='yes' /><param name='filter' value='publish=yes' /></object></div>                
 <script type='text/javascript'>                    
 var divElement = document.getElementById('viz1535230266344');                   
  var vizElement = divElement.getElementsByTagName('object')[0];                    vizElement.style.width='800px';vizElement.style.height='627px';                    var scriptElement = document.createElement('script');                    scriptElement.src = 'https://public.tableau.com/javascripts/api/viz_v1.js';                    vizElement.parentNode.insertBefore(scriptElement, vizElement);                </script>


### Price and Location
* Rich people live in the suburban area (zip code 98039)
* Center of the city is very expansive (zip code 98119)


<!-- price and location -->
<div class='tableauPlaceholder' id='viz1535229821044' style='position: relative'><noscript><a href='#'><img alt='Price ' src='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;PR&#47;PRICE_0&#47;Price&#47;1_rss.png' style='border: none' /></a></noscript><object class='tableauViz'  style='display:none;'><param name='host_url' value='https%3A%2F%2Fpublic.tableau.com%2F' /> <param name='embed_code_version' value='3' /> <param name='site_root' value='' /><param name='name' value='PRICE_0&#47;Price' /><param name='tabs' value='no' /><param name='toolbar' value='yes' /><param name='static_image' value='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;PR&#47;PRICE_0&#47;Price&#47;1.png' /> <param name='animate_transition' value='yes' /><param name='display_static_image' value='yes' /><param name='display_spinner' value='yes' /><param name='display_overlay' value='yes' /><param name='display_count' value='yes' /><param name='filter' value='publish=yes' /></object></div>                
 <script type='text/javascript'>                    var divElement = document.getElementById('viz1535229821044');                    var vizElement = divElement.getElementsByTagName('object')[0];                    vizElement.style.width='800px';vizElement.style.height='627px';                    var scriptElement = document.createElement('script');                    scriptElement.src = 'https://public.tableau.com/javascripts/api/viz_v1.js';                    vizElement.parentNode.insertBefore(scriptElement, vizElement);                </script>


### Seasonality
* Real estate industry has seasonaly trend, price and sales flucturate througout the year
* Winter is the low season, summer is hot season
* both volumns and price has significant increase at spring


<!-- season -->
<div class='tableauPlaceholder' id='viz1535229948502' style='position: relative'><noscript><a href='#'><img alt='Season ' src='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;PR&#47;PRICE_1&#47;Season&#47;1_rss.png' style='border: none' /></a></noscript><object class='tableauViz'  style='display:none;'><param name='host_url' value='https%3A%2F%2Fpublic.tableau.com%2F' /> <param name='embed_code_version' value='3' /> <param name='site_root' value='' /><param name='name' value='PRICE_1&#47;Season' /><param name='tabs' value='no' /><param name='toolbar' value='yes' /><param name='static_image' value='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;PR&#47;PRICE_1&#47;Season&#47;1.png' /> <param name='animate_transition' value='yes' /><param name='display_static_image' value='yes' /><param name='display_spinner' value='yes' /><param name='display_overlay' value='yes' /><param name='display_count' value='yes' /><param name='filter' value='publish=yes' /></object></div>                
 <script type='text/javascript'>                    var divElement = document.getElementById('viz1535229948502');                    var vizElement = divElement.getElementsByTagName('object')[0];                    vizElement.style.width='800px';vizElement.style.height='627px';                    var scriptElement = document.createElement('script');                    scriptElement.src = 'https://public.tableau.com/javascripts/api/viz_v1.js';                    vizElement.parentNode.insertBefore(scriptElement, vizElement);                </script>


### Structure of the house and floor plan
* the unit price of household with basement is statistically higher than those without basement
* the unit price of household with **waterfront** view is statistically higher than
those without waterfront view
* ill-designed house(those has lower ratio of #bath/#bed) is cheaper


<!-- floor plan -->
<div class='tableauPlaceholder' id='viz1535230093876' style='position: relative'><noscript><a href='#'><img alt='Floor plan ' src='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;PR&#47;PRICE_1&#47;Floorplan&#47;1_rss.png' style='border: none' /></a></noscript><object class='tableauViz'  style='display:none;'><param name='host_url' value='https%3A%2F%2Fpublic.tableau.com%2F' /> <param name='embed_code_version' value='3' /> <param name='site_root' value='' /><param name='name' value='PRICE_1&#47;Floorplan' /><param name='tabs' value='no' /><param name='toolbar' value='yes' /><param name='static_image' value='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;PR&#47;PRICE_1&#47;Floorplan&#47;1.png' /> <param name='animate_transition' value='yes' /><param name='display_static_image' value='yes' /><param name='display_spinner' value='yes' /><param name='display_overlay' value='yes' /><param name='display_count' value='yes' /><param name='filter' value='publish=yes' /></object></div>                
 <script type='text/javascript'>                    var divElement = document.getElementById('viz1535230093876');                    var vizElement = divElement.getElementsByTagName('object')[0];                    vizElement.style.width='1000px';vizElement.style.height='827px';                    var scriptElement = document.createElement('script');                    scriptElement.src = 'https://public.tableau.com/javascripts/api/viz_v1.js';                    vizElement.parentNode.insertBefore(scriptElement, vizElement);                </script>

### Customer View and House
* People hesitate when location is not ideal like island(zipcode 98070) or far away from the city(zip code 98022 98117), they would double check the house
* When the price is above 1 Million, people pay more visits before purchase


<!-- double check -->
<div class='tableauPlaceholder' id='viz1535230170177' style='position: relative'><noscript><a href='#'><img alt='Dashboard 5 ' src='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;PR&#47;PRICE_1&#47;Dashboard5&#47;1_rss.png' style='border: none' /></a></noscript><object class='tableauViz'  style='display:none;'><param name='host_url' value='https%3A%2F%2Fpublic.tableau.com%2F' /> <param name='embed_code_version' value='3' /> <param name='site_root' value='' /><param name='name' value='PRICE_1&#47;Dashboard5' /><param name='tabs' value='no' /><param name='toolbar' value='yes' /><param name='static_image' value='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;PR&#47;PRICE_1&#47;Dashboard5&#47;1.png' /> <param name='animate_transition' value='yes' /><param name='display_static_image' value='yes' /><param name='display_spinner' value='yes' /><param name='display_overlay' value='yes' /><param name='display_count' value='yes' /><param name='filter' value='publish=yes' /></object></div>                
 <script type='text/javascript'>                    var divElement = document.getElementById('viz1535230170177');                    var vizElement = divElement.getElementsByTagName('object')[0];                    vizElement.style.width='800px';vizElement.style.height='627px';                    var scriptElement = document.createElement('script');                    scriptElement.src = 'https://public.tableau.com/javascripts/api/viz_v1.js';                    vizElement.parentNode.insertBefore(scriptElement, vizElement);                </script>


# Machine Learning Model

Detailed script is over <a href="https://wesleytao.github.io/OneConnect/">here</a>


# Evaluation Criteria
 We will assess how you approach in this open ended problem, your initial data analysis, why you think a certain approach is suited to solve this problem. We would want to know why you chose a particular evaluation metric, loss function etc, what is your inference from the results.
