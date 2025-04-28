# Sistema Integrado de Gestão Médica - NEXSUS
## 1. Visão Geral
Criar uma aplicação web que armazene dados de faturamento em um banco de dados robusto, analisando-os utilizando técnicas de data science e inteligência artificial e apresentando os resultados e insights em um dashboard interativo acessível de forma segura em qualquer dispositivo. O sistema ainda salvará os dados em um banco de dados firebird dos aplicativos SUS. Desenvolver uma aplicação web para gestão de atendimentos médicos com integração de diversas fontes de dados (PDF, XLSX, webservices e arquivos TXT). A aplicação fará o processamento, tratamento e consolidação dos dados em um banco central (Nexsus) e usará técnicas de Data Science e Inteligência Artificial para gerar análises e dashboards interativos. O sistema será desenvolvido em conformidade com as normas da LGPD, garantindo segurança, privacidade e rastreabilidade.

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
- **Dependências:** PyPDF2, openpyxl, pandas, requests, fdb.

## 2. Arquitetura e Tecnologias
### Back-end e Segurança:
*	•	Framework Principal: Django + Django REST Framework (DRF) O Django já vem configurado com proteções embutidas (contra CSRF, XSS, SQL Injection etc.) e, usando o DRF, você conseguirá estruturar APIs RESTful seguras para a comunicação com o front-end.
*	•	Autenticação e Autorização:
+	Implementaremos uma autenticação robusta utilizando JSON Web Tokens (JWT) ou OAuth2 para garantir que somente usuários autorizados acessem os dados.
+	Será adotado um sistema de controle de acesso baseado em papéis (RBAC), para definir quais operações cada tipo de usuário pode executar.
*	•	Banco de Dados: Utilizaremos o PostgreSQL para base produção e SQLite para base desenvolvimento.
+	Conexões via TLS para garantir a confidencialidade em trânsito.
+	Mecanismos de criptografia e backups seguros para proteção dos dados em repouso.
+	•	Integração de IA e Ciência de Dados:
+	Utilizaremos bibliotecas como Pandas para limpeza e manipulação dos dados.
+	Scikit-learn ou TensorFlow/Keras podem ser aplicados para construir modelos preditivos ou de classificação com base nos dados armazenados.
+	Estruturar rotinas periódicas (por exemplo, via cron jobs ou tarefas agendadas com o Celery) para processar os dados, gerar métricas e criar relatórios automáticos.
+	•	Boas Práticas de Segurança Adicionais:
+	Validação e sanitização completa de todas as entradas no lado do cliente e do servidor.
+	Testes de penetração utilizando ferramentas especializadas para identificar e corrigir vulnerabilidades.
+	Implementação de logs centralizados e monitoramento para detecção precoce de atividades suspeitas.
###Front-end e Dashboard Interativo:
+  •	Framework e Biblioteca:
+  Tecnologias utilizadas html, css e javascript.
  
+  •	Componentes de Visualização:
+ 	Serão utilizadas bibliotecas de gráficos interativos como Chart.js para exibir relatórios analíticos e dashboards. Esse componente pode oferecer funcionalidades de filtragem, seleção de período e personalização dos gráficos, permitindo que o usuário explore os dados de diferentes ângulos.
•	Comunicação com o Back-end:
+  front-end deve consumir as APIs RESTful do back-end, utilizando chamadas seguras (HTTPS, tokens de autenticação) para manusear e exibir os dados de forma dinâmica.com websockets para atualizações em tempo real nos gráficos.
Integração de IA e Ciência de Dados:
+	Pipeline de Dados e Relatórios Analíticos:
+	Extração e Transformação: scripts automatizados que periodicamente extraiam os dados do banco, façam limpeza e transformações necessárias.
+	Análise e Modelagem:
+	Algoritmos de machine learning para identificar padrões, prever tendências ou segmentar dados.
+	Relatórios analíticos que sumarizem resultados, quais podem ser disponibilizados de forma interativa no dashboard e exportáveis para formatos como PDF ou CSV.
+•	Feedback e Alertas:
+	Notificações no sistema para alertar os usuários quando determinados indicadores alcançarem valores críticos ou quando novas análises forem geradas.

## 2.1 – Levantamento de Requisitos

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

  
## 3. Fluxo Geral da Aplicação
1.	Acesso e Autenticação: Usuários acessam o dashboard via web e efetuam login. O sistema utiliza JWT ou outro método seguro, garantindo acesso somente a usuários autenticados.
2.	Interação e Visualização: O front-end, usando frameworks modernos, consome as APIs seguras do back-end e exibe um dashboard interativo com gráficos e relatórios, responsivos em qualquer dispositivo.
3.	Análise e Atualização dos Dados: Em paralelo, processos de IA e ciência de dados analisam os dados armazenados, atualizando periodicamente os relatórios e identificando insights relevantes (como tendências, anomalias ou predições).
4.	Feedback e Segurança: Todas as comunicações são realizadas por HTTPS, e os mecanismos de logs e monitoramento garantem a integridade do sistema, permitindo identificar e reagir rapidamente a qualquer incidente.

