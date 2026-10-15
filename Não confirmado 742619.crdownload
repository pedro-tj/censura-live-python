import json
import queue
import sys
import numpy as np
import sounddevice as sd
from vosk import Model, KaldiRecognizer

# Configurações de Áudio
SAMPLE_RATE = 16000  # Taxa de amostragem ideal para o Vosk
BLOCKSIZE = 8000     # Tamanho do bloco de áudio processado

# Lista de palavras proibidas (adicione o que quiser em letras minúsculas)
PALAVRAS_PROIBIDAS = ["palavrao1", "palavrao2", "xingamento"]

# Fila para gerenciar os blocos de áudio
q = queue.Queue()

def callback(indata, frames, time, status):
    """Esta função é chamada a cada novo bloco de áudio capturado do microfone."""
    if status:
        print(status, file=sys.stderr)
    q.put(bytes(indata))

def main():
    # Caminho para o modelo Vosk descompactado
    model_path = "model" 
    
    print("Carregando o modelo de IA... Aguarde.")
    model = Model(model_path)
    rec = KaldiRecognizer(model, SAMPLE_RATE)
    rec.SetWords(True)

    print("🎙️ Sistema de censura ativado! Ouvindo o microfone...")

    # Abre o fluxo de entrada do microfone e saída para o sistema/virtual audio cable
    with sd.RawInputStream(samplerate=SAMPLE_RATE, blocksize=BLOCKSIZE, dtype='int16',
                           channels=1, callback=callback):
        
        with sd.OutputStream(samplerate=SAMPLE_RATE, channels=1, dtype='int16') as out:
            while True:
                data = q.get()
                
                # Se reconhecer fala no bloco de áudio
                if rec.AcceptWaveform(data):
                    resultado = json.loads(rec.Result())
                    texto = resultado.get("text", "")
                    
                    if texto:
                        print(falta_imprimir := f"Você disse: {texto}")
                        
                        # Verifica se alguma palavra proibida está no texto transcrito
                        censurado = False
                        for palavra in PALAVRAS_PROIBIDAS:
                            if palavra in texto:
                                censurado = True
                                break
                        
                        # Se achou palavrão, podemos agir (ex: tocar som de bipe ou silenciar)
                        if censurado:
                            print("⚠️ [CENSURADO] Palavra proibida detectada!")
                            # Aqui você pode enviar um sinal de mudo ou gerar o bipe
                            # Gerando um bipe simples de 1 segundo para saída:
                            t = np.linspace(0, 1, SAMPLE_RATE, endpoint=False)
                            beep = (np.sin(2 * np.pi * 1000 * t) * 32767).astype(np.int16)
                            out.write(beep.tobytes())
                            continue

                # Passa o áudio original adiante se estiver limpo
                out.write(data)

if __name__ == "__main__":
    try:
        main()
    except KeyboardInterrupt:
        print("\nEncerrando o sistema de censura.")