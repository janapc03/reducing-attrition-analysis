# Reducing Attrition Analysis
## Description

Employee attrition has long been a concerns of many companies. The departure of a good employee can affect an organization in many ways, including decreased performance, increased costs, and challenges in recruiting and training new employees. If the primary reasons for employee attrition can be identified, companies can use the information to take preventative measures in order to avoid a large number of employees leaving the organization. The purpose of this analysis is to discern whether gender and the distance an employee works from home has an effect on attrition, and if such effects are different for women compared to men.

The analysis involves conducting a hypothesis test using logistic regression. All code was completed in R using JupyterNotebook.

---

## Exploratory Data Analysis

<img width="598" height="516" alt="Screenshot 2025-11-19 at 2 32 22 PM" src="https://github.com/user-attachments/assets/65649a92-4dbd-4838-af12-c0992201d9b3" />

An initial exploratory data analysis suggested that employees that work further from home seem to be more likely to depart from their organization. Additionally, for each case of attrition, the interquartile range of distances from the employee's home to work is similar for males and females. This suggests that gender does not have an effect on attrition, but further analysis is needed to investigate this relationship.

---

## Logistic Regression Model

Since the outcome variable is binary, a logistic regression model was used. The following shows the R code used to estimate the proposed model and a summary of the results:
```
# Construct response variable
mydata <- mydata %>% mutate(Attrition = ifelse(Attrition == "Yes", 1, 0))

# Estimate a binary logistic regression
my_binary_log_model <- glm(formula = Attrition ~ DistanceFromHome * Gender,
       data = mydata,
       family = "binomial")

# Obtain summary of results
tidy(my_binary_log_model) %>%  
    mutate(exp.estimate = exp(estimate)) %>% 
    mutate_if(is.numeric, round, 3)
```
Output:

<img width="582" height="191" alt="Screenshot 2025-11-19 at 2 42 03 PM" src="https://github.com/user-attachments/assets/82d5c0b7-7827-4061-9823-17711f16a492" />

---

## Findings and Suggestions

The results show that at a 5% significance level, there is sufficient evidence to suggest that distance from home and attrition are positively correlated. In contrast, there is not enough evidence to suggest that odds of attrition are associated with gender or that there is a differential effect of gonder on the relationship between home and the odds of attrition.

*Based on this analysis, hiring managers should take into consideration how far an employee candidate lives from the office.* For every unit increase in the candidate's distance from home to the workplace, the odds of attrition increase by 2.8%, thus this is a significant factor to take into consideration when hiring new employees.