## 4. Módulos do Sistema
A aplicação ficará organizada em torno de um módulo principal (main) que integrará e disparará as execuções dos demais módulos:
1.	Módulo Main: Responsável por iniciar e orquestrar todos os módulos do sistema. Essa camada gerencia o fluxo de trabalho e a execução sequencial ou paralela dos módulos conforme a demanda.
2.	Módulo 1 – Processamento de PDF para Atendimento:
Ler arquivos em PDF.
Extrair os campos: DATA_ATEND, COD_PAC, COD_PROC_AUREO, PROC_AUREO e VALOR_AUREO.
Inserir esses dados na tabela Atendimento da base Aureo.
3.	Módulo 2 – Processamento de XLSX para Cadastro de Pacientes:
Ler planilhas Excel, identificar duplicidades e completar campos vazios utilizando dados de registros já existentes.
Inserir/atualizar os dados na tabela Paciente com campos como: COD_PAC, CNS_PAC, CPF, NOME, DTNASC, SEXO, RACA, NACIONALIDADE, CODLOG, LOGRADOURO, NUMERO, COMPL, BAIRRO, MUNICIPIO, CEP, TELEFONE.
4.	Módulo 3 – Integração com Webservice do CNES:
Baixar dados do webservice do CNES.
Armazenar em Profissional os campos: CNS_PROF, NOME_PROF, CBO_PROF e CH_PROF.
5.	Módulo 4 – Integração com API ViaCEP:
Usar a biblioteca viacep para obter os dados do endereço, e inserir na tabela Cep os campos: CEP, COD_LOG, LOGRADOURO, BAIRRO e IBGE.
6.	Módulo 5 – Atualização via Webservice CADWEB:
Consultar o webservice CADWEB para validar e corrigir dados ausentes ou incorretos.
Atualizar os campos CNS_PAC (na tabela Paciente) e CNS_PROF (na tabela Profissional).
7.	Módulo 6 – Cadastro de Estabelecimento:
Permitir que o usuário cadastre manualmente ou confirme os dados do estabelecimento, salvando CNES_ESTAB e NOME_ESTAB na tabela Estabelecimento.
8.	Módulo 7 – Cadastro de Usuário:
Tela para criação de novo usuário, armazenando USUARIO e SENHA na tabela Usuario.
9.	Módulo 8 – Auditoria de Acessos:
Capturar e armazenar, em tempo real, informações de acesso dos usuários (tabela Auditoria com os campos USUARIO, DATA_ACESSO e HORA_ACESSO).
10.	Módulo 9 – Importação de Procedimentos via Arquivo TXT:
Fornecer uma interface para o usuário indicar a localização de um arquivo TXT.
Ler e inserir os dados na tabela Procedimento.
11.	Módulo 10 – Geração de Inserts na Tabela Produção:
Inserir registros na tabela Producao com o mapeamento dos campos conforme regra de negócio:
Exemplo:
PRD_UID recebe CNES_ESTAB
PRD_CMP recebe um valor padrão (ex.: "*")
PRD_CNSMED recebe CNS_PROF
PRD_CBO recebe CBO_PROF
Para os campos PRD_FLH e PRD_SEQ, gerar numerações automáticas com formatação (ex.: 000 e 00, com increments e reinícios conforme especificado) utilizando um dicionário para guardar os últimos valores por PRD_CNSMED.
Demais campos recebem valores conforme o mapeamento descrito no enunciado.
12.	Módulo 11 – Integração com Banco Firebird:
Conectar ao banco Firebird (usuário SYSDBA, senha masterkey).
Realizar inserts da tabela Producao para a tabela S_PRD no banco Firebird, mapeando os mesmos campos.
13.	Módulo 12 – Geração de Estatísticas Financeiras:
Processar os dados armazenados para gerar relatórios e análises financeiras, utilizando técnicas de Data Science e algoritmos de IA para identificar tendências e gerar insights.
14.	Módulo 13 – Dashboard Interativo:
Gerar um dashboard interativo, responsivo e criado com HTML, CSS e JavaScript.
Exibir as estatísticas financeiras, com gráficos dinâmicos (utilizando bibliotecas como Chart.js, D3.js ou Plotly) e filtros para exploração dos dados.

## 5. Telas da Aplicação
O sistema terá as seguintes telas, projetadas para oferecer uma experiência de uso intuitiva e segura:
+	Tela de Login: Acesso seguro com autenticação via JWT ou OAuth2.
+	Tela de Recuperação de Senha: Fluxo para redefinir senha, com validações e envio de e-mail se necessário.
+	Tela CRUD: Para gerenciamento completo de registros (atendimentos, pacientes, profissionais, etc.).
+	Tela Dashboard: Exibição dos relatórios financeiros, gráficos interativos e insights de análise de dados.
+	Tela de Importação de Dados: Interface para seleção de arquivos (PDF, XLSX, TXT) e integração via webservices.

## 6. Considerações Finais
+	Integração Contínua / Deploy: Recomenda-se a utilização de Docker para containerização, pipelines CI/CD (por exemplo, via GitHub Actions) e deploy em um ambiente Cloud seguro.
+	Testes e Validação: Desenvolva testes automatizados (unitários e integrados) para cada módulo, garantindo a qualidade do código e a segurança contra vulnerabilidades.
+	Evolução do Sistema: Com o MVP implementado, novas funcionalidades (novos dashboards, aprimoramentos dos modelos de IA e Data Science) poderão ser incorporadas, sempre com monitoramento e auditoria para atender novos requisitos legais e de negócio.
    Essa proposta unifica o projeto apresentado anteriormente com os novos requisitos para a gestão de atendimentos médicos, garantindo uma solução robusta, segura e que traz insights valiosos para a tomada de decisões.
    Gostaria de aprofundar algum dos módulos específicos, discutir estratégias para a integração com os webservices ou quem sabe explorar ideias para os modelos preditivos? Posso também detalhar como configurar cada parte da infraestrutura ou como estruturar os testes automatizados para garantir a qualidade e a segurança da aplicação.






