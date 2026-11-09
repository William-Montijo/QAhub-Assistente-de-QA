# Histórico de versões — QAhub

Autor: William Montijo. As versões mais novas ficam no topo.
As versões anteriores à v29 estão como foram registradas no cabeçalho do `app.py`, sem datas.

## v29 — 2026-11-08

### Adicionado
- **Várias User Stories (US) no mesmo app.** Caixa de US no topo de cada aba, com seletor, nome editável, botão **Nova US**, visão geral (cenários e status por US) e exclusão com confirmação. Cada US guarda história, critérios, cenários, execução, defeitos, retestes e código/link do card. Projeto, sprint, QA, data e logos são compartilhados.
- **Histórico por US.** Botões **Salvar US atual** e **Salvar todas as US**. O título de cada versão salva mostra o nome da US.
- **Abrir como US.** Abre uma versão do histórico como US, sem apagar as que já estão abertas: reaproveita a US já aberta com aquela versão, usa a US atual se estiver vazia ou cria uma nova.
- **Arquivos exportados com o nome da US** (por exemplo, `Login_cenarios.pdf`).
- **Aba Status Report.** Resumo de todas as US só com total e status (aprovados, reprovados, bloqueados, não executados), tabela por US e texto pronto para o e-mail diário, com copiar, baixar `.txt` e abrir no e-mail.
- **Formato End-to-end (E2E).** Um teste com título geral e etapas digitadas pelo QA (ação e resultado esperado), sem depender de critérios de aceite. Construtor de etapas na aba Cenários: adicionar, subir, descer e remover.
- **Execução do E2E por etapa**, com status, observação e evidência próprios. O status do teste é calculado: qualquer etapa reprovada reprova o teste, e as etapas seguintes ainda não executadas ficam Bloqueadas automaticamente.
- **Defeito do E2E aponta a etapa que falhou**, com os passos até ela, o esperado da etapa e a observação como resultado obtido.
- **Exportações do E2E** em Markdown e PDF listam cada etapa com resultado esperado e, na execução, status, observações e evidências.
- **Status Report** mostra também as etapas aprovadas dos testes E2E.
- Aviso na aba Cobertura quando a US não tem critérios de aceite.

### Alterado
- Nome do assistente padronizado como **IArgus** em todos os textos.
- IArgus agora fica dentro do cabeçalho, alinhado ao lado do título, menor (150 px) e **parado** (rola junto com a página). A cabeça e as antenas não são mais cortadas pela barra superior do Streamlit.
- As abas ficam logo abaixo do cabeçalho; a caixa de US vem depois delas.
- O botão **Abrir versão** virou **Abrir como US** e não pede mais confirmação para substituir o trabalho atual.
- Duplicar um teste E2E copia as etapas com status e evidências zerados.
- Mensagens de erro do histórico mostram o motivo real.
- **Desempenho com imagens de evidência:** o tratamento de cada imagem (validar, redimensionar e converter) agora é feito uma única vez e guardado na sessão de cada pessoa, com limite de 150 MB. Antes era refeito a cada clique, várias vezes por imagem, em todas as abas. Num teste com 8 capturas de tela (cerca de 12 MB), uma ação simples caiu de 6,5 s para 2,0 s. O cache não é compartilhado entre pessoas, não entra no histórico `.qahub` e some quando a sessão termina.
- **PDFs sob demanda:** os PDFs (cenários, cada defeito, relatório de todos os defeitos e retestes) deixaram de ser gerados a cada clique. Agora aparece **Gerar PDF**; depois de gerado, vira **Baixar**, e o arquivo fica guardado na sessão (limite de 200 MB) enquanto o conteúdo não mudar. Se o texto, as evidências, os dados do cabeçalho ou as logos mudarem, o app avisa que o PDF ficou desatualizado e oferece "Gerar PDF novamente". Nos testes, uma interação comum passou de 6 PDFs gerados para 0 e ficou de 2 a 3 vezes mais rápida com 4 a 24 defeitos com imagens. As mensagens de erro continuam as mesmas.
- **Miniaturas das evidências:** as imagens mostradas na tela são miniaturas JPEG já na largura exibida (280 px, ou 240 px nas evidências extras do defeito), criadas uma vez por imagem e guardadas na sessão (limite de 60 MB). Antes, o Streamlit reabria, redimensionava e regravava cada imagem a cada clique. PNG com transparência aparece sobre fundo branco. A imagem original continua intacta no histórico e nos PDFs. Nos testes, uma interação comum caiu de 1,1 s para 0,5 s com 4 defeitos, de 2,9 s para 1,1 s com 12 e de 6,1 s para 2,8 s com 24.
- README atualizado (formatos, abas, várias US, E2E, Status Report e IArgus).

