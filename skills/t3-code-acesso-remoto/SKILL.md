---
name: t3-code-acesso-remoto
description: Configura o T3 Code (app desktop) no PC Windows para ser usado remotamente pelo celular via T3 Connect (relay gerenciado), com alternativas Tailscale e rede local. Use quando pedirem "usar o T3 Code pelo celular", "acesso remoto do T3 Code", "parear T3 Code com o celular", "T3 Connect".
---

# T3 Code: acesso remoto pelo celular

Fonte oficial: https://github.com/pingdotgg/t3code/blob/main/docs/user/remote-access.md

## Visão geral

O PC é o "host": ele roda o servidor e os agentes (Claude Code, Codex). O celular é só cliente.
O host precisa ficar **ligado, sem suspender, com o T3 Code aberto**.

Rotas disponíveis (o app usa a primeira que responder):

| Rota | Quando usar | Comando / onde |
|---|---|---|
| **T3 Connect** (recomendada) | Qualquer rede (5G, Wi-Fi), sem abrir porta no roteador | Desktop: Settings → Sharing & access → T3 Connect. CLI: `t3 up` |
| Tailscale HTTPS | Já usa Tailscale nos dois aparelhos | `t3 serve --tailscale-serve` ou `t3 pair --tailscale` |
| Rede local | Celular no mesmo Wi-Fi | Ativar *Network access* ou `t3 serve --lan` / `t3 up --lan` |
| SSH gerenciado | Host remoto Linux/Mac Apple Silicon (não serve para PC Windows) | Adicionar host SSH no app desktop |

## Passo a passo (T3 Connect, validado em Windows 11)

### 1. Instalar/atualizar no PC
```powershell
winget install T3Tools.T3Code --accept-package-agreements --accept-source-agreements
```
Se já estiver instalado, o winget atualiza. Alternativa sem instalar: `npx t3@latest`.
O T3 Code precisa de ao menos um agente logado: `claude auth login` ou `codex login`.

### 2. Abrir o app e ligar o T3 Connect
1. Abrir **T3 Code (Beta)**. A primeira abertura após atualizar pode demorar ~30 s na tela de logo.
2. Engrenagem (canto inferior esquerdo) → **Sharing & access**.
3. Em **T3 Connect**, clicar **Sign in** e fazer login (Apple, GitHub, Google, Microsoft ou e-mail).
   **O login é feito pelo usuário**; o agente não digita credenciais.
4. Confirmar: a chave do T3 Connect fica ligada e aparece "Tunnel connected" e "1 of 3 tunnels in use".
   Cada conta liga até 3 máquinas (plano pago do T3 Chat aumenta).

### 3. Conectar o celular
1. Instalar o app **T3 Code** (iOS/Android).
2. Entrar com a **mesma conta** usada no PC.
3. Em Settings → *Add environment*, na seção **"Or use the managed relay"**, o host aparece com bolinha verde e "Connected". Deixar a chave ligada e tocar em ✓.
4. Aba **Chats** → abrir projeto → enviar mensagem de teste. Se o agente responder, está concluído.

Não é necessário escanear QR nem preencher endereço/código: isso é só para conexão direta (LAN/Tailscale).

### 4. Manter o PC acessível
O PC precisa não suspender. Configuração do usuário (o agente não altera configurações do sistema):
```powershell
powercfg /change standby-timeout-ac 0
```
Em notebook, a tampa fechada ainda suspende, a menos que se mude a ação da tampa.
Reverter: `powercfg /change standby-timeout-ac 30`.

## Segurança
- Links de pareamento e códigos são como senhas: não colocar em screenshots, logs ou issues.
- Cada dispositivo novo precisa de um link novo (`t3 pair` gera sem reiniciar o servidor).
- Revogar acessos: Sharing & access → *Revoke others*, ou `t3 auth`.

## Solução de problemas
- Host não aparece no celular: conferir se é a mesma conta; deixar o T3 Code aberto no PC; ver "Tunnel connected" em Sharing & access.
- App demora a abrir no PC após atualização: aguardar até ~30 s.
- Erro do T3 Connect: ver a página de troubleshooting linkada no guia oficial.

## Quando for um agente executando
- Dá para abrir o app e navegar até Sharing & access por computer-use, mas o **login** e o **app do celular** são sempre do usuário.
- Não alterar configurações de energia do Windows: passar o comando ao usuário.
