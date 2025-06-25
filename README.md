## 📊 Finance KPI Dashboard (Power BI)

This project showcases how raw financial data can be transformed into insightful, interactive visuals using Power BI.
Built with **2 fact tables** (`Actual` and `Targets`) and **2 dimension tables** (`dimPeople` and `Calendar`), 
the dashboard highlights performance against targets : month over month, category wise performance and as per team members.

---

![Finance KPI Dashboard](https://github.com/user-attachments/assets/77099a1e-5ede-4528-abc4-6e56d9a2a06f)


### Steps Involved

1. **Data Prep** – Connected and cleaned the data using *Power Query* (yes, including that sweet unpivot magic).
2. **Data Modeling** – Created a semantic model with clear relationships between tables (hello, star schema with multiple fact tables ✨).
3. **DAX Measures** – Built smart calculations using DAX, like YTDs, variances, and even dynamic titles and emoji indicators.
4. **Dashboard Design** – Designed an interactive KPI dashboard with new card visuals, custom labels, sparklines, and filter-friendly visuals.

---

![Finance Data Model](https://github.com/user-attachments/assets/d459d816-5082-4b06-b709-0fd169720bd1)



#### What I practiced

- How to unpivot like a pro in Power Query  
- Modeling multiple fact tables effectively  
- Writing DAX for YTD, % Variance, and KPI measures  
- Using DAX for dynamic titles & emoji indicators (`🟢` for positive trend, `🔴`for negative trend)  
- FILTER function in action 
- Custom data labels on line/column charts  
- Adding mini *Sparklines* in table visuals for instant trends  

---



![DAX measures for Analysis](https://github.com/user-attachments/assets/4425d3ad-f5fe-49c7-8fe4-e62d62fd0754)


## 🧠 Sample DAX Logic

```DAX
Total Sales Actual = SUM(Actual[Sales])
Total Sales Target = SUM(Targets[Sales])
Variance = [Total Sales Actual] - [Total Sales Target]
Variance % = DIVIDE([Variance], [Total Sales Target])

```

```dax
Months Target Reached = 
    VAR months_with_target_reached = FILTER(ALL('Calendar'), [Variance] > 0)
    RETURN COUNTROWS(months_with_target_reached)

Trend Chart Title = 
    VAR month_count = COUNTROWS('Calendar')
    RETURN "We met targets for " & [Months Target Reached] & " out of " & month_count & " months"
```

```dax
Variance Pct Label = 
    VAR up = "🟢"
    VAR down = "🔴"
    VAR formatted_var_pct = FORMAT(ABS([Variance %]), "0.0%")
    RETURN formatted_var_pct & " " & IF([Variance %] > 0, up, down)
```
