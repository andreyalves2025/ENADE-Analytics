# ENADE Analytics

Repositório do Projeto Integrador ENADE Analytics, da disciplina de Business Intelligence (2026).

Curso Superior de Tecnologia em Gestão da Informação, IFPR Campus Pinhais.

Equipe: Andrey Dmitrievich Muniz Alves, Arthur Mendes de Vasconcelos, Leonardo Henrique Maximo e Maira Aparecida Michelon.

Vídeo Apresentação: https://drive.google.com/file/d/1QJ0VBYxCWTl04pFYMD-TUapekCLx4DeG/view

## Descrição do projeto

O ENADE Analytics é uma solução de Business Intelligence, do dado bruto ao dashboard. Ele apoia a preparação dos concluintes do curso para o ENADE 2026. A partir de simulados respondidos por estudantes voluntários, o projeto organiza as respostas em um Data Warehouse e identifica, de forma agregada e anônima, as forças e fraquezas da turma por eixo temático do componente específico e por nível de dificuldade. O resultado é apresentado em um dashboard interativo no Power BI. O projeto integra conhecimentos de gestão de projetos, modelagem de dados, ETL, OLAP, mineração de dados e visualização.

## Objetivo geral

Desenvolver uma solução de BI que permita à coordenação do curso identificar, com dados, as lacunas de conhecimento dos concluintes por eixo temático do ENADE 2026. A solução também deve acompanhar a evolução dessas lacunas ao longo do semestre e apoiar a decisão de onde direcionar as ações de reforço.

## Justificativa

Hoje, o acompanhamento da preparação para o ENADE é informal: cada professor percebe, à sua maneira, onde os alunos têm mais dificuldade, mas não existe um retrato consolidado do curso. Sem essa visão, fica difícil decidir em quais eixos reforçar as aulas de revisão, quais turmas precisam de mais atenção e se o desempenho está melhorando. O ENADE Analytics substitui impressões por evidências: transforma as respostas dos simulados em indicadores claros, sempre agregados e anônimos, para que o reforço chegue onde é realmente necessário.

## Público-alvo

O público-alvo divide-se em dois grupos.

- **Coordenação e professores do curso:** são quem usa o dashboard. Precisam de uma visão clara e rápida dos pontos fortes e fracos da turma para planejar revisões e ações de reforço.
- **Estudantes concluintes:** participam voluntariamente dos simulados e são os beneficiários finais. Recebem reforço direcionado às suas lacunas, e seus dados pessoais ficam protegidos.

## Escopo

Entre as principais entregas, destacam-se:

- banco de questões de simulado, classificado por eixo temático e por nível de dificuldade (Fácil, Médio, Difícil);
- aplicação de um simulado-piloto com estudantes voluntários (Google Forms), com termo de consentimento (TCLE);
- anonimização dos participantes por pseudônimo, sem nome, CPF, e-mail ou matrícula;
- processo de ETL no Power Query, do formulário ao modelo;
- Data Warehouse em esquema estrela (1 fato e 4 dimensões);
- análise de padrões e lacunas de conhecimento (OLAP e mineração);
- dashboard interativo com storytelling de dados, que responde às perguntas da coordenação;
- uso de IA generativa como apoio (revisão de questões, documentação e resumos).

**Fora do escopo:** identificar estudantes individualmente, usar os resultados para avaliação formal, substituir o ENADE oficial e usar ferramentas pagas.

### Perguntas que o dashboard responde

1. Quais eixos temáticos têm o pior desempenho médio?
2. Existe diferença de desempenho entre turmas ou grupos? (O piloto tem só a turma GTI6, e o modelo já está preparado para outras.)
3. As lacunas estão concentradas em poucos estudantes ou distribuídas pela turma?
4. O desempenho melhora ao longo do semestre? (O piloto é a linha de base.)

### Primeiros resultados (simulado-piloto, 02/10/2026, n = 11)

- Taxa de acerto geral de **54,5%**, abaixo da meta de 60%.
- **Forças** (≥ 60%): Engenharia de Software, Governança de TI e Ética, Segurança da Informação, Dados e BI.
- **Fraquezas** (< 50%): Gestão de Projetos, Banco de Dados, Redes e Infraestrutura.
- Questões de nível médio tiveram o menor acerto (40%).
- **5 de 11** participantes atingiram a meta.

## Descrição técnica

O projeto segue o ciclo clássico de BI: coleta, ETL, Data Warehouse, análise e visualização. A gestão é feita por marcos definidos no briefing da coordenação. O modelo de dados usa um esquema estrela com grão de **uma resposta de um aluno a uma questão em um simulado**.

| Tabela | Conteúdo |
|---|---|
| `Fato_Respostas` | id_simulado, id_questao, id_dificuldade, id_turma, codigo_aluno, resposta_aluno, acertou, resultado, carimbo_data_hora |
| `Dim_Questao_Eixo` | id_questao, numero, tema, rotulo_questao, eixo_tematico, gabarito |
| `Dim_Dificuldade` | id_dificuldade, nivel, criterio |
| `Dim_Simulado` | id_simulado, simulado, data_aplicacao, semana_semestre |
| `Dim_Turma` | id_turma, turma, curso |

<img width="1364" height="688" alt="Esquema estrela ENADE Analytics" src="https://github.com/user-attachments/assets/fc136b64-2827-4fb1-bc9a-b88f65e2cb05" />

### Tecnologias

- **Coleta:** Google Forms (simulado e TCLE);
- **Armazenamento e base anonimizada:** Microsoft Excel (.xlsx);
- **ETL:** Power Query;
- **Modelo de dados e medidas:** Power BI Desktop (esquema estrela e DAX);
- **Visualização:** Power BI Desktop (dashboard com 5 páginas);
- **Apoio:** IA generativa (revisão de questões, documentação e resumos);
- **Gestão:** marcos semanais (M0 a M5) definidos no briefing.

Todas as ferramentas são gratuitas.

## Roteiro de execução do ENADE Analytics

Antes de começar, instale o **Power BI Desktop** (gratuito, pela Microsoft Store ou pelo site da Microsoft). Ele roda apenas em Windows.

1. **Baixar os arquivos.** Baixe [ENADE Analytics.zip](https://github.com/user-attachments/files/35489478/ENADE.Analytics.zip) que contém os arquivos "ENADE Analytics.pbix" pronto para rodar no Power BI e "ENADE Analytics Dados.xlsx" com as repostas do simulado já devidamente anonimizadas. Extraia o conteúdo.
2. **Abrir o dashboard.** Dê dois cliques no `.pbix` ou, no Power BI Desktop, use Arquivo → Abrir. Os dados do piloto já estão no arquivo e as páginas abrem prontas.
3. **Navegar pelas páginas.**
   - Visão geral: indicadores da turma.
   - Forças e fraquezas: desempenho por eixo e dificuldade.
   - Os alunos: distribuição por faixas, sempre agregada.
   - Questões e erros: onde e como a turma erra.
   - Próximos passos: recomendações.

   Use as segmentações (simulado, turma, eixo) para filtrar.
4. **Sem Power BI?** Veja o **PDF** do dashboard disponível neste repositório.

## LGPD e ética

- Nenhuma coluna contém nome, CPF, e-mail ou matrícula. Os participantes são identificados apenas por pseudônimo sequencial (A01…A11).
- O pseudônimo nunca aparece em visual: o dashboard mostra somente agregados.
- A participação é voluntária e precedida do Termo de Consentimento Livre e Esclarecido (TCLE).
- Os resultados não são usados para aprovação, reprovação ou avaliação formal dos estudantes.
