# 🏆 Bolão Copa do Mundo PRO - Motor Quantitativo Preditivo

![Python Version](https://img.shields.io/badge/python-3.8%2B-blue)
![Pandas](https://img.shields.io/badge/pandas-Data_Analysis-150458)
![NumPy](https://img.shields.io/badge/numpy-Numerical_Computing-013243)
![License](https://img.shields.io/badge/license-MIT-green)

Um pipeline preditivo desenvolvido em Python para o Campeonato do Mundo, desenhado com uma arquitetura matemática de nível institucional (Sportsbook Standard). Este algoritmo não apenas gera palpites para bolões, mas calcula probabilidades reais utilizando os mesmos paradigmas das grandes casas de apostas desportivas.

## 🚀 Diferenciais e Arquitetura Matemática

Diferente de scripts básicos que confiam apenas em gols passados, este motor foi construído sob as pilares da Engenharia Quantitativa:

* 📊 **Ingestão Autônoma (Scraping Avançado):** Conecta-se diretamente à API oculta da ESPN, puxando o chaveamento atualizado e resultados ao vivo da Copa, com disfarce de *User-Agent* e estratégia de retentativas (*Backoff*).
* 📈 **Elo Rating Dinâmico e Retrospecto Histórico:** As equipes não começam do zero. O algoritmo converte a posição oficial do Ranking da FIFA numa curva logarítmica de força inicial (Base Elo). A cada jogo encerrado, o Rating é atualizado dinamicamente usando um modelo Bayesiano (K-Factor).
* 🧠 **Distribuição de Poisson & Ajuste de Dixon-Coles:** Calcula a expectativa de golos (xG) de cada equipe e aplica a Função Paramétrica de Dixon-Coles ($\rho = 0.18$) para corrigir o "desprezo" matemático por empates, modelando perfeitamente a retranca do futebol real (jogos como 0x0 e 1x1).
* 🎲 **Simulação de Monte Carlo:** A malha estatística joga virtualmente cada partida **10.000 vezes** utilizando matrizes do NumPy para extrair o cume da densidade probabilística (o placar mais provável).
* 💰 **Mercados de Apostas Embutidos:** Retorna automaticamente as probabilidades reais para os mercados de **Over 2.5 Gols** e **BTTS** (Ambas Marcam).

## 🛠️ Instalação e Requisitos

Este projeto foi otimizado para não depender do pesadíssimo `SciPy`, utilizando as funções vetorizadas do `NumPy` e a biblioteca padrão `math` do Python para máxima performance.

1. Clone o repositório:
```
git clone [https://github.com/SEU_USUARIO/bolao-copa-pro.git](https://github.com/SEU_USUARIO/bolao-copa-pro.git)
cd bolao-copa-pro
```
2. Crie e ative um ambiente virtual (Recomendado)
```
python -m venv .venv
source .venv/bin/activate  # No Windows use: .venv\Scripts\activate
```
3. Instale as dependências executando:
```
pip install -r requirements.txt
```
   Conteúdo do requirements.txt:
```
requests>=2.31.0
pandas>=2.0.0
numpy>=1.24.0
urllib3>=1.26.15
```

## 💻 Como Usar

Com as bibliotecas instaladas, basta executar o script principal. Ele fará o download dos dados mais recentes, calculará o Elo de todas as equipas e imprimirá no terminal a previsão dos próximos jogos ainda não iniciados.
```
python bolao_copa_pro.py
```

Exemplo de Output do Terminal
```
🗓️ 24/06 22:00 | Scotland vs Brazil
   📈 Elo Rating: Scotland (1554) vs Brazil (1835)
   📊 Probs: Scotland (15.1%) | Empate (15.4%) | Brazil (69.5%)
   🎯 Top 3 Placares: 0 x 1 (14.2%) | 0 x 2 (11.5%) | 1 x 1 (9.8%) (xG: 0.89 x 2.24)
   🎲 Mercados Base: Over 2.5 (60.4%) | Ambas Marcam (51.0%)
   🔥 Palpite de Valor: Vitória de Brazil
-----------------------------------------------------------------
```

## 🧠 Como interpretar os dados:

* xG (Expected Goals): Quantos gols o modelo matemático espera que cada equipa marque pela sua força absoluta.

* Top 3 Placares: O Top 1 é o placar recomendado para o seu Bolão. O Top 2 e Top 3 ajudam-no a perceber se vale a pena arriscar uma diferença de gols  para se destacar dos seus amigos.

* Palpite de Valor: O algoritmo possui um "Threshold de Empate" de 12%. Se as probabilidades de vitória das duas equipas forem demasiado próximas, o sistema ignorará pequenos favoritismos irreais e apontará o "Empate Técnico".

## ⚠️ Disclaimer Legal

Este software foi desenvolvido com propósitos estritamente educacionais, focados em estudo de estatística, Ciência de Dados e preenchimento de Bolões recreativos entre amigos. Não é uma ferramenta de aconselhamento financeiro. As probabilidades matemáticas, mesmo quando altamente calibradas, não garantem lucros em casas de apostas reais devido à natureza imprevisível do desporto.

