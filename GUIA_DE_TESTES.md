# Guia de testes — QAhub v29

Roteiro para conferir, no navegador, tudo o que foi feito. Marque cada item.
Se algo não sair como o "Esperado", anote o número do item e me envie, de preferência com uma captura de tela.

## 0. Antes de começar

```bash
python -m pip install -r requirements.txt
python -m streamlit run app.py
```

- Python 3.10 ou mais novo.
- Pasta do projeto: `app.py`, `requirements.txt`, `.streamlit/config.toml` e `.gitignore` juntos.
- O que **eu não consegui ver no navegador** (preste atenção): posição do IArgus, layout das abas e da caixa de US, botão de copiar, link "Abrir no e-mail" e o visual no celular. O resto foi validado com testes automáticos.

## 1. Cabeçalho e IArgus
- [ ] 1.1 O título é **"IArgus · Assistente de QA"**.
- [ ] 1.2 O IArgus fica ao lado do título, pequeno, com **cabeça e antenas inteiras** (não cortadas pela barra do "Deploy").
- [ ] 1.3 Ao rolar a página, o IArgus **sobe junto com o conteúdo** (não fica seguindo a tela).
- [ ] 1.4 O IArgus não cobre nenhum botão nem o título.

## 2. Abas e caixa de US
- [ ] 2.1 As abas ficam logo abaixo do cabeçalho: Cenários, Cobertura, Execução, Defeitos, Reteste, Exportar, **Status Report**, Histórico.
- [ ] 2.2 No topo de **cada aba**, abaixo das abas, aparece a caixa "User Story (US) em edição".
- [ ] 2.3 Ao trocar de aba, a caixa continua mostrando a mesma US.

## 3. Várias User Stories
- [ ] 3.1 Clique em **Carregar exemplo** e depois em **Gerar Cenários** (US 1).
- [ ] 3.2 Escreva um nome em **Nome da US** (ex.: "Login") e confirme com Enter. O seletor mostra `1. Login · 4 cenário(s)`.
- [ ] 3.3 Preencha o **Código do card** na lateral (ex.: PROJ-1).
- [ ] 3.4 Clique em **Nova US**. Esperado: tudo vazio (texto, cenários, código do card).
- [ ] 3.5 Cole outra história, gere cenários, dê outro nome e outro código de card.
- [ ] 3.6 Troque pelo seletor entre as duas US. Esperado: cada uma volta com o seu texto, cenários e código de card.
- [ ] 3.7 Com 2 US, abra **Visão geral das US**. Esperado: tabela com cenários e status de cada uma.
- [ ] 3.8 Projeto, sprint, QA e logos da lateral **não mudam** ao trocar de US.
- [ ] 3.9 **Excluir esta US**: o botão só habilita depois de marcar "Confirmar exclusão" e quando há mais de uma US.

## 4. Formatos de cenário
- [ ] 4.1 Na lateral, em "Formato de saída", teste **BDD (Gherkin)**, **Passo a Passo** e **Texto Único / Resumo**: um cenário por critério.
- [ ] 4.2 O formato **End-to-end (E2E)** aparece na lista (veja a seção 5).

## 5. Formato E2E (fluxo por etapas)
- [ ] 5.1 Escolha **End-to-end (E2E)**. Sem escrever nada, clique em **Gerar Cenários**. Esperado: **1 teste** chamado `E2E · Novo fluxo`.
- [ ] 5.2 Abra o teste. Preencha a primeira etapa: **ação** e **resultado esperado** (ex.: "Cadastrar usuário com dados válidos" / "Usuário criado").
- [ ] 5.3 Clique em **Adicionar etapa** 3 vezes e preencha: "Conferir usuário na lista", "Excluir o usuário", "Conferir que sumiu da lista".
- [ ] 5.4 Teste os botões **↑**, **↓** e **✕** de cada etapa.
- [ ] 5.5 Na aba **Execução**, o teste E2E mostra **status, observação e evidência por etapa**.
- [ ] 5.6 Marque a etapa 1 como **Aprovado** e a etapa 2 como **Reprovado** (com uma observação). Clique em **Salvar execução**.
  - Esperado: etapas 3 e 4 ficam **Bloqueado** (bloqueio automático) e o teste fica **Reprovado**.
- [ ] 5.7 Na aba **Defeitos**, o defeito foi criado e o título termina com **"— falha na etapa 2"**; os passos para reproduzir vão só até a etapa 2.
- [ ] 5.8 Depois do defeito, as etapas ficam **travadas** na Execução (aviso explicando).
- [ ] 5.9 Na aba **Reteste**, registre um reteste **Aprovado**. Esperado: o teste volta a Aprovado e a falha original continua guardada.
- [ ] 5.10 Na aba **Cobertura**, para uma US sem critérios aparece um aviso informando isso.
- [ ] 5.11 **Duplicar** o teste E2E: a cópia vem com as etapas e todos os status zerados.

## 6. Execução, defeitos e reteste (formatos comuns)
- [ ] 6.1 Em **Execução**, marque cenários como Aprovado, Reprovado e Bloqueado e clique em **Salvar execução**.
- [ ] 6.2 Anexe uma imagem de evidência (PNG/JPG) a um cenário reprovado.
- [ ] 6.3 Em **Defeitos**, confira o defeito criado, o card do bug e as evidências.
- [ ] 6.4 Em **Reteste**, registre uma tentativa e veja o histórico por cenário.

