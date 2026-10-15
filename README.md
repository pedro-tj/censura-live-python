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
