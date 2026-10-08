# Koushin 🌙

O Koushin é um aplicativo leve para a **bandeja do Windows** que lê o que você está assistindo no **mpv** e exibe no **Discord Rich Presence** (capa, episódio e progresso). Se você entrar no **AniList/MyAnimeList**, ele também pode sincronizar seu progresso.

A ideia é simples: **baixar → executar → esquecer que está ali**.

---

<p align="center">
  <img src="./assets/discord-rpc.png" width="400" alt="Prévia do Discord Rich Presence do Koushin">
</p>

---

## Recursos ✨

### Discord Rich Presence
- 🎬 Mostra o título do anime + episódio no Discord
- 🖼️ Usa a capa do AniList quando disponível
- ⏱️ Mostra progresso/tempo e atualiza ao avançar ou voltar na reprodução
- ⏸️ Reprodução pausada aparece como pausada

### Integração com AniList/MAL (opcional)
- 🔐 Login com um clique pela bandeja do sistema
- ✅ Sincroniza seu progresso no AniList/MAL quando você chega a **~80% assistido**
- 🪪 Ícone opcional do seu perfil do AniList no Discord (um ícone do MAL poderá ser adicionado em uma atualização futura)
- 🔁 Se o anime estiver como **Concluído** / **Repetindo** no AniList/MAL, o Discord mostrará **Assistindo novamente**

### Qualidade de vida
- 🛑 **Selecionar anime correto…** permite corrigir manualmente uma detecção incorreta
- ⚠️ Avisos opcionais de episódios filler (animefillerlist.com)
- 🔄 Verificador de atualizações integrado
- 🪟 Opção de iniciar com o Windows + atalho no Menu Iniciar (para aparecer na Pesquisa do Windows)

### Simulwatching (hospedar + participar) 🧑‍🤝‍🧑
- Hospede uma sessão e compartilhe seu estado de reprodução com amigos
- Entre na sessão de um amigo e acompanhe o estado pela bandeja + Discord
- Quem entrar pode opcionalmente **Sincronizar meu AniList** a partir dos eventos de progresso de 80% do anfitrião
- Funciona pela internet (pode exigir encaminhamento de porta; UPnP/NAT-PMP é tentado automaticamente quando possível)

---

## Download / instalação 📥

1. Acesse **Releases**: https://github.com/flugeru/Koushin-PTBR/releases/tag/v1.0.0
2. Baixe **`Koushin.exe`**
3. Execute (não é necessário instalar)

O Koushin ficará na **bandeja do sistema**.

---

## Configuração do mpv (obrigatória) 🎞️

O Koushin conversa com o mpv através do canal IPC. Faça isso uma vez:

1. Pressione `Win + R` → digite `%AppData%\\mpv`
2. Crie ou edite `mpv.conf`
3. Adicione esta linha:

```conf
input-ipc-server=\\.\pipe\mpv-pipe
```

4. Reinicie o mpv

### Alternativa: iniciar o mpv com IPC uma vez

```bash
mpv.exe --input-ipc-server=\\.\pipe\mpv-pipe "seu-anime.mkv"
```

---

## Primeiro uso / menu da bandeja 🧷

Clique com o botão direito no ícone da bandeja para acessar recursos como:

- **Entrar no AniList…** / **Sair do AniList**
- **Ativar Rich Presence do Discord**
- **Mostrar perfil do AniList no Discord**
- **Avisar sobre episódios filler**
- **Selecionar anime acorreto…** (correção manual)
- **Executar ao iniciar o Windows**
- **Simulwatching** (Hospedar / Entrar / Parar)
- **Verificar atualizações…**
- **Sair**

Na primeira execução, o Koushin também cria um atalho no Menu Iniciar para aparecer na Pesquisa do Windows.

---

## Login no AniList (opcional) 🔐

No menu da bandeja: **Entrar no AniList…**

Isso habilita:
- sincronização do progresso em ~80%
- exibição opcional do seu perfil no Discord
- capas/metadados melhores quando disponíveis

---

## Simulwatching (Hospedar / Entrar) 🧑‍🤝‍🧑

### Hospedar
1. Bandeja → **Simulwatching → Hospedar uma sessão…**
2. Uma pequena página do navegador será aberta para você escolher um **código** (3–18 letras/números)
3. Você receberá um convite no formato `IP:PORTA` + seu **código**
4. Envie essas informações para seu amigo

Se seu amigo não conseguir conectar, talvez seja necessário encaminhar essa porta TCP para seu PC no roteador (o Koushin tenta UPnP/NAT-PMP, mas isso não é garantido).

### Entrar
1. Bandeja → **Simulwatching → Entrar em uma sessão…**
2. Uma pequena página do navegador será aberta
3. Digite o `IP:PORTA` do anfitrião e o código

Enquanto estiver conectado:
- seu Discord + bandeja acompanham o estado do anfitrião
- **Sincronizar meu AniList** fica disponível para quem entrou na sessão

### Participantes
O Koushin mostra uma contagem atualizada de **Participantes** no status do Simulwatching (anfitrião + participantes).

---

## Variáveis de ambiente (opcional) ⚙️

Se quiser alterar os padrões:

- `MPV_PIPE` — caminho do canal IPC do mpv (padrão: `\\.\pipe\mpv-pipe`)
- `POLL_MS` — intervalo de consulta do mpv em milissegundos (mínimo de ~200)
- `HTTP_USER_AGENT` — user agent usado nas requisições ao AniList

---

## Onde o Koushin armazena os dados 🗂️

O Koushin armazena configurações e associações na pasta de configuração do usuário (AppData). Alguns arquivos típicos:

- `auth.json` (token do AniList + configurações)
- `overrides.json` (seleções manuais de anime)
- `koushin.log` (log de depuração)

---

## Solução de problemas 🛠️

### O status do Discord não aparece
- Verifique se o **Discord para desktop** está aberto
- Discord → Configurações → Privacidade de atividade → ative **Compartilhar minha atividade**

### O Rich Presence do Discord está desativado
- Bandeja → **Ativar Rich Presence do Discord**
- Quando desativado, o Koushin continuará atualizando a descrição da bandeja e sincronizando o AniList (se ativado), mas não atualizará/limpará a atividade do Discord.

### O mpv não foi detectado
- Confirme se `input-ipc-server=\\.\pipe\mpv-pipe` está no seu `mpv.conf`
- Reinicie o mpv depois de editar o arquivo

### Anime incorreto / correspondência errada
- Use **Selecionar anime correto…** no menu da bandeja para fixar a entrada correta do AniList

### Avisos de filler incorretos / tudo aparece como filler
- Se o animefillerlist.com não tiver uma página correspondente para a série, o Koushin ignora os avisos de filler para aquele anime (ele não marcará tudo como filler).

### O episódio parece estar um número abaixo (começa em 0)
- Alguns grupos de release nomeiam episódios como `E00..E12`. O Koushin detecta esse padrão e ajusta para `1..13`.

### O Simulwatching não consegue conectar
- A causa mais comum é a falta de encaminhamento da porta no roteador do anfitrião.

---

## Compilar a partir do código-fonte 🧰

```bash
git clone https://github.com/flugeru/Koushin-PTBR.git
cd Koushin-PTBR
go mod tidy
go build -trimpath -ldflags="-H=windowsgui" -o Koushin.exe
```

> A opção `-trimpath` remove caminhos locais do binário. O build recomendado não usa packers ou obfuscação.

---

## Licença 📄

MIT