## 7. Evidências em miniatura
- [ ] 7.1 As evidências aparecem como **miniaturas** nas abas Execução, Defeitos e Reteste.
- [ ] 7.2 A tela responde **rápido** ao clicar (compare com a sensação de antes, se tiver muitas imagens).
- [ ] 7.3 A imagem **original** vai inteira para o PDF (confira no PDF da seção 8).

## 8. PDFs sob demanda
- [ ] 8.1 Na aba **Exportar**, o botão é **Gerar PDF**. Clique. Esperado: ele vira **Baixar PDF**.
- [ ] 8.2 Baixe e abra o PDF: cabeçalho, logos, cenários e, se houver, evidências.
- [ ] 8.3 Sem mudar nada, clique em qualquer outra coisa. Esperado: o **Baixar PDF** continua lá (não precisa gerar de novo).
- [ ] 8.4 Mude o **Nome do QA** na lateral. Esperado: aparece "O conteúdo mudou…" e o botão vira **Gerar PDF novamente**.
- [ ] 8.5 Em **Defeitos**: **Gerar PDF deste defeito** e **Gerar relatório em PDF**, e depois baixar.
- [ ] 8.6 Em **Reteste**: **Gerar PDF de todos os retestes** e baixar.

## 9. Status Report
- [ ] 9.1 Abra a aba **Status Report** com 2 ou mais US abertas.
- [ ] 9.2 Esperado: números gerais (Total, Aprovados, Reprovados, Bloqueados, Não executados), tabela por US e uma linha de **Total geral**.
- [ ] 9.3 A linha "Executados: X de Y (Z%) · Aprovação sobre os executados: W%" confere com os números.
- [ ] 9.4 Se houver um teste E2E, aparece "Etapas dos testes E2E aprovadas: X de Y".
- [ ] 9.5 Em **Texto para o e-mail**: edite o texto, clique em **Copiar texto do e-mail** e cole em outro lugar para conferir.
- [ ] 9.6 **Baixar .txt** baixa o texto.
- [ ] 9.7 **Abrir no e-mail** abre o seu programa de e-mail com assunto e corpo preenchidos *(depende de ter um programa de e-mail configurado)*.

## 10. Histórico (.qahub)
- [ ] 10.1 Na aba **Histórico**, clique em **Salvar US atual**. Depois em **Salvar todas as US**.
- [ ] 10.2 Cada versão salva mostra o **nome da US** no título.
- [ ] 10.3 **Baixar meu histórico (.qahub)** baixa o arquivo.
- [ ] 10.4 Recarregue a página (F5): o trabalho some (é esperado, o app não guarda nada no servidor).
- [ ] 10.5 Em **Abrir meu histórico**, envie o `.qahub`. Esperado: as versões voltam.
- [ ] 10.6 Clique em **Abrir como US** numa versão. Esperado: abre como uma US (ou usa a atual se estiver vazia) **sem apagar as outras**.
- [ ] 10.7 Clique em **Abrir como US** numa versão que já está aberta. Esperado: só troca para ela e mostra a mensagem.

## 11. IA (opcional)
- [ ] 11.1 Ligue **Usar IA** na lateral. O campo **API Key** começa **vazio**.
- [ ] 11.2 Aparece o aviso de **Privacidade** na lateral e outro acima do botão Gerar Cenários, citando o provedor.
- [ ] 11.3 O campo **Base URL** é **somente leitura** (fixa do provedor). Não existe mais a opção "Outro (compatível com OpenAI)".
- [ ] 11.4 Em **Azure OpenAI**, digite um endereço que não seja do Azure (ex.: `http://localhost`) e gere. Esperado: aviso de endpoint inválido e uso do motor local.
- [ ] 11.5 *(opcional, precisa de chave)* Gere cenários com uma chave sua e confira o resultado.
- [ ] 11.6 No formato E2E o aviso acima do botão some (o E2E não usa IA).

## 12. Importação e exportações
- [ ] 12.1 Em "Importar requisitos de PDF ou Word", envie um arquivo. Esperado: o texto extraído preenche o campo.
- [ ] 12.2 Na aba **Exportar**: Markdown, CSV e os arquivos para Xray, TestRail e Azure DevOps baixam sem erro.
- [ ] 12.3 Os nomes dos arquivos incluem o **nome da US** (ex.: `Login_cenarios.csv`).
- [ ] 12.4 Abra um CSV no Excel: não deve aparecer nenhuma fórmula executando.

## 13. Conferências gerais
- [ ] 13.1 Nenhuma tela mostra uma caixa vermelha de erro técnico (traceback).
- [ ] 13.2 O app abre e responde bem no **celular** (ou em janela estreita): o IArgus e a caixa de US não se sobrepõem.
- [ ] 13.3 No terminal podem aparecer avisos amarelos de funções "descontinuadas" do Streamlit (como `use_container_width`). Não afetam o uso e entram no próximo bloco da lista (compatibilidade).

## Se algo falhar
Me envie: o **número do item**, o que você esperava, o que aconteceu, uma captura de tela e, se houver, o texto do erro que apareceu no terminal.
