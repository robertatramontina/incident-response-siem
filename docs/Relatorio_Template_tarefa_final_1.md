# Relatório de Investigação - Tarefa 1
## Operation Shadow Pulse: Initial Access

**UC 01480 - Analisar Evidências de Ataques Cibernéticos**

---

## 📋 Informações do Formando

| Campo | Informação |
|-------|------------|
| **Nome Completo** | Roberta Tramontina |
| **Nº de Formando** | |
| **Data de Entrega** | 12/02/2026 |
| **Sessão** | 11 - Initial Access |

---

## 🎯 Sumário Executivo

**Incidente:** Operation Shadow Pulse - Fase 1
**Período Investigado:** 25/12/2025 - 01/01/2026 (Semana 1)
**Severidade:** [ ] Baixa [ ] Média [ ] Alta [ ] Crítica

**Resumo (3-5 linhas):**
```
Durante a fase inicial do incidente foram identificadas múltiplas tentativas de acesso não autorizado provenientes de IPs com histórico malicioso, incluindo um nó de saída Tor, associados a atividades de brute force e scanning. O vetor de entrada está relacionado com tentativas de autenticação remota e exploração de serviços expostos. Não foi confirmada, nesta fase, a comprometimento definitivo de uma conta, porém houve impacto ao nível de aumento de carga, geração de alertas de segurança e risco elevado de intrusão. O incidente indica uma campanha automatizada de reconhecimento e força bruta contra a infraestrutura.
```

---

## 🔍 Lab 0a: Cyber Threat Intelligence (CTI) - 3 pts

### IOCs Validados em Plataformas CTI

| IOC | Plataforma | Malicioso? | País/ASN | Confidence/Detection | Notas |
|-----|-----------|------------|----------|---------------------|-------|
| 185.220.101.45 | AbuseIPDB | [x] Sim [ ] Não | Alemanha / AS60729 | 88% / 6502 reports | IP altamente malicioso, usado como nó de saída Tor, frequentemente associado a brute force | 
| 185.220.101.45 | VirusTotal | [x] Sim [ ] Não | Alemanha / AS60729 | 15/93 | Marcado por múltiplos motores como malicious, associado a RDP brute force |
| 91.219.237.89 | AbuseIPDB | [ ] Sim [x] Não | Hungria | 0% Não encontrado na database | Não existe histórico de abuso registado no AbuseIPDB para este IP |
| 45.155.205.233 | AbuseIPDB | [x] Sim [ ] Não | Russia / AS208677 | 8% / 1604 reports | Brute-Force, Hacking, Web App Attack, Exploited Host |
| update-service.xyz | URLScan | [ ] Sim [x] Não | N/A| Sem resultados | Domínio não possui scans registados no URLScan |
| update-service.xyz | WHOIS | N/A | N/A | Data criação: Not available | WHOIS sem dados disponíveis |

### Evidências (Screenshots)

**Screenshot 1 – AbuseIPDB (185.220.101.45) – Visão Geral**  
![L0a_S1_AbuseIPDB_185.220.101.45](L0a_S1_AbuseIPDB_185.220.101.45.png)

**Screenshot 2 – AbuseIPDB (185.220.101.45) – Reports**  
![L0a_S2_AbuseIPDB_185.220.101.45](L0a_S2_AbuseIPDB_185.220.101.45.png)

**Screenshot 3 – VirusTotal (185.220.101.45)**  
![L0a_S3_VirusTotal_185.220.101.45](L0a_S3_VirusTotal_185.220.101.45.png)

**Screenshot 4 – Tor Exonerator (185.220.101.45)**  
![L0a_S4_TorExonerator_185.220.101.45](L0a_S4_TorExonerator_185.220.101.45.png)

**Screenshot 5 – URLScan (update-service.xyz)**  
![L0a_S5_URLScan_update-service.xyz](L0a_S5_URLScan_update-service.xyz.png)

