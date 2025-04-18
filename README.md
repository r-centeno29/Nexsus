# Sistema de Gestão de Atendimentos Médicos Aureo

Este projeto consiste em uma aplicação web integrada, escrita em Python com Django, para a gestão de atendimentos médicos. O sistema processa dados provenientes de diversas fontes (PDF, Excel, webservices e arquivos TXT) e os armazena em um banco de dados central (Aureo). Além disso, utiliza técnicas de Data Science e Inteligência Artificial para geração de relatórios financeiros, insights e dashboards interativos, acessíveis de forma segura e responsiva em qualquer dispositivo, em conformidade com as normas da LGPD.

---

## 4.1 – Definição do Escopo do Projeto

**Objetivo:**  
Desenvolver uma aplicação web que integre módulos de importação e processamento de dados (PDF, XLSX, TXT e webservices) e que:
- Armazene os dados em um banco robusto, centralizando informações em diversas tabelas (Atendimento, Paciente, Profissional, Cep, Procedimento, Produção, Estabelecimento, Usuário e Auditoria).
- Utilize técnicas de Data Science e IA para análise dos dados e geração de relatórios financeiros.
- Exiba os resultados por meio de um dashboard interativo e responsivo.
- Assegure o tratamento seguro dos dados e a conformidade com a LGPD.

**Principais Funcionalidades:**  
- Importação de dados (PDF, Excel, TXT) e integração via webservices (CNES, CADWEB, viacep).  
- Processamento, limpeza, e consolidação dos dados.  
- Geração automática de registros e incrementos nas tabelas (ex.: numeração automática nos campos de Produção).  
- Integração com banco Firebird para replicação dos dados.
- Criação de relatórios e estatísticas financeiras.
- Interface de usuário com telas de login, recuperação de senha, CRUD, dashboard e importação de dados.
- Controle de acesso e auditoria para perfis de usuário: Super, Admin e Operador.

---

## 4.2 – Levantamento de Requisitos

### Requisitos Funcionais
- **Importação e Processamento de Dados:**  
  - Módulo para leitura de arquivos PDF que extraia os campos `DATA_ATEND`, `COD_PAC`, `COD_PROC_AUREO`, `PROC_AUREO` e `VALOR_AUREO` para a tabela Atendimento.  
  - Módulo para leitura de arquivos XLSX, tratamento de duplicidades e atualização de dados na tabela Paciente.  
  - Integração com webservices para obtenção de dados do CNES (tabela Profissional) e CADWEB (atualização dos campos CNS_PAC e CNS_PROF).  
  - Módulo para consulta à API viacep e armazenamento dos dados na tabela Cep.  
  - Módulo para importação de arquivos TXT, carregando dados na tabela Procedimento.
  - Módulo de inserção na tabela Produção, com regras de mapeamento e incremento automático dos campos `PRD_FLH` e `PRD_SEQ`.
  - Integração com banco Firebird para espelhamento dos dados de Produção na tabela S_PRD.
  - Módulo para geração de estatísticas financeiras e dashboard interativo.

- **Interface e Segurança:**  
  - Tela de login com autenticação robusta (JWT ou OAuth2).  
  - Tela de recuperação de senha.  
  - Tela CRUD para gerenciamento de todos os registros.  
  - Tela de importação de dados.  
  - Dashboard interativo com gráficos e filtros dinâmicos.

### Requisitos Não Funcionais
- **Segurança:**  
   - Criptografia dos dados sensíveis (em repouso e em trânsito).  
   - Validação e sanitização de todas as entradas.  
   - Logs e auditorias detalhadas (tabela Auditoria).  
   - Conformidade com a LGPD, garantindo transparência e consentimento.
- **Desempenho e Escalabilidade:**  
   - Utilização de PostgreSQL (ou SQLite para desenvolvimento) com otimizações para consultas.
   - Deploy com Docker e pipelines CI/CD para manter a integridade do sistema.
- **Usabilidade:**  
   - Interface intuitiva, responsiva e compatível com dispositivos móveis.
- **Manutenibilidade:**  
   - Estrutura modular com separação clara de responsabilidades entre os módulos.
   - Testes automatizados para garantir a qualidade e segurança.

---

## 4.3 – Construção do(s) Diagrama(s) de Casos de Uso

