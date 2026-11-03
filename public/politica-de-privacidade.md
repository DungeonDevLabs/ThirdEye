# Política de Privacidade — ThirdEye

- **Aplicativo:** ThirdEye (`app.dungeondevlabs.thirdeye`) — Android
- **Desenvolvedor / controlador dos dados:** DungeonDev Labs
- **Vigência a partir de:** 3 de novembro de 2026
- **Última atualização:** 3 de novembro de 2026

> Aplicativo para monitorar câmeras IP (RTSP/ONVIF) da **sua própria rede**, gravar rotinas e — se você
> quiser — enviar os vídeos para o **seu próprio Google Drive**.

## Resumo em 30 segundos

| O que o app faz com dados | O que o app NÃO faz |
| --- | --- |
| Guarda a configuração das câmeras **no próprio aparelho** | Não cria conta no app nem envia seus dados para servidores do desenvolvedor |
| Grava vídeos **na memória do aparelho** | Não tem anúncios, rastreadores, analytics ou SDK de crash reporting |
| Só usa o Google Drive **se você conectar**, e envia para **a sua conta** | Não vende, aluga ou compartilha dados com terceiros para marketing |

---

## 1. Quem é o responsável pelos dados

O ThirdEye é desenvolvido e distribuído por **DungeonDev Labs** ("nós"), que atua como controlador das
informações tratadas pelo aplicativo na forma descrita nesta política.

O app foi projetado para funcionar de forma **local**: os dados das suas câmeras e as gravações ficam no seu
aparelho. Não mantemos servidores, banco de dados ou painéis com informações dos usuários. O único envio
para fora do aparelho que o app é capaz de fazer é para o **Google Drive da conta que você autorizar** — e
apenas quando você ativa esse recurso.

## 2. Quais dados o app trata

| Dado | Onde fica | Para que serve |
| --- | --- | --- |
| Endereço/IP, porta, protocolo, usuário e senha das câmeras; marca, modelo e canais | Somente no aparelho, no armazenamento privado do app | Conectar, autenticar e exibir as câmeras |
| Parâmetros de vídeo (resolução, codec, taxa de quadros), presets e patrulhas PTZ | Somente no aparelho | Manter a qualidade do stream e mover a câmera |
| Vídeos gravados (arquivos MP4) e o índice das gravações | Armazenamento privado do app (memória interna ou cartão SD) | Guardar e reproduzir as gravações da rotina |
| Preferências da rotina: horários, duração dos blocos, dias de retenção, destino do arquivo | Somente no aparelho | Executar a gravação automática do jeito que você configurou |
| E-mail e nome de exibição da Conta Google conectada | Somente no aparelho | Mostrar qual conta está conectada ao Drive |
| Token de acesso do Google (OAuth) | Gerenciado pelo Google Play Services no aparelho; o app não grava o token | Enviar, baixar e apagar vídeos no seu Drive sem pedir login toda vez |
| Preferências de envio: enviar automaticamente, apenas em Wi-Fi, apagar do aparelho após enviar | Somente no aparelho | Respeitar o seu consumo de dados e de espaço |
| QR Code de compartilhamento da câmera | Gerado na hora, na tela; só existe em arquivo se você salvar/compartilhar | Transferir a configuração de uma câmera para outro aparelho |
| Resultado do diagnóstico de rede (teste de conexão com a câmera) | Exibido na tela; não é enviado para lugar nenhum | Ajudar a descobrir por que uma câmera não conecta |
| Digital / PIN do aparelho | Processado pelo próprio Android; o app nunca recebe nem armazena esses dados | Confirmar ações sensíveis (iniciar/parar a gravação contínua) |

O app não solicita nome, CPF, telefone, endereço, data de nascimento, localização, contatos, SMS,
arquivos pessoais nem microfone.

## 3. O que o app não faz

- **Não temos servidor.** Nenhum dado das câmeras ou das gravações passa por nós.
- **Não há login no app.** Não criamos conta, perfil ou identificador de usuário.
- **Sem publicidade e sem rastreamento.** O app não inclui SDKs de anúncios, analytics, attribution ou
  crash reporting (por exemplo: Firebase, AdMob, Facebook SDK).
- **Sem venda de dados.** Não vendemos, alugamos nem cedemos dados a terceiros.
- **Sem coleta de localização.** O app não pede permissão de localização; para encontrar câmeras na rede ele
  usa apenas a rede local (Wi-Fi/Ethernet) à qual o aparelho está conectado.

