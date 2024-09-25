# Introduction 
Survey of BMI and physical activity

<p>Surveys are given to a carefully selected sample of people with the goal of generalizing the results to a much larger population.</p>

<p>The National Health and Nutrition Examination Survey (NHANES) data is a complex survey of tens of thousands of people designed to assess the health and nutritional status of adults and children in the United States. The NHANES data includes many measurements related to overall health, physical activity, diet, psychological health, socioeconomic factors and more.</p>

<p>Depending on the sampling design, each person has a sampling weight that quantifies how many people in the larger population their data is meant to represent. In this notebook, survey methods that use sampling weights are applied to estimate and model relationships between measurements.</p>

# Analysis 
NHANES data is available as a library in R. This analysis focuses on a common health indicator, Body Mass Index (BMI kg/m<sup>2</sup>), and how it relates to physical activity. The data will be visualized and survey-weighted regression will be used to test for associations.The alaysis can be found here [Analysis](notebook_final.ipynb).

# Conclusion
<p>A linear regression model was fitted where the association of physical activity with BMI could vary by smoking status. The interaction between physical activity and smoking has a small p-value, suggesting that the association does indeed vary by smoking status. The difference between physically active and non-physically active individuals is larger in magnitude among the non-smoker population.</p>
