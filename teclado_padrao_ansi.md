# Configuração de Teclado ANSI (US) com Acentos em Português no Fedora

Este guia explica como configurar um teclado ANSI (US) no Fedora para digitar caracteres em português (como `ç`, `á`, `ã`) usando dead keys (teclas mortas) ou Compose Key.

## 📋 Pré-requisitos
- Fedora Linux (testado na versão 40+)
- Acesso sudo
- Ambiente GNOME (ou outro ambiente desktop)

## 🛠️ Solução 1: Layout US Internacional com Dead Keys

### Passo a Passo

1. **Defina o layout internacional com dead keys:**
   ```bash
   sudo localectl set-x11-keymap us intl
   ```

2. **Aplique as configurações imediatamente:**
   ```bash
   setxkbmap -layout us -variant intl
   ```

3. **Verifique se as dead keys estão ativas:**
   ```bash
   xev | grep keysym
   ```
   
   Pressione ', `, ~ e verifique se aparecem:
    * dead_acute (para ')
    * dead_grave (para `)
    * dead_tilde (para ~)

4. Teste os acentos:
    * ' + a → á
    * ` + a → à
    * ~ + a → ã
    * " + u → ü
    * ç → Use AltGr + ,

## 🔧 Solução 2: Usar Compose Key (Alternativa)
1. Habilite a Compose Key:
  ```bash
  gsettings set org.gnome.desktop.input-sources xkb-options "['compose:ralt']"
  ```
  (Configura o Alt direito como Compose Key)

2. Combinações úteis:
  * Compose + ' + a → á
  * Compose + ~ + a → ã
  * Compose + , + c → ç

# 🚨 Solução de Problemas

| Problema            | Solução                                                                 |
|---------------------|-------------------------------------------------------------------------|
| `'a` em vez de `á`  | Execute `setxkbmap -layout us -variant intl`                            |
| `~a` em vez de `ã`  | Verifique se o pacote `x11-xkb-utils` está instalado                    |
| `ç` não funciona    | Use `AltGr + ,`, ou mapeie manualmente com `xmodmap`                    |
