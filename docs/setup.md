# Setup

## Pré-requisitos

- n8n instalado.
- Ollama instalado.
- Google Sheets configurado.
- Telegram configurado no n8n.

## Planilha

Crie uma planilha com as abas:

- Aulas
- Relatorios
- Banco_Atividades
- Config

Use os CSVs em `examples/` como referência.

## Importação

1. Importe o workflow sanitizado no n8n.
2. Configure as credenciais do Google Sheets, Ollama e Telegram.
3. Ajuste os nodes `Ler Aula` e `Atualizar Aula` para sua planilha.
4. Cadastre uma aula com status `Pendente`.
5. Execute o workflow.

Resultado esperado: `status = Material gerado` e material preenchido na coluna `material_gerado`.
