# Iara — IA para a Procuradoria no Super Sapiens

A **Iara** conduz o trabalho do procurador no Super Sapiens a partir de uma conversa no app
Claude: lê o processo, tria, prepara, minuta pelo modelo do órgão, assina e lança a atividade.
Você pede em português; nada é gravado no Super Sapiens sem o seu "sim".

## Por que a Iara

Copiar trechos do processo num chat de IA resolve uma pergunta. A Iara foi feita para o
trabalho inteiro, com as travas que o serviço público exige.

| | Chat de IA comum (copiar e colar) | Iara |
|---|---|---|
| Acesso ao processo | O que você colar | Lê o Super Sapiens direto: juntadas, partes, tarefas, atividades |
| Processo sigiloso | Depende de você não colar | Bloqueado por padrão antes de qualquer envio à IA |
| Gravar no Super Sapiens | Manual | Feito pela Iara, só depois do seu "sim" a um texto que mostra o antes e o depois |
| Minuta | Texto solto para colar | Criada pelo modelo do Super Sapiens, editável no editor de sempre |
| Rotina da unidade | Repetida a cada conversa | Guardada: roteiros e procedimentos valem nas próximas vezes |
| Suas teses e orientações | Coladas de novo | Lidas da sua biblioteca de notas, com a fonte citada |

A API do Super Sapiens também pode ser usada diretamente — por scripts próprios ou por uma IA com
acesso livre a ela. A diferença está no que fica entre a IA e o sistema:

| | Uso direto da API (script próprio ou IA com acesso livre) | Iara |
|---|---|---|
| Caminho de cada ação | Qualquer chamada, do jeito que o script ou a IA montar | Cada ação tem a sua ferramenta, com as suas travas: ler documento confere o sigilo, minuta sai pela ferramenta de minuta, assinatura pela de assinatura; a consulta livre fica para listar, buscar e contar |
| Texto do processo | Vem junto nas respostas, sem conferir sigilo | Retirado das consultas livres; só chega pela leitura que confere o sigilo antes |
| Alterações | Executadas na hora, como foram montadas | Descritas em português pelo programa (como está → como fica), com nomes no lugar de números, e só executadas com o seu "sim"; no máximo 100 por vez |
| Senha e assinatura | A credencial circula pelo script ou pela conversa | A Iara recusa qualquer senha num pedido ao Super Sapiens; assinatura só pela ferramenta própria, com a senha guardada no Windows |
| Saber como fazer | Cada um descobre as rotas e os campos | Procedimentos já testados no Super Sapiens (juntar, peticionar, mover, etiquetar, ofício...) e catálogo da API, que avisa quando a versão muda |
| Registro | Depende de quem escreveu o script | Cada alteração fica registrada no seu computador |

E a **iAGU**, a IA do próprio Super Sapiens? Ela trabalha dentro da minuta. A Iara também minuta, e
vai além:

| | iAGU | Iara |
|---|---|---|
| Onde atua | Dentro da minuta | Na minuta e em todo o caminho: carregamento, triagem, preparo, assinatura, juntada ou peticionamento |
| Suas notas e teses | Não usa | Lê a sua biblioteca, cita a fonte e guarda as suas correções |
| Várias tarefas de uma vez | Não permite | Mesma pergunta a muitas tarefas, respostas lado a lado; triagem pelo seu roteiro |
| Rotina da unidade | Não permite | Roteiros, procedimentos e "lembre disso" que valem nas próximas vezes |
### Segurança

- **Sigilo antes de tudo.** Processo com sinal de sigilo — ou sem informação sobre isso — não vai para
  IA na nuvem. A trava está no próprio programa, não depende de lembrar: a Iara confere antes de
  entregar qualquer conteúdo do processo.
- **Nada é gravado sem o seu "sim".** Antes de etiquetar, mover, criar, assinar ou peticionar, a Iara
  mostra em português como está e como vai ficar. O "sim" vale só para aquele pedido, por 5 minutos;
  no máximo 100 alterações por vez. Peticionar, só com aceite expresso.
- **Cada ação pelo seu caminho.** Ler documento, minutar, assinar e peticionar têm ferramentas
  próprias, com as suas travas; a consulta livre ao Super Sapiens serve para listar, buscar e contar,
  e o texto do processo não vem por ela.
- **Senha fora da conversa.** O login é numa página que abre no seu navegador; a senha vai direto ao
  Super Sapiens e fica guardada protegida pelo Windows. A assinatura de minutas usa essa senha
  guardada, sem passar pela conversa.
- **Resumo conferido.** Ao resumir documento longo, cada trecho citado como literal é conferido com
  o original; o que não confere é recusado. O resumo fica marcado como da Iara, não do Super Sapiens.
- **Nada sai do seu computador.** O registro de uso guarda só qual ferramenta rodou e quanto tempo
  levou; relatos de problema passam por filtro que tira CPF, CNPJ, número de processo e e-mail.
- **Instalação conferida.** O instalador confere se o arquivo baixado é exatamente o publicado, e cada
  versão só é publicada depois de passar nos testes.

### Do carregamento ao peticionamento

```
carregar ──► triar ──► preparar ──► minutar ──► revisar ──► assinar ──► juntar / peticionar
```