### Corrigido
- Acentuação em "Pré-condições" na descrição exportada para Jira e Azure DevOps.
- Importação de `datetime` duplicada no `app.py`, agora uma só.
- **Segurança da IA:** o campo "API Key" não vem mais preenchido com chaves configuradas no servidor (variáveis como `OPENAI_API_KEY`), que ficavam visíveis para qualquer pessoa que abrisse o app público. Cada pessoa digita a própria chave, e a legenda do campo avisa isso.
- **Segurança da IA (Base URL):** o endereço do provedor deixou de ser livre. Os provedores com endereço conhecido usam sempre o oficial, mesmo que outro valor seja enviado, e o campo "Base URL" ficou somente leitura. No Azure OpenAI, só endereços oficiais do Azure por https são aceitos (`*.openai.azure.com`, `*.cognitiveservices.azure.com` e `*.services.ai.azure.com`), o que impede apontar o servidor para endereços internos. Endereço recusado mostra um aviso e o app usa o motor local.
- **Privacidade da IA:** com "Usar IA" ligado, a coluna lateral e a área acima do botão "Gerar Cenários" avisam que o texto da história (inclusive o importado de PDF ou Word) e os critérios são enviados ao provedor escolhido, e lembram de não colar dados sensíveis. O aviso cita o provedor selecionado e some quando a IA está desligada ou no formato E2E, que não usa IA.

### Removido
- **Histórico local em SQLite** (variável `QAHUB_HISTORY_PATH` e arquivo `~/.qahub/history.sqlite3`). O app usa só o arquivo portátil `.qahub`, como já fazia na prática.
- Provedor "Outro (compatível com OpenAI)", que aceitava qualquer endereço.
- Leitura de chaves de IA por variável de ambiente (campo `env` dos provedores e `import os`).
- Código sem uso: `display_argus` (e seu CSS), `generate_with_ai`, `PROMPTS`, `GENERATORS`, `gen_bdd`, `gen_steps`, `gen_summary`, `bug_report_markdown` e `history_writable`.
- Notas de versão do cabeçalho do `app.py` (movidas para este arquivo).

## v28
- Assistente renomeado para IArgus (analogia com IA); posição ajustada para não cobrir o título.
- IArgus maior e colado no topo da página (a cabeça não é mais coberta pela barra superior do Streamlit), preenchendo o espaço até a linha das abas.

## v26
- IArgus flutuava sobre a página no canto superior direito (posição fixa); saiu do cabeçalho, que voltou à altura original e não empurra mais o conteúdo para baixo.

## v24
- IArgus sem plano de fundo (PNG transparente); avatar no canto superior esquerdo do cabeçalho, e o título "Cenários de teste" virou "IArgus · Assistente de QA".

## v23
- IArgus na abertura e em todas as abas; imagem embutida, ausente dos PDFs e do histórico.
  (Substituído nas versões seguintes pelo avatar no cabeçalho.)

## v22
- Cabeçalho do PDF compacto em 4 colunas e 3 linhas (Nome do QA, Projeto e Data | Sprint, Código do card e Link Jira/Azure).
- Novo campo "Data do relatório" no cabeçalho, salvo no histórico portátil.

## v20
- Salvar atualiza o mesmo registro, sem criar versões a cada clique.
- Execução em lote: status, observações e evidências só são confirmados pelo botão Salvar execução.

## v19
- Uso 100% online: a opção "Neste computador" saiu da tela. Todo QA guarda o próprio histórico no arquivo portátil `.qahub` (baixar antes de fechar, abrir na próxima vez) — ninguém mistura histórico com ninguém.
- Botão "Baixar meu histórico (.qahub)" na aba Histórico, com todas as versões salvas, cenários, defeitos, retestes e imagens.
- Botão "Abrir meu histórico" recebe o arquivo `.qahub`, traz as versões de volta e pode abrir a mais recente direto no app.
- Aviso visível no modo portátil lembrando de baixar o arquivo antes de fechar.

## v17
- Logo da sua empresa (QAhub) no rodapé de todas as páginas do PDF.

## v16
- Imagens visíveis no histórico de defeitos e prévia dos anexos do reteste.
- Confirmação persistente com resultado e quantidade de imagens salvas.
- Status de execução editável após reteste aprovado, preservando a falha original.

## v15
- Aba Reteste com listas na tela: resumo por item (quantas vezes retestou e todos os resultados) e uma linha para cada tentativa registrada.
- Contador de retestes no título de cada cenário nas abas Execução e Reteste.

## v14
- Aba Reteste com tentativas vinculadas ao cenário e ao defeito.
- Histórico de cada tentativa salvo localmente sem apagar a falha original.

## v11
- Importação de requisitos de arquivos PDF e Word (.docx) direto para o campo de texto.
- Relatório de defeito por cenário reprovado (passos, esperado x obtido, evidências), com cópia e download na aba Execução e consolidado na aba Exportar.

## v6
- Edição por cenário, rastreabilidade de critérios e rascunhos de revisão.
- Execução com status, observações e evidências PNG/JPG no relatório.
- Histórico local por projeto/sprint em SQLite, salvo explicitamente. (Removido na v29.)
- Exportação CSV genérica com proteção contra fórmulas em planilhas.

## Recursos base preservados desde as primeiras versões
- Cabeçalho do PDF compacto: logo do cliente, nome do QA, projeto, data, sprint, código do card e link.
- Campos editáveis e upload de logo PNG/JPG/JPEG, independentes da marca QAhub.
- Logo QAhub embutida na interface e no ícone da aba.
- Interface clara em laranja, preto e branco. PDF preservado, sem logo.
- PDF A4 com títulos hierárquicos, tabelas com colunas e rodapé numerado.
- Acentos preservados e pontuação normalizada, sem pontos de interrogação para emojis.
- Campos individuais editáveis antes de copiar/baixar.
- Botão de download em PDF (requer `pip install fpdf2`).
