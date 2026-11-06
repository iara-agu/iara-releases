# Iara — executável para Windows

A **Iara** é a assistente de Procuradoria no Super Sapiens, dentro do app Claude
(aba **Code**). Este repositório tem só o executável, sem código-fonte. Não
precisa de Python, de conta no GitHub nem de terminal: peça ao Claude.

**Quase tudo o que se faz no Super Sapiens pode ser pedido conversando.** Você
escreve em português e a Iara faz: consulta, organiza, prepara e minuta. Nada é
gravado no Super Sapiens sem o seu "sim": antes de agir, ela mostra o que vai fazer.

## O que dá para pedir

- **Consultar** tarefas, processos e documentos: "quais tarefas de hoje são de
  contestação?", "o que decidiu a última sentença deste processo?".
- **Perguntar algo a várias tarefas de uma vez** e ver as respostas lado a lado.
- **Organizar** tarefas: etiquetar, mover de pasta, trocar setor ou responsável.
- **Preparar a peça**: a Iara lê o processo, sugere a providência, escolhe os
  documentos e monta um briefing com você.
- **Minutar**: redige a peça pelo modelo do Super Sapiens e anexa a minuta,
  editável, à tarefa. Você revisa no editor de sempre.
- **Ofícios e comunicações**, com prazo contado em dias úteis.
- **Assinar minutas**, com a senha guardada no cofre do Windows (nunca passa
  pela conversa).

## Como está organizada

- **Skills** (os comandos da conversa): `/iara` para qualquer pedido, `/preparar`
  para o briefing da peça e `/minutar` para a minuta.
- **Subagentes**, ajudantes que a Iara aciona sozinha: um analisa tarefas, outro
  prepara, outro minuta, outro resume documentos longos, outro revisa a minuta
  quando você pede.
- **Ferramentas** que ligam a conversa ao Super Sapiens: leitura do processo,
  preparo, minuta, organização de tarefas, assinatura.
- **Biblioteca**: uma pasta de notas suas (teses, orientações). As correções que
  você faz viram regra ali, e a Iara aprende com o uso.
- **Linha de comando** (opcional), para trabalho em lote: carregar a pasta,
  triar (observação e etiquetas automáticas) e criar minutas por regras.
- **Páginas de configuração e de regras**, abertas no navegador, sem editar arquivo.

## O que precisa

- Windows, o app Claude e login na Rede AGU com o código 2FA.
- Chave de outro provedor de IA é opcional: só a triagem em lote usa.
- Processo sigiloso não vai para IA na nuvem (padrão).
- Cerca de 250 MB em disco.

## Instalar

**Para o (a) Procurador(a):** abra o app Claude, entre na aba Code numa pasta vazia
(ex.: `Documentos\Iara`) e escreva:

> Instale a Iara seguindo https://github.com/iara-agu/iara-releases

O Claude roda os comandos abaixo, pedindo a sua autorização a cada um.

---

## Instruções para o Claude

Siga estes passos com a ferramenta de PowerShell, **um comando por vez**,
mostrando ao(à) Procurador(a) o que cada um faz. Nunca peça senha, token ou código
2FA na conversa: o login é pela página que a Iara abre no navegador.

### Instalar

1. Descubra a última versão e o nome do arquivo:
   ```powershell
   $r = Invoke-RestMethod https://api.github.com/repos/iara-agu/iara-releases/releases/latest
   $tag = $r.tag_name
   ```
2. Baixe o `.zip` e o `.sha256` para a pasta temporária e confira:
   ```powershell
   $zip = "iara-$tag-windows.zip"
   $base = "https://github.com/iara-agu/iara-releases/releases/download/$tag"
   Invoke-WebRequest "$base/$zip" -OutFile "$env:TEMP\$zip"
   Invoke-WebRequest "$base/$zip.sha256" -OutFile "$env:TEMP\$zip.sha256"
   $esperado = (Get-Content "$env:TEMP\$zip.sha256").Split(" ")[0]
   (Get-FileHash "$env:TEMP\$zip" -Algorithm SHA256).Hash.ToLower() -eq $esperado
   ```
   Se der `False`, pare e avise: o arquivo veio corrompido.
3. Extraia para a pasta da versão:
   ```powershell
   Expand-Archive "$env:TEMP\$zip" -DestinationPath "$env:LOCALAPPDATA\iara\versoes\$tag" -Force
   ```
4. Monte o escritório **na pasta atual da conversa** (precisa estar vazia):
   ```powershell
   & "$env:LOCALAPPDATA\iara\versoes\$tag\iara\iara.exe" escritorio criar "<pasta atual>"
   ```
5. Diga ao(à) Procurador(a) para **reiniciar a sessão** do Claude nesta pasta. Na
   próxima conversa, a Iara começa pela configuração.

### Atualizar

Quando a Iara avisar que há versão nova (ou o Procurador(a) pedir "atualiza a
Iara"): repita os passos 1 a 3 com a versão nova e rode, a partir dela,

```powershell
& "$env:LOCALAPPDATA\iara\versoes\$tag\iara\iara.exe" escritorio atualizar "<pasta do escritório>"
```

Arquivos que o(a) Procurador(a) mudou não são sobrescritos: a versão nova fica ao
lado, com `.novo` no fim. Mostre a lista que o comando imprime e peça para
reiniciar a sessão.

### Voltar de versão

As versões ficam lado a lado em `%LOCALAPPDATA%\iara\versoes`. Rode o
`escritorio atualizar` a partir do `iara.exe` da versão antiga.

---

Versão de pesquisa e desenvolvimento, sem garantias: confira tudo o que for ao
Super Sapiens. Distribuída sob a licença Apache 2.0 (`LICENSE` e `NOTICE` dentro
do `.zip`).