**Screenshot 6 – WHOIS (update-service.xyz)**  
![L0a_S6_Whois_Domain](L0a_S6_Whois_Domain.png)

### Análise CTI

**Perguntas de Investigação CTI:**

1. **Qual o IP com maior Confidence Score no AbuseIPDB?**
   - Resposta: 185.220.101.45
   - Score: 88%

2. **Algum IP é um Tor exit node?**
   - [x] Sim [ ] Não
   - Qual IP: 185.220.101.45

3. **Quando foi criado o domínio `update-service.xyz`?**
   - Data de criação: Not Available
   - Registrar: N/A

4. **Os IPs pertencem ao mesmo ASN ou país?**
   - [ ] Sim [x] Não
   - Explicação: Os IPs pertencem a países e ASN diferentes (Alemanha, Hungria e Rússia), indicando infraestrutura distribuída.

5. **Com base nos resultados CTI, os IOCs são credíveis como maliciosos?**
   - [x] Sim [ ] Não [ ] Inconclusivo
   - Justificação: Dois IPs apresentam múltiplos reports, alto volume de denúncias e deteções por motores de segurança, incluindo associação a brute force e Tor exit node.

### Conclusões CTI

```
[Resumo de 2-3 parágrafos sobre a validação CTI:
- Que plataformas confirmaram os IOCs como maliciosos?
As plataformas AbuseIPDB e VirusTotal confirmaram atividade maliciosa associada aos IPs 185.220.101.45 e 45.155.205.233, indicando múltiplos reports, classificações como malicious e associação a brute force, ataques web e acessos não autorizados. O URLScan e o serviço WHOIS não apresentaram resultados para o domínio update-service.xyz, o que, em contexto de CTI, pode indicar domínio recente ou utilizado temporariamente em campanhas maliciosas.

- Existe correlação entre os IOCs (mesma campanha, país, ASN)?
Não existe correlação direta ao nível de país ou ASN, uma vez que os IPs pertencem a infraestruturas distintas localizadas na Alemanha, Rússia e Hungria. Contudo, todos estão associados a comportamentos semelhantes (brute force e scanning), sugerindo possível participação numa campanha automatizada distribuída.

- Os IOCs têm histórico de ataques anteriores?
Sim. Os IPs 185.220.101.45 e 45.155.205.233 apresentam milhares de reports no AbuseIPDB e referências históricas a tentativas de brute force, ataques a aplicações web e acessos não autorizados, demonstrando reutilização em atividades maliciosas ao longo do tempo.

- Qual o nível de confiança na validação?]
O nível de confiança é elevado, uma vez que múltiplas plataformas CTI independentes apresentam concordância na classificação maliciosa dos principais IPs e existe coerência entre os tipos de ataques observados.
```

---

## 🛡️ Lab 0b: CVE Research - 3 pts

### Inventário de Software TechNova

| Sistema | Hostname | Software | Versão | Exposição |
|---------|----------|----------|--------|-----------|
| Firewall | FW-01 | pfSense | 2.6.0 | Internet |
| Web Server | WEB01 | IIS | 10.0.17763 | DMZ |
| Web Server | WEB02 | Apache | 2.4.52 | Internet |
| Web Server | WEB02 | PHP | 8.1.2 | Internet |
| Domain Controller | DC01 | Windows Server | 2022 | Interno |
| File Server | FS01 | Windows Server | 2019 | Interno |

### Matriz de Vulnerabilidades

