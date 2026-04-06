# Sistema de Gestão para Clínica de Psicologia

> Projeto acadêmico desenvolvido na disciplina de Engenharia de Software do curso de Bacharelado em Ciência da Computação da PUC Goiás.

---

## Sobre o Projeto

Sistema web de gestão voltado a clínicas de psicologia e profissionais autônomos da área da saúde mental. O objetivo é digitalizar e automatizar os principais fluxos operacionais do consultório: agendamento, prontuário eletrônico, comunicação com pacientes, controle financeiro e emissão de laudos.

O projeto foi desenvolvido com base em levantamento de requisitos realizado junto a usuários reais, incluindo gestora de clínica multidisciplinar, psicóloga autônoma, secretária e paciente.

---

## Informações Acadêmicas

| Campo | Informação |
|---|---|
| Instituição | Pontifícia Universidade Católica de Goiás (PUC Goiás) |
| Escola | Escola Politécnica e de Artes |
| Curso | Bacharelado em Ciência da Computação |
| Disciplina | Engenharia de Software |
| Professora | Adriana Silveira de Souza |
| Ano | 2026 |

---

## Integrantes

| Nome |
|---|
| Amanda Barbosa Ferreira Agapito |
| Igor Pinto de Castro Ferreira |
| João Pedro Gonçalves Ferreira |
| Mateus Lucas Prado Amorim |
| Pedro Lourençoni Lima |

---

## Status do Projeto

```
Entrega 1 - Levantamento de Requisitos   ██████████  Concluída
Entrega 2 - Modelagem e Análise          ░░░░░░░░░░  Pendente
Entrega 3 - Projeto de Arquitetura       ░░░░░░░░░░  Pendente
Entrega 4 - Implementação                ░░░░░░░░░░  Pendente
Entrega 5 - Testes e Validação           ░░░░░░░░░░  Pendente
```

---

## Entregas

### Entrega 1 - Levantamento de Requisitos ✅

Primeira entrega do projeto, focada na elicitação, análise e documentação inicial dos requisitos do sistema. Foram aplicadas múltiplas técnicas de levantamento e os resultados foram consolidados em documento único.

**Técnicas utilizadas:**

- **Entrevistas semiestruturadas** com gestora da Clínica Espaço Terapêutico (Karla Niana) e psicóloga autônoma (Marla Gonçalves)
- **Questionários** aplicados com secretária (Carol) e paciente (Ana Julia Monteiro)
- **Análise de sistema análogo** da plataforma Agenday (app.agenday.tech)
- **Análise do processo de negócio** da clínica

**Artefatos produzidos:**

| Artefato | Arquivo |
|---|---|
| Documento consolidado final | `docs/Levantamento_Requisitos_Clinica_Psicologia_Final.pdf` |
| Estudo de sistema análogo (completo) | `docs/01-estudo-sistema-analogo/estudo_sistema_analogo_agenday.pdf` |
| Síntese do sistema análogo | `docs/01-estudo-sistema-analogo/documento_sintese_agenday.pdf` |
| Transcrição da Entrevista 1 (Karla Niana) | `docs/02-entrevistas/Transcrição da Entrevista 1.pdf` |
| Descrição da Entrevista 1 | `docs/02-entrevistas/entrevista_1-1.pdf` |
| Entrevista 2 (Marla Gonçalves) | `docs/02-entrevistas/Entrevista-Marla.docx.pdf` |
| Questionários aplicados | `docs/03-questionarios/questionarios.pdf` |
| Síntese dos requisitos dos questionários | `docs/03-questionarios/questionarios_trabalho.pdf` |
| EOR - Especificação de Objetivos e Requisitos | `docs/04-requisitos/` |
| Matriz de Rastreabilidade | `docs/05-matriz-rastreabilidade/` |

**Contexto de levantamento:**

