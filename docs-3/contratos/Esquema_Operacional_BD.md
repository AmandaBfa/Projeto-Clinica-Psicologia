# Esquema Operacional de Banco de Dados (Nível C4)

**Sistema:** Sistema de Gestão para Clínica de Psicologia
**SGBD:** PostgreSQL · **Autor:** João Pedro Gonçalves Ferreira
**Origem:** derivado do modelo relacional [`docs-2/modelagem/MER.dbml`](../../docs-2/modelagem/MER.dbml)

> Descrição das relações (tabelas) com atributos, **tipos** e **tamanhos**. PK = chave
> primária; FK = chave estrangeira; NN = *not null*; UQ = *unique*. Escopo reduzido — o módulo
> financeiro (Pagamento, Recibo) fica para a evolução futura.

## Identidade e acesso

### Usuario
| Coluna | Tipo | Tamanho | Restrições |
|--------|------|---------|------------|
| id | UUID | 16 bytes | PK |
| email | VARCHAR | 255 | NN, UQ |
| senha_hash | VARCHAR | 255 | NN (argon2id) |
| nome | VARCHAR | 150 | NN |
| ativo | BOOLEAN | 1 byte | NN, default true |
| mfa_habilitado | BOOLEAN | 1 byte | NN, default false |
| criado_em | TIMESTAMP | 8 bytes | NN |
| atualizado_em | TIMESTAMP | 8 bytes | NN |

### Papel
| Coluna | Tipo | Tamanho | Restrições |
|--------|------|---------|------------|
| id | SERIAL | 4 bytes | PK |
| nome | VARCHAR | 50 | NN, UQ (ADMIN/PROFISSIONAL/SECRETARIA/PACIENTE) |

### UsuarioPapel
| Coluna | Tipo | Tamanho | Restrições |
|--------|------|---------|------------|
| usuario_id | UUID | 16 bytes | PK, FK → Usuario(id) |
| papel_id | INT | 4 bytes | PK, FK → Papel(id) |

## Domínio clínico

### Clinica
| Coluna | Tipo | Tamanho | Restrições |
|--------|------|---------|------------|
| id | UUID | 16 bytes | PK |
| razao_social | VARCHAR | 200 | NN |
| cnpj | VARCHAR | 14 | UQ |
| endereco | VARCHAR | 255 | |
| telefone | VARCHAR | 20 | |
| criado_em | TIMESTAMP | 8 bytes | NN |

### Profissional
| Coluna | Tipo | Tamanho | Restrições |
|--------|------|---------|------------|
| id | UUID | 16 bytes | PK |
| usuario_id | UUID | 16 bytes | FK → Usuario(id), NN, UQ |
| clinica_id | UUID | 16 bytes | FK → Clinica(id) |
| crp | VARCHAR | 20 | NN, UQ |
| bio | TEXT | variável | |
| ativo | BOOLEAN | 1 byte | NN, default true |
| permite_autoagendamento | BOOLEAN | 1 byte | NN, default false |

### Especialidade
| Coluna | Tipo | Tamanho | Restrições |
|--------|------|---------|------------|
| id | SERIAL | 4 bytes | PK |
| nome | VARCHAR | 100 | NN, UQ |

### ProfissionalEspecialidade
| Coluna | Tipo | Tamanho | Restrições |
|--------|------|---------|------------|
| profissional_id | UUID | 16 bytes | PK, FK → Profissional(id) |
| especialidade_id | INT | 4 bytes | PK, FK → Especialidade(id) |

### AgendaConfig
| Coluna | Tipo | Tamanho | Restrições |
|--------|------|---------|------------|
| id | UUID | 16 bytes | PK |
| profissional_id | UUID | 16 bytes | FK → Profissional(id), NN |
| dia_semana | SMALLINT | 2 bytes | NN (0=Dom..6=Sab) |
| hora_inicio | TIME | 8 bytes | NN |
| hora_fim | TIME | 8 bytes | NN |
| duracao_slot_min | INT | 4 bytes | NN, default 50 |