| Software | Versão | CVE ID | CVSS | Descrição | Exploit Público? | Risk Score | Prioridade |
|----------|--------|--------|------|-----------|-----------------|------------|------------|
| Apache | 2.4.52 | CVE-2022-22720 | 9.8 | HTTP Request Smuggling (falha ao fechar ligação em erro, permitindo manipulação de requests) | [ ] Sim [x] Não | 128 | [ ] Baixa [ ] Média [ ] Alta [x] Crítica |
| Apache | 2.4.52 | CVE-2022-23943 | 9.8 | Out-of-bounds write em mod_sed (corrupção de memória; possível crash/RCE) | [ ] Sim [x] Não | 128 | [ ] Baixa [ ] Média [ ] Alta [x] Crítica |
| pfSense | 2.6.0 | CVE-2023-29974 | 9.8 | Permite comprometer contas via requisitos fracos de password | [ ] Sim [x] Não | 128 | [ ] Baixa [ ] Média [ ] Alta [x] Crítica |
| Windows Server 2019 | DC | CVE-2020-1472 | 10.0 | Zerologon – Netlogon Elevation of Privilege (elevação de privilégios até Domain Admin) | [x] Sim [ ] Não | 120 | [ ] Baixa [ ] Média [ ] Alta [x] Crítica |
| Windows Server | 2022 | CVE-2021-36934 | 7.8 | Permissões incorretas no SAM permitem leitura de hashes e escalada para SYSTEM (HiveNightmare) | [x] Sim | 98 | [ ] Baixa [ ] Média [x] Alta [ ] Crítica |

**Fórmula Risk Score:** `(CVSS × 10) + (Exploit Público × 20) + (Internet Exposed × 30)`

## Lab 0b – Pesquisa de Vulnerabilidades (NVD + Exploit-DB)

### Apache HTTP Server

**Screenshot 7 – CVE-2022-22720**  
Vulnerabilidade de HTTP Request Smuggling no Apache HTTP Server 2.4.52 e anteriores.  
CVSS: 9.8 (Crítico)

![Apache CVE-2022-22720](L0b_S1_NVD_Apache_CVE-2022-22720.png)

**Screenshot 8 – CVE-2022-23943**  
Out-of-bounds write no módulo mod_sed, permitindo potencial corrupção de memória e possível RCE.  
CVSS: 9.8 (Crítico)

![Apache CVE-2022-23943](L0b_S2_NVD_Apache_CVE-2022-23943.png)

**Screenshot 9 – Pesquisa no Exploit-DB (Apache CVEs)**  
Não foram encontrados exploits públicos diretamente associados a estes CVEs no Exploit-DB.

![ExploitDB Apache](L0b_S3_ExploitDB_Apache_Search.png)

---

### pfSense 2.6.0

**Screenshot 10 – CVE-2023-29974**  
Permite comprometer contas de utilizador devido a requisitos fracos de palavra-passe.  
CVSS: 9.8 (Crítico)

![pfSense CVE-2023-29974](L0b_S4_NVD_pfSense_CVE-2023-29974.png)

**Screenshot 11 – Pesquisa no Exploit-DB**  
Não foram encontrados exploits públicos associados a este CVE.

![ExploitDB pfSense](L0b_S5_ExploitDB_pfSense_CVE-2023-29974.png)

---

### Windows Server 2019

**Screenshot 12 – CVE-2020-1472 – Zerologon**  
Falha no protocolo Netlogon que permite elevação de privilégios até Domain Admin.  
CVSS: 10.0 (Crítico)

![Windows CVE-2020-1472](L0b_S6_NVD_Windows_CVE-2020-1472.png)

**Screenshot 13 – Exploit Público – Zerologon**  
Exploit disponível no Exploit-DB para Windows (Netlogon Elevation of Privilege).

![ExploitDB Zerologon](L0b_S7_ExploitDB_Windows_Zerologon.png)

---

### Windows Server 2022

**Screenshot 14 - CVE-2021-36934 – HiveNightmare / SeriousSAM**  
Permissões incorretas nos ficheiros SAM permitem leitura de hashes de passwords e possível escalada para privilégios SYSTEM.  
CVSS: 7.8 (Alta)

![Windows CVE-2021-36934](L0b_S8_NVD_Windows_CVE-2021-36934.png)

**Screenshot 15 – Pesquisa no Exploit-DB – HiveNightmare**  
Pesquisa realizada no Exploit-DB não retornou resultados para este CVE.