| Stakeholder | Perfil | Contribuição |
|---|---|---|
| Karla Niana | Proprietária e terapeuta - Clínica Espaço Terapêutico | Regras de negócio, fluxo operacional, gestão multidisciplinar |
| Marla Gonçalves | Psicóloga clínica autônoma, Goiânia | UX mobile, autoagendamento, controle financeiro simplificado |
| Carol | Secretária / assistente administrativa | Gargalos operacionais, automação de agenda e cobrança |
| Ana Julia Monteiro | Paciente | Preferências de agendamento, comunicação e acesso a documentos |
| Agenday (análogo) | Plataforma SaaS para psicólogos | Referências funcionais e boas práticas do mercado |

---

### Entrega 2 - Modelagem e Análise *(em breve)*

> Esta seção será preenchida na próxima entrega do projeto.

---

### Entrega 3 - Projeto de Arquitetura *(em breve)*

> Esta seção será preenchida na próxima entrega do projeto.

---

### Entrega 4 - Implementação *(em breve)*

> Esta seção será preenchida na próxima entrega do projeto.

---

### Entrega 5 - Testes e Validação *(em breve)*

> Esta seção será preenchida na próxima entrega do projeto.

---

## Escopo do Sistema

O sistema abrange o ciclo completo de atendimento em clínicas de psicologia, desde o agendamento inicial até o acompanhamento financeiro e entrega de laudos. É direcionado a dois perfis principais:

- **Clínicas multidisciplinares de pequeno porte** com até ~15 profissionais e secretaria dedicada
- **Psicólogos autônomos** que trabalham de forma independente, com ou sem compartilhamento de consultório

**Módulos previstos:**

- Cadastro de pacientes, responsáveis, profissionais e salas
- Agendamento com verificação de disponibilidade em tempo real
- Lembretes e confirmações automáticas via WhatsApp e e-mail
- Controle de presença e frequência
- Módulo financeiro: cobranças, links de pagamento, recibos e inadimplência
- Prontuário eletrônico com modelos por especialidade
- Geração e entrega controlada de laudos clínicos
- Relatórios e indicadores operacionais e gerenciais
- Controle de acesso por perfil (administrador, secretária, profissional, paciente)
- Integrações: WhatsApp, Google Calendar, gateway de pagamento

**Requisitos não funcionais principais:**

- Conformidade com a LGPD (Lei n. 13.709/2018)
- Interface responsiva com prioridade para mobile
- Disponibilidade 24/7 (uptime mínimo de 99%)
- Criptografia de dados em trânsito e em repouso
- Rastreabilidade de ações por usuário e timestamp

---

## Estrutura do Repositório

```
Projeto-Clinica-Psicologia/
│
├── README.md
└── docs/
    ├── Levantamento_Requisitos_Clinica_Psicologia_Final.pdf
    │
    ├── 01-estudo-sistema-analogo/
    │   ├── estudo_sistema_analogo_agenday.pdf
    │   └── documento_sintese_agenday.pdf
    │
    ├── 02-entrevistas/
    │   ├── Transcrição da Entrevista 1.pdf
    │   ├── entrevista_1-1.pdf
    │   ├── Entrevista-Marla.docx.pdf
    │   └── documento_mais_simples
    │
    ├── 03-questionarios/
    │   ├── questionarios.pdf
    │   └── questionarios_trabalho.pdf
    │
    ├── 04-requisitos/              ← EOR
    ├── 05-matriz-rastreabilidade/  ← Matriz de Rastreabilidade
    │
    ├── 06-modelagem/               ← (em breve)
    ├── 07-arquitetura/             ← (em breve)
    ├── 08-implementacao/           ← (em breve)
    └── 09-testes/                  ← (em breve)
```

---

## Referências

- BRASIL. Lei n. 13.709, de 14 de agosto de 2018. Lei Geral de Proteção de Dados Pessoais (LGPD).
- CONSELHO FEDERAL DE PSICOLOGIA (CFP). Resolução CFP n. 001/2009. Prontuários e registro documental.
- AGENDAY TECH. Perfil da startup no Founders Club, 2025. Disponível em: https://foundersclub.com.br/startups/agenday-tech/
- AGENDAY TECH. Instagram oficial: [@agenday.tech](https://www.instagram.com/agenday.tech/)