### Sala
| Coluna | Tipo | Tamanho | Restrições |
|--------|------|---------|------------|
| id | UUID | 16 bytes | PK |
| clinica_id | UUID | 16 bytes | FK → Clinica(id), NN |
| nome | VARCHAR | 100 | NN |
| tipo | VARCHAR | 20 | NN (INDIVIDUAL/MULTIDISCIPLINAR) |
| capacidade | INT | 4 bytes | NN, default 1 |

### Paciente
| Coluna | Tipo | Tamanho | Restrições |
|--------|------|---------|------------|
| id | UUID | 16 bytes | PK |
| usuario_id | UUID | 16 bytes | FK → Usuario(id) (opcional) |
| nome | VARCHAR | 150 | NN |
| cpf | VARCHAR | 11 | UQ |
| data_nascimento | DATE | 4 bytes | |
| email | VARCHAR | 255 | |
| telefone | VARCHAR | 20 | |
| canal_preferido_lembrete | VARCHAR | 20 | (WHATSAPP/EMAIL/AMBOS) |
| observacoes | TEXT | variável | |
| ativo | BOOLEAN | 1 byte | NN, default true |
| criado_em | TIMESTAMP | 8 bytes | NN |

### VinculoProfissionalPaciente
| Coluna | Tipo | Tamanho | Restrições |
|--------|------|---------|------------|
| profissional_id | UUID | 16 bytes | PK, FK → Profissional(id) |
| paciente_id | UUID | 16 bytes | PK, FK → Paciente(id) |
| inicio | DATE | 4 bytes | NN |
| fim | DATE | 4 bytes | |

## Agendamento e atendimento

### Agendamento
| Coluna | Tipo | Tamanho | Restrições |
|--------|------|---------|------------|
| id | UUID | 16 bytes | PK |
| profissional_id | UUID | 16 bytes | FK → Profissional(id), NN |
| paciente_id | UUID | 16 bytes | FK → Paciente(id), NN |
| sala_id | UUID | 16 bytes | FK → Sala(id) (nulo se ONLINE) |
| inicio | TIMESTAMP | 8 bytes | NN |
| fim | TIMESTAMP | 8 bytes | NN |
| modalidade | VARCHAR | 20 | NN (PRESENCIAL/ONLINE) |
| tipo_sessao | VARCHAR | 30 | NN (ANAMNESE/RETORNO/AVALIACAO/GRUPAL) |
| status | VARCHAR | 20 | NN (AGENDADO/CONFIRMADO/REALIZADO/CANCELADO/FALTOU) |
| recorrencia_id | UUID | 16 bytes | (agrupa série recorrente) |
| observacoes | TEXT | variável | |
| criado_por | UUID | 16 bytes | FK → Usuario(id) |
| criado_em | TIMESTAMP | 8 bytes | NN |
| atualizado_em | TIMESTAMP | 8 bytes | NN |

Índices: (profissional_id, inicio), (paciente_id, inicio), (sala_id, inicio).

### Atendimento
| Coluna | Tipo | Tamanho | Restrições |
|--------|------|---------|------------|
| id | UUID | 16 bytes | PK |
| agendamento_id | UUID | 16 bytes | FK → Agendamento(id), NN, UQ |
| iniciado_em | TIMESTAMP | 8 bytes | |
| finalizado_em | TIMESTAMP | 8 bytes | |
| duracao_min | INT | 4 bytes | |
| presenca | BOOLEAN | 1 byte | NN |
| observacoes | TEXT | variável | |

## Prontuário

### Prontuario
| Coluna | Tipo | Tamanho | Restrições |
|--------|------|---------|------------|
| id | UUID | 16 bytes | PK |
| paciente_id | UUID | 16 bytes | FK → Paciente(id), NN, UQ |
| aberto_em | TIMESTAMP | 8 bytes | NN |
| encerrado_em | TIMESTAMP | 8 bytes | |