## 4. Integração com o Google Drive (opcional)

O envio para o Google Drive é **opcional** e desligado por padrão. Ele só acontece depois que você toca em
"Conectar" e autoriza o acesso na tela do Google.

**Qual permissão pedimos ao Google:** apenas o escopo
`https://www.googleapis.com/auth/drive.file`. Com ele o app **só enxerga os arquivos e pastas que ele mesmo
criou** — não consegue listar, abrir ou alterar os outros arquivos da sua conta.

**O que é enviado:**

- os vídeos que você gravou, dentro de uma pasta do app (por exemplo `ThirdEye/…`);
- o nome e o tamanho dos arquivos, para o Drive organizar as pastas por dia;
- o e-mail e o nome de exibição da conta, apenas para mostrar na tela qual conta está conectada.

Também consultamos o espaço livre do Drive para avisar quando o armazenamento estiver acabando, e apagamos
os vídeos mais antigos que passarem do prazo de retenção configurado na rotina. Essas exclusões atingem
somente arquivos criados pelo ThirdEye.

**O que é enviado ao Google fora do Drive:** nada além dos dados padrão que o Android/Google Play já troca
com o Google para instalar e manter o app atualizado (tratados pela própria Google, segundo as políticas
dela).

> **Como revogar.** Dentro do app: *Configurações → Google Drive → Desconectar*. Fora do app: acesse
> [myaccount.google.com/permissions](https://myaccount.google.com/permissions) e remova o acesso do
> ThirdEye. Os vídeos já enviados continuam no seu Drive até você apagá-los.

## 5. Compartilhamento com terceiros

| Com quem | O que | Quando |
| --- | --- | --- |
| Google (Google Drive / Google Play Services) | Os vídeos e o e-mail da conta, conforme descrito no item 4 | Somente se você conectar sua conta do Google |
| Fabricante do aparelho / provedor do sistema (backup do Android) | Cópia dos dados do app, se o backup automático estiver ligado no aparelho | Conforme a configuração de backup do seu Android |
| Autoridades públicas | Nada — não temos dados para fornecer; o app não envia informações para nós | — |

Não há transferência internacional de dados por parte do desenvolvedor, porque não recebemos dados. Quando
você usa o Google Drive, o tratamento é feito pela Google nas regiões em que ela opera e conforme a política
de privacidade dela.

## 6. Por quanto tempo os dados ficam e como apagar

- **Vídeos no aparelho:** ficam até você apagar, até o espaço acabar ou até vencer o prazo de retenção
  configurado na rotina (que apaga automaticamente os mais antigos).
- **Vídeos no Google Drive:** ficam na sua conta até você apagar no app, no Drive ou até vencer o prazo de
  retenção configurado.
- **Configuração das câmeras e preferências:** ficam no aparelho enquanto o app estiver instalado.

**Como apagar:**

1. **Uma gravação:** tela *Gravações* → selecione o vídeo → excluir (apaga do aparelho e, se estiver no
   Drive, também do Drive).
2. **Uma câmera:** toque na câmera → editar → excluir. Isso remove IP, usuário e senha salvos.
3. **Conta do Google:** *Configurações → Google Drive → Desconectar* (o app apaga o e-mail, o nome e o
   estado de conexão) e revogue o acesso em
   [myaccount.google.com/permissions](https://myaccount.google.com/permissions).
4. **Tudo:** desinstalar o app remove as configurações e os vídeos guardados na memória do aparelho. Vídeos
   já enviados ao Drive precisam ser apagados lá.
5. **Backup do Android:** se o seu aparelho mantém backup automático, pode existir uma cópia dos dados do
   app no backup da sua Conta Google. Ela é controlada por você em *Configurações do Android → Google →
   Backup*.

## 7. Segurança

- Os dados das câmeras e as preferências ficam no armazenamento privado do app, protegido pelo sandbox do
  Android e pela criptografia do aparelho. Outros apps não conseguem ler esses arquivos.
- O acesso ao Google Drive usa OAuth 2.0 do Google; o token é gerenciado pelo Google Play Services e não é
  gravado pelo ThirdEye.
- Vídeos salvos no aparelho ficam em pasta privada do app e só são compartilhados quando você usa a opção
  de abrir/compartilhar (via `FileProvider` do Android).
- As ações sensíveis da rotina (iniciar/parar a gravação contínua) podem ser confirmadas com a sua digital
  ou o PIN do aparelho.

> **Atenção às câmeras.** Muitas câmeras IP usam HTTP ou RTSP *sem criptografia (TLS)* na rede local. Nesse
> caso, o vídeo e as credenciais trafegam na sua rede sem criptografia e podem ser interceptados por quem
> estiver nela. Recomendamos manter uma rede Wi-Fi confiável, trocar a senha padrão da câmera, desabilitar o
> acesso externo (UPnP / port forwarding) e, se precisar acessar de fora, usar uma VPN em vez de expor a
> câmera na internet.

## 8. Permissões do Android e para que servem

| Permissão | Por quê |
| --- | --- |
| Internet e estado da rede/Wi-Fi | Conectar às câmeras da sua rede e ao Google Drive quando você autoriza |
| Serviço em primeiro plano (`FOREGROUND_SERVICE` / `SPECIAL_USE`) | Manter a gravação contínua rodando em segundo plano, com aviso permanente na barra de notificações |
| Notificações | Mostrar o aviso da gravação em andamento e o resultado dos envios |
| Manter ativo (`WAKE_LOCK`) | Evitar que o aparelho durma no meio de uma gravação |
| Iniciar após reiniciar (`RECEIVE_BOOT_COMPLETED`) | Religar a rotina de gravação depois que o celular reinicia ou o app é atualizado |
| Câmera | Somente para **ler o QR Code** de importação de câmeras. O app não tira fotos nem grava vídeos com a câmera do celular |

## 9. Crianças e adolescentes

O ThirdEye é uma ferramenta de monitoramento de câmeras para uso doméstico/profissional e **não é destinado
a menores de 18 anos**. Não coletamos intencionalmente dados de crianças ou adolescentes. Se você é
responsável legal e acredita que um menor usou o app, basta desinstalá-lo ou apagar os dados conforme o item
6 — não guardamos informações em nossos sistemas para excluir.

Lembrete importante: se as câmeras alcançarem áreas com outras pessoas (funcionários, visitantes, vizinhos,
áreas comuns de condomínio), o tratamento das imagens é de sua responsabilidade como controlador, inclusive
quanto a avisos e base legal adequada.

## 10. Seus direitos (LGPD e GDPR)

Como o app não envia dados para nós, a maior parte do controle já está nas suas mãos: você pode ver,
alterar e apagar as informações diretamente nas telas do aplicativo. Ainda assim, a Lei Geral de Proteção de
Dados (Lei nº 13.709/2018) e, para usuários na União Europeia, o GDPR, garantem direitos que você pode
exercer entrando em contato conosco:

- confirmação de que tratamos dados seus e acesso a eles;
- correção de dados incompletos, inexatos ou desatualizados;
- anonimização, bloqueio ou eliminação de dados desnecessários ou excessivos;
- portabilidade dos dados (no app, isso é feito exportando as câmeras por QR Code);
- eliminação dos dados tratados com consentimento e revogação desse consentimento (por exemplo, desconectando
  o Google Drive);
- informação sobre compartilhamento de dados (descrito no item 5);
- oposição a um tratamento e petição à autoridade de proteção de dados (no Brasil, a
  [ANPD](https://www.gov.br/anpd/)).

Bases legais que utilizamos: execução do serviço que você solicitou (art. 7º, V da LGPD) e consentimento
(art. 7º, I), dado na hora de conectar o Google Drive. Não fazemos tratamento para marketing nem
perfilamento.

Respondemos pedidos em até **15 dias** pelo canal de contato do item 12. Podemos pedir informações
adicionais apenas para confirmar a identidade do solicitante.

## 11. Alterações desta política

Podemos atualizar esta política para refletir mudanças no app, em requisitos legais ou nas lojas de
aplicativos. A data de "última atualização" no topo deste documento sempre indica a versão vigente, e a
versão atual ficará disponível neste mesmo endereço. Mudanças relevantes também serão informadas nas notas
de atualização do app na Play Store.

## 12. Contato

- **Desenvolvedor:** DungeonDev Labs
- **E-mail:** luidy.moura.dev@gmail.com
- **Aplicativo:** ThirdEye (`app.dungeondevlabs.thirdeye`) — Android

Este é o mesmo e-mail informado na ficha do app na Google Play Store e serve para dúvidas sobre privacidade,
pedidos de titular e solicitações de exclusão de dados.

---

*Política de Privacidade do ThirdEye · versão de 3 de novembro de 2026 · DungeonDev Labs*

*Documento redigido em português. Se houver tradução para outro idioma, a versão em português prevalece.*


