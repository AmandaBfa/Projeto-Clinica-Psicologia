# Especificação de Requisitos de Software (ERS) — v2

**Sistema:** Sistema de Gestão para Clínica de Psicologia
**Versão:** 2.0
**Data:** 2026-05-07
**Autor:** Igor Pinto de Castro Ferreira
**Disciplina:** Arquitetura e Desenho de Software — PUC Goiás · 2026.1
**Padrão:** IEEE 830-1998

---

## Histórico de revisões

| Versão | Data | Descrição | Autor |
|---|---|---|---|
| 1.0 | 2026-04-04 | EOR original (Entrega 1) | Mateus |
| 2.0 | 2026-05-07 | Reestruturação no padrão IEEE 830, refinamento de RFs e RNFs | Igor |

---

## 1. Introdução

### 1.1 Propósito
Especificar de forma completa, consistente e verificável os requisitos do Sistema de Gestão para Clínica de Psicologia, servindo de base contratual entre a equipe de desenvolvimento e os stakeholders, e como insumo para os artefatos de modelagem (casos de uso, MER, protótipos).

### 1.2 Escopo
O sistema é uma plataforma web responsiva para gestão integrada de clínicas de psicologia de pequeno porte e psicólogos autônomos. Contempla agendamento, prontuário eletrônico, financeiro, comunicação automatizada e controle de acesso.

### 1.3 Definições, acrônimos e abreviações
- **RF** — Requisito Funcional
- **RNF** — Requisito Não Funcional
- **RBAC** — *Role-Based Access Control*
- **LGPD** — Lei Geral de Proteção de Dados (Lei 13.709/2018)
- **CFP** — Conselho Federal de Psicologia
- **MER** — Modelo Entidade-Relacionamento
- Demais termos: vide *Dicionário de Dados* (`joao-pedro/Dicionario_Dados.md`)

### 1.4 Referências
- IEEE 830-1998 — *Recommended Practice for Software Requirements Specifications*
- ISO/IEC 25010:2011 — Modelo de qualidade
- Documento de Visão (`amanda/Documento_Visao.md`)
- EOR v1 (Entrega 1) — `docs/04-requisitos/`
- Estudo do sistema análogo Agenday (`docs/01-estudo-sistema-analogo/`)
- Lei 13.709/2018 — LGPD
- Resolução CFP nº 11/2018 — atendimento online e prontuário eletrônico

### 1.5 Visão geral
Seções: 2. Descrição Geral, 3. Requisitos Específicos (RFs, RNFs, interfaces, restrições).

---

## 2. Descrição geral

### 2.1 Perspectiva do produto
Aplicação web *standalone*, integrada a serviços externos (mensageria WhatsApp/e-mail, eventualmente provedores de pagamento). Não substitui sistemas contábeis ou prontuários hospitalares.

### 2.2 Funções do produto (resumo)
Vide seção 3.2 — Lista de RFs.

### 2.3 Características dos usuários

| Tipo | Frequência de uso | Habilidade técnica |
|---|---|---|
| Administrador da clínica | Diária | Média |
| Profissional (psicólogo) | Diária | Baixa-média |
| Secretária | Diária, sessão longa | Média |
| Paciente | Ocasional | Variável (baixa a alta) |

### 2.4 Restrições gerais
- RG01 — Conformidade com LGPD obrigatória.
- RG02 — Aderência à Resolução CFP nº 11/2018 para prontuário online.
- RG03 — Implementação web, sem app nativo na primeira versão.
- RG04 — Tecnologias open-source preferenciais.

### 2.5 Premissas e dependências
- PD01 — Stakeholders disponíveis para validação ao longo do projeto.
- PD02 — Provedor de WhatsApp Business contratado ou substituto compatível.
- PD03 — Provedor de e-mail SMTP disponível.

---

## 3. Requisitos específicos

### 3.1 Requisitos de interface externa

#### 3.1.1 Interfaces de usuário
- IUS01 — Interface web responsiva, suportando resoluções de 320px a 1920px.
- IUS02 — Suporte a navegadores Chrome, Edge, Safari e Firefox (últimas 2 versões).
- IUS03 — Acessibilidade WCAG 2.1 nível AA.
- IUS04 — Idioma padrão: pt-BR.