Exemplo simplificado de casos de uso (pode ser detalhado em diagramas utilizando [draw.io](https://app.diagrams.net/) ou similar):

- **Administrar Dados:**
  - Ator: **Admin / Super**
  - Caso de uso: Importar dados, corrigir registros, visualizar e gerar relatórios financeiros, auditar acessos.

- **Gestão do Atendimento:**
  - Ator: **Operador**
  - Caso de uso: Consultar atendimentos, cadastrar procedimentos, atualizar informações de pacientes e profissionais.

- **Acesso ao Sistema:**
  - Ator: **Todos os Usuários**
  - Caso de uso: Login, recuperação de senha e gerenciamento de sessão.

*Observação: Incluir diagramas elaborados (em svg/png) na pasta `/docs/figma` ou links para os protótipos.*

---

## 4.4 – Construção dos Documentos de Casos de Uso

Cada caso de uso será detalhado em um documento (pode ser no próprio repositório ou linkado em uma Wiki).  
Exemplo:

### Caso de Uso: Importação de Dados de PDF
- **Ator:** Operador
- **Pré-condições:** O usuário deve estar logado e possuir permissão para importar dados.
- **Fluxo Principal:**  
  1. O usuário acessa a tela de importação.  
  2. Seleciona o arquivo PDF contendo os dados.  
  3. O sistema processa o arquivo, extrai os dados necessários e os insere na tabela Atendimento.  
- **Fluxos Alternativos:**  
  - Caso o arquivo esteja corrompido ou não contenha os dados esperados, o sistema exibe um erro informativo e possibilita nova tentativa.
- **Pós-condições:**  
  - Os dados processados são armazenados corretamente, e o usuário recebe um feedback de sucesso.

*Documentos similares devem ser criados para cada funcionalidade importante do sistema.*

---

## 4.5 – Construção do Diagrama de Dados (DER)

Segue um exemplo textual simplificado do DER. Para uma visualização completa, utilize ferramentas como MySQL Workbench ou Draw.io:

- **Tabelas Principais e Seus Atributos:**

| Tabela          | Principais Atributos                                                   |
|-----------------|------------------------------------------------------------------------|
| Atendimento     | DATA_ATEND, COD_PAC, COD_PROC_AUREO, PROC_AUREO, VALOR_AUREO            |
| Paciente        | COD_PAC, CNS_PAC, CPF, NOME, DTNASC, SEXO, RACA, NACIONALIDADE, ...     |
| Profissional    | CNS_PROF, NOME_PROF, CBO_PROF, CH_PROF                                   |
| Cep             | CEP, COD_LOG, LOGRADOURO, BAIRRO, IBGE                                  |
| Procedimento    | (Campos importados via TXT)                                            |
| Producao        | PRD_UID, PRD_CMP, PRD_CNSMED, PRD_CBO, PRD_FLH, PRD_SEQ, ...             |
| Estabelecimento | CNES_ESTAB, NOME_ESTAB                                                 |
| Usuario         | USUARIO, SENHA                                                         |
| Auditoria       | USUARIO, DATA_ACESSO, HORA_ACESSO                                        |

*Incluir o diagrama em imagem no repositório, no diretório `/docs`.*

---

## 4.6 – Construção do Diagrama de Classes do Modelo de Dados

Exemplo simplificado das classes de domínio:

```plaintext
+---------------------+
|      Atendimento    |
+---------------------+
| - data_atend        |
| - cod_pac           |
| - cod_proc_aureo    |
| - proc_aureo        |
| - valor_aureo       |
+---------------------+

+---------------------+
|      Paciente       |
+---------------------+
| - cod_pac           |
| - cns_pac           |
| - cpf               |
| - nome              |
| - dt_nasc           |
| - sexo              |
| - raca              |
| - nacionalidade     |
| ...                 |
+---------------------+

+---------------------+
|    Profissional     |
+---------------------+
| - cns_prof          |
| - nome_prof         |
| - cbo_prof          |
| - ch_prof           |
+---------------------+


ID	  Descrição	                                                  Módulo
RF01	Ler arquivos PDF e extrair dados de atendimento	              1
---
RF02	Processar arquivos Excel para completar dados de pacientes	  2
---
RF03	Integração com webservice CNES para dados profissionais	      3
---
RF04	Integração com ViaCEP para dados de endereço	                4
---
RF05	Integração com CADWEB para validação de CNS	5
RF06	Cadastro manual de estabelecimentos	6
RF07	Gerenciamento de usuários do sistema	7
RF08	Registro de auditoria de acesso	8
RF09	Processamento de arquivos TXT com procedimentos	9
RF10	Geração automática de registros de produção	10
RF11	Exportação para banco Firebird (S_PRD)	11
RF12	Geração de estatísticas financeiras	12
RF13	Dashboard interativo para análise de dados	13
Requisitos Não-Funcionais
ID	Categoria	Descrição
RNF01	Desempenho	Processar arquivos PDF de até 50 páginas em <5s
RNF02	Segurança	Autenticação de usuários com senha criptografada
RNF03	Usabilidade	Interface intuitiva com seleção de arquivos por diálogo
RNF04	Confiabilidade	Validação de dados antes da inserção no banco
RNF05	Compatibilidade	Suporte a Windows 10+ e principais navegadores
RNF06	Disponibilidade	Sistema operacional 24/7 com tolerância a falhas
RNF07	Capacidade	Armazenar até 1 milhão de registros de atendimento
RNF08	Escalabilidade	Arquitetura que permite aumento de capacidade
