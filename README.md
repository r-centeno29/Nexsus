# Sistema Integrado de Gestão Médica - AUREO
## Índice
1. [Visão Geral](#1-visão-geral)
2. [Requisitos](#2-requisitos)
3. [Arquitetura](#3-arquitetura)
4. [Diagramas](#4-diagramas)
5. [Módulos](#5-módulos)
6. [Modelos de Dados](#6-modelos-de-dados)
7. [Telas](#7-telas)
8. [Instalação](#8-instalação)
9. [Configuração](#9-configuração)
10. [Uso](#10-uso)
11. [Roadmap](#11-roadmap)
12. [Contribuição](#12-contribuição)
13. [Licença](#13-licença)

## 1. Visão Geral
Sistema completo para gestão de atendimentos médicos com:

- ✅ Processamento de múltiplos formatos (PDF, Excel, TXT)
- 🔗 Integração com webservices oficiais (CNES, ViaCEP, CADWEB)
- 🗃️ Banco de dados centralizado PostgreSQL
- 📊 Análise de dados com Python e IA
- 📈 Dashboards interativos
- 🔒 Total conformidade com LGPD

**Stack Tecnológica:**
- **Frontend:** HTML5, CSS3, JavaScript (ES6+), Chart.js
- **Backend:** Python 3.9+, Django 4.2
- **Banco de Dados:** PostgreSQL 14+ (produção)
- **Integrações:** CNES, ViaCEP, CADWEB, Firebird
- **Dependências:** PyPDF2, openpyxl, pandas, requests

## 2. Requisitos

### 2.1 Funcionais

#### Autenticação
| ID | Descrição | Status |
|----|-----------|--------|
| RF01 | Login multi-nível (Super, Admin, Operador) | ✅ |
| RF02 | Recuperação de senha com token | ✅ |

#### Processamento
| ID | Descrição | Status |
|----|-----------|--------|
| RF03 | Importação PDF → Atendimento | ✅ |
| RF04 | Processamento XLSX → Paciente | ✅ |
| RF05 | Integração CNES → Profissional | ✅ |

### 2.2 Não-Funcionais

| ID | Descrição | Métrica |
|----|-----------|---------|
| RNF01 | Performance | <2s resposta |
| RNF02 | Segurança | AES-256 |
| RNF03 | Disponibilidade | 99.5% uptime |

## 3. Arquitetura

### 4.1 Não-Funcionais

| ID | Descrição | Métrica |
|----|-----------|---------|
| RNF01 | Performance | <2s resposta |
| RNF02 | Segurança | AES-256 |
| RNF03 | Disponibilidade | 99.5% uptime |

```mermaid
graph TD
    A[Frontend] --> B[Django]
    B --> C[PostgreSQL]
    B --> D[CNES API]
    B --> E[ViaCEP]
    B --> F[Firebird]
    C --> G[Data Science]
    G --> H[Dashboards]

## 4. Diagramas
### 2.2 Não-Funcionais

| ID | Descrição | Métrica |
|----|-----------|---------|
| RNF01 | Performance | <2s resposta |
| RNF02 | Segurança | AES-256 |
| RNF03 | Disponibilidade | 99.5% uptime |
