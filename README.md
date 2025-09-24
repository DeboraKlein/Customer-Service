# 📊 Customer Service Dashboard  

## 🚀 Overview  
This Power BI dashboard provides a comprehensive analysis of **Customer Service performance**, transforming complex data into actionable insights. It includes metrics for **response requests, resolution time, and customer interactions**, helping improve efficiency and service quality.  

## 🔍 Key Features  
- **Performance Cards:**  
  - Response Requests  
  - Average Daily Responses & Requests  
  - Average Response Time (Days & Minutes)  
- **Visual Analytics:**  
  - Column Chart: Open vs. Responded Requests (by Month)  
  - Bar Chart: **Top 5 Request Events** (with detailed tooltips)  
  - Area Chart: **Response Time Trends** (with a tooltip matrix view)  
  - Bar Chart: **Top Requests by Users**

 ## 📐 DAX Measures
Custom DAX formulas were crafted to enhance time intelligence and performance tracking:

### 📊 Request & Response Metrics

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
### ⏱️ Time Intelligence

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
## 🌐 Dashboard Access  
[🔗 View the Power BI Dashboard](https://app.powerbi.com/view?r=eyJrIjoiODVmZTk2OTAtZTM1Mi00NzdhLTg3NWUtZjE4ZWYxOGJhZmI4IiwidCI6IjY1OWNlMmI4LTA3MTQtNDE5OC04YzM4LWRjOWI2MGFhYmI1NyJ9)  


## 📸 Dashboard Preview  

![Dashboard Overview](https://github.com/user-attachments/assets/b2fa652b-002e-4978-92b0-382b9e07844a)  
![Tooltip 1](https://github.com/user-attachments/assets/00295448-8cf5-4f4b-ac08-ae0f8ea5e75f)  
![Tooltip 2](https://github.com/user-attachments/assets/04b911f7-fb9e-4e6c-b2c4-b8eefe9db06e)  


## 🛠️ Challenges & Optimizations  
- **Precise Time Calculations:**  
  - Developed a custom DAX formula to convert resolution time into **days, hours, minutes, and seconds** for clear tracking.  
- **Dynamic Tooltips:**  
  - Integrated additional **drill-through visuals** for deeper insights into request statuses and response trends.  

## 🎯 Impact  
This dashboard enhances **data-driven decision-making** by providing detailed analytics on customer service efficiency, response trends, and request resolution timelines.  

## 👏 Credits  
Special thanks to **Hashtag Treinamentos** for their valuable insights and learning resources!  

## 📢 Connect  
Want to explore more Power BI and data analytics projects? Let’s connect and exchange ideas!  

---

Would you like any tweaks to highlight specific technical aspects or goals? 😊
