# Arquitetura do TutorOps

## Visão geral

O TutorOps utiliza n8n como camada de orquestração para automatizar a criação de material docente.

```text
Google Sheets
→ n8n
→ Ollama local
→ Google Sheets
→ Telegram
```

## Componentes

### Google Sheets

Base operacional do workflow.

- Aba `Aulas`: aulas a processar.
- Aba `Relatorios`: prevista para registros pós-aula.
- Aba `Banco_Atividades`: banco de atividades práticas.
- Aba `Config`: parâmetros do projeto.

### n8n

Responsável por:

- ler aulas pendentes;
- enviar dados para o AI Agent;
- preparar dados de atualização;
- atualizar a planilha;
- notificar via Telegram.

### Ollama

Executa o modelo local de IA, sem uso de API paga de LLM.

Modelo usado na versão inicial:

```text
llama3.2:3b
```

### Telegram

Canal operacional para avisar que o plano de aula foi gerado e registrado.

## Workflow

```text
Manual Trigger
→ Ler Aula
→ Gerar Plano de Aula IA
→ Ollama Chat Model
→ Preparar Atualização
→ Atualizar Aula
→ Send a text message
```

## Limitações conhecidas

- A versão v1 grava o plano completo na célula `material_gerado`.
- A geração automática em Google Docs foi adiada para v2 por exigência de callback HTTPS válido no OAuth do Google.
- O modelo `llama3.2:3b` pode exigir prompt restritivo para evitar imprecisões técnicas.