### EvolucaoSessao
| Coluna | Tipo | Tamanho | Restrições |
|--------|------|---------|------------|
| id | UUID | 16 bytes | PK |
| prontuario_id | UUID | 16 bytes | FK → Prontuario(id), NN |
| atendimento_id | UUID | 16 bytes | FK → Atendimento(id) |
| profissional_id | UUID | 16 bytes | FK → Profissional(id), NN |
| tipo | VARCHAR | 30 | NN (ANAMNESE/SESSAO_REGULAR/.../CORRECAO) |
| texto_cifrado | TEXT | variável | NN (AES-256) |
| evolucao_corrigida_id | UUID | 16 bytes | FK → EvolucaoSessao(id) |
| registrado_em | TIMESTAMP | 8 bytes | NN |
| hash_integridade | CHAR | 64 | (SHA-256) |

### Anexo
| Coluna | Tipo | Tamanho | Restrições |
|--------|------|---------|------------|
| id | UUID | 16 bytes | PK |
| evolucao_id | UUID | 16 bytes | FK → EvolucaoSessao(id), NN |
| nome_arquivo | VARCHAR | 255 | NN |
| mime_type | VARCHAR | 100 | NN |
| tamanho_bytes | BIGINT | 8 bytes | NN (máx 10 MB) |
| storage_uri | VARCHAR | 500 | NN |
| carregado_em | TIMESTAMP | 8 bytes | NN |

## Comunicação

### Lembrete
| Coluna | Tipo | Tamanho | Restrições |
|--------|------|---------|------------|
| id | UUID | 16 bytes | PK |
| agendamento_id | UUID | 16 bytes | FK → Agendamento(id), NN |
| canal | VARCHAR | 20 | NN (WHATSAPP/EMAIL) |
| agendar_para | TIMESTAMP | 8 bytes | NN |
| status | VARCHAR | 20 | NN (PENDENTE/ENVIADO/CONFIRMADO/FALHADO/REENVIO) |
| tentativas | INT | 4 bytes | NN, default 0 |
| enviado_em | TIMESTAMP | 8 bytes | |
| resposta | TEXT | variável | |

### TemplateMensagem
| Coluna | Tipo | Tamanho | Restrições |
|--------|------|---------|------------|
| id | UUID | 16 bytes | PK |
| clinica_id | UUID | 16 bytes | FK → Clinica(id), NN |
| tipo | VARCHAR | 30 | NN (LEMBRETE_24H/LEMBRETE_2H/CONFIRMACAO) |
| canal | VARCHAR | 20 | NN |
| conteudo | TEXT | variável | NN |

## LGPD e auditoria

### ConsentimentoLGPD
| Coluna | Tipo | Tamanho | Restrições |
|--------|------|---------|------------|
| id | UUID | 16 bytes | PK |
| paciente_id | UUID | 16 bytes | FK → Paciente(id), NN |
| versao_termo | VARCHAR | 20 | NN |
| aceito_em | TIMESTAMP | 8 bytes | NN |
| revogado_em | TIMESTAMP | 8 bytes | |
| ip_origem | VARCHAR | 45 | |

### LogAuditoria
| Coluna | Tipo | Tamanho | Restrições |
|--------|------|---------|------------|
| id | UUID | 16 bytes | PK |
| usuario_id | UUID | 16 bytes | FK → Usuario(id) |
| acao | VARCHAR | 50 | NN (CREATE/UPDATE/DELETE/READ/EXPORT/LOGIN) |
| entidade | VARCHAR | 50 | NN |
| entidade_id | UUID | 16 bytes | |
| ip_origem | VARCHAR | 45 | |
| payload_antes | JSONB | variável | |
| payload_depois | JSONB | variável | |
| registrado_em | TIMESTAMP | 8 bytes | NN |
| severidade | VARCHAR | 10 | (INFO/WARN/ALTA) |

Índices: (entidade, entidade_id), (usuario_id, registrado_em).