![ExploitDB HiveNightmare](L0b_S9_ExploitDB_Windows_CVE-2021-36934.png)

**Screenshot 16 – Exploit Público – HiveNightmare (GitHub PoC)**  
Embora não exista registo deste CVE no Exploit-DB, foi identificado um Proof of Concept público no GitHub (repositório chron1k/oxide_hive) que demonstra a exploração do CVE-2021-36934, permitindo a leitura das hives SAM/SECURITY/SYSTEM e posterior escalada de privilégios.

![PoC GitHub HiveNightmare](L0b_S10_GitHub_PoC_CVE-2021-36934.png)
---

### Análise de Vulnerabilidades

**Perguntas de Investigação CVE:**

1. **Qual o CVE com maior CVSS score encontrado?**
   - CVE ID: CVE-2020-1472
   - CVSS: 10.0
   - Software afetado: Windows Server 2019 (Domain Controller)

2. **Quantos CVEs críticos (CVSS >= 9.0) afetam a infraestrutura?**
   - Total: 4
   - Lista: CVE-2022-22720 (Apache) | CVE-2022-23943 (Apache) | CVE-2023-29974 (pfSense) | CVE-2020-1472 (Windows Server – Zerologon)

3. **Existe exploit público para algum CVE?**
   - [x] Sim [ ] Não
   - Quantos: 1
   - CVEs com exploit: CVE-2020-1472 (Zerologon)

4. **Que sistema da TechNova está mais vulnerável?**
   - Sistema: Web Server WEB02 (Apache 2.4.52)
   - Justificação: ossui dois CVEs críticos (CVSS 9.8), encontra-se exposto à Internet e é um alvo típico para exploração remota de vulnerabilidades em serviços web.

5. **Qual o vetor de entrada mais provável baseado nos CVEs?**
   - [x] Exploração web (Apache/IIS)
   - [ ] Exploração Windows (PrintNightmare, Zerologon)
   - [ ] Exploração Firewall (pfSense)
   - [ ] Brute Force
   - Justificação: Apesar do CVE-2020-1472 possuir exploit público, o WEB02 encontra-se exposto à Internet e apresenta dois CVEs críticos (CVSS 9.8) exploráveis remotamente, tornando-o o alvo mais provável para exploração inicial. O Domain Controller permanece como sistema de maior impacto caso seja comprometido.


### Conclusões CVE

```
Resumo de 2-3 parágrafos sobre as vulnerabilidades:
- Quais são os CVEs mais críticos encontrados?
A análise de vulnerabilidades permitiu identificar múltiplos CVEs críticos na infraestrutura TechNova, com destaque para o CVE-2020-1472 (Zerologon) em Windows Server, com CVSS 10.0, e os CVEs CVE-2022-22720 e CVE-2022-23943 no Apache HTTP Server, ambos com CVSS 9.8. Foi ainda identificado o CVE-2023-29974 no pfSense 2.6.0, também classificado como crítico. Estes resultados demonstram a presença de vulnerabilidades de elevada severidade em serviços essenciais.

- Que sistemas estão em maior risco?
Os sistemas em maior risco são o Web Server WEB02 (Apache 2.4.52), por se encontrar exposto à Internet e possuir vulnerabilidades críticas exploráveis remotamente, e o Domain Controller DC01, devido ao impacto severo do Zerologon, que pode resultar em comprometimento total do domínio. Apesar de apenas o Zerologon possuir exploit público confirmado no Exploit-DB, a ausência de exploit público para os restantes CVEs não elimina o risco, uma vez que estes podem ser explorados através de ferramentas privadas ou técnicas customizadas.

- Existe sobreposição entre CVEs e o ataque observado?
Embora o ataque observado esteja focado em brute force RDP, existe potencial sobreposição entre as vulnerabilidades identificadas e fases posteriores do ataque, nomeadamente escalada de privilégios e movimento lateral. Recomenda-se aplicação prioritária de patches de segurança para Apache, pfSense e Windows Server, desativação de serviços desnecessários, revisão de políticas de autenticação e reforço da monitorização de eventos de segurança.
```

