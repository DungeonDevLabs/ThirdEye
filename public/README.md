# public

Arquivos públicos do projeto — documentos que ficam expostos no repositório
[`DungeonDevLabs/ThirdEye`](https://github.com/DungeonDevLabs/ThirdEye) e servem de link oficial
(fora do app).

| Arquivo | Para que serve |
| --- | --- |
| [`politica-de-privacidade.md`](politica-de-privacidade.md) | Política de Privacidade do ThirdEye, usada na ficha do app na Play Store |
| [`servico-em-primeiro-plano.md`](servico-em-primeiro-plano.md) | Texto e roteiro do vídeo para a declaração de `FOREGROUND_SERVICE_SPECIAL_USE` (*Conteúdo do app → Permissões de serviço em primeiro plano*) |

## URL para a Play Console

Com o repositório público, o link direto do documento é:

```
https://github.com/DungeonDevLabs/ThirdEye/blob/main/public/politica-de-privacidade.md
```

Cole essa URL em **Play Console → Conteúdo do app → Política de privacidade**.

> A página precisa abrir **sem login**. Teste em uma janela anônima: se abrir, está ok.
> Também vale colocar o mesmo link na descrição da ficha do app, se quiser.

### Se quiser uma página com "cara de site"

O GitHub Pages só publica a partir da raiz do repositório ou da pasta `/docs` (não da `/public`).
Se um dia fizer questão de um HTML estilizado, crie `docs/index.html` e ative em
**Settings → Pages → Branch `main` / `/docs`**. O `.md` continua sendo a fonte da verdade.

## Contato na política

O e-mail de contato já está definido no item 12 de `politica-de-privacidade.md`:

- **E-mail:** luidy.moura.dev@gmail.com

Se trocar de endereço, atualize o documento **e** use o mesmo e-mail na ficha do app na Play Store — a loja
exige um contato de privacidade funcional e que seja realmente monitorado.

## Como manter atualizada

- Mudou algo no app (nova permissão, novo SDK, novo envio de dados)? Atualize o documento **e** a data de
  "Última atualização" — ela aparece em dois lugares: no topo e no fim do arquivo.
- Só mexa no repositório público se o `keystore.properties` e a pasta `keystore/` continuarem no
  `.gitignore` (eles **nunca** podem ir para um repositório público).

## Respostas para o formulário "Segurança dos dados" (Play Console)

O documento foi escrito para casar com estas respostas:

| Pergunta do formulário | Resposta |
| --- | --- |
| Coleta ou compartilha dados? | **Não coleta** dados para o desenvolvedor. Os vídeos vão para o Drive **do próprio usuário** (o usuário é o destinatário) — declarar "nenhum dado coletado" e explicar no campo livre que a gravação é local/na conta do usuário |
| Dados criptografados em trânsito | Sim para o Google Drive (HTTPS). Para câmeras locais depende do protocolo da câmera (muitas usam HTTP/RTSP sem TLS) — o documento avisa isso no item 7 |
| Dados criptografados em repouso | Sim, no armazenamento privado do app (criptografia do aparelho) |
| Usuários podem solicitar exclusão? | Sim — exclusão direto no app (item 6) + e-mail de contato |
| Dados de menores | Não |
| Rastreamento / publicidade | Não |
| Permissões sensíveis | `CAMERA` apenas para leitura de QR Code; `FOREGROUND_SERVICE_SPECIAL_USE` para gravação contínua (justificar o subtipo no formulário — texto pronto em [`servico-em-primeiro-plano.md`](servico-em-primeiro-plano.md)) |
