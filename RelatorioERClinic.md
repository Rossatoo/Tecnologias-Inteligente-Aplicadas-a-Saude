# Relatório Técnico – Funcionamento do ER Clinic com Inteligência Artificial

## 1. Introdução
O **ER Clinic** é um software de gestão para clínicas e consultórios que incorporou recursos de **Inteligência Artificial (IA)** baseados em modelos de linguagem. Essa integração permite que pacientes e usuários interajam com o sistema em linguagem natural, como se estivessem conversando com uma recepcionista virtual.  
O sistema utiliza a API do **ChatGPT (LLM – Large Language Model)** em conjunto com uma camada de **orquestração de intenções**, conhecida popularmente como “porteiro”.

---

## 2. O “Porteiro” 
O **porteiro** é um componente responsável por identificar o que o cliente deseja, interpretando a frase digitada ou falada.  
- Atua como um **roteador de intenções**  
- Baseia-se em **palavras-chave, contexto e prompts** para determinar a ação correta.  
- Exemplo:  
  - “Quero marcar uma consulta” → Encaminha para módulo **Agenda**.  
  - “Preciso do recibo de pagamento” → Encaminha para módulo **Financeiro**.  
  - “Quero ver meu exame” → Encaminha para módulo **Prontuário**.  

Esse mecanismo organiza o fluxo e evita que todo o processamento seja feito por um único agente genérico.

---

## 3. Uso da API do ChatGPT
O ER Clinic utiliza a **API do ChatGPT** para interpretar e gerar respostas em linguagem natural.  
- Cada chamada à API gera custos em **tokens**:  
  - **Prompt tokens** → texto enviado para a IA.  
  - **Completion tokens** → resposta retornada pela IA.  
- Para otimizar custos, são aplicadas técnicas de **engenharia de prompts**, que consistem em elaborar instruções claras e concisas para guiar o modelo.  

---

## 4. Treinamento por Prompts
O sistema não é treinado como em Machine Learning tradicional. Em vez disso, utiliza prompts especializados que direcionam o comportamento da IA.  
- Exemplo de prompt:  
  > “Você é um assistente de clínica. Se o cliente falar de horários, encaminhe para Agenda. Se falar de pagamentos, encaminhe para Financeiro.”  

Dessa forma, o modelo consegue simular diferentes especializações sem precisar ser reprogramado.

---

## 5. LLMs e LangChain
- **LLM (Large Language Model):** é o núcleo de IA usado (no caso, ChatGPT), que entende e gera linguagem natural.  
- **LangChain:** é um framework que facilita a criação de **agentes especializados (VMs)** e a construção de fluxos conversacionais complexos.  
  - Permite encadear prompts.  
  - Oferece integração com APIs externas (ex.: banco de dados do ER Clinic).  
  - Dá suporte à criação de **multiagentes** com papéis distintos.

---

## 6. Arquitetura Multi-Agente (VMs)
O desenvolvedor do ER Clinic compara os agentes a **“VMs” (máquinas virtuais)**, cada uma configurada com um papel específico:  
- **VM Agenda** → gerencia marcação de consultas.  
- **VM Financeiro** → trata de cobranças, recibos e pagamentos.  
- **VM Prontuário** → acessa e organiza exames e dados clínicos.  

Essas VMs são isoladas em termos de **prompt e regras**, mas trabalham juntas dentro do fluxo orquestrado pelo “porteiro”.

---

## 7. Exemplo de Funcionamento
1. Usuário: “Quero pagar minha consulta de ontem.”  
2. **Porteiro:** identifica a intenção como “Financeiro”.  
3. **VM Financeiro:** recebe o pedido, aciona as rotinas do ER Clinic e gera a resposta.  
4. **Resposta ao usuário:** “Localizei o pagamento pendente, deseja gerar um boleto ou pagar via Pix?”  

Esse processo garante **fluidez**, **automatização** e **redução de tempo no atendimento**.

---

## 8. Conclusão
O ER Clinic utiliza uma arquitetura moderna de **IA conversacional**, combinando:  
- **Classificação de intenções (porteiro).**  
- **API do ChatGPT com engenharia de prompts.**  
- **LLMs + LangChain para agentes especializados.**  
- **VMs (multiagentes) isoladas por domínio funcional.**  

Essa abordagem permite um atendimento humanizado, inteligente e integrado aos módulos internos do software.
