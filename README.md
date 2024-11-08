# **CardioMetrix Pro**

## **Descrição**

Este projeto tem como objetivo a leitura e decodificação de arquivos XCM de Holter Cardíaco, processamento e análise de sinais ECG. Ele inclui:

1. **HolterXCMDecryptor**: Classe para decodificar arquivos XCM de Holter, realizar validações no cabeçalho e nos dados, e processar os canais de ECG.
2. **ECGDisplay**: Classe para visualização e análise avançada dos sinais de ECG, incluindo o uso de templates gerados pelo **NeuroKit2** para criar um sinal de ECG realista e calcular métricas de variabilidade da frequência cardíaca (VFC) e outros parâmetros avançados de ECG.

## **Funcionalidades**

- **Leitura e Validação de Cabeçalho**: O arquivo XCM é lido e validado conforme as informações do cabeçalho, com verificações de versão, taxa de amostragem, número de canais, e bits por amostra.
- **Decodificação de Dados ECG**: Os dados do ECG são extraídos e validados, com remoção de offset DC, normalização e remoção de outliers.
- **Exibição de Sinal ECG**: A classe **ECGDisplay** processa e exibe o sinal ECG, detectando picos R e ajustando o sinal conforme templates gerados pelo **NeuroKit2**.
- **Cálculo de Métricas Avançadas**: A classe **ECGDisplay** pode calcular métricas avançadas de ECG, como variabilidade da frequência cardíaca (VFC) e análise espectral da frequência cardíaca.

## **Requisitos**

Para rodar o projeto, você precisará de:

- Python 3.x
- Pacotes de dependências:
    - `numpy`
    - `scipy`
    - `matplotlib`
    - `neurokit2`

Você pode instalar as dependências com o seguinte comando:

```bash
pip install numpy scipy matplotlib neurokit2
```

## **Uso**

1. **Decodificar um arquivo XCM**: Utilize a classe `HolterXCMDecryptor` para carregar e decodificar um arquivo XCM.
   
```python
decryptor = HolterXCMDecryptor()
header, channels = decryptor.decrypt_data('caminho/para/seu/arquivo.xcm')
```

2. **Exibir o sinal ECG**: Utilize a classe `ECGDisplay` para criar e exibir o sinal ECG a partir dos canais decodificados.

```python
ecg_display = ECGDisplay(decryptor)
ecg, peaks = ecg_display.create_ecg(channels[0])  # Usando o primeiro canal como exemplo

# Plotando o sinal ECG
plt.plot(ecg)
plt.title('Sinal ECG Processado')
plt.xlabel('Tempo (amostras)')
plt.ylabel('Amplitude')
plt.show()
```

3. **Calcular métricas avançadas**: Após detectar os picos R, calcule métricas avançadas como VFC e espectro de potência.

```python
metrics = ecg_display.calculate_advanced_metrics(peaks, channels[0])
print(metrics)
```

## **Exemplo de Saída**

Após a decodificação do arquivo XCM e a exibição do sinal ECG, você pode obter as seguintes saídas:

- Cabeçalho validado com as informações do arquivo XCM, como a versão, taxa de amostragem, número de canais, etc.
- Um sinal ECG processado com os picos R detectados.
- Métricas avançadas, incluindo a variabilidade da frequência cardíaca (VFC) e a análise espectral de potência.

## **Licença**

Este projeto está licenciado sob a Licença MIT. Veja o arquivo `LICENSE` para mais detalhes.
