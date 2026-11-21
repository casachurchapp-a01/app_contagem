# Casa Church · Controle de Lugares

App para os obreiros marcarem os lugares do templo em tempo real.
Instala direto pelo navegador (sem App Store nem Play Store) e usa uma **Planilha Google** como banco de dados. **Custo: zero.**

## O que tem

- **Mapa do Templo:** púlpito, corredor central, Ala Oeste e Ala Leste, F1 a F14 com 11 lugares por ala (308 no total)
- **Toque na cadeira:** alterna entre livre (verde) e ocupado (vermelho)
- **Toque no "F" da fileira:** abre a fileira ampliada, com lugares numerados e botões para ocupar ou liberar a fileira inteira
- **Aviso de lotação:** mostra a % e para qual ala e fileiras direcionar as pessoas
- **Contadores:** Livres, Ocupados, Total e % de Lotação
- **Tempo real:** todos os obreiros veem as mesmas marcações (atualiza a cada 3 segundos)
- **Sem sinal no templo?** As marcações ficam na fila do celular e sobem sozinhas quando a internet voltar
- **Modo Edição (só líder):** adicionar fileira ao fundo (F15, F16…), remover a última, mudar lugares por ala e salvar para todos
- **Relatório:** presentes, livres, lotação por ala e por fileiras, mapa de ocupação, **Exportar PDF** e **Enviar no WhatsApp**
- **Encerrar culto (só líder):** trava o mapa e guarda os números na planilha
- **Histórico:** cada toque fica registrado na aba Log (quem, onde e quando)

---

## Passo 1 · Criar a planilha (10 minutos, uma vez só)

1. Entre na conta Google da igreja e crie uma **Planilha em branco** (ex.: "Casa Church Lugares")
2. Menu **Extensões → Apps Script**
3. Apague o que estiver lá e cole todo o conteúdo do arquivo `apps-script/Codigo.gs`
4. Clique no disquete para salvar
5. No topo, escolha a função **setup** e clique em **Executar**
   - O Google vai pedir autorização. Clique em *Revisar permissões*, escolha a conta da igreja, depois *Avançado → Acessar (não seguro)*. É o seu próprio script, pode confiar
6. Volte na planilha: vão aparecer as abas **Config**, **Cultos** e **Log**
7. Na aba **Config**, **troque os PINs**:
   - `pinObreiro` (padrão 1234): para toda a equipe
   - `pinLider` (padrão 4321): só para o líder dos obreiros

## Passo 2 · Publicar o backend

1. No Apps Script: **Implantar → Nova implantação**
2. Na engrenagem, escolha **App da Web**
3. Preencha:
   - Executar como: **Eu**
   - Quem pode acessar: **Qualquer pessoa**
4. **Implantar** e copie a URL que termina em `/exec`

> Mexeu no código depois? Use **Implantar → Gerenciar implantações → editar (lápis) → Nova versão**. Assim a URL continua a mesma.

## Passo 3 · Colocar a URL no app

**Opção A, recomendada:** abra o `index.html`, procure por `API_URL: ''` no começo do script e cole a URL entre as aspas:

```js
const CONFIG = {
  API_URL: 'https://script.google.com/macros/s/SEU_CODIGO/exec'
};
```

Assim todo obreiro já entra conectado.

**Opção B:** deixe em branco e cole a URL em *Conexão com a planilha*, na tela de login de cada celular.

## Passo 4 · Publicar no GitHub Pages

1. Crie um repositório no GitHub (ex.: `casa-church-lugares`)
2. Envie todos os arquivos desta pasta (a pasta `apps-script` pode ir junto, não atrapalha)
3. **Settings → Pages →** branch `main`, pasta `/ (root)` → **Save**
4. Em 1 ou 2 minutos o app fica em `https://SEU-USUARIO.github.io/casa-church-lugares/`

## Passo 5 · Instalar no celular

- **iPhone (Safari):** abrir o link → botão **Compartilhar** → **Adicionar à Tela de Início**
- **Android (Chrome):** abrir o link → menu **⋮** → **Instalar app** (ou *Adicionar à tela inicial*)

Pronto: ícone da Casa Church na tela, abre em tela cheia, igual app de loja.

---

## Teste de 5 minutos com a equipe

1. Líder e dois obreiros instalam e entram com o PIN
2. Um obreiro toca em **Começar culto** com a data e hora de hoje. Os outros escolhem a mesma data e hora (ou tocam no culto em *Cultos recentes*) e caem no mesmo mapa
3. Cada um marca lugares e confere se aparecem no celular do outro em até 3 segundos
4. Um obreiro liga o modo avião, marca 3 lugares (aparecem com contorno tracejado), desliga o modo avião e vê tudo sincronizar
5. Líder entra em **Modo Edição**, adiciona uma fileira, salva e confere a F15 nos outros celulares
6. Líder abre **Relatório**, envia no WhatsApp e encerra o culto
7. Confira a aba **Cultos** e a aba **Log** na planilha

## Perguntas rápidas

**É grátis mesmo?** Sim. O Google Apps Script grátis dá conta folgado de uma equipe de obreiros num culto.

**Quantos obreiros ao mesmo tempo?** Uns 10 tranquilo. Se forem muitos mais, aumente `atualizacaoSeg` na aba Config para 5.

**O logo é o oficial?** O `logo.svg` é uma versão desenhada a partir da referência. Para usar o arquivo oficial, substitua o `logo.svg` (mesmo nome) e, se quiser, os ícones `icon-192.png` e `icon-512.png`.

**Atualizei o app e o celular mostra a versão antiga.** Troque `v1` por `v2` no começo do `sw.js` e publique de novo.

**Dá pra usar sem planilha?** Dá. Sem URL configurada, o app roda em *Modo local*: funciona offline, mas só naquele celular. PINs do modo local: obreiro 1234, líder 4321.