1. **Carregar**: a Iara lê o processo e guarda uma ficha dele — as etapas seguintes não começam do zero.
2. **Triar**: pelo seu roteiro (veja abaixo), com a proposta de etiqueta, observação ou pasta para
   cada tarefa; só grava as linhas que você aprovar.
3. **Preparar**: decide com você a providência e monta o briefing (teses, documentos, notas da
   biblioteca).
4. **Minutar**: redige e cria a minuta pelo modelo do Super Sapiens, editável. Peças com texto
   pronto (como as do Pró-Estratégia) também.
5. **Revisar, assinar e lançar a atividade**: junta ao processo ou peticiona eletronicamente,
   encerrando a tarefa.

Documento longo é lido uma vez e vira um resumo organizado que serve a todas as etapas; quando o
Super Sapiens já tem o Formulário de IA do documento, a Iara usa o dele. Cada etapa é opcional: dá
para pedir a minuta direto, com uma instrução sua.

### Rotinas estruturadas

- **Roteiro de triagem seu**: você define as perguntas (de múltipla escolha ou abertas) e o que fazer
  com cada resposta — etiqueta, observação, pasta. Serve, por exemplo, para análise de relevância. A
  Iara lê os processos e responde; a proposta segue as suas regras ao pé da letra, e resposta
  duvidosa fica para você decidir.
- **Fluxos de várias etapas**, como o ciclo do Pró-Estratégia: nota juntada ao processo sem encerrar
  e, depois, petição protocolada encerrando a tarefa — cada passo com a sua confirmação.
- **"Lembre disso"**: o procedimento que deu certo fica guardado para as próximas conversas;
  "daqui pra frente, na contestação, sempre olhe X" vira regra sua.

### Biblioteca em formato livre

- Uma pasta com as suas notas, do jeito que você já escreve — no Obsidian ou em qualquer editor de texto.
- Não exige formato: a nota vale pelo título. Quem quiser, marca etiqueta ou assunto. O que a Iara não
  entende vira aviso, não erro.
- PDF, Word e páginas salvas na pasta viram nota com um pedido.
- O briefing diz de qual nota e seção veio cada tese. Suas correções viram regra na nota.

### Reserva: triagem automática em lote

Para volumes grandes, a Iara tem uma triagem automática pela linha de comando, que o Claude roda
para você: acha o ato que move cada tarefa e aplica etiquetas e observação por regras fixas, testadas
antes de salvar; também cria minutas em lote por regras. Ela usa outro provedor de IA (OpenAI,
Maritaca, Anthropic) ou um modelo que roda no próprio computador, sem internet (Ollama) — opção útil
para processo sigiloso. É opcional: o uso diário é todo pela conversa.

## Instalar, passo a passo

Leva uns 15 minutos. Você não precisa saber programar: o Claude faz a parte técnica e pede a sua
autorização antes de cada passo.

**Antes de começar:** um computador com **Windows**, seu usuário e senha da **Rede AGU** com o
código **2FA** à mão, e uma conta no Claude com plano que inclua o **Claude Code**.

1. **Crie uma pasta vazia para a Iara.** Abra o Explorador de Arquivos, entre em **Documentos**,
   clique com o botão direito num espaço vazio → **Novo** → **Pasta** e dê o nome `Iara`.
   Deixe-a vazia.
2. **Instale o app Claude para Windows.** Baixe em <https://claude.ai/download>, instale e entre
   com a sua conta Claude.
3. **Abra a aba Code na pasta da Iara.** No app Claude, clique em **Code** no alto da janela.
   Ao iniciar a conversa, escolha a pasta `Documentos\Iara` que você criou.
4. **Peça a instalação.** Copie a frase abaixo, cole na conversa e envie:

   > Instale a Iara: rode `irm https://github.com/iara-agu/iara-releases/releases/latest/download/instalar.ps1 | iex` nesta pasta.

5. **Autorize.** O Claude vai pedir permissão: clique em **Permitir**. Espere aparecer **"Pronto."**
   (se aparecer "Falta: ...", peça ao Claude para resolver o que falta).
6. **Reinicie a conversa.** Abra uma conversa nova no app Claude, na mesma pasta `Documentos\Iara`.
7. **Primeiro uso.** Escreva `/iara`. A Iara conduz a configuração e abre a página de login no
   navegador: é **lá**, e não na conversa, que você digita a senha e o código 2FA.

Nunca digite senha nem código 2FA na conversa.

## Atualizar

Quando a Iara avisar que há versão nova, responda que sim — ou peça "atualize a Iara". Depois,
abra uma conversa nova na mesma pasta.

O que é seu fica: suas regras, roteiros, notas e configurações não são tocados. Se você tinha
alterado algum arquivo da própria Iara, a sua versão fica guardada e a Iara avisa.

Algo deu errado depois de atualizar? Peça ao Claude: "volte a Iara para a versão anterior (as
versões ficam em `%USERPROFILE%\iara\versoes`; rode o `iara.exe` da anterior com `escritorio
atualizar` nesta pasta)".

---

Versão de pesquisa e desenvolvimento, sem garantias: confira tudo o que for ao Super Sapiens.
Distribuída sob a licença Apache 2.0. Este repositório tem só o programa pronto, sem código-fonte.
