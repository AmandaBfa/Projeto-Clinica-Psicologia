# Contrato de Operação (Larman, cap. 11)

**Sistema:** Sistema de Gestão para Clínica de Psicologia
**Autor:** João Pedro Gonçalves Ferreira

> Conforme Larman (cap. 11), um **contrato de operação** descreve o efeito de uma operação do
> sistema sobre os objetos do domínio em termos de **pré-condições** e **pós-condições**
> (mudanças de estado), sem descrever *como* isso é feito. Abaixo, **um exemplo** referente à
> operação central do escopo.

## Contrato CO1 — criarAgendamento

| Campo | Descrição |
|-------|-----------|
| **Operação** | `criarAgendamento(profissionalId, pacienteId, salaId, inicio, fim, modalidade, tipoSessao)` |
| **Referências cruzadas** | Caso de uso **UC01 — Agendar Consulta** |
| **Pré-condições** | • O paciente e o profissional existem e estão ativos. <br>• O profissional possui agenda configurada para o dia/horário. <br>• Se modalidade = PRESENCIAL, a sala informada existe. |
| **Pós-condições** | • Foi criada uma instância `a` de **Agendamento** *(criação de instância)*. <br>• `a.status` foi definido como **AGENDADO** *(modificação de atributo)*. <br>• `a` foi associado ao **Profissional**, ao **Paciente** e (se presencial) à **Sala** informados *(formação de associações)*. <br>• Os atributos `a.inicio`, `a.fim`, `a.modalidade` e `a.tipoSessao` foram preenchidos com os valores recebidos *(modificação de atributos)*. <br>• Foi criada uma instância de **Lembrete** associada a `a`, com `status = PENDENTE` *(criação de instância e associação)*. <br>• Foi criado um registro de **LogAuditoria** com `acao = CREATE` referenciando `a`. |

> **Observação.** A verificação de conflito de horário (profissional + sala + paciente) é uma
> **pré-condição garantida pela `AgendaPolicy`** antes da criação; se houver conflito, a
> operação não ocorre e nenhuma das pós-condições acima se aplica (ver o diagrama de sequência
> `c4-seq-criarAgendamento.puml`, fluxo "indisponível").
