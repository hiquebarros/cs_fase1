# Sistema de Verificação para Decolagem

## Explicação do projeto

Este projeto simula um **sistema de telemetria e verificação de condições** para autorizar ou abortar a decolagem de uma nave (Missão Aurora Siger). O fluxo é:

1. **Telemetria** – A função `obter_dados_sistema()` simula uma chamada a uma API que retorna dados da nave:
   - Temperaturas interna e externa (°C)
   - Integridade estrutural (ok ou falha)
   - Energia: capacidade total, carga atual, consumo na decolagem e perdas
   - Pressão dos tanques (bar)
   - Status dos módulos críticos (navegação, comunicação, controle de voo)

2. **Verificação** – A função `verificar_condicoes()` valida se todas as condições estão dentro das faixas seguras:
   - Temperatura interna entre 18°C e 27°C
   - Temperatura externa entre -10°C e 40°C
   - Integridade estrutural = ok
   - Pressão dos tanques entre 3,0 e 4,5 bar
   - Todos os módulos críticos operacionais
   - Energia disponível suficiente para decolagem + perdas

3. **Resultado** – O sistema retorna **"PRONTO PARA DECOLAR"** se tudo estiver ok, ou uma mensagem de **"DECOLAGEM ABORTADA"** com o motivo (ex.: temperatura fora da faixa, energia insuficiente, etc.).

4. **Análise IA** – A função `analise_ia()` processa os dados e retorna:
   - **Classificação** dos parâmetros (ex.: temperatura interna ALTA/NORMAL, pressão PRÓXIMA DO LIMITE)
   - **Anomalias detectadas** (ex.: temperatura externa muito baixa, pressão próxima do limite)
   - **Sugestões de risco** (ex.: margem energética baixa, possível falha de subsistema crítico)

Os dados são gerados de forma aleatória a cada execução, então o resultado pode variar entre "PRONTO PARA DECOLAR" e "DECOLAGEM ABORTADA".

---

## Prints da execução

A saída é organizada em três blocos: **Telemetria recebida** (dados formatados por categoria), **Resultado da verificação** (pronto/abortado) e **Análise assistida por IA** (classificação, anomalias e riscos).

### Exemplo 1 – Decolagem abortada

```
================ TELEMETRIA RECEBIDA ================

Temperaturas
  Interna : 17.09 °C
  Externa : 7.10 °C

Estrutura
  Integridade estrutural : OK

Energia
  Capacidade total       : 1000 kWh
  Carga atual            : 89.47 %
  Consumo decolagem      : 400 kWh
  Perdas energéticas     : 14.44 kWh

Propulsão
  Pressão dos tanques    : 3.58 bar

Módulos críticos
  navegacao       : OK
  comunicacao     : FALHA
  controle_voo    : OK

================ RESULTADO DA VERIFICAÇÃO ================
DECOLAGEM ABORTADA - Temperatura interna fora da faixa segura

================ ANÁLISE ASSISTIDA POR IA ================

Classificação dos dados
  temperatura_interna  : NORMAL

Anomalias detectadas
  Nenhuma anomalia detectada

Sugestões de risco
  - Possível falha de subsistema crítico

==========================================================
```

### Exemplo 2 – Pronto para decolar

Quando todas as condições são atendidas, a saída terá **RESULTADO DA VERIFICAÇÃO: PRONTO PARA DECOLAR** e a seção de análise pode mostrar classificações, anomalias ou riscos conforme os valores gerados.

*(Os valores exatos mudam a cada execução por causa do uso de `random`.)*

---

## Instruções de execução do código

### Pré-requisitos

- Python 3.x
- Jupyter Notebook (ou JupyterLab) instalado no ambiente

### Opção 1 – Executar pelo Jupyter Notebook

1. Ative o ambiente virtual do projeto (se estiver usando um):
   ```bash
   # Windows (PowerShell/CMD)
   venv\Scripts\activate

   # Windows (Git Bash / WSL)
   source venv/Scripts/activate
   ```

2. Inicie o Jupyter:
   ```bash
   jupyter notebook
   ```
   Ou, se preferir JupyterLab:
   ```bash
   jupyter lab
   ```

3. No navegador, abra o arquivo **`main.ipynb`**.

4. Execute as células em ordem: use **Shift+Enter** em cada célula ou o botão **Run All** no menu para rodar o notebook inteiro.

### Opção 2 – Executar como script Python

1. Salve o conteúdo das células de código do `main.ipynb` em um arquivo `.py` (por exemplo `main.py`) com as funções `obter_dados_sistema`, `verificar_condicoes`, `analise_ia` e o bloco `if __name__ == "__main__": main()`.

2. No terminal, na pasta do projeto:
   ```bash
   python main.py
   ```

### Estrutura do projeto

- **`main.ipynb`** – Notebook organizado em 4 partes:
  1. **Telemetria** – `obter_dados_sistema()` (simulação da API)
  2. **Verificação das condições** – `verificar_condicoes()` (validação para decolagem)
  3. **Análise IA** – `analise_ia()` (classificação, anomalias e sugestões de risco)
  4. **Execução** – `main()` (exibe telemetria formatada, resultado da verificação e análise IA)
- **`README.md`** – Este arquivo (explicação, exemplos de saída e instruções de execução).
