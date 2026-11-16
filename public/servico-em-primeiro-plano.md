# Serviço em primeiro plano (`FOREGROUND_SERVICE_SPECIAL_USE`)

Documento de apoio para a declaração de **Permissões de serviço em primeiro plano** na Play Console
(*Conteúdo do app → Permissões de serviço em primeiro plano → Uso especial*). Traz o texto pronto para o
campo de descrição, o roteiro do vídeo exigido e o checklist do que precisa estar visível na gravação.

Para a explicação técnica (por que `specialUse` para as câmeras IP e por que `camera`/`microphone` só entram na
opção de câmera deste celular), veja os comentários em
[`app/src/main/AndroidManifest.xml`](../app/src/main/AndroidManifest.xml) (linhas 8–22 e 60–78)
e em `ScheduledRecordingService.kt` / `MotionListenerService.kt`.

## 1. Por que `specialUse` (resumo)

| Tipo de FGS | Serve? | Motivo |
| --- | --- | --- |
| `dataSync` | **Não** | Tem limite de ~6 h a cada 24 h (Android 15+); a rotina grava 24 h por dia. Também não pode ser iniciado no boot em apps com target 35+. |
| `mediaProcessing` | **Não** | Mesmo limite de ~6 h/24 h; é para processar mídia já existente, não para capturar stream contínuo. |
| `camera` | **Sim, só para a câmera física** | Declarado apenas quando o usuário cadastra a câmera do próprio celular como uma câmera da rotina. As câmeras IP pela rede continuam em `specialUse`. |
| `microphone` | **Sim, junto de `camera`** | Usado somente quando a câmera do celular grava com som; não se aplica às câmeras IP. |
| `connectedDevice` | **Não** | Pressupõe uma sessão de interação com um acessório/conexão; a tarefa aqui é gravar e arquivar vídeo de forma contínua. |
| `specialUse` | **Sim** | Único tipo sem teto de tempo, com subtipo declarado no manifesto (`PROPERTY_SPECIAL_USE_FGS_SUBTYPE`). É o tipo usado pelas câmeras IP. |

## 2. Campo "Descrever o uso da permissão" — texto pronto (pt-BR)

> Copie o bloco abaixo inteiro. Ele responde às duas coisas que o formulário pede: o que o app faz com a
> permissão e por que a tarefa não pode ser adiada, pausada ou reiniciada.

```text
O ThirdEye grava continuamente as câmeras IP (RTSP/ONVIF) que o próprio usuário já possui, na rede local dele.
Quando o usuário liga a "Rotina" de gravação no app, o serviço em primeiro plano passa a receber o vídeo dessas
câmeras sem interrupção: fecha um arquivo MP4 a cada 5/10/15/30 ou 60 minutos (padrão 15), envia cada arquivo
para o Google Drive do próprio usuário (ou salva no aparelho, se for a opção que ele escolheu), apaga do celular
o arquivo já enviado e apaga do Drive o que passou do prazo de retenção configurado. O mesmo serviço também
executa a ronda automática de PTZ (passar pelas posições salvas da câmera). Enquanto roda, existe uma notificação
permanente com o número de câmeras, a duração dos vídeos, o destino e o botão "Parar".
Opcionalmente, o usuário pode cadastrar a câmera do próprio celular como uma câmera da rotina; nesse caso o
mesmo serviço também abre a lente (e o microfone, quando o som está ligado), com os tipos `camera` e
`microphone` do Android.

Por que a tarefa precisa começar imediatamente e não pode ser pausada ou reiniciada:

1) O conteúdo é um evento em tempo real e irrepetível. A cena que a câmera transmite agora não existe depois:
   se a captura atrasar ou parar, aquele trecho é perdido para sempre — não há como reprocessar nem tentar de
   novo. Um arquivo MP4 precisa ser escrito de forma contínua a partir do stream, com o cabeçalho e os frames
   em sequência.

2) O valor do produto é a cobertura contínua. A rotina fica ligada de dia e de noite, por vários dias, para
   registrar o que aconteceu enquanto ninguém está olhando. Pausar e retomar manualmente — ou deixar o sistema
   suspender o processo — cria buracos no vídeo exatamente quando algo importante acontece, e é justamente a
   continuidade que o usuário comprou ao instalar o app.

3) Precisa rodar fora da tela. O uso típico é ligar a rotina e deixar o celular carregando com a tela apagada
   (ou sair do app para atender uma ligação, usar outro app). Sem serviço em primeiro plano o Android encerra o
   processo em segundo plano: os arquivos em escrita ficariam truncados/corrompidos e a gravação morreria em
   silêncio, sem o usuário perceber.

4) Não é trabalho adiável. WorkManager/JobScheduler executam "quando o sistema decidir", com janela de minutos,
   e não mantêm um socket RTSP aberto nem um arquivo MP4 em escrita contínua. Qualquer atraso rompe o
   encadeamento dos arquivos e abre um buraco na gravação.

5) Nenhum outro tipo de serviço em primeiro plano descreve a gravação das câmeras IP: dataSync e mediaProcessing
   têm limite de 6 horas por 24 horas (a rotina é contínua, sem janela); camera e microphone cobrem apenas a
   câmera física e o microfone do aparelho e são declarados só quando o usuário cadastra a câmera deste celular
   (as câmeras IP pela rede continuam em specialUse); connectedDevice pressupõe uma sessão de interação com um
   acessório, e não gravação e arquivamento contínuos.

6) O usuário tem controle explícito e visível: o app não grava nada sem o usuário ligar a rotina, ligar/parar
   passa por confirmação (biometria/PIN quando configurado) e o botão "Parar" está sempre presente na
   notificação. Nada é enviado ao desenvolvedor: o destino é o Google Drive do próprio usuário ou o
   armazenamento do aparelho.

Opcionalmente, no celular que apenas acompanha as câmeras, o usuário pode ligar "Manter conexão para avisos
imediatos". Nesse caso um segundo serviço em primeiro plano mantém a conexão direta com o celular principal
para receber os avisos de movimento, também com notificação permanente. Ele precisa rodar com o app fora da
tela porque o movimento pode acontecer a qualquer momento; sem ele, o Android encerraria o processo e o aviso
só apareceria quando o app fosse aberto de novo.
```

