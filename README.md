README – Pipeline CI/CD com GitHub Actions e GitHub Pages

Este documento descreve o funcionamento completo do pipeline CI/CD desenvolvido utilizando GitHub Actions, com deploy automatizado no GitHub Pages. Ele reúne informações essenciais sobre estrutura do projeto, workflows, erros encontrados, soluções aplicadas e a lógica de execução do pipeline.

----------------------------------------

ESTRUTURA DO PROJETO

A organização do repositório segue a estrutura padrão utilizada para pipelines GitHub Actions, garantindo clareza, modularidade e separação adequada entre os artefatos da aplicação e os arquivos responsáveis pela automação.


atividade_pipeline/
 ├── site/
 │    └── index.html
 └── .github/
      └── workflows/
           ├── ci.yml
           └── cd.yml
    

----------------------------------------

PIPELINE CI/CD

O pipeline foi dividido em dois workflows principais: um responsável pela integração contínua (CI) e outro dedicado ao deploy contínuo (CD). Essa divisão permite maior controle sobre cada etapa e facilita o rastreamento de falhas, bem como a reexecução parcial do pipeline sempre que necessário.



1. Integração Contínua (CI) — .github/workflows/ci.yml

O CI é acionado automaticamente a cada push realizado na branch 'main'. Seu objetivo é verificar se o arquivo 'site/index.html' está presente e válido antes de permitir que o processo de deploy seja iniciado.

Comando utilizado:

test -f site/index.html



2. Deploy Contínuo (CD) — .github/workflows/cd.yml

Após o sucesso do CI, o workflow de deploy copia os arquivos do diretório 'site/' para o diretório temporário 'public/', e utiliza a action 'peaceiris/actions-gh-pages@v3' para publicar o conteúdo automaticamente na branch 'gh-pages', a qual alimenta o GitHub Pages.



----------------------------------------

PÁGINA PUBLICADA

A página final pode ser acessada através do link:

https://thonnymuniz.github.io/atividade_pipeline_mackenzie/



----------------------------------------

PROBLEMA ENCONTRADO E SOLUÇÃO

Durante o desenvolvimento, foi identificado um erro 403 relacionado às permissões padrão do GITHUB_TOKEN. Como o token estava configurado apenas para leitura, o processo de deploy não conseguiu efetuar o commit automatizado na branch 'gh-pages'.

SOLUÇÃO:

1. Acessar Settings → Actions → General
2. Alterar a permissão para: Read and Write Permissions
3. Forçar nova execução com:
   git commit --allow-empty -m 'Forçando novo deploy'
   git push



----------------------------------------

ORDEM REAL DE EXECUÇÃO DO PIPELINE

1. Push enviado à branch 'main'
2. CI é acionado
3. Runner executa checkout
4. Validação do arquivo index.html
5. CD inicia a preparação do deploy
6. Geração da pasta public/
7. Cópia dos arquivos de site/
8. Commit automático na branch gh-pages
9. GitHub Pages atualiza o site



----------------------------------------

TECNOLOGIAS UTILIZADAS

- Git & GitHub
- GitHub Actions
- GitHub Pages
- HTML5
- Ubuntu Runner



----------------------------------------

AUTOR

Thonny Tonzar Muniz – MBA em Engenharia de Dados, Universidade Presbiteriana Mackenzie
