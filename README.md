# Medical Management System - Aureo

![Python](https://img.shields.io/badge/python-3.8+-blue.svg)
![Django](https://img.shields.io/badge/django-4.0-brightgreen.svg)
![PostgreSQL](https://img.shields.io/badge/postgresql-13+-blue.svg)
![LGPD](https://img.shields.io/badge/LGPD-compliant-green.svg)

## Índice
1. [Visão Geral](#1-visão-geral)
2. [Requisitos](#2-requisitos)
   - [Funcionais](#21-requisitos-funcionais)
   - [Não Funcionais](#22-requisitos-não-funcionais)
3. [Arquitetura](#3-arquitetura)
4. [Diagramas](#4-diagramas)
   - [Casos de Uso](#41-diagrama-de-casos-de-uso)
   - [Dados (DER)](#42-diagrama-de-dados-der)
   - [Classes](#43-diagrama-de-classes)
5. [Módulos](#5-módulos-do-sistema)
6. [Telas](#6-telas)
7. [Instalação](#7-instalação)
8. [Configuração](#8-configuração)
9. [Uso](#9-uso)
10. [Contribuição](#10-contribuição)
11. [Licença](#11-licença)

## 1. Visão Geral
Sistema web integrado para gestão de atendimentos médicos que processa dados de múltiplas fontes (PDF, Excel, webservices) e armazena em banco de dados central (Aureo), com análise via técnicas de data science e IA para geração de relatórios e dashboards interativos.

**Stack Tecnológica:**
- **Front-end:** HTML5, CSS3, JavaScript
- **Back-end:** Python 3.8+ com Django 4.0
- **Banco de Dados:** PostgreSQL/SQLite
- **Integrações:** CNES, ViaCEP, CADWEB

## 2. Requisitos

### 2.1 Requisitos Funcionais

| ID    | Descrição | Prioridade |
|-------|-----------|------------|
| RF01  | Autenticação com três níveis de usuário (Super, Admin, Operador) | Alta |
| RF02  | Processamento de arquivos PDF para tabela Atendimento | Alta |
| RF03  | Processamento de arquivos XLSX para tabela Paciente | Alta |
| RF04  | Integração com webservice CNES | Média |
| RF05  | Geração automática de sequências para produção | Alta |
| RF06  | Dashboard interativo com visualizações financeiras | Alta |

### 2.2 Requisitos Não-Funcionais

| ID    | Descrição | Métrica |
|-------|-----------|---------|
| RNF01 | Tempo de resposta | < 2s para operações comuns |
| RNF02 | Disponibilidade | 99.5% uptime |
| RNF03 | Segurança | Criptografia AES-256 |
| RNF04 | Compatibilidade | Chrome, Firefox, Edge |

## 3. Arquitetura