#### 3.1.2 Interfaces de hardware
Não há requisitos específicos de hardware além de dispositivo com navegador moderno.

#### 3.1.3 Interfaces de software
- ISO01 — Integração com WhatsApp Business API (ou Twilio / Z-API).
- ISO02 — Integração com servidor SMTP (TLS).
- ISO03 — Geração de PDF para recibos.

#### 3.1.4 Interfaces de comunicação
- ICM01 — HTTPS com TLS 1.2 ou superior.
- ICM02 — REST API interna documentada (OpenAPI 3).

### 3.2 Requisitos funcionais

#### 3.2.1 Cadastros e autenticação

| ID | Requisito | Prioridade | Origem |
|---|---|---|---|
| RF01 | O sistema deve permitir cadastro de **profissionais** com nome, CRP, especialidade, e-mail, telefone, agenda padrão. | Alta | Karla, Marla |
| RF02 | O sistema deve permitir cadastro de **pacientes** com dados pessoais, contatos, consentimento LGPD e canal preferido de comunicação. | Alta | Karla, Carol |
| RF03 | O sistema deve autenticar usuários por e-mail e senha, com verificação em duas etapas opcional. | Alta | Karla |
| RF04 | O sistema deve oferecer recuperação de senha por e-mail. | Média | Carol |
| RF05 | O sistema deve permitir cadastro/edição de especialidades e tipos de sessão configuráveis pela clínica. | Média | Karla |

#### 3.2.2 Agendamento

| ID | Requisito | Prioridade | Origem |
|---|---|---|---|
| RF06 | O sistema deve permitir agendar consulta selecionando profissional, data/hora, modalidade (presencial/online) e tipo. | Alta | Karla, Marla, Ana Julia |
| RF07 | O sistema deve impedir agendamentos com sobreposição de horário para o mesmo profissional ou paciente. | Alta | Karla |
| RF08 | O sistema deve permitir cancelamento e remarcação com regras de antecedência configuráveis. | Alta | Karla |
| RF09 | O sistema deve oferecer autoatendimento de agendamento ao paciente, configurável por profissional. | Média | Marla |
| RF10 | O sistema deve sugerir horários alternativos quando o slot escolhido estiver indisponível. | Baixa | Marla |

#### 3.2.3 Comunicação

| ID | Requisito | Prioridade | Origem |
|---|---|---|---|
| RF11 | O sistema deve enviar lembrete automático via WhatsApp e/ou e-mail 24h e 2h antes da sessão. | Alta | Todos |
| RF12 | O sistema deve aceitar confirmação ou cancelamento do lembrete pelo paciente. | Alta | Karla |
| RF13 | O sistema deve permitir templates de mensagem configuráveis por clínica. | Média | Karla |
| RF14 | O sistema deve enviar lembrete de pagamento antes do vencimento. | Média | Carol |

#### 3.2.4 Atendimento e Prontuário

| ID | Requisito | Prioridade | Origem |
|---|---|---|---|
| RF15 | O sistema deve permitir registrar atendimento (presença/falta, duração, observações) ao final da sessão. | Alta | Karla, Marla |
| RF16 | O sistema deve manter prontuário eletrônico com anamnese, evoluções por sessão e anexos. | Alta | Karla |
| RF17 | O sistema deve permitir anexar arquivos (PDF, imagem) ao prontuário com tamanho máximo de 10 MB por arquivo. | Média | Marla |
| RF18 | O sistema deve permitir exportar prontuário em PDF (transferência ao paciente, mediante consentimento). | Média | Karla |

#### 3.2.5 Financeiro

| ID | Requisito | Prioridade | Origem |
|---|---|---|---|
| RF19 | O sistema deve registrar pagamentos por sessão (dinheiro, PIX, cartão, plano). | Alta | Carol, Karla |
| RF20 | O sistema deve emitir recibo em PDF com dados fiscais mínimos. | Alta | Karla |
| RF21 | O sistema deve apresentar dashboard financeiro (recebíveis, inadimplência, fluxo). | Média | Karla |
| RF22 | O sistema deve gerar relatório de comissão por profissional (configurável). | Média | Karla |

