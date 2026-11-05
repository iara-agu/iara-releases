# Iara — executável para Windows

A **Iara** é a assistente do procurador no Super Sapiens, dentro do app Claude
(aba **Code**). Este repositório tem só o executável, sem código-fonte. Não
precisa de Python, de conta no GitHub nem de terminal: peça ao Claude.

**Para o procurador:** abra o app Claude, entre na aba Code numa pasta vazia
(ex.: `Documentos\Iara`) e escreva:

> Instale a Iara seguindo https://github.com/iara-agu/iara-releases

O Claude roda os comandos abaixo, pedindo a sua autorização a cada um.

---

## Instruções para o Claude

Siga estes passos com a ferramenta de PowerShell, **um comando por vez**,
mostrando ao procurador o que cada um faz. Nunca peça senha, token ou código
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
5. Diga ao procurador para **reiniciar a sessão** do Claude nesta pasta. Na
   próxima conversa, a Iara começa pela configuração.

### Atualizar

Quando a Iara avisar que há versão nova (ou o procurador pedir "atualiza a
Iara"): repita os passos 1 a 3 com a versão nova e rode, a partir dela,

```powershell
& "$env:LOCALAPPDATA\iara\versoes\$tag\iara\iara.exe" escritorio atualizar "<pasta do escritório>"
```

Arquivos que o procurador mudou não são sobrescritos: a versão nova fica ao
lado, com `.novo` no fim. Mostre a lista que o comando imprime e peça para
reiniciar a sessão.

### Voltar de versão

As versões ficam lado a lado em `%LOCALAPPDATA%\iara\versoes`. Rode o
`escritorio atualizar` a partir do `iara.exe` da versão antiga.

---

Versão de pesquisa e desenvolvimento, sem garantias: confira tudo o que for ao
Super Sapiens. Distribuída sob a licença Apache 2.0 (`LICENSE` e `NOTICE` dentro
do `.zip`).
