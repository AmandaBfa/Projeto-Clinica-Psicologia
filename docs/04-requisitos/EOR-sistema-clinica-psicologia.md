# Especificação de Objetivos e Requisitos (EOR)
## Sistema de Gestão para Clínica de Psicologia

---

**Projeto:** Sistema de Gestão para Clínica de Psicologia
**Disciplina:** Engenharia de Software
**Instituição:** Pontifícia Universidade Católica de Goiás — PUC Goiás
**Data:** Abril de 2026
**Versão:** 1.0

---

## Sumário

1. [Introdução](#1-introdução)
2. [Descrição do Problema](#2-descrição-do-problema)
3. [Stakeholders e Usuários](#3-stakeholders-e-usuários)
4. [Objetivos do Sistema](#4-objetivos-do-sistema)
5. [Requisitos Funcionais](#5-requisitos-funcionais)
6. [Requisitos Não Funcionais](#6-requisitos-não-funcionais)
7. [Restrições](#7-restrições)
8. [Glossário](#8-glossário)
9. [Referências](#9-referências)

---

## 1. Introdução

### 1.1 Propósito

Este documento tem por objetivo especificar os requisitos do **Sistema de Gestão para Clínica de Psicologia**, um software web destinado a apoiar clínicas multidisciplinares e psicólogos autônomos no gerenciamento de agendamentos, prontuários eletrônicos, finanças e comunicação com pacientes.

### 1.2 Escopo

O sistema abrange o ciclo completo de atendimento em clínicas de psicologia e saúde mental, desde o agendamento inicial até o acompanhamento financeiro e entrega de laudos. O produto é direcionado a dois perfis principais de uso:

- **Clínicas multidisciplinares de pequeno porte** (com equipes de até ~15 profissionais e secretaria dedicada)
- **Psicólogos autônomos** (que trabalham de forma independente, com ou sem compartilhamento de consultório)

### 1.3 Definições e Abreviações

| Sigla / Termo | Definição |
|---|---|
| EOR | Especificação de Objetivos e Requisitos |
| RF | Requisito Funcional |
| RNF | Requisito Não Funcional |
| LGPD | Lei Geral de Proteção de Dados (Lei nº 13.709/2018) |
| Prontuário | Registro eletrônico do histórico clínico do paciente |
| Responsável | Pai, mãe ou responsável legal do paciente menor de idade |
| Laudo | Documento clínico emitido após avaliação ou intervenção |
| Anamnese | Ficha inicial de coleta de dados do paciente |

### 1.4 Visão Geral do Documento

As seções seguintes descrevem o problema atual, os stakeholders envolvidos, os objetivos do sistema e os requisitos funcionais e não funcionais levantados por meio de entrevistas com usuários reais (secretária e profissional de saúde), questionários aplicados a pacientes e ao corpo clínico, e análise de sistema análogo (plataforma Agenday).

---

## 2. Descrição do Problema

### 2.1 Contexto Atual

As clínicas de psicologia e profissionais autônomos da área operam hoje com processos predominantemente manuais e fragmentados. As principais ferramentas utilizadas são:

- **WhatsApp** para agendamento, confirmação e lembretes
- **Google Calendar** para controle de agenda
- **Planilhas eletrônicas** para controle financeiro
- **Sistemas legados** parcialmente adotados, sem integração entre módulos

### 2.2 Problemas Identificados

Com base nas entrevistas realizadas com a **Clínica Espaço Terapêutico** (Karla Niana, gestora) e com a **Psicóloga Autônoma Marla Gonçalves**, e nos questionários respondidos por secretária e paciente, foram identificados os seguintes problemas:

| # | Problema | Impacto | Fonte |
|---|---|---|---|
| P01 | Agendamento manual via WhatsApp consome grande parte do tempo da secretaria | Alto | Entrevistas + Questionários |
| P02 | Ausência de lembretes automatizados gera 2 a 3 faltas por semana | Alto | Entrevista Marla |
| P03 | Conflitos de agenda (profissional × sala × horário) são resolvidos manualmente, com risco de erros | Alto | Questionário secretária |
| P04 | Controle financeiro manual em planilhas, sem notificações de inadimplência | Alto | Entrevistas + Questionários |
| P05 | Emissão de recibos é um processo tedioso e sujeito a erros, envolvendo múltiplas pessoas | Médio | Questionário secretária |
| P06 | Não há bloqueio de entrega de laudos quando há pagamento pendente | Médio | Entrevista Clínica |
| P07 | Dificuldade de controle de evolução do tratamento por etapa por profissional | Médio | Entrevista Clínica |
| P08 | Cobrança por cancelamentos tardios é difícil de aplicar sem comprovação de horário | Médio | Entrevista Marla |
| P09 | Pacientes não têm autonomia para agendar, dependendo de contato humano em horários inoportunos | Médio | Questionário paciente |
| P10 | Prontuários e modelos de relatório são preenchidos manualmente, sem padronização | Baixo | Entrevista Clínica |

### 2.3 Oportunidade

A automação dos fluxos de agendamento, comunicação, financeiro e prontuário pode reduzir significativamente a carga operacional da secretaria, diminuir a taxa de faltas e melhorar a experiência dos pacientes, ao mesmo tempo em que garante conformidade com a LGPD no tratamento de dados sensíveis de saúde.

---

## 3. Stakeholders e Usuários

### 3.1 Stakeholders

| Stakeholder | Papel | Interesse no Sistema |
|---|---|---|
| Gestora da Clínica (Karla Niana) | Proprietária e responsável clínica | Controle operacional, financeiro e de qualidade |
| Psicóloga Autônoma (Marla Gonçalves) | Usuária final independente | Redução de tarefas administrativas e de não comparecimentos |
| Secretária (Carol) | Operadora principal do sistema | Automação de agendamento, cobranças e lembretes |
| Profissionais de Saúde | Psicólogos, fonoaudiólogos, fisioterapeutas etc. | Acesso a prontuários, agenda e modelos de relatório |
| Pacientes / Responsáveis | Consumidores dos serviços | Facilidade de agendamento e comunicação |

### 3.2 Perfis de Usuário

#### 3.2.1 Administrador / Gestora
- Acesso total ao sistema
- Visualiza relatórios gerenciais e financeiros
- Configura profissionais, salas, horários e políticas do sistema

#### 3.2.2 Secretária
- Gerencia agenda de todos os profissionais
- Realiza cadastro de pacientes e responsáveis
- Acompanha cobranças, emissão de recibos e inadimplência
- Comunica-se com pacientes via sistema (WhatsApp/e-mail)

#### 3.2.3 Profissional de Saúde
- Acessa a própria agenda
- Registra prontuários e evolução clínica
- Solicita geração de laudos e relatórios
- Visualiza histórico do paciente

#### 3.2.4 Paciente / Responsável
- Autoagenda consultas via link público
- Recebe lembretes e cobranças automáticas
- Assina presença e recebe laudos e documentos

---

## 4. Objetivos do Sistema

| Código | Objetivo | Prioridade |
|---|---|---|
| OBJ-01 | Automatizar o processo de agendamento com verificação de disponibilidade em tempo real (profissional + sala + horário) | Alta |
| OBJ-02 | Reduzir a taxa de faltas por meio de lembretes automáticos enviados por WhatsApp e/ou e-mail | Alta |
| OBJ-03 | Integrar o controle financeiro ao fluxo de agendamento, gerando cobranças e links de pagamento automaticamente | Alta |
| OBJ-04 | Centralizar os prontuários eletrônicos dos pacientes com modelos padronizados por tipo de atendimento | Alta |
| OBJ-05 | Permitir controle de acesso baseado em perfis (administrador, secretária, profissional, paciente) | Alta |
| OBJ-06 | Possibilitar o autoagendamento pelo paciente/responsável sem necessidade de contato humano | Média |
| OBJ-07 | Registrar automaticamente horário de cancelamentos para viabilizar cobrança de taxa conforme política da clínica | Média |
| OBJ-08 | Gerar relatórios e indicadores operacionais e financeiros para a gestão da clínica | Média |
| OBJ-09 | Garantir conformidade com a LGPD no armazenamento e tratamento de dados clínicos e pessoais | Alta |
| OBJ-10 | Integrar com canais de pagamento (Pix, cartão, transferência) e com o Google Calendar | Média |

---

## 5. Requisitos Funcionais

Os requisitos funcionais estão organizados por módulo. A prioridade segue a classificação: **Alta**, **Média** ou **Baixa**.

---

### 5.1 Módulo de Cadastro

| Código | Requisito | Descrição | Prioridade |
|---|---|---|---|
| RF-01 | Cadastro de Paciente | O sistema deve permitir o cadastro de pacientes com os campos: nome completo, data de nascimento, telefone, e-mail, nome do responsável (se menor), plano de saúde (se houver) e origem/indicação. | Alta |
| RF-02 | Cadastro de Responsável Legal | Para pacientes menores de idade, deve ser possível cadastrar responsável legal com nome, CPF, telefone e relação com o paciente. | Alta |
| RF-03 | Cadastro de Profissional | O sistema deve permitir cadastrar profissionais com: nome, CRP/registro de classe, especialidade, disponibilidade de horários e salas associadas. | Alta |
| RF-04 | Cadastro de Sala / Consultório | O sistema deve permitir cadastrar salas com: identificação, tipo (individual, multidisciplinar) e horários disponíveis. | Alta |
| RF-05 | Cadastro de Planos e Pacotes | O sistema deve permitir cadastrar planos de atendimento (número de sessões, valor total, validade), associáveis a pacientes. | Média |

---

### 5.2 Módulo de Agendamento

| Código | Requisito | Descrição | Prioridade |
|---|---|---|---|
| RF-06 | Verificação de Disponibilidade | Ao criar um agendamento, o sistema deve verificar simultaneamente: disponibilidade do profissional, disponibilidade da sala e disponibilidade do paciente/responsável, impedindo conflitos. | Alta |
| RF-07 | Criação de Agendamento pela Secretaria | A secretaria deve poder criar, editar e cancelar agendamentos em nome de qualquer paciente. | Alta |
| RF-08 | Autoagendamento pelo Paciente | O sistema deve disponibilizar link público de autoagendamento, onde o paciente visualiza os horários disponíveis e seleciona sem contato com a secretaria. | Média |
| RF-09 | Agendamento Recorrente | O sistema deve suportar a criação de consultas recorrentes (ex.: toda segunda-feira às 14h por 12 semanas), com possibilidade de edição individual ou em lote. | Alta |
| RF-10 | Agendamento Multidisciplinar | O sistema deve permitir agendar sessões sequenciais com múltiplos profissionais no mesmo dia para o mesmo paciente, priorizando salas disponíveis e fluxo de atendimento. | Média |
| RF-11 | Bloqueio de Feriados | O sistema deve bloquear automaticamente o agendamento em feriados nacionais, estaduais e em datas configuradas como não úteis pela clínica. | Alta |
| RF-12 | Substituição por Ausência de Profissional | Em caso de ausência de profissional, o sistema deve permitir cancelamento ou redistribuição da sessão, com notificação automática ao paciente. | Média |
| RF-13 | Registro de Cancelamento com Timestamp | Todo cancelamento deve ser registrado com data e hora exata para fins de aplicação de política de cancelamento tardio. | Alta |

---

### 5.3 Módulo de Lembretes e Comunicação

| Código | Requisito | Descrição | Prioridade |
|---|---|---|---|
| RF-14 | Lembrete Automático de Consulta | O sistema deve enviar lembrete automático (WhatsApp e/ou e-mail) ao paciente/responsável com antecedência mínima de 24 horas antes da consulta. | Alta |
| RF-15 | Confirmação de Consulta | O sistema deve enviar mensagem de confirmação de agendamento imediatamente após a criação da consulta. | Alta |
| RF-16 | Notificação de Cancelamento | O sistema deve enviar notificação automática ao paciente em caso de cancelamento ou alteração de consulta. | Alta |
| RF-17 | Follow-up Pós-Consulta | O sistema deve enviar mensagem de acompanhamento automático após a realização da sessão, podendo incluir coleta de feedback ou orientações. | Baixa |
| RF-18 | Respostas a Dúvidas Frequentes (FAQ) | O sistema deve permitir que um módulo de automação responda a perguntas comuns dos pacientes (horários, endereço, serviços oferecidos) via WhatsApp ou chat. | Baixa |
| RF-19 | Encaminhamento para Atendimento Humano | Em situações não resolvidas pela automação, o sistema deve encaminhar o contato para a secretaria ou profissional responsável. | Média |

---

### 5.4 Módulo de Controle de Presença

| Código | Requisito | Descrição | Prioridade |
|---|---|---|---|
| RF-20 | Registro de Presença | O sistema deve permitir o registro de presença de pacientes em cada sessão, com assinatura digital ou confirmação pelo responsável. | Alta |
| RF-21 | Listagem de Presença por Sessão | O sistema deve gerar lista de presença por sessão, com identificação do paciente/responsável, data, hora e profissional. | Alta |
| RF-22 | Controle de Faltas | O sistema deve registrar e exibir o histórico de faltas do paciente, diferenciando faltas com e sem aviso prévio. | Média |
| RF-23 | Relatório de Frequência | O sistema deve gerar relatório de frequência por paciente e por período, com percentual de presença e ausências. | Média |

---

### 5.5 Módulo Financeiro

| Código | Requisito | Descrição | Prioridade |
|---|---|---|---|
| RF-24 | Geração de Cobrança Automática | Após a confirmação de um agendamento, o sistema deve gerar automaticamente a cobrança correspondente (sessão avulsa ou débito em pacote). | Alta |
| RF-25 | Envio de Link de Pagamento | O sistema deve enviar link de pagamento (Pix ou cartão) ao paciente/responsável via WhatsApp e/ou e-mail. | Alta |
| RF-26 | Registro de Pagamento | O sistema deve registrar os pagamentos recebidos, identificando: data, valor, método (Pix, cartão, transferência, dinheiro) e sessão correspondente. | Alta |
| RF-27 | Controle de Inadimplência | O sistema deve identificar automaticamente pagamentos em atraso e notificar a secretaria, sem bloquear automaticamente novos agendamentos (conforme política da clínica). | Alta |
| RF-28 | Emissão de Recibo | O sistema deve gerar recibo digital ao paciente após confirmação de pagamento, no formato adequado para reembolso por plano de saúde. | Alta |
| RF-29 | Bloqueio de Entrega de Laudo por Pendência | O sistema deve impedir a liberação de laudos e relatórios clínicos enquanto houver pagamento pendente vinculado ao paciente. | Alta |
| RF-30 | Controle de Pacotes de Sessões | O sistema deve controlar o saldo de sessões em pacotes, notificando o paciente e a secretaria quando o saldo estiver próximo do esgotamento ou vencimento. | Média |
| RF-31 | Cobrança por Cancelamento Tardio | O sistema deve suportar a aplicação de taxa de cancelamento (ex.: 50% do valor da sessão) quando o cancelamento ocorrer com menos de X horas de antecedência, conforme configuração da clínica. | Média |
| RF-32 | Relatório Financeiro | O sistema deve gerar relatórios financeiros com: receita por período, inadimplência, pagamentos por modalidade, sessões realizadas e canceladas. | Média |
| RF-33 | Suporte a Tarifas Diferenciadas | O sistema deve permitir configurar valores diferentes por paciente (ex.: tarifa social), por profissional ou por tipo de serviço. | Média |

---

### 5.6 Módulo de Prontuário Eletrônico

| Código | Requisito | Descrição | Prioridade |
|---|---|---|---|
| RF-34 | Criação de Prontuário | O sistema deve permitir a criação de prontuário eletrônico para cada paciente, vinculado ao seu cadastro. | Alta |
| RF-35 | Modelos de Prontuário por Especialidade | O sistema deve disponibilizar templates pré-configurados por tipo de atendimento (ex.: avaliação de TDAH, intervenção psicológica, fonoaudiologia). | Alta |
| RF-36 | Registro de Evolução Clínica por Sessão | O sistema deve permitir que o profissional registre a evolução clínica ao final de cada sessão, vinculada à data e ao profissional responsável. | Alta |
| RF-37 | Acesso Multiprofissional ao Prontuário | O sistema deve permitir que múltiplos profissionais de uma mesma equipe acessem o prontuário de um paciente, conforme permissões configuradas. | Média |
| RF-38 | Anamnese Digital | O sistema deve disponibilizar formulário digital de anamnese (ficha inicial) para preenchimento pelo profissional durante ou antes da primeira sessão. | Alta |
| RF-39 | Geração de Laudo / Relatório Clínico | O sistema deve suportar a geração de laudos e relatórios clínicos a partir dos dados registrados no prontuário e na evolução, com status "Aguardando Revisão Clínica" antes da liberação. | Alta |
| RF-40 | Entrega de Laudo ao Paciente | O sistema deve permitir o envio do laudo ao paciente/responsável via e-mail ou WhatsApp após aprovação do profissional responsável. | Média |
| RF-41 | Controle de Etapas do Tratamento | O sistema deve permitir registrar e acompanhar a etapa atual do tratamento de cada paciente (ex.: avaliação, intervenção, alta). | Média |

---

### 5.7 Módulo de Relatórios e Indicadores

| Código | Requisito | Descrição | Prioridade |
|---|---|---|---|
| RF-42 | Painel de Indicadores Operacionais | O sistema deve exibir painel com: volume de consultas por período, taxa de cancelamento, taxa de faltas, serviços mais demandados e performance por profissional. | Média |
| RF-43 | Relatório de Atendimentos | O sistema deve gerar relatório detalhado de atendimentos por período, profissional, tipo de serviço e status (realizado, cancelado, falta). | Média |
| RF-44 | Estatísticas de Diagnósticos e Laudos | O sistema deve permitir a geração de estatísticas clínicas agregadas (ex.: frequência de diagnósticos de TDAH) em formato anonimizado. | Baixa |
| RF-45 | Exportação de Relatórios | Os relatórios devem poder ser exportados nos formatos PDF e CSV. | Média |

---

### 5.8 Módulo de Controle de Acesso

| Código | Requisito | Descrição | Prioridade |
|---|---|---|---|
| RF-46 | Autenticação de Usuários | O sistema deve exigir autenticação (login e senha) para todos os usuários com perfil de staff (administrador, secretária, profissional). | Alta |
| RF-47 | Perfis de Acesso | O sistema deve implementar perfis de acesso distintos: Administrador, Secretária, Profissional de Saúde e Paciente/Responsável, com permissões diferenciadas. | Alta |
| RF-48 | Log de Ações | O sistema deve registrar log de ações realizadas por cada usuário (criação, edição, cancelamento de agendamentos, acesso a prontuários). | Média |

---

### 5.9 Módulo de Integrações

| Código | Requisito | Descrição | Prioridade |
|---|---|---|---|
| RF-49 | Integração com Google Calendar | O sistema deve sincronizar a agenda de consultas com o Google Calendar do profissional, permitindo visualização e gestão bidirecional. | Média |
| RF-50 | Integração com Gateway de Pagamento | O sistema deve integrar com gateway de pagamento para processar transações via Pix, cartão de crédito e débito. | Alta |
| RF-51 | Integração com WhatsApp | O sistema deve enviar mensagens automatizadas via WhatsApp (lembretes, confirmações, cobranças, documentos). | Alta |
| RF-52 | Importação de Dados de Planilhas | O sistema deve suportar importação de dados básicos (pacientes, histórico financeiro) a partir de planilhas CSV/XLSX para facilitar a migração inicial. | Baixa |

---

## 6. Requisitos Não Funcionais

| Código | Requisito | Descrição | Prioridade |
|---|---|---|---|
| RNF-01 | Usabilidade | A interface deve ser intuitiva e não exigir treinamento técnico especializado. O fluxo de autoagendamento pelo paciente deve ser concluído sem orientações externas. | Alta |
| RNF-02 | Responsividade | O sistema deve funcionar corretamente em dispositivos móveis (smartphones) e desktops, priorizando a visualização mobile para consultas rápidas entre sessões. | Alta |
| RNF-03 | Disponibilidade | O sistema deve estar disponível 24 horas por dia, 7 dias por semana, com uptime mínimo de 99%, para suportar autoagendamentos fora do horário comercial. | Alta |
| RNF-04 | Segurança e LGPD | O sistema deve tratar dados pessoais e clínicos em conformidade com a Lei nº 13.709/2018 (LGPD), incluindo: consentimento explícito, controle de acesso, criptografia em trânsito (HTTPS/TLS) e em repouso, e direito de exclusão de dados. | Alta |
| RNF-05 | Criptografia | Dados sensíveis (prontuários, laudos, dados financeiros) devem ser armazenados com criptografia adequada. | Alta |
| RNF-06 | Desempenho | O sistema deve responder a operações comuns (carregamento de agenda, consulta de prontuário) em até 3 segundos em condições normais de uso. | Média |
| RNF-07 | Escalabilidade | A arquitetura do sistema deve suportar crescimento no número de usuários e volume de dados sem degradação significativa de desempenho, prevendo expansão para aplicativo móvel nativo no futuro. | Média |
| RNF-08 | Compatibilidade de Navegadores | O sistema deve ser compatível com as versões atuais dos principais navegadores: Chrome, Firefox, Safari e Edge. | Média |
| RNF-09 | Rastreabilidade | Toda ação relevante (cancelamento, edição de prontuário, liberação de laudo) deve ser rastreável por usuário, data e hora. | Alta |
| RNF-10 | Backup | O sistema deve realizar backup automático dos dados com frequência mínima diária, com possibilidade de restauração. | Alta |
| RNF-11 | Multicanalidade | O sistema deve suportar comunicação com pacientes por WhatsApp e e-mail, sendo o WhatsApp o canal primário de notificações no contexto brasileiro. | Alta |

---

## 7. Restrições

| Código | Restrição | Descrição |
|---|---|---|
| REST-01 | Restrição Legal | O sistema deve observar integralmente a LGPD (Lei nº 13.709/2018) e as resoluções do CFP (Conselho Federal de Psicologia) sobre prontuários e sigilo profissional. |
| REST-02 | Restrição de Pagamentos | A clínica opera exclusivamente como particular (sem convênios diretos); o sistema não precisa integrar com operadoras de plano de saúde, mas deve emitir recibos para reembolso. |
| REST-03 | Restrição de Automação Financeira | O sistema não deve bloquear automaticamente novos agendamentos por inadimplência, limitando-se a notificar a secretaria (conforme política da Clínica Espaço Terapêutico). |
| REST-04 | Restrição de Aprovação de Laudo | Nenhum laudo ou relatório clínico pode ser entregue ao paciente sem aprovação prévia do profissional responsável e sem pagamento quitado. |
| REST-05 | Restrição de Plataforma | O sistema deve ser entregue como aplicação web (SaaS), sendo o aplicativo móvel nativo uma evolução futura não contemplada no escopo atual. |

---

## 8. Glossário

| Termo | Definição |
|---|---|
| Agendamento Recorrente | Consulta que se repete em periodicidade fixa ao longo de um período (ex.: semanalmente). |
| Anamnese | Ficha de coleta de informações iniciais do paciente, realizada na primeira consulta. |
| Atendimento Multidisciplinar | Atendimento onde o paciente é assistido por profissionais de mais de uma especialidade (ex.: psicologia + fonoaudiologia) em um mesmo dia. |
| Autoagendamento | Funcionalidade que permite ao paciente/responsável agendar consulta de forma autônoma, sem intermediário humano. |
| CRP | Conselho Regional de Psicologia; órgão regulador da profissão de psicólogo no Brasil. |
| Evolução Clínica | Registro feito pelo profissional ao final de cada sessão, documentando o progresso do tratamento. |
| Gateway de Pagamento | Serviço intermediário que processa transações financeiras online (ex.: Pix, cartão). |
| Inadimplência | Situação em que o paciente possui pagamentos em atraso. |
| Laudo | Documento clínico formal emitido após avaliação diagnóstica ou intervenção, assinado pelo profissional responsável. |
| LGPD | Lei Geral de Proteção de Dados Pessoais (Lei nº 13.709/2018), que regulamenta o uso de dados pessoais no Brasil. |
| Pacote de Sessões | Conjunto de sessões pré-pagas com desconto ou condições especiais. |
| Prontuário Eletrônico | Registro digital do histórico clínico, atendimentos e evolução de um paciente. |
| Recibo | Documento financeiro emitido pela clínica ao paciente, utilizado para reembolso por plano de saúde. |
| SaaS | Software as a Service; modelo de entrega de software via internet, sem instalação local. |
| Timestamp | Registro automático de data e hora de uma ação no sistema. |

---

## 9. Referências

1. **Entrevista 1** — Clínica Espaço Terapêutico, realizada com Karla Niana (gestora). Transcrição disponível em `docs/02-entrevistas/Transcrição da Entrevista 1.pdf`.
2. **Entrevista 2** — Psicóloga Autônoma Marla Gonçalves. Transcrição disponível em `docs/02-entrevistas/Entrevista-Marla.docx.pdf`.
3. **Questionários** — Respostas de secretária (Carol) e paciente (Ana Julia Monteiro). Dados disponíveis em `docs/03-questionarios/questionarios_trabalho.pdf` e `docs/03-questionarios/questionarios.pdf`.
4. **Estudo de Sistema Análogo** — Análise da plataforma Agenday. Documentos em `docs/01-estudo-sistema-analogo/`.
5. BRASIL. **Lei nº 13.709, de 14 de agosto de 2018** — Lei Geral de Proteção de Dados Pessoais (LGPD).
6. CFP — Conselho Federal de Psicologia. **Resolução CFP nº 01/2009** — Normas de atuação dos psicólogos em relação ao prontuário.

---

*Documento elaborado com base em levantamento de requisitos realizado junto a usuários reais por meio de entrevistas semiestruturadas, questionários e análise de sistema análogo (Agenday).*