## 3. Versão em inglês (en-US)

> O formulário normalmente é em português, mas o revisor pode ser de outro idioma. Se o campo aceitar texto
> longo, cole a versão em inglês **depois** da portuguesa; se não aceitar, use só a inglesa.

```text
ThirdEye continuously records the user's own IP cameras (RTSP/ONVIF) on the local network. When the user turns
on the recording routine, the foreground service keeps reading the camera stream without interruption: it
closes one MP4 file every 5/10/15/30 or 60 minutes (15 by default), uploads each file to the user's own Google
Drive (or saves it on the device, if that is the option the user chose), deletes the local copy after upload and
deletes from Drive whatever is older than the retention period. The same service also runs the automatic PTZ
tour through the saved camera positions. While it runs, an ongoing notification shows the number of cameras,
the video length, the destination and a "Stop" button.
Optionally, the user can add the phone's own camera as a routine camera; in that case the same service also
opens the lens (and the microphone, when sound is on), using the Android `camera` and `microphone` service
types.

Why the task must start immediately and cannot be paused or restarted:

1) The content is a real-time, unrepeatable event. What the camera transmits right now will not exist later; if
   capture is delayed or stopped, that footage is lost forever — there is nothing to reprocess or retry, and an
   MP4 file must be written continuously from the stream.

2) The product's value is continuous coverage. The routine stays on day and night for days, to record what
   happens while nobody is watching. Pausing/resuming manually, or letting the system suspend the process,
   leaves gaps in the video exactly when something important happens.

3) It must run while the app is not on screen. The typical use is to turn the routine on and leave the phone
   charging with the screen off, or leave the app to take a call. Without a foreground service Android kills the
   background process: open files would be truncated/corrupted and the recording would die silently.

4) It is not deferrable work. WorkManager/JobScheduler run "whenever the system decides", with minutes of
   latency, and cannot keep an RTSP socket open nor an MP4 file being written continuously.

5) No other foreground service type describes IP camera recording: dataSync and mediaProcessing are capped at 6
   hours per 24 hours (the routine is continuous); camera and microphone cover only the device's physical camera
   and microphone and are declared only when the user adds this phone's camera (IP cameras on the network stay
   on specialUse); connectedDevice assumes an interaction session with an accessory, not continuous recording
   and archiving.

6) The user keeps explicit control: nothing is recorded unless the user turns the routine on, starting/stopping
   requires confirmation (biometrics/PIN when configured) and the "Stop" action is always in the notification.
   Nothing is sent to the developer: the destination is the user's own Google Drive or the device storage.

Optionally, on the phone that only watches the cameras, the user can turn on "Keep connection for immediate
alerts". A second foreground service then keeps a direct connection to the main phone to receive motion alerts,
also with an ongoing notification. It must run while the app is not on screen because motion can happen at any
time; without it, Android would kill the process and the alert would only appear when the app is opened again.
```

