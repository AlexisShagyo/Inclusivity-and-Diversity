# 🕵️‍♀️Project Overview

Companies need a workforce of diverse talents and backgrounds to succeed in an increasingly complex and heterogeneous world. Diversity and inclusion are business imperatives, not just nice-to-haves.

## Task

- Define relevant KPIs in hiring, promotion, performance and turnover, and create a visualisation
- Write what you think some root causes of their slow progress might be

## Methods
In order to answer these questions, I made DAX measures to summarize the data that is needed for the visual presentation. This is the list of measures that were done: 

***1. Calculating the Percentage of Females promoted***
```sql
% of Promoted Female = 
    VAR TotalFemales = COUNTROWS(FILTER('Pharma Group AG', 'Pharma Group AG'[Gender] = "Female"))
    VAR PromotedFemales = COUNTROWS(FILTER('Pharma Group AG', 'Pharma Group AG'[Gender] = "Female" && 'Pharma Group AG'[Promotion in FY21?] = "Yes"))
    RETURN 
        DIVIDE(PromotedFemales, TotalFemales, 0) * 100
```

***2. Calculating the Percentage of Males promoted***
```sql
% of Promoted Male = 
    VAR TotalMales = COUNTROWS(FILTER('Pharma Group AG', 'Pharma Group AG'[Gender] = "Male"))
    VAR PromotedMales = COUNTROWS(FILTER('Pharma Group AG', 'Pharma Group AG'[Gender] = "Male" && 'Pharma Group AG'[Promotion in FY21?] = "Yes"))
    RETURN 
        DIVIDE(PromotedMales, TotalMales, 0) * 100
```

***3. Average Performance Rating for Female***
```sql
Avg Rating for Female = 
    CALCULATE(
        AVERAGE('Pharma Group AG'[FY20 Performance Rating]), 
        'Pharma Group AG'[Gender] = "Female"
    )
```

***4. Average Performance Rating for Male***
```sql
Avg Rating for Male = 
    CALCULATE(
        AVERAGE('Pharma Group AG'[FY20 Performance Rating]), 
        'Pharma Group AG'[Gender] = "Male"
    )
```

***5. Calculating the In Base Group Turnover rate***
```sql
In Base Group Turnover = 
    VAR TotalPeople = COUNTROWS('Pharma Group AG')
    VAR PeopleWithY = COUNTROWS(FILTER('Pharma Group AG', 'Pharma Group AG'[In base group for turnover ] = "Y"))
    RETURN 
        DIVIDE(PeopleWithY, TotalPeople, 0) * 100
```

***6. Counting how many employees left the company***
```sql
Leavers = 
    COUNTROWS(FILTER('Pharma Group AG', SEARCH("FY20", 'Pharma Group AG'[Leaver FY], 1, 0) > 0))
```

-----------------
<br>

## 📊 Visualization

<img src="https://github.com/AlexisShagyo/Images/blob/main/Inclusivity%20and%20Diversity.jpg" alt="Image" width="800" height="450">
<br>

## 📚 Insights

- Most promotions occur among employees in their early to late 30s, accounting for 17.8% of promotions.

- Males in their 20s have a higher chance of being promoted (5.83%) compared to females (1.94%).

- The performance ratings for both male and female employees are below average.

- Most employees who have left the company come from the Operations and Sales & Marketing departments. In the Sales & Marketing department, males make up 65% of the workforce, yet their performance is rated at an average of 2.30. In contrast, females, who comprise 35% of the department, have a higher performance rating of 2.49. Despite this, 16% of males receive promotions, while only 3% of females are promoted.
