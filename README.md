# Filtro FIR Passa-Baixa para Processamento de Áudio

## 📌 Descrição
Este projeto consiste na implementação de um filtro digital FIR passa-baixa para a remoção de ruídos em sinais de áudio corrompidos. O objetivo é melhorar a qualidade do áudio mantendo as componentes de baixa frequência, onde a voz humana está concentrada, e eliminando ruídos de alta frequência.

## 📂 Estrutura do Projeto
- `FiltroFIR.ipynb` - Contém os scripts em Python para leitura, processamento e filtragem dos sinais de áudio, além dos gráficos gerados na análise do filtro.
- `audios/` - Arquivos de áudio originais e filtrados.
- `audios_filtrados/` - Arquivos de áudio filtrados. 
- `README.md` - Documentação do projeto.

## 🛠 Tecnologias Utilizadas
- **Python**
- **NumPy** - Para manipulação de sinais e cálculos matemáticos.
- **Matplotlib** - Para visualização dos sinais no domínio do tempo e da frequência.
- **SciPy** - Para manipulação de arquivos de áudio e funções de filtragem.

## 📖 Embasamento Teórico
### 🔹 Transformada de Fourier
Os sinais de áudio são convertidos do domínio do tempo para o domínio da frequência usando a Transformada de Fourier Discreta (DFT), permitindo a identificação e remoção de ruídos de alta frequência.

### 🔹 Filtro FIR Passa-Baixa
O filtro FIR passa-baixa é implementado utilizando a técnica de janelamento com a **Janela de Hamming**, que suaviza as oscilações na resposta em frequência e melhora a qualidade do filtro.

A resposta ao impulso do filtro é definida como:

$ h[n] = \frac{sin(\omega_c(n - \alpha))}{\pi(n - \alpha)} \cdot w[n] $

Onde:
- $\omega_c = 2\pi f_c / f_s$ é a frequência de corte normalizada.
- $\alpha = (L-1)/2$ é o deslocamento para tornar o filtro causal.
- $w[n]$ é a **Janela de Hamming**: $ w[n] = 0.54 - 0.46 \cos(2\pi n / (L - 1)) $.

## 🔧 Implementação
### 🔹 Processamento do Áudio
1. **Leitura do arquivo de áudio** usando `wavfile.read()`.
2. **Transformação para o domínio da frequência** com `numpy.fft.fft()`.
3. **Aplicação do filtro FIR**:
   - Definição da frequência de corte $f_c$.
   - Escolha do número de coeficientes $L$ do filtro.
   - Aplicação da Janela de Hamming.
4. **Retorno ao domínio do tempo** com a Transformada Inversa de Fourier (`ifft`).
5. **Salvamento do áudio filtrado**.

### 🔹 Ajuste de Parâmetros
Foram realizados diversos testes para encontrar os melhores valores de $\omega_c$ e $L$ para cada áudio:
- Para o **Áudio 1** (voz masculina), os melhores parâmetros foram **$\omega_c = 3000 Hz$** e **$L = 1000$**.
- Para o **Áudio 2** (voz feminina), os melhores parâmetros foram **$\omega_c = 2500 Hz$** e **$L = 100$**.

## 🎯 Resultados
Os gráficos gerados mostraram que os filtros implementados foram eficazes na remoção do ruído, preservando a qualidade da voz original. O ajuste correto do parâmetro \(L\) foi essencial para minimizar oscilações indesejadas na resposta em frequência.

## 📌 Como Executar
1. Clone este repositório:
   ```sh
   git clone https://github.com/seu-usuario/nome-do-repositorio.git
   cd nome-do-repositorio
   ```
2. Instale as dependências necessárias:
   ```sh
   pip install numpy scipy matplotlib
   ```
3. Execute o script principal:
   ```sh
   python codigo/filtro_audio.py
   ```
4. O áudio filtrado será salvo na pasta `audios/`.

## 📄 Conclusão
Este projeto demonstrou a importância dos filtros digitais para o tratamento de sinais, mostrando que é possível recuperar um áudio corrompido por ruídos com a devida análise da frequência e ajustes nos parâmetros do filtro.

---
📌 **Autor:** Vinícius Filgueiras, Vinícius Lavor, Matheus Maia