## 4. Campo "Link de vídeo" — roteiro

O vídeo precisa provar que a tarefa é contínua e que ela **continua com o app fora da tela**. Grave a tela do
celular (60 a 120 s), com legendas em português, sem música. Publique como **"Não listado"** no YouTube e cole o
link — não use link privado com senha (o revisor não consegue abrir).

| Tempo | O que mostrar |
| --- | --- |
| 0:00–0:10 | App aberto na tela inicial, com as câmeras IP já cadastradas e uma prévia ao vivo tocando (deixa claro que a fonte é uma câmera de rede). |
| 0:10–0:25 | Tela **Rotina** → ligar a chave (mostrar a confirmação por biometria/PIN) → escolher as câmeras, a *Duração de cada vídeo* (ex.: 5 min, para o vídeo ficar curto) e o destino (*Google Drive*). Legenda: "o usuário liga a rotina". |
| 0:25–0:35 | A notificação **"Gravação contínua ativa"** aparecendo na barra, com o texto "N câmera(s) • vídeos de 5 min enviados ao Drive" e o botão **Parar**. |
| 0:35–0:50 | Sair do app (Home), apagar a tela, mostrar que a notificação **continua lá**. Se possível, mostrar o relógio andando para provar a passagem do tempo real. |
| 0:50–1:05 | Voltar ao app → tela **Gravações**: mostrar os arquivos aparecendo em sequência, com horários **encadeados sem buraco** (ex.: 21:00–21:05, 21:05–21:10, 21:10–21:15). É o ponto central da revisão. |
| 1:05–1:20 | Um dos arquivos aberto tocando (ou no Drive, na pasta do app) e o envio concluído. |
| 1:20–1:30 | Tocar em **Parar** na notificação e mostrar a gravação encerrando e a notificação sumindo. |

Cuidados que evitam reprovação:

- **Não** edite o vídeo de forma que pareça que a gravação só funciona com o app aberto — o trecho com a tela
  apagada é obrigatório.
- Deixe o **relógio do sistema** visível em algum momento (barra de status), para provar que os arquivos são de
  horários diferentes.
- Use uma câmera real (ou o stream de teste da própria câmera). Não use emulador com imagem estática.
- Se o vídeo passar de 2 min, tudo bem — melhor completo do que curto e inconclusivo.

## 5. Checklist antes de enviar

- [ ] Subtipos no manifesto iguais ao texto enviado:
      `ScheduledRecordingService` = "Gravação contínua de câmeras IP da rede local e envio ao Google Drive"
      (linhas 60–68) e `MotionListenerService` = "Conexão com o celular principal da conta para avisos imediatos
      de movimento das câmeras" (linhas 70–78).
- [ ] Tipos de serviço do `ScheduledRecordingService` = `specialUse|camera|microphone`; `camera`/`microphone`
      valem só para a opção de câmera deste celular e não mudam a justificativa de `specialUse` das câmeras IP.
- [ ] Marcar **Outro** em "Quais tarefas exigem que o app use a permissão" — nenhuma categoria pronta descreve
      gravação contínua de câmera IP.
- [ ] Link do vídeo abre em janela anônima, sem login.
- [ ] Descrição e política de privacidade contam a mesma história (`politica-de-privacidade.md`, item 8).
- [ ] Notificação fixa com ação **Parar** visível no vídeo (é o que os revisores procuram primeiro).
- [ ] Se o vídeo mostrar o aviso imediato de movimento, a notificação fixa do `MotionListenerService` também aparece.
- [ ] Nenhuma menção a "monitoramento de terceiros": o app grava as câmeras **do próprio usuário**.

## 6. Se a Play recusar

A recusa mais comum é "a tarefa caberia em outro tipo". Aí **não** é caso de trocar para `dataSync` — o limite de
6 h a cada 24 h quebra a rotina. O caminho é responder na própria revisão apontando:

1. o limite de 6 h/24 h de `dataSync` e `mediaProcessing` (documentação de limites de serviço em primeiro plano
   do Android 15+);
2. que `camera` e `microphone` cobrem só a câmera física e o microfone do aparelho, usados apenas na opção de
   câmera deste celular, e não as câmeras IP pela rede (essas seguem em `specialUse`);
3. os arquivos MP4 encadeados no vídeo, provando que a gravação não tem janela nem pausa.

Se ainda assim for exigido outro tipo, a alternativa é **mudar o produto**: limitar cada sessão contínua a menos
de 6 h e retomar por `WorkManager` (com o buraco declarado ao usuário), o que altera o comportamento atual de 24 h
— decisão de produto, não de manifesto.


