# QAhub — Assistente diário de QA

Desenvolvido por **William Montijo**

App em Streamlit que ajuda Analistas de QA a transformar histórias de usuário,
requisitos e critérios de aceitação em cenários de teste prontos para uso, e a
organizar a rotina da sprint: execução, defeitos, retestes e relatórios em PDF.

## O que o app faz

- Gera cenários de teste em três formatos: **BDD (Gherkin)**, **Passo a Passo** e
  **Resumo com Resultado Esperado**.
- Mostra a **cobertura** dos critérios e sugere cenários para os buracos encontrados.
- Registra a **execução** de cada cenário (Aprovado, Reprovado, Bloqueado) com
  evidências em imagem.
- Abre **defeitos** a partir dos cenários reprovados, com card do bug próprio,
  evidências da execução e anexos extras.
- Guarda o **histórico de retestes** ligado ao cenário e ao defeito de origem,
  preservando a falha original.
- Exporta **PDF** (cabeçalho com a logo do cliente, rodapé com a logo da empresa,
  código e link do card), **CSV**, Markdown e arquivos para Xray, TestRail e
  Azure DevOps.
- Importa requisitos de **PDF e Word**.
- Guarda o trabalho no arquivo **`.qahub`**: cada pessoa tem o seu próprio
  histórico, que ela mesma baixa e reabre. Nada fica salvo no servidor.
- Opcional: botão **"Usar IA"** para gerar cenários com um modelo externo. A chave
  é digitada por cada pessoa e nunca fica salva no app.

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
| `.streamlit/config.toml` | Cores e aparência da página. |

## Avisos

- O histórico só existe no arquivo `.qahub` de cada pessoa. Se ela fechar a página
  sem baixar, o trabalho da sessão é perdido.
- O link publicado é público: quem tiver o endereço consegue abrir o app.
