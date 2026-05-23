# Análise de Vulnerabilidades Web com Base no OWASP Top 10

## Sobre o Projeto

Este repositório contém o trabalho de conclusão da disciplina de Segurança da Informação, com foco na análise e exploração controlada de vulnerabilidades em aplicações web utilizando o **OWASP Juice Shop** como ambiente de estudo.

**Autores:** Daniel de Souza de Aguiar, Letícia Siguinolfi de Lima  
**Instituição:** Faculdade Donaduzzi - Análise e Desenvolvimento de Sistemas

## Objetivo

Demonstrar, na prática, a exploração de vulnerabilidades críticas em aplicações web com base no **OWASP Top 10 (2021)**:
- SQL Injection (A03)
- Broken Access Control (A01)  
- Cross-Site Scripting (A03)
- Security Misconfiguration (A05)

## Ferramentas Utilizadas

| Ferramenta | Versão | Finalidade |
|:---|:---:|:---|
| Gobuster | 3.8.2 | Enumeração de diretórios |
| sqlmap | 1.10.2 | Automação de SQL Injection |
| Burp Suite | Community | Interceptação de requisições |
| cURL | - | Testes manuais de API |
| Docker | - | Isolamento do ambiente |

## Estrutura do Repositório

```bash
resumo-expandido-owasp-top10/
├── README.md
├── HOW_TO_RUN.md
├── resumo_expandido.pdf
│
├── imagens/
│   ├── sqli_login_bypass.png
│   ├── sqli_tabela_users.png
│   ├── broken_access_admin.png
│   ├── idor_carrinho.png
│   ├── xss_payloads.png
│   ├── xss_confirmacao.png
│   ├── directory_listing_ftp.png
│   ├── metrics_exposed.png
│   ├── sqli_sqlmap_execucao.png
│   └── xss_persistente_alerta.png
│
├── payloads/
│   ├── sqli_payloads.txt
│   ├── xss_payloads.txt
│   ├── idor_endpoints.txt
│   └── security_misconfiguration.txt
│
└── referencias/
    └── referencias.bib
```                          

## Vulnerabilidades Exploradas

- SQL Injection (SQLi)
- Broken Access Control (IDOR)
- Cross-Site Scripting (XSS)
- Security Misconfiguration
- Server-Side Request Forgery (SSRF)
- Remote Code Execution (RCE)
- OS Command Injection
- Authentication Bypass


