# QAhub — Assistente diário de QA

Desenvolvido por **William Montijo**

App em Streamlit que ajuda Analistas de QA a transformar histórias de usuário,
requisitos e critérios de aceitação em cenários de teste prontos para uso, e a
organizar a rotina da sprint: execução, defeitos, retestes e relatórios em PDF.

O **IArgus** é o assistente do QAhub e aparece no cabeçalho, no topo da página.
Sua imagem está embutida no app e não entra nos relatórios.

## O que o app faz

- Gerencia **várias User Stories (US)** no mesmo app: uma caixa logo abaixo das abas permite
  criar, nomear, trocar e excluir US. Cada US tem seus próprios cenários, execução,
  defeitos, retestes e código/link do card; projeto, sprint, QA e logos são comuns.
- Gera cenários de teste em quatro formatos: **BDD (Gherkin)**, **Passo a Passo**,
  **Texto Único / Resumo** e **End-to-end (E2E)**. No E2E você monta o fluxo etapa por
  etapa (ação e resultado esperado), sem precisar de critérios de aceite, e cada etapa é
  validada na execução, com status, observação e evidência próprios.
- Mostra a **cobertura** dos critérios e sugere cenários para os buracos encontrados.
- Registra a **execução** de cada cenário (Aprovado, Reprovado, Bloqueado) com
  evidências em imagem.
- Abre **defeitos** a partir dos cenários reprovados, com card do bug próprio,
  evidências da execução e anexos extras.
- Guarda o **histórico de retestes** ligado ao cenário e ao defeito de origem,
  preservando a falha original.
- Exporta **PDF** (cabeçalho com a logo do cliente, rodapé com a logo da empresa,
  código e link do card), **CSV**, Markdown e arquivos para Xray, TestRail e
  Azure DevOps. Os PDFs são gerados sob demanda: clique em **Gerar PDF** e depois em
  **Baixar** (o app avisa se o conteúdo mudou e o PDF ficou desatualizado).
- **Status Report** diário: resumo de todas as US só com o total e os status
  (aprovados, reprovados, bloqueados, não executados), com texto pronto para enviar por e-mail.
- Importa requisitos de **PDF e Word**.
- Guarda o trabalho no arquivo **`.qahub`** (um registro por US; dá para salvar uma ou todas): cada pessoa tem o seu próprio
  histórico, que ela mesma baixa e reabre. Nada fica salvo no servidor.
- Opcional: botão **"Usar IA"** para gerar cenários com um modelo externo. A chave
  é digitada por cada pessoa e nunca fica salva no app. O endereço de cada provedor é
  fixo (no Azure só são aceitos endereços oficiais do Azure), e o texto digitado é enviado
  ao provedor escolhido (o app avisa na tela): não cole dados sensíveis.

## Como rodar no seu computador

```bash
python -m pip install -r requirements.txt
python -m streamlit run app.py
```

Requer Python 3.10 ou mais novo.

## Como rodar online

O app foi feito para o **Streamlit Community Cloud**: basta apontar este
repositório lá e o site fica no ar com um link. Sem banco de dados e sem contas.

## Estrutura

| Arquivo | O que é |
| --- | --- |
| `app.py` | O app inteiro, em um único arquivo (inclui as imagens da interface). |
| `requirements.txt` | Bibliotecas necessárias. |
| `CHANGELOG.md` | Histórico de versões do app. |
| `GUIA_DE_TESTES.md` | Roteiro para testar tudo, passo a passo. |
| `.streamlit/config.toml` | Cores e aparência da página. |
| `.gitignore` | Arquivos que o Git deve ignorar (inclui `*.qahub`). |

## Avisos

- O histórico só existe no arquivo `.qahub` de cada pessoa. Se ela fechar a página
  sem baixar, o trabalho da sessão é perdido.
- O link publicado é público: quem tiver o endereço consegue abrir o app.
