# Customer Service Dashboard  

## Overview  
This Power BI dashboard provides a comprehensive analysis of **Customer Service performance**, transforming complex data into actionable insights. It includes metrics for **response requests, resolution time, and customer interactions**, helping improve efficiency and service quality.  

## Data Disclaimer

All data used in this dashboard is entirely fictitious and was created for training and demonstration purposes only. No real customer, financial, or operational information is represented.


## SLA Compliance
This dashboard adopts a high-performance standard by setting the SLA threshold at 3 days, in alignment with best practices in customer service. While the legal maximum response time in Brazil is 7 days (as defined by Decree No. 11.034/2022), this dashboard goes further by applying a more rigorous benchmark.

All service requests were resolved within this 3-day window, resulting in a 100% SLA compliance rate. This not only demonstrates operational consistency but also reinforces the team's commitment to delivering fast and reliable support.

### SLA Compliance: 100% “All service requests were resolved within 3 days, demonstrating consistent SLA compliance and operational efficiency.”

This metric is displayed prominently in the dashboard to communicate service excellence and build trust with stakeholders.

## Key Features  
- **Performance Cards:**  
  - Response Requests  
  - Average Daily Responses & Requests  
  - Average Response Time (Days & Minutes)  
- **Visual Analytics:**  
  - Column Chart: Open vs. Responded Requests (by Month)  
  - Bar Chart: **Top 5 Request Events** (with detailed tooltips)  
  - Area Chart: **Response Time Trends** (with a tooltip matrix view)  
  - Bar Chart: **Top Requests by Users**

 ## DAX Measures
Custom DAX formulas were crafted to enhance time intelligence and performance tracking:

### Request & Response Metrics

### Average Time
````
Average Time = 
AVERAGEX(
    fOcorrencias,
    fOcorrencias[Resolution Date] - fOcorrencias[Request Date]
)
````
### Total Open Requests
````
Open requests = COUNT(fOcorrencias[Request Date])
````
### Total Response Requests
````
Response Request = CALCULATE(
    COUNT(fOcorrencias[Resolution Date]),
    USERELATIONSHIP(dcalendar[Date], fOcorrencias[Resolution Date])

````
### Time Intelligence

### Average Daily Requests
````
Average Daily Requests = 
VAR vworkdays = DISTINCTCOUNT(fOcorrencias[Request Date])
RETURN DIVIDE([Open requests], vworkdays)
````
### Average Daily Responses
````
Average Daily Responses = 
VAR vworkdays = CALCULATE(
    DISTINCTCOUNT(fOcorrencias[Resolution Date]),
    USERELATIONSHIP(dcalendar[Date], fOcorrencias[Resolution Date])
)
RETURN DIVIDE([Response Request], vworkdays)
````
### Average Response Time (in Minutes)
````
Average Response Time = 
AVERAGE(fOcorrencias[Resolution Time (s)]) * 24 * 60
````
### Average Response (Formatted as mm:ss)
````
Average Response = 
VAR TotalTime = AVERAGE(fOcorrencias[Resolution Time (s)])
VAR InteireDay = INT(TotalTime)
VAR HorasRestantes = (TotalTime - InteireDay) * 24
VAR HorasInteiras = INT(HorasRestantes)
VAR MinutosRestantes = (HorasRestantes - HorasInteiras) * 60
VAR MinutosInteiros = INT(MinutosRestantes)
VAR SegundosRestantes = (MinutosRestantes - MinutosInteiros) * 60
VAR SegundosInteiros = ROUND(SegundosRestantes, 0)
RETURN FORMAT(MinutosInteiros, "00") & "m and " & FORMAT(SegundosInteiros, "00") & "s"
````
### Chart Total Response Time (as numeric mmss)
````
Chart Total Response Time = 
VAR TotalTime = AVERAGE(fOcorrencias[Resolution Time (s)])
VAR HorasRestantes = TotalTime * 24
VAR HorasInteiras = INT(HorasRestantes)
VAR MinutosRestantes = (HorasRestantes - HorasInteiras) * 60
VAR MinutosInteiros = INT(MinutosRestantes)
VAR SegundosRestantes = (MinutosRestantes - MinutosInteiros) * 60
VAR SegundosInteiros = ROUND(SegundosRestantes, 0)
RETURN VALUE(FORMAT(MinutosInteiros, "00") & FORMAT(SegundosInteiros, "00"))
````
### Response Time (Formatted as dd hh mm ss)
````
Response Time = 
VAR TotalTime = SUM(fOcorrencias[Resolution Time (s)])
VAR InteireDay = INT(TotalTime)
VAR HorasRestantes = (TotalTime - InteireDay) * 24
VAR HorasInteiras = INT(HorasRestantes)
VAR MinutosRestantes = (HorasRestantes - HorasInteiras) * 60
VAR MinutosInteiros = INT(MinutosRestantes)
VAR SegundosRestantes = (MinutosRestantes - MinutosInteiros) * 60
VAR SegundosInteiros = ROUND(SegundosRestantes, 0)
RETURN
FORMAT(InteireDay, "00") & " Day(s)       " &
FORMAT(HorasInteiras, "00") & " Hour(s)       " &
FORMAT(MinutosInteiros, "00") & " Minute(s)       " &
FORMAT(SegundosInteiros, "00") & " Second(s)"
````
## Dashboard Access  
[🔗 View the Power BI Dashboard](https://app.powerbi.com/view?r=eyJrIjoiODVmZTk2OTAtZTM1Mi00NzdhLTg3NWUtZjE4ZWYxOGJhZmI4IiwidCI6IjY1OWNlMmI4LTA3MTQtNDE5OC04YzM4LWRjOWI2MGFhYmI1NyJ9)  


## Dashboard Preview  

![Dashboard Cover](https://github.com/user-attachments/assets/467a9dc5-f9d8-4bcb-b5c7-7de71bbb54a9)  
![Dashboard Overview](https://github.com/user-attachments/assets/c3f21721-bedb-44fb-89df-8244ab635493)  
![Dashboard Operational Efficiency](https://github.com/user-attachments/assets/96eb3d86-3ade-4c78-ba67-823833dcafb3)  

## How to Use

1. Download the `.pbix` file from this repository.
2. Open it using **Power BI Desktop**.
3. The dashboard is ready to explore — no data connection updates required.


## Challenges & Optimizations  
- **Precise Time Calculations:**  
  - Developed a custom DAX formula to convert resolution time into **days, hours, minutes, and seconds** for clear tracking.  
- **Dynamic Tooltips:**  
  - Integrated additional **drill-through visuals** for deeper insights into request statuses and response trends.  

## Impact  
This dashboard enhances **data-driven decision-making** by providing detailed analytics on customer service efficiency, response trends, and request resolution timelines.  

## Connect  
Want to explore more Power BI and data analytics projects? Let’s connect and exchange ideas!  

---

Would you like any tweaks to highlight specific technical aspects or goals? 
