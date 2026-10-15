# 🎙️ Censura de Áudio em Tempo Real para Lives (Python + Vosk)

Script em Python desenvolvido para interceptar o áudio do microfone em tempo real, transcrevê-lo de forma 100% offline utilizando inteligência artificial (**Vosk**), detectar palavras proibidas (palavrões/xingamentos) e aplicar censura automática (como silenciar ou disparar um som de bipe) antes de enviar o áudio para o OBS Studio.

Criado e testado no ambiente **BigLinux**.

---

## 🚀 Funcionalidades
* **100% Offline:** Utiliza o Vosk para reconhecimento de fala localmente, sem envio de dados para nuvens ou APIs pagas.
* **Baixa Latência:** Processamento rápido em blocos de áudio.
* **Filtro Customizável:** Lista simples em Python para adicionar os termos indesejados.
* **Compatível com Linux:** Ideal para uso com PipeWire/PulseAudio e OBS Studio.

---

## 🛠️ Requisitos e Instalação

### 1. Dependências do Sistema
No seu terminal do BigLinux, certifique-se de ter o Python e as bibliotecas de desenvolvimento de áudio instaladas:
```bash
sudo pacman -S python python-pip portaudio

```

*(Caso utilize outra base de gerenciador de pacotes, adapte para o comando correspondente).*

### 2. Instalar as Bibliotecas Python

Instale os pacotes necessários via pip:

```bash
pip install pyaudio numpy vosk

```

### 3. Baixar o Modelo de Voz (Vosk)

1. Acesse a [página oficial de modelos do Vosk](https://alphacephei.com/vosk/models).
2. Baixe um modelo compacto em Português (ex: `vosk-model-small-pt-br-0.3`).
3. Extraia o conteúdo da pasta baixada para dentro da raiz do projeto e renomeie a pasta para **`model`**.

---

## ⚙️ Como Usar

1. Abra o arquivo `censura_live.py` e edite a lista de palavras proibidas conforme sua necessidade:
```python
PALAVRAS_PROIBIDAS = ["palavrao1", "palavrao2", "xingamento"]

```


2. Execute o script pelo terminal:
```bash
python censura_live.py

```


3. No **OBS Studio**, configure a entrada de áudio do microfone apontando para a saída virtual correspondente do seu sistema (via PipeWire/QpwGraph ou PulseAudio).

---

## 🤝 Contribuindo

Sinta-se à vontade para abrir *issues* ou enviar *pull requests* com melhorias, otimizações de latência ou novas funcionalidades!

## 📄 Licença

Este projeto está sob a licença MIT. Sinta-se livre para usar e modificar.

---

## 👨‍💻 Autor

Desenvolvido por **Pedro Bezerra** (Inforecarga).

Acompanhe mais conteúdos sobre tecnologia, manutenção e automação no canal do YouTube!

```

```
