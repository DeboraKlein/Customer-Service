## 📊 Painel de Atendimento ao Cliente - SAC
### 🚀 Visão Geral
Este painel em Power BI oferece uma análise abrangente da performance do atendimento ao cliente, transformando dados complexos em insights acionáveis. Ele monitora
métricas essenciais como volume de solicitações, tempo de resolução, conformidade com SLA e interações com clientes, permitindo maior eficiência e qualidade no 
serviço.

### 🔐 Aviso sobre os Dados
Todos os dados utilizados neste painel são totalmente fictícios e foram criados exclusivamente para fins de treinamento e demonstração. Nenhuma informação real de 
clientes, finanças ou operações está representada.

### ✅ Conformidade com SLA
O painel adota um padrão de alta performance ao definir o limite de SLA em 3 dias, superando o prazo legal de 7 dias estabelecido pelo Decreto nº 11.034/2022 no 
Brasil.

Todas as solicitações foram resolvidas dentro desse prazo de 3 dias, resultando em uma taxa de conformidade com SLA de 100% — um indicador claro de consistência 
operacional e compromisso com um suporte rápido e confiável.

🟢 Conformidade com SLA: 100% “Todas as solicitações foram resolvidas em até 3 dias, demonstrando eficiência operacional e conformidade com o SLA.”

Este indicador é exibido de forma destacada no painel para reforçar a excelência do serviço e gerar confiança nos stakeholders.

### 🔍 Principais Funcionalidades
📋 Cartões de Performance
Cliente com maior número de solicitações (com gráfico de barras no tooltip mostrando os 5 principais)

Solicitações reabertas (com gráfico de barras no tooltip por tipo de evento)

Média diária de solicitações

Média diária de respostas

📊 Visualizações Analíticas
Gráfico de barras: Top 5 solicitações pendentes de resposta do cliente por evento

Gráfico de área: Solicitações abertas por dia da semana

Gráfico de área: Solicitações abertas por dia do mês

Gráfico de colunas: Solicitações abertas vs. respondidas (mensal)

Gráfico de barras: Top 5 tipos de solicitação (com tooltips detalhados)

Gráfico de área: Tendência de tempo de resposta (com matriz em tooltip)

Gráfico de barras: Solicitações por usuário

### 📐 Medidas DAX
Fórmulas DAX personalizadas foram desenvolvidas para aprimorar a inteligência temporal e o rastreamento de performance:

📊 Métricas de Solicitação e Resposta
Average Time
````
Average Time = 
AVERAGEX(
    fOcorrencias,
    fOcorrencias[Resolution Date] - fOcorrencias[Request Date]
)
````
Open requests
````
Open requests = COUNT(fOcorrencias[Request Date])
````
Response Request
````
Response Request = CALCULATE(
    COUNT(fOcorrencias[Resolution Date]),
    USERELATIONSHIP(dcalendar[Date], fOcorrencias[Resolution Date])
)
````
###⏱️ Inteligência Temporal
Average Daily Requests
````
Average Daily Requests = 
VAR vworkdays = DISTINCTCOUNT(fOcorrencias[Request Date])
RETURN DIVIDE([Open requests], vworkdays)
````
Average Daily Responses
````
Average Daily Responses = 
VAR vworkdays = CALCULATE(
    DISTINCTCOUNT(fOcorrencias[Resolution Date]),
    USERELATIONSHIP(dcalendar[Date], fOcorrencias[Resolution Date])
)
RETURN DIVIDE([Response Request], vworkdays)
````
Average Response Time
````
Average Response Time = 
AVERAGE(fOcorrencias[Resolution Time (s)]) * 24 * 60
````
### 🧮 Formatação de Tempo
Average Response
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
RETURN FORMAT(MinutosInteiros, "00") & "m e " & FORMAT(SegundosInteiros, "00") & "s"
````
Chart Total Response Time
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
Response Time
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
FORMAT(InteireDay, "00") & " Dia(s)       " &
FORMAT(HorasInteiras, "00") & " Hora(s)       " &
FORMAT(MinutosInteiros, "00") & " Minuto(s)       " &
FORMAT(SegundosInteiros, "00") & " Segundo(s)"
````
## 🌐 Acesso ao Painel
### 🔗 Visualizar o Painel Power BI

### 📸 Prévia do Painel

## 🧰 Como Usar
Baixe o arquivo .pbix deste repositório.

Abra com o Power BI Desktop.

O painel está pronto para exploração — sem necessidade de atualizar conexões de dados.

## 🛠️ Desafios & Otimizações
Cálculos Precisos de Tempo:

Fórmulas DAX personalizadas para converter tempo de resolução em dias, horas, minutos e segundos com rastreamento claro.

Tooltips Dinâmicos:

Visualizações adicionais integradas via tooltip para aprofundar a análise de status e tendências de resposta.

Insights de Eficiência Operacional:

Identificação de que há as solicitações pendentes de resposta do cliente podendo indicar falhas de comunicação.

Padrões consistentes de abertura de solicitações por dia útil e dia do mês, auxiliando no planejamento de equipe.

Eventos com alta taxa de reabertura destacados para revisão de processos.

🎯 Impacto

Este painel fortalece a tomada de decisão orientada por dados, revelando tendências na eficiência do atendimento, comportamento de resposta e prazos de resolução. 
Ele apoia a gestão proativa e a melhoria contínua.

📢 Conecte-se

Quer explorar mais projetos em Power BI e análise de dados? Vamos trocar ideias!
