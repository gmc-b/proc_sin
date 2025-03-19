# Processamento de Sinais

Esse projeto realiza análise de sinais fisiológicos.

## **Funcionalidades**

O código foi desenvolvido para processar arquivos `.acq`, que contêm dados de sinais temporais. Ele realiza as seguintes funções:

1. **Leitura de arquivos `.acq`**:
   - Extrai dados do cabeçalho.
   - Armazena os dados de tempo e de cada canal.

2. **Detecção de oscilações**:
   - Detecta picos e vales nos sinais.
   - Pareia picos e vales com base na menor diferença de tempo.
   - Extrai as 5 primeiras oscilações (pares de picos e vales) para cada canal.

3. **Geração de gráficos**:
   - Cria imagens para os sinais, destacando os picos e vales detectados.
   - Salva os gráficos em pastas específicas para cada arquivo.

4. **Geração de planilha Excel**:
   - Armazena os resultados (altura máxima, altura mínima e amplitude) em uma planilha Excel.

5. **Organização de pastas**:
   - Cria uma pasta de saída (`Output`) para armazenar os resultados.
   - Dentro da pasta `Output`, cria subpastas para cada arquivo `.acq` processado, contendo os gráficos gerados.

---




### Estrutura de Pastas 

```bash
Proc_Sin/
├── Data/                  # Pasta contendo os arquivos .acq
│   ├── arquivo1.acq
│   ├── arquivo2.acq
│   └── ...
│
├── Output/                # Pasta de saída (gerada automaticamente)
│   ├── arquivo1/          # Subpasta para o arquivo1.acq
│   │   ├── CH1.png        # Gráfico do canal CH1
│   │   ├── CH2.png        # Gráfico do canal CH2
│   │   └── ...
│   ├── arquivo2/          # Subpasta para o arquivo2.acq
│   │   ├── CH1.png        # Gráfico do canal CH1
│   │   ├── CH2.png        # Gráfico do canal CH2
│   │   └── ...
│   │
│   └── resultados.xlsx    # Planilha com os resultados
│
├── parametros.json        # Arquivo JSON com parâmetros de configuração
│
└── main.py              # Código Python
```

### Parâmetros
Cada canal obtém ondas com características diferentes, portanto o arquivo ```parametros.json``` permite o ajuste específico por canal dos parâmetros de detecção de picos.

- peak_prominence: Define a proeminência mínima dos picos (quanto o pico se destaca em relação à linha base adjacente do sinal).
- peak_min_distance: Define a distância mínima (em número de amostras) entre picos adjacentes.
```bash
{
    "CH1": {
        "peak_prominence": 0.2,      # Proeminência mínima dos picos
        "peak_min_distance": 40      # Distância mínima entre picos
    },
    "CH2": {
        "peak_prominence": 0.3,
        "peak_min_distance": 50
    }
}
```
### Arquivo Excel
O arquivo excel contém o valores dos 5 primeiros pares detectados. Abaixo é mostrado um exemplo com apenas os dois primeiros pares por simplicidade
| File      | Channel | Pair | Max  | Min  | Amplitude |
|-----------|---------|------|------|------|-----------|
| **file1** | **CH1** | 1    | 7.00 | 1.00 | 6.00      |
|           |         | 2    | 6.00 | 0.00 | 6.00      |
|           | **CH2** | 1    | 5.00 | 2.00 | 3.00      |
|           |         | 2    | 2.00 | 1.00 | 1.00      |
| **file2** | **CH1** | 1    | 8.00 | 2.00 | 6.00      |
|           |         | ..   | ...  | ...  | ...       |

## **Instalação**

### Download
0. Para esse projeto é necessário ter python instalado em sua máquina
1. Baixe o arquivo
2. Descompacte-o em uma pasta e copie o nome do caminho para pasta (Ex: C:/exemplo/proc_sin)

### Instalação de bibliotecas
1. Abra seu terminal (Ex: powershell) e digite o comando ```cd``` com o caminho para o diretório do projeto

```bash
cd C:/exemplo/proc_sin
```

2. Para instalar as bibliotecas necessárias, execute o seguinte comando:

```bash
pip install -r requirements.txt

```

## **Utilização**

1. Certifique-se que os arquivos ```.acq``` estão na pasta Data
2. Abra seu terminal (Ex: powershell) e digite o comando ```cd``` com o caminho para o diretório do projeto

```bash
cd C:/exemplo/proc_sin
```

3. Para executar o programa utilize o comando
```bash
python main.py
```
