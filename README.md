
# Analisador e filtro de áudio musical

**Sistematização · Métodos Matemáticos**  
Do sinal ao espectro — aplicação em gravação de violão

| Campo | Informação |
|-------|------------|
| **Aluno** | Gabriel Mendes Boaventura |
| **RA** | 22251646 |
| **Curso** | Engenharia de Computação |
| **Instituição** | CEUB |

---

## Sobre o projeto

Análise e filtragem de um sinal real de violão (~38 s, 48 kHz), percorrendo:

1. **Série de Fourier** — aproximação de onda quadrada e fenômeno de Gibbs  
2. **Transformada de Fourier (FFT)** — espectro e identificação de picos  
3. **Filtragem + IFFT** — notch de 60 Hz e reconstrução do sinal  
4. **Transformada de Laplace** — função de transferência, polos e zeros

---

## Estrutura de diretórios

```
analisador_e_filtro_de_audio_.../
│
├── audio/                              # Áudios de entrada
│   ├── gravacao_real_violao.wav        # Gravação principal (48 kHz, ~38 s)
│   ├── audio_com_ruido.wav
│   ├── audio_filtrado.wav
│   └── audio_musical_ideal.wav
│
├── main/
│   └── output/
│       ├── audio/                      # Áudios gerados pelo notebook
│       │   ├── gravacao_violao_filtrada.wav
│       │   └── gravacao_violao_reconstruida.wav
│       └── graficos/                   # Figuras geradas
│           ├── 01_onda_quadrada.png
│           ├── 02_serie_fourier.png
│           ├── 03_fenomeno_gibbs.png
│           ├── 04_forma_onda_original.png
│           ├── 05_espectro_original.png
│           ├── 06_comparacao_sinal.png
│           ├── 07_comparacao_espectro.png
│           ├── 08_resposta_frequencia_laplace.png
│           └── 09_polos_zeros.png
│
├── Sistematizacao_Metodos_Matematicos_Violao.ipynb
└── README.md
```

---

## Como executar

1. Instale as dependências:

```bash
pip install numpy scipy matplotlib
```

2. Abra o notebook:

```bash
jupyter notebook Sistematizacao_Metodos_Matematicos_Violao.ipynb
```

3. Garanta que `audio/gravacao_real_violao.wav` esteja acessível.  
   O notebook procura o arquivo em caminhos comuns; se necessário, ajuste `ARQUIVO_AUDIO` na célula de configuração.

4. Execute todas as células. Os gráficos e áudios de saída serão gravados em `main/output/`.

---

## Principais resultados

| Etapa | Resultado |
|-------|-----------|
| Série de Fourier | Aproximação da onda quadrada; fenômeno de Gibbs (~9%) |
| FFT do violão | Picos ~390 Hz, ~162 Hz, ~218 Hz; energia abaixo de 1 kHz |
| Filtro notch 60 Hz | Q = 30; RMS da diferença ≈ 0,000185 |
| Reconstrução IFFT | Erro máximo ≈ 2,8 × 10⁻¹⁶ |
| Laplace (plano s) | Zeros: 0 ± j 376,99; Polos: −6,28 ± j 376,94 (estável) |

---

## Parâmetros do filtro

- Frequência de rejeição: **60 Hz**  
- Fator de qualidade: **Q = 30**  
- ω₀ = 2π · 60 ≈ 376,99 rad/s  

Modelo analógico:

```
H(s) = (s² + ω₀²) / (s² + (ω₀/Q)s + ω₀²)
```

---

## Ferramentas

- NumPy, SciPy (`scipy.signal`, `scipy.io.wavfile`), Matplotlib  
- Filtro notch IIR: `signal.iirnotch` + `filtfilt`  
- Análise no plano s: `signal.freqs`, `np.roots`  
- Áudio principal: `audio/gravacao_real_violao.wav` (48 kHz, 38,1 s)