---

## 🚪 Lab 1: Initial Access - 6 pts

### Análise de Brute Force

**Query DQL Base:**
`data.win.system.eventID: 4625`

**Resultado:** 143 eventos de login falhado

### Tabela de Ataques

| Protocolo | Event ID | Nº Tentativas Falhadas | Nº Sucessos | IP Atacante Principal | Conta Comprometida | Timestamp Compromisso |
|-----------|----------|------------------------|-------------|----------------------|-------------------|---------------------|
| RDP | 4625 / 4624 | 10 | 2 | 91.219.237.89 | svc_backup | 2025-12-28 03:28:45|

### Agregação de IPs Atacantes

| IP Atacante | Nº Tentativas | Usernames Alvo | Validado CTI? |
|-------------|---------------|----------------|---------------|
| 91.219.237.89 | 10 | administrator, admin, root, svc_backup, sql_admin, maria.silva | [ ] Sim [x] Não |
| 203.0.113.50 | 8 | root, administrator, guest, test | [ ] Sim [x] Não |
| 185.220.101.45 | 4 | guest, test, webadmin, pedro.santos | [x] Sim [ ] Não |
| 45.155.205.233 | 4 | administrator, admin, iis_admin | [x] Sim [ ] Não |

### Screenshots Wazuh

**Screenshot 17: Brute Force (Event ID 4625)**
![L1_S1_4625_91.219.237.89](L1_S1_4625_91.219.237.89.png)
![L1_S2_4625_91.219.237.89](L1_S2_4625_91.219.237.89.png)

*Legenda: Dashboard Wazuh detalhando a campanha de brute force do IP 91.219.237.89. A evidência combinada mostra 10 tentativas contra contas administrativas e de serviço, com intervalos irregulares para evitar deteção.*

**Screenshot 18: Login Bem-Sucedido (Event ID 4624)**
![L1_S3_4624_91.219.237.89](L1_S3_4624_91.219.237.89.png)

*Legenda: Evento de login bem-sucedido (4624) da conta svc_backup a partir do IP 91.219.237.89. Identificam-se dois acessos: um via rede (LogonType 3) em 28/12 e outro via RDP (LogonType 10) em 01/01.*

### IOCs Extraídos do SIEM

| Tipo | Valor | Contexto | Fonte | Validado CTI? |
|------|-------|----------|-------|---------------|
| IP | 91.219.237.89 | Brute Force / Sucesso | Wazuh Event 4625/4624 | [ ] Sim [x] Não |
| IP | 185.220.101.45 | Brute Force | Wazuh Event 4625 | [x] Sim [ ] Não |
| IP | 45.155.205.233 | Brute Force | Wazuh Event 4625 | [x] Sim [ ] Não |
| IP | 203.0.113.50 | Brute Force | Wazuh Event 4625 | [ ] Sim [x] Não |
| Conta | svc_backup | Comprometida | Wazuh Event 4624 | N/A |
| Host | WEB01 | Alvo do Ataque | Wazuh agent.name | N/A |

### Perguntas de Investigação Lab 1

1. **Quantas tentativas de brute force foram detetadas no total?**
   - Resposta: 26

2. **Quantos IPs diferentes participaram no ataque?**
   - Resposta: 4

3. **O atacante conseguiu acesso?**
   - [x] Sim [ ] Não
   - Evidência: Identificado o Event ID 4624 (Login Bem-Sucedido) originado pelo IP externo 91.219.237.89.

4. **Qual a conta comprometida?**
   - Conta:svc_backup
   - Tipo: [ ] Domain Admin [x] Service Account [ ] User Account

