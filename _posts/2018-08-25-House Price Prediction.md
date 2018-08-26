---
layout: post
title: "House Price Prediction"
date: "2018-08-20 10:49:23 -0400"
---

# Introduction  
The problem involves analyzing housing prices that were sold between May 2014 and May 2015. In this post, we are going to perform two task. 1) exploratory data analysis 2) use machine learning model to predict the sale price fo the houses.


# Dataset Description and its Features  
The dataset contains 21,614 samples and 20 features. The data can be download <a href="file/data.csv">here</a>.
### feature table

**Code** | **Name**  
ID | Notation for a house  
Date | Date house was sold  
Price | House price (target variable)  
Bedrooms | Number of bedrooms  
Bathrooms | Number of bathrooms
Sqft_Living | Square footage of the home  
Sqft_Lot | Square footage of the lot  
Floors | Total floors (levels) in house  
Waterfront | House which has a view to a waterfront  
View | Has been viewed  
Condition | How good the condition is overall  
Grade | Overall grade given to the housing unit  
Sqft_Above | Square footage of the house apart  from basement  
Sqft_Basement | Square footage of the basement  
Yr_Built | Built Year
Yr_Renovated | Year when house was renovated  
Zipcode | zip  
Lat | Latitude coordinate  
Long | Longitude coordinate  
Sqft_Living15 | Living room area in 2015 (implies some renovations).  This might or might have affected the lotsize area 21)
Sqft_lot15 | Lot size area in 2015 (implies some renovations)


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

A detailed script is over <a href="https://wesleytao.github.io/OneConnect/">here</a>

### Loss Function
Mean squared error: easy to train the model
Considering the logarithm for y value, the metric would be mean sqaured log error  
### Metric
CV error for parameter tunning
test error for model comparison and report

### Rationale for model selection
Although some features exhibit **a linear relationship** with our target value, the best model for this problem set would be a **tree-based model**. The tree-base model would exploit the full **combination** of these variables and give the state-of-the-art prediction accuracy.  
Features might have an **interaction effect**, and this could be difficult for linear models to find out. A Stepwise Forward Selection Process with all the possible interaction variables and higher-order terms might work but not efficient and seems too arbitrary.

**Basemodel**   
Linear Model Elastic-Net (L1 and L2 penalty both included)
During the training process, the model with higher penalty yeild lower score.
The model with small penalty fails to converge and it means all the variables are linear related to the target and they don't have much collinearity.(further test needed)

**FinalModel**  
Fine-tuned Light gradient Boosting model, this algorithm is currently the best model

## Results and Interpretation
<table>
  <thead>
    <tr>
      <th>Model</th>
      <th>CV Error</th>
      <th>Test error</th>
      <th>Training Time + Test Time</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>ElasticNet</td>
      <td>0.0678</td>
      <td>0.06947</td>
      <td>2.02s + 0.015s</td>
    </tr>
    <tr>
      <td>RandomForest</td>
      <td>0.03557</td>
      <td>0.03653</td>
      <td>1.3763s+ 0.028s</td>
    </tr>

    <tr>
      <td>LightGBM</td>
      <td>0.02628</td>
      <td>0.02666</td>
      <td>0.0525s+0.0638s</td>
    </tr>

  </tbody>
</table>

### Important features Ranking
1. Location  ( represented as zip code latitude and longituted)
2. Area   (Sqft_Lot, Sqft_Above)
3. Grade & Condition & Renovation
4. Seasonality (seasonl sale)
5. Floor plan and Design (eg 2b3b 2 floor)
6. View
7. Waterfront

<img src="https://wesleytao.github.io/blog/figs/feature_importance.png" alt="img">
