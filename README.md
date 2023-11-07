Welcome to your new dbt project!

### Using the starter project

Try running the following commands:
- dbt run
- dbt test


### Resources:
- Learn more about dbt [in the docs](https://docs.getdbt.com/docs/introduction)
- Check out [Discourse](https://discourse.getdbt.com/) for commonly asked questions and answers
- Join the [dbt community](http://community.getbdt.com/) to learn from other analytics engineers
- Find [dbt events](https://events.getdbt.com) near you
- Check out [the blog](https://blog.getdbt.com/) for the latest news on dbt's development and best practices


# DBT - primeiros passos

Tema: dbt
Created by: Renato Cruz

# DBT data

### Sobre

O dbt (Data Build Tool) é uma ferramenta open-source que permite que você transforme, modele e orquestre seus dados de forma eficiente e escalável. Neste guia, vamos explorar um projeto dbt simples passo a passo, perfeito para iniciantes que desejam começar a trabalhar com dados.

# Dbt Cloud

### Requisto

- [ ]  Python instalado;
- [ ]  Command Line Tools (bash ou powershell)
- [ ]  Conhecimento básico em Git, Github ou GitLab

### Gerenciando vários projetos do bigquery

1. Crie projetos na Google Cloud. Neste exemplo vamos chamá-los de `xebia-data-preprod` e `xebia-data-prod` .

![1-1024x670.png.webp](DBT%20-%20primeiros%20passos%200630605d271d4c25bb78fccda20d7937/1-1024x670.png.webp)

O console do BigQuery deve ser parecido com isto, para ambos os projetos, onde platform é o conjunto de dados com os dados que queremos transformar. 

![2.png.webp](DBT%20-%20primeiros%20passos%200630605d271d4c25bb78fccda20d7937/2.png.webp)

![3.png.webp](DBT%20-%20primeiros%20passos%200630605d271d4c25bb78fccda20d7937/3.png.webp)

1. Crie uma conta de serviço na GCP

Para conectar o dbt Cloud a ambos os projetos, precisamos fornecer uma conta de serviço que tenha acesso a eles.

Primeiro, criaremos a conta de serviço em nosso projeto `xebia-data-preprod` :

![4-1024x424.png.webp](DBT%20-%20primeiros%20passos%200630605d271d4c25bb78fccda20d7937/4-1024x424.png.webp)

A seguir, geraremos uma `chave JSON` para ser usada no dbt Cloud. Para isso, devemos clicar na conta de serviço criada, navegar até a aba Chaves e criar a chave JSON. Um arquivo será gerado e baixado para o seu computador.

![5-1024x556.png.webp](DBT%20-%20primeiros%20passos%200630605d271d4c25bb78fccda20d7937/5-1024x556.png.webp)

Por fim, copiaremos o e-mail da conta de serviço criada e forneceremos acesso ao outro projeto ( `xebia-data-prod` ).

![6-1024x404.png.webp](DBT%20-%20primeiros%20passos%200630605d271d4c25bb78fccda20d7937/6-1024x404.png.webp)

1. Crie o projeto dbt Cloud

Do lado do dbt Cloud, vamos começar criando nosso novo projeto. Vamos chamá-lo de `xebia-data-platform` .

![7-1024x268.png.webp](DBT%20-%20primeiros%20passos%200630605d271d4c25bb78fccda20d7937/7-1024x268.png.webp)

A princípio não definiremos a conexão com o BigQuery, pois teríamos que atualizá-lo posteriormente para utilizar uma Variável de Ambiente , gerando retrabalho. Basta clicar no botão ' `Pular`'  por enquanto.

Depois de fazer isso, a próxima etapa (Configurar seu ambiente) será automaticamente ignorada.

![8-1024x211.png.webp](DBT%20-%20primeiros%20passos%200630605d271d4c25bb78fccda20d7937/8-1024x211.png.webp)

Finalmente, configure seu repositório com sua plataforma git preferida.

![9-1024x387.png.webp](DBT%20-%20primeiros%20passos%200630605d271d4c25bb78fccda20d7937/9-1024x387.png.webp)

1. Configure os ambientes no dbt Cloud

A seguir, criaremos três ambientes: `dev` , `preprod` e `prod` . `Dev` é um ambiente de desenvolvimento, enquanto `preprod` e `prod` são ambientes de implantação.

![10-1024x312.png.webp](DBT%20-%20primeiros%20passos%200630605d271d4c25bb78fccda20d7937/10-1024x312.png.webp)

O resultado final deverá ficar assim:

![11-1024x385.png.webp](DBT%20-%20primeiros%20passos%200630605d271d4c25bb78fccda20d7937/11-1024x385.png.webp)

1. Configure as variáveis de ambiente no dbt Cloud

A próxima etapa é criar uma variável de ambiente para cada ambiente. Isso nos permitirá usar o projeto `xebia-data-preprod` GCP no ambiente `preprod` dbt Cloud e o projeto `xebia-data-prod` GCP no ambiente `prod` dbt Cloud.

Para criar uma variável de ambiente é bastante simples: na página Ambientes , selecione Variáveis de ambiente e clique em ' `Adicionar variável`' *.*

Chamaremos nossa variável `DBT_GCP_PROJECT` e definiremos os valores da seguinte forma:

![12-1024x339.png.webp](DBT%20-%20primeiros%20passos%200630605d271d4c25bb78fccda20d7937/12-1024x339.png.webp)

Como temos apenas dois projetos GCP, usaremos o mesmo projeto para `preprod` e `dev` , porém é possível implementar a mesma lógica com três ou mais projetos.

Uma vez definida a variável, podemos configurar a conexão com o BigQuery, usando a variável recém-criada para alternar entre projetos dependendo do ambiente em uso.

1. Configure os detalhes da conexão no DBT cloud

Para definir a conexão com o BigQuery, primeiro devemos navegar até as Configurações da conta. Lá podemos encontrar todos os nossos projetos. Clicaremos no projeto que acabamos de criar e depois em ' `Configurar Conexão`' .

![13-1024x250.png.webp](DBT%20-%20primeiros%20passos%200630605d271d4c25bb78fccda20d7937/13-1024x250.png.webp)

A próxima etapa é definir o tipo de conexão como BigQuery e importar o `arquivo JSON` que geramos da conta de serviço. Feito isso, todas as demais informações deverão ser preenchidas.

![14-1024x1001.png.webp](DBT%20-%20primeiros%20passos%200630605d271d4c25bb78fccda20d7937/14-1024x1001.png.webp)

Por fim, substituiremos o `ID do projeto` que foi preenchido automaticamente pela variável que criamos:

```bash
{{ env_var("DBT_GCP_PROJECT") }}
```

![15-1024x1007.png.webp](DBT%20-%20primeiros%20passos%200630605d271d4c25bb78fccda20d7937/15-1024x1007.png.webp)

Como etapa adicional, configuraremos as Credenciais de Desenvolvimento . Para fazer isso, navegue até a página ' `Credenciais`' , selecione o projeto e escolha um nome de ' `Conjunto de dados`' exclusivo para você `- dbt_NAME` (nome do usuário).

![16-1024x365 png](https://github.com/PlatosSD/dbt_demo/assets/32683908/5ab0ee01-8332-4520-bff3-51d9ffdfefe4)

A partir de agora, seu projeto dbt já deverá estar funcionando com dois projetos diferentes do GCP. Tudo o que resta fazer é definir o pipeline de implantação para cada ambiente individual.

1. Configure seu pipeline de implementação para cada ambiente

> Editar: você pode seguir as etapas sobre como configurar seu pipeline de implantação neste novo artigo
(*[CI/CD em dbt Cloud com GitHub Actions: Automatizando a implantação de vários ambientes](https://xebia.com/blog/ci-cd-in-dbt-cloud-with-github-actions-automating-multiple-environments-deployment/)*)
> 

Como o objetivo deste artigo não é sobre as melhores práticas de configuração da implantação, não nos aprofundaremos nisso. Algumas dicas gerais:

- Defina um Job para executar o ambiente *de* `preprod` **quando uma solicitação pull for criada, no dbt Cloud.
- Siga [este link](https://docs.getdbt.com/guides/orchestration/custom-cicd-pipelines/3-dbt-cloud-job-on-merge) de `prod` **para configurar o ambiente para ser executado assim que o PR for mesclado.
- Defina um Job para executar o ambiente de `prod` **diariamente, no dbt Cloud.

Após construir os modelos para cada ambiente, e também no IDE Develop, você deverá ter dois projetos parecidos com as imagens abaixo:

![17.png.webp](DBT%20-%20primeiros%20passos%200630605d271d4c25bb78fccda20d7937/17.png.webp)

![18 png](https://github.com/PlatosSD/dbt_demo/assets/32683908/375f4fff-88af-4287-8f3c-aef4e39ec67c)

1. Conclusão

### ****CI/CD em dbt Cloud com GitHub Actions: Automatizando a implantação de vários ambientes****

1.Crie um `Job` para construir o ambiente diariamente

A primeira etapa na configuração de nosso pipeline de CI/CD no dbt Cloud é criar um Job que seja executado diariamente. Dessa forma, garantimos que estamos nos desenvolvendo com as transformações mais atualizadas, sem comprometer muitos recursos.

Para criar o Job, navegaremos até a guia Jobs, no item Deploy da barra superior, e clicaremos no botão `Create Job` *.*

![1-1024x297.png.webp](DBT%20-%20primeiros%20passos%200630605d271d4c25bb78fccda20d7937/1-1024x297.png.webp)

Nomearemos o trabalho como `Build preprod` e selecionaremos o ambiente *de* `preprod` .

![2-1024x569.png.webp](DBT%20-%20primeiros%20passos%200630605d271d4c25bb78fccda20d7937/2-1024x569.png.webp)

Manteremos as *`configurações de execução`* como padrão, apenas com o comando dbt build. Você pode editar isso dependendo de seus requisitos.

Para os `Triggers` , definiremos o `Schedule` para ser executado diariamente pela manhã.

![3-1024x456.png.webp](DBT%20-%20primeiros%20passos%200630605d271d4c25bb78fccda20d7937/3-1024x456.png.webp)

O primeiro passo da nossa configuração está feito, basta *Salvar* o Job e ele começará a rodar diariamente.

1. Crie um `Job` para construir os modelos modificados no ambiente de `preprod` em cada PR

A seguir, criaremos um `Job` que é acionado sempre que um `Pull Request` é aberto. Este `Job` deve executar os testes e validações necessários para garantir que as alterações no código estejam prontas para serem mescladas no branch principal. A tarefa criará apenas os modelos modificados e seus modelos downstream dependentes.

Chamaremos o trabalho de “ `CI preprod`*”* e selecionaremos o ambiente *de* `preprod` .

![4-1024x602.png.webp](DBT%20-%20primeiros%20passos%200630605d271d4c25bb78fccda20d7937/4-1024x602.png.webp)

Nas configurações de execução, definimos o seguinte:

- Defina “Adiar para o estado de execução anterior?” para o **`preprod build`**. Isso garante que nosso trabalho de CI não será acionado caso haja problemas com o ambiente.
- Defina os comandos para`dbt build --select state:modified+`

![5-1024x529.png.webp](DBT%20-%20primeiros%20passos%200630605d271d4c25bb78fccda20d7937/5-1024x529.png.webp)

Executamos este comando para construir apenas os modelos modificados e seus modelos downstream dependentes, que são identificados pelo símbolo '+' no final do comando.

Você pode estar se perguntando por que seguimos esse processo de construção de CI/CD, em vez de construir o projeto inteiro. Existem alguns motivos principais:

✅ Construir os modelos modificados e modelos downstream relacionados é o ideal. Apenas os modelos necessários são executados para detectar quaisquer problemas causados pelas modificações.

❌ Construir os modelos modificados com modelos upstream e downstream relacionados executando “`dbt build --select +state:modified+`” (observe o '+' extra antes de *state* ) pode ser uma opção, mas preferimos atualizar o ambiente de `preprod` diariamente para que possamos não exigem dados novos em cada execução de CI.

❌ Construir todo o projeto é muito pesado, um desperdício de recursos e provavelmente demorado.

❌ Construir apenas modelos alterados é insuficiente, pois não identifica problemas nos modelos posteriores.

Por fim, para definir o gatilho *de* `Integração Contínua (CI)` , tudo o que precisamos fazer é selecionar a opção `Executar em Pull Request?` caixa de seleção.

Observação: para habilitar o gatilho de CI, você deve conectar seu projeto dbt Cloud ao GitHub, GitLab ou Azure DevOps.

![6-1024x227.png.webp](DBT%20-%20primeiros%20passos%200630605d271d4c25bb78fccda20d7937/6-1024x227.png.webp)

Depois que o gatilho for definido, `salve` o trabalho e crie uma solicitação pull para verificar se o trabalho de CI está funcionando. Cada `Pull Request` novo ou atualizado deve acionar uma execução de `Job` no ambiente dbt Cloud.

![7-1024x406.png.webp](DBT%20-%20primeiros%20passos%200630605d271d4c25bb78fccda20d7937/7-1024x406.png.webp)

1. Crie um `Job` para construir o ambiente de `prod`

A seguir, definiremos o Job para executar o ambiente de **`prod` . O objetivo é ter um Job que execute o ambiente de produção por um `Schedule` e que seja executado assim que um Pull Request for mesclado.

Por último, não há opções nativas do dbt, então teremos que definir uma ação do GitHub para executar o trabalho usando a API do dbt Cloud. O mesmo pode ser feito usando Azure DevOps ou GitLab, mas vamos nos concentrar no GitHub neste artigo.

Primeiramente, criaremos um novo `Job`, nomeá-lo `Build prod` e selecionaremos `prod` como ambiente.

![8-1024x556.png.webp](DBT%20-%20primeiros%20passos%200630605d271d4c25bb78fccda20d7937/8-1024x556.png.webp)

Manteremos as `configurações de execução` como padrão, apenas com o comando `dbt build` .

Para o gatilho agendamento, também configuraremos o `Schedule` para ser executado diariamente pela manhã.

![9-1024x455.png.webp](DBT%20-%20primeiros%20passos%200630605d271d4c25bb78fccda20d7937/9-1024x455.png.webp)

A configuração do trabalho do lado do dbt está concluída, agora a configuração começa a se tornar mais desafiadora. Definiremos um GitHub Actions para chamar a API dbt Cloud assim que o PR for mesclado.

1. Configure um `Gihub Actions`

Para configurar o `GitHub Action`, primeiro precisaremos de algumas informações do dbt: `Account Id`*,* `Job Id`*,* `Project Id` e `API Key` .

Para os dois primeiros, navegaremos até a guia API na configuração do trabalho. Lá, podemos encontrar o *`ID da conta`* e *o `ID do trabalho`* . Devemos salvar esses valores para serem usados posteriormente.

![10-1024x478.png.webp](DBT%20-%20primeiros%20passos%200630605d271d4c25bb78fccda20d7937/10-1024x478.png.webp)

Na mesma página, procuraremos o URL. Lá podemos encontrar o `ID do projeto` .

![11-1024x143.png.webp](DBT%20-%20primeiros%20passos%200630605d271d4c25bb78fccda20d7937/11-1024x143.png.webp)

Por fim, navegaremos até a página *de acesso à API* na opção *Configurações da conta* . Lá podemos encontrar o valor *da chave API* .

![12-1024x528.png.webp](DBT%20-%20primeiros%20passos%200630605d271d4c25bb78fccda20d7937/12-1024x528.png.webp)

Com todos os quatro parâmetros em mãos, podemos acessar nosso repositório GitHub para configurar a ação.

Assim que o repositório estiver aberto, navegaremos para *Configurações* > *Segredos e variáveis* > *Ações.* Criaremos um `New repository secret` , nomeando-o `DBT_API_KEY` e definindo-o como o valor *da chave API* que copiamos do dbt.

![13-1024x625.png.webp](DBT%20-%20primeiros%20passos%200630605d271d4c25bb78fccda20d7937/13-1024x625.png.webp)

Depois de definido, navegaremos até a guia *Variáveis* e definiremos os outros três valores como Variáveis. Como esses valores não são confidenciais, não há necessidade de defini-los como segredos.

```bash
DBT_ACCOUNT_ID
```

```bash
DBT_JOB_ID
```

```bash
DBT_PROJECT_ID
```

Agora, faltam apenas duas etapas para finalizar nossa configuração: Adicionar um script python que chamará a API e definir a ação GitHub que executará o script. Faremos ambos no IDE *de desenvolvimento* do dbt .

Depois de aberto, primeiro criaremos uma nova pasta chamada *python* . Lá podemos centralizar todos os nossos scripts python. Dentro desta pasta, criaremos um arquivo chamado `run_and_monitor_dbt_job.py` . Copie o conteúdo desta [gist](https://gist.github.com/b-per/f4942acb8584638e3be363cb87769b48) para o novo arquivo. Este script tem tudo que você precisa para chamar a API dbt Cloud, as entradas necessárias são alimentadas na próxima etapa, como variáveis de ambiente.

O resultado final deve ficar assim.

![14-1024x607.png.webp](DBT%20-%20primeiros%20passos%200630605d271d4c25bb78fccda20d7937/14-1024x607.png.webp)

A próxima etapa é *finalmente* definir a ação do GitHub.

Primeiro criaremos uma pasta chamada *.github* , com uma subpasta chamada *workflows* e um arquivo chamado `dbt_run_on_merge.yml` . Copie o código a seguir e cole-o no novo arquivo. Como está conectado com *segredos* e *variáveis* , você não precisa editá-lo.

```yaml
name: run dbt Cloud job on push

# This filter says only run this job when there is a push to the main branch

# This works off the assumption that you've restricted this branch to only all PRs to push to the default branch

# Update the name to match the name of your default branch

on:

 push:

   branches:

     - 'main'

jobs:

 # the job calls the dbt Cloud API to run a job

 run_dbt_cloud_job:

   name: Run dbt Cloud Job

   runs-on: ubuntu-latest

 # Set the environment variables needed for the run

   env:

     DBT_ACCOUNT_ID: ${{ vars.DBT_ACCOUNT_ID }}

     DBT_PROJECT_ID: ${{ vars.DBT_PROJECT_ID }}

     DBT_PR_JOB_ID:  ${{ vars.DBT_JOB_ID }}

     DBT_API_KEY: ${{ secrets.DBT_API_KEY }}

     DBT_JOB_CAUSE: 'GitHub Pipeline CI Job'

     DBT_JOB_BRANCH: ${{ github.ref_name }}

   steps:

     - uses: "actions/checkout@v3"

     - uses: "actions/setup-python@v4"

       with:

         python-version: "3.9"

     - name: Run dbt Cloud job

       run: "python python/run_and_monitor_dbt_job.py"
```

Por fim, é assim que seu projeto deve ficar, com as novas pastas e arquivos.

![15.png.webp](DBT%20-%20primeiros%20passos%200630605d271d4c25bb78fccda20d7937/15.png.webp)

Agora só falta criar um `Pull Request` com nossas alterações recém-feitas, mesclar e esperar a mágica acontecer!

Você pode verificar se a execução foi bem-sucedida no GitHub, na guia *Actions* , ou no dbt, na guia *Jobs*

`GitHub Actions`

![16.png.webp](DBT%20-%20primeiros%20passos%200630605d271d4c25bb78fccda20d7937/16.png.webp)

`Job de DBT`

![17-1024x69 png](https://github.com/PlatosSD/dbt_demo/assets/32683908/f7899652-715c-4b9f-9dc3-ea9e58567d53)

### Referências

[textos]

[Managing Multiple BigQuery Projects With One dbt Cloud Project](https://xebia.com/blog/managing-multiple-bigquery-projects-with-one-dbt-cloud-project/)

[Loading and transforming data into BigQuery using dbt](https://medium.com/google-cloud/loading-and-transforming-data-into-bigquery-using-dbt-65307ad401cd)

[CI/CD in dbt Cloud with GitHub Actions: Automating multiple environments deploymentting-multiple-environments-deployment](https://xebia.com/blog/ci-cd-in-dbt-cloud-with-github-actions-automating-multiple-environments-deployment/)

[vídeos]

[Getting Started With dbt | Set Up dbt Cloud for Google BigQuery](https://www.youtube.com/watch?v=6zDTbM6OUcs)

---

# Dbt Core

### Requisto

- [ ]  Python instalado;
- [ ]  Command Line Tools (bash ou powershell)
- [ ]  Conhecimento básico em Git, Github ou GitLab

### Parte 1 - Criação de ambiente virtual

1. Crie uma pasta dedicada ao ambiente de projeto;
2. Crie o ambiente virtual

```bash
python -m venv venv
```

```bash
virtualenv venv
```

1. Ative o ambiente virtual

```bash
source scripts/activate
```

```bash
source venv/bin/activate
```

1. Instale o dbt

```bash
pip install dbt-core dbt-bigquery
```

1. Verifique se a instalação foi bem sucedida

```bash
dbt –version
```

1. Inicie o dbt

```bash
dbt init NOME_DA_PASTA
```

O projeto é construído logo após executar o comando acima e se parece com a imagem abaixo.

[https://www.notion.so](https://www.notion.so)

O arquivo `[README.md](http://README.md)` descreverá o propósito e o escopo geral do projeto. Já o arquivo `dbt_project.yml` irá gerenciar e operar as pastas e arquivos do projeto. A pasta `Models` conterá os exemplos de códigos e nossos novos códigos. Observe que cada arquivo `SQL` dentro de `Models` é um modelo dentro do projeto.

Obs. : Todo projeto dbt precisa de um arquivo dbt_project.yml - é assim que o dbt sabe que um diretório é um projeto dbt. Ele também contém informações importantes que informam ao dbt como operar em seu projeto.

### Parte 2 - Criação de repositório no GitHub

1. Crie um novo repositório
2. No bash, inicialize o repositório do projeto

```bash
git init
git branch -M main
git add .
git commit -m "DESCREVA o COMMIT"
git remote add origin <https://PROJECT_GIT_REPO>
git push -u origin main
git checkout -b development
```

### Parte 3 - Conexão com database Warehouse

Além disso, deverá ser criado o arquivo `profiles.yml` na raiz do dbt instalado. O caminho deste local pode ser parecido com `Windows (C:) > Users > SeuNome > .dbt`. 

Este arquivo irá receber as seguintes informações:

```yaml
dbt_etl_v1: # this needs to match the profile in your dbt_project.yml file
  target: test

  outputs:    
    test:
      type: bigquery # database type
      method: service-account # authentication method
      keyfile: # C:\Users\YourName\YourFolder\project_bigquery_service_account.json # project_bigquery_service_account.json
      project: sonic-aria-366017 # project id
      dataset: Staging # Replace this with dbt_you_name, e. g. dbt_bilbo
      thereds: 1
      timeout_seconds: 300
      location: US
      priority: interactive

    dev:
      type: bigquery # database type
      method: service-account # authentication method
      keyfile: C:\Users\YourName\YourFolder\project_bigquery_service_account.json # project_bigquery_service_account.json
      project: # project id
      dataset: Staging # Replace this with dbt_you_name, e. g. dbt_bilbo
      thereds: 1
      timeout_seconds: 300
      location: US
      priority: interactive
    
    prod:
      type: bigquery # database type
      method: service-account # authentication method
      keyfile: C:\Users\YourName\YourFolder\project_bigquery_service_account.json # project_bigquery_service_account.json 
      project: # project id
      dataset: Staging # Replace this with dbt_you_name, e. g. dbt_bilbo
      thereds: 1
      timeout_seconds: 300
      location: US
      priority: interactive
```

Para maiores informações sobre `profiles.yml` consultar links abaixos:

[About profiles.yml](https://docs.getdbt.com/docs/core/connect-data-platform/profiles.yml)

[BigQuery setup](https://docs.getdbt.com/docs/core/connect-data-platform/bigquery-setup)

[dbt-bigquery](https://github.com/dbt-labs/dbt-bigquery)

1. Teste a conexão com o banco

```bash
dbt debug --connection
```

Para mais informações sobre conexão, consultar o link abaixo:
[About dbt debug command](https://docs.getdbt.com/reference/commands/debug)

### Parte 4 e 5 - Construir modelos dbt’s, executar, testar e gerar documentação

1. Modelos dbt devem ser do tipo `SQL` e ficar dentro da pasta `Models`.

- - - - 

### Referências

[textos]

[What is dbt?](https://docs.getdbt.com/docs/introduction)

[Quickstart for dbt Cloud and BigQuery](https://docs.getdbt.com/quickstarts/bigquery?step=1)

[vídeos]

[dbt (data build tool) Crash Course For Beginners (dbt Core) | Full Tutorial](https://www.youtube.com/watch?v=toSAAgLUHuk&list=LL&index=1)

[Getting Started With dbt | Set Up dbt Cloud for Google BigQuery](https://www.youtube.com/watch?v=6zDTbM6OUcs)