5. **Qual o timestamp do primeiro compromisso bem-sucedido?**
   - Data/Hora: Dec 28, 2025 @ 03:28:45.000
   - Query DQL usada: data.win.system.eventID: 4624 AND data.win.eventdata.IpAddress: 91.219.237.89

6. **Que técnicas MITRE ATT&CK são aplicáveis?**
   - [x] T1110.001 - Brute Force: Password Guessing
   - [x] T1078 - Valid Accounts
   - [x] T1021.001 - Remote Services: RDP
 

### Timeline - Fase 1 (Initial Access)

| # | Timestamp | Host | Event ID | Evento | IP Origem | MITRE ATT&CK |
|---|-----------|------|----------|--------|-----------|--------------|
| 1 | 25/12/2025 14:30:01 | WEB01 | 4625 | Início do Brute Force (padrão automatizado) | 91.219.237.89 | T1110.001 |
| 2 | 26/12/2025 14:32:03 | WEB01 | 4625 | Tentativas continuam via Nó de Saída Tor | 185.220.101.45 | T1110.001 |
| 3 | 28/12/2025 03:28:45 | WEB01 | 4624 | Login bem-sucedido (Conta Comprometida) | 91.219.237.89 | T1078 |
| 4 | 01/01/2026 04:15:00 | WEB01 | 4624 | Acesso Remoto via RDP (Persistência)| 91.219.237.89 | T1021.001 |


### Análise e Conclusões - Lab 1

```
O incidente iniciou-se a 25 de dezembro de 2025, aproveitando estrategicamente o período de feriados para minimizar a probabilidade de deteção imediata pelas equipas de segurança. Foi identificado um ataque de brute force persistente e distribuído, totalizando 143 tentativas de login falhado (Event ID 4625) contra o servidor WEB01. Embora o volume total seja elevado, a investigação focou-se nos 4 IPs principais que somam 26 tentativas, com destaque para o IP húngaro 91.219.237.89, que demonstrou maior intensidade através de scripts automatizados.

A conta de serviço svc_backup foi comprometida com sucesso a 28 de dezembro. A escolha desta conta sugere que o atacante visava um alvo com privilégios de serviço, que frequentemente possuem passwords mais fracas ou estáticas, facilitando a exploração via password guessing. O incidente destaca-se pela transição deliberada de um LogonType 3 (Network), no momento do compromisso inicial, para um LogonType 10 (RDP) no dia 1 de janeiro, indicando que o atacante estabeleceu uma sessão interativa para preparar os próximos passos de movimentação lateral.

A investigação SIEM correlacionou-se com os dados de CTI, confirmando a participação de infraestrutura maliciosa conhecida, como o nó de saída Tor 185.220.101.45. O impacto inicial é classificado como Crítico, uma vez que o atacante obteve acesso legítimo a um servidor na DMZ utilizando uma conta de serviço, criando uma ponte para a rede interna da TechNova.
```

---

## 📊 Mapeamento MITRE ATT&CK - Fase 1

| Tática | Técnica | ID | Evidência | Severidade |
|--------|---------|-----|-----------|------------|
| Initial Access | Brute Force: Password Guessing | T1110.001 | Event ID 4625 (26 eventos) | [ ] Baixa [ ] Média [ ] Alta [x] Crítica |
| Initial Access | Valid Accounts | T1078 | Event ID 4624 (login svc_backup) | [ ] Baixa [ ] Média [ ] Alta [x] Crítica |
| Initial Access | Remote Services: RDP | T1021.001 | LogonType 10 (RDP) | [ ] Baixa [ ] Média [ ] Alta [x] Crítica |

---

## 🎯 Conclusões Gerais - Tarefa 1

### Resumo de Findings

**CTI (Lab 0a):**
- Total de IOCs validados: 4 IPs e 1 Domínio.
- IOCs confirmados como maliciosos: 2 IPs (185.220.101.45 e 45.155.205.233).
- Plataformas consultadas: AbuseIPDB, VirusTotal, TorExonerator, URLScan e WHOIS.

