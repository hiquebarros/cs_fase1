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

Os dados são gerados de forma aleatória a cada execução, então o resultado pode variar entre "PRONTO PARA DECOLAR" e "DECOLAGEM ABORTADA".

---

## Prints da execução

### Exemplo 1 – Decolagem abortada (temperatura interna)

```
Dados recebidos da API:
temperatura_interna : 17.993242370343765
temperatura_externa : 12.717041484312816
integridade_estrutural : 1
energia_capacidade_total : 1000
carga_atual_percentual : 63.694666201184674
consumo_decolagem : 400
perdas_energeticas : 36.79259378943534
pressao_tanques : 4.744940285949863
modulos_criticos : {'navegacao': True, 'comunicacao': True, 'controle_voo': True}

Resultado da verificação:
DECOLAGEM ABORTADA - Temperatura interna fora da faixa segura
```

### Exemplo 2 – Pronto para decolar

Quando todas as condições são atendidas, a saída pode ser:

```
Dados recebidos da API:
temperatura_interna : 22.5
temperatura_externa : 25.0
integridade_estrutural : 1
energia_capacidade_total : 1000
carga_atual_percentual : 85.0
consumo_decolagem : 400
perdas_energeticas : 30.0
pressao_tanques : 3.8
modulos_criticos : {'navegacao': True, 'comunicacao': True, 'controle_voo': True}

Resultado da verificação:
PRONTO PARA DECOLAR
```

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

1. Salve o conteúdo das células de código do `main.ipynb` em um arquivo `.py` (por exemplo `main.py`) com as funções `obter_dados_sistema`, `verificar_condicoes` e o bloco `if __name__ == "__main__": main()`.

2. No terminal, na pasta do projeto:
   ```bash
   python main.py
   ```

### Estrutura do projeto

- **`main.ipynb`** – Notebook com telemetria, verificação de condições e execução.
- **`readme.md`** – Este arquivo (explicação, prints e instruções de execução).
# cs_fase1