#### 3.2.6 Relatórios e indicadores

| ID | Requisito | Prioridade | Origem |
|---|---|---|---|
| RF23 | O sistema deve gerar relatório de ocupação de agenda por profissional e por período. | Média | Karla, Marla |
| RF24 | O sistema deve gerar relatório de no-shows e remarcações. | Média | Karla |
| RF25 | O sistema deve permitir exportar relatórios em PDF e CSV. | Baixa | Karla |

#### 3.2.7 Controle de acesso e auditoria

| ID | Requisito | Prioridade | Origem |
|---|---|---|---|
| RF26 | O sistema deve implementar RBAC com papéis: Admin, Profissional, Secretária, Paciente. | Alta | Karla |
| RF27 | O sistema deve registrar log de auditoria com usuário, timestamp, IP e ação. | Alta | LGPD |
| RF28 | O sistema deve registrar consentimento LGPD do paciente, com versionamento e revogação. | Alta | LGPD |
| RF29 | O sistema deve permitir ao paciente exportar seus dados pessoais (direito à portabilidade). | Média | LGPD |
| RF30 | O sistema deve permitir ao paciente solicitar exclusão de dados (anonimização para fins de prontuário). | Média | LGPD |

#### 3.2.8 Portal do paciente

| ID | Requisito | Prioridade | Origem |
|---|---|---|---|
| RF31 | O paciente deve poder visualizar suas próximas sessões. | Média | Ana Julia |
| RF32 | O paciente deve poder baixar recibos. | Média | Ana Julia |
| RF33 | O paciente deve poder atualizar dados de contato. | Baixa | Ana Julia |

### 3.3 Requisitos não funcionais
Detalhados na **Especificação Suplementar (ISO/IEC 25010)** — `igor/Especificacao_Suplementar_ISO25010.md`. Resumo:

| ID | Característica ISO 25010 | Resumo |
|---|---|---|
| RNF01 | Performance Efficiency | Resposta < 2s em 95% das requisições |
| RNF02 | Reliability | Disponibilidade ≥ 99% mensal |
| RNF03 | Security | TLS 1.2+, criptografia em repouso, auditoria, RBAC |
| RNF04 | Compatibility | Chrome/Edge/Safari/Firefox últimas 2 versões; responsivo 320-1920px |
| RNF05 | Usability | Onboarding ≤ 10 min sem treinamento; WCAG 2.1 AA |
| RNF06 | Maintainability | Cobertura de testes ≥ 70% no backend |
| RNF07 | Portability | Containerização Docker; deploy multi-cloud |
| RNF08 | Functional Suitability | 100% dos RFs Alta com testes de aceitação |

### 3.4 Restrições de design
- RD01 — Backend stateless para escalabilidade horizontal.
- RD02 — Banco de dados relacional (PostgreSQL preferencial) com migrações versionadas.
- RD03 — Frontend SPA (React, Vue ou similar) — decisão na Entrega 3.
- RD04 — Comunicação backend/frontend via REST + JSON.

### 3.5 Atributos do sistema
Atendimento aos atributos ISO 25010 (vide Suplementar).

### 3.6 Outros requisitos
- OR01 — Backups diários automáticos com retenção mínima de 30 dias.
- OR02 — Documentação de API publicada via Swagger/OpenAPI.
- OR03 — Logs estruturados (JSON) para observabilidade.

---

## Anexo A — Rastreabilidade Necessidade ↔ RF

| Necessidade | RFs |
|---|---|
| N01 — Agenda unificada | RF06, RF07, RF08, RF10 |
| N02 — Prontuário seguro | RF15, RF16, RF17, RF18, RF26, RF27 |
| N03 — Lembretes automáticos | RF11, RF12, RF13 |
| N04 — Controle financeiro | RF19, RF20, RF21, RF22 |
| N05 — LGPD | RF27, RF28, RF29, RF30 |
| N06 — Mobile | (cobertura via RNF04) |
| N07 — Controle de acesso | RF26 |