**CVE (Lab 0b):**
- Total de CVEs identificados: 5
- CVEs críticos (CVSS >= 9.0): 4
- CVEs com exploit público: 1 (CVE-2020-1472 - Zerologon).

**Initial Access (Lab 1):**
- Tentativas de brute force: 26
- IPs atacantes: 91.219.237.89, 203.0.113.50, 185.220.101.45, 45.155.205.233
- Contas comprometidas: 1
- Sistemas afetados: WEB01

### Avaliação de Impacto

**Confidencialidade:** [ ] Nenhum [ ] Baixo [x] Médio [ ] Alto
**Integridade:** [ ] Nenhum [ ] Baixo [ ] Médio [ ] Alto
**Disponibilidade:** [ ] Nenhum [ ] Baixo [ ] Médio [ ] Alto

**Justificação:**
O impacto principal reside na quebra de confidencialidade através do compromisso da conta svc_backup. Embora não tenha havido interrupção de serviço, o atacante obteve acesso legítimo ao sistema, o que permite o roubo de dados ou a preparação de ataques internos mais graves.
### Indicadores de APT

Marque os indicadores de APT observados:
- [x] Ataque coordenado de múltiplos IPs
- [x] Uso de infraestrutura C2 (domínio update-service.xyz)
- [x] Timing estratégico (férias de Natal)
- [x] Foco em contas privilegiadas
- [x] Persistência após compromisso inicial

### Próximos Passos de Investigação

**Para Tarefa 2 (Sessão 12 - Lateral Movement):**
```
1. Investigar se o atacante utilizou a conta svc_backup para aceder a outros servidores (ex: DC01 ou FS01) via RDP ou SMB.
2. Analisar logs de sistema em busca de ferramentas de extração de credenciais (ex: Mimikatz) para elevar privilégios.
3. Verificar se houve criação de novas contas ou persistência em outros sistemas da rede TechNova.
4. Monitorizar o tráfego de saída para detetar possível exfiltração de dados sensíveis a partir do servidor WEB01.```

---

## 📎 Anexos

### Checklist de Entregáveis

- [x] Relatório completo em PDF
- [x] Screenshot 1: AbuseIPDB
- [x] Screenshot 2: VirusTotal/URLScan
- [x] Screenshot 3: NVD/Exploit-DB
- [x] Screenshot 4: Brute Force (4625)
- [x] Screenshot 5: Login Bem-Sucedido (4624)
- [x] Todas as tabelas preenchidas
- [x] Todas as perguntas respondidas
- [x] Mapeamento MITRE ATT&CK completo

### Queries DQL Utilizadas

```
dql
# Query 1: Todos os logins falhados
data.win.system.eventID: 4625

# Query 2: Login falhado de IP específico
data.win.system.eventID: 4625 AND data.win.eventdata.IpAddress: "91.219.237.89"

# Query 3: Login bem-sucedido de IP externo
data.win.system.eventID: 4624 AND data.win.eventdata.IpAddress: "91.219.237.89"
```

### Fontes Consultadas

**CTI:**
- AbuseIPDB: https://www.abuseipdb.com/
- VirusTotal: https://www.virustotal.com/
- URLScan.io: https://urlscan.io/
- WHOIS: https://who.is/

**CVE:**
- NVD: https://nvd.nist.gov/
- Exploit-DB: https://www.exploit-db.com/

**MITRE ATT&CK:**
- https://attack.mitre.org/

---

## ✍️ Declaração de Honra

Declaro que este trabalho foi realizado por mim de forma individual, e que toda a informação externa foi devidamente citada.

**Assinatura:** Roberta Tramontina	
**Data:** 12/02/2026

---

*UC 01480 - Analisar Evidências de Ataques Cibernéticos*
*Tarefa 1 - Initial Access - Sessão 11*
*Técnico/a Especialista em Cibersegurança*
