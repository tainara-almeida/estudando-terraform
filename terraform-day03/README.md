# Conseguindo ajuda

Embora seja importante ter o conhecimento prévio para executar suas tarefas, é muito comum que você encontre novos e diferentes desafios ao longo do caminho. Dito isso, é importante também saber onde encontrar as respostas para seus problemas.

## Notas

* O sufixo -h em qualquer comando retornará algumas informações sobre o comando que você precisa saber mais sobre
* É melhor tentar descobrir as coisas sozinho antes de pesquisar online

---

# Dependências

Na maioria das vezes, o Terraform infere dependências entre recursos com base na configuração fornecida, para que os recursos sejam criados e destruídos na ordem correta. Ocasionalmente, no entanto, o Terraform não pode inferir dependências entre diferentes partes da sua infraestrutura, e você precisará criar uma dependência explícita com o argumento depends_on.

Terraform versão 0.13 adicionou a capacidade de criar dependências explícitas entre módulos e recursos. As versões anteriores permitiam apenas dependências explícitas de recursos.

## Notas

* https://learn.hashicorp.com/tutorials/terraform/dependencies

---

# Terraform Commands & Verbose

O Terraform possui logs detalhados que podem ser ativados definindo a variável de ambiente TF_LOG para qualquer valor. Isso fará com que logs detalhados apareçam em stderr.

Você pode definir TF_LOG para um dos níveis de log TRACE, DEBUG, INFO, WARN ou ERROR para alterar o detalhamento dos logs. TRACE é o mais detalhado e é o padrão se TF_LOG for definido com algo diferente de um nome de nível de log.

Para persistir a saída registrada, você pode definir TF_LOG_PATH para forçar o log a sempre ser anexado a um arquivo específico quando o log estiver habilitado. Observe que mesmo quando TF_LOG_PATH é definido, TF_LOG deve ser definido para que qualquer registro seja habilitado.

Se você encontrar um bug no Terraform, inclua o registro detalhado usando um serviço como o gist.

## Notas

* Leitura Extra:
  * https://www.terraform.io/docs/internals/debugging.html

---

# Taint

O comando terraform taint marca manualmente um recurso gerenciado pelo Terraform como contaminado, forçando-o a ser destruído e recriado na próxima aplicação.

Este comando não modifica a infraestrutura, mas modifica o arquivo de estado para marcar um recurso como corrompido. Uma vez que um recurso é marcado como contaminado, o próximo plano mostrará que o recurso será destruído e recriado e a próxima aplicação implementará esta mudança.

## Notas

* Leitura extra:
  * https://www.terraform.io/docs/commands/taint.html

---

# Gráfico

O comando terraform graph é usado para gerar uma representação visual de uma configuração ou plano de execução. A saída está no formato DOT, que pode ser usado pelo GraphViz para gerar gráficos.

## Notas

* Leitura Extra:
  * https://www.terraform.io/docs/commands/graph.html
* Conteúdo Extra:
  * https://www.youtube.com/watch?v=Frmwdter-vQ&feature=youtu.be [português]
* A saída do gráfico de terraform está no formato DOT, que pode ser facilmente convertido em uma imagem usando o ponto fornecido pelo GraphViz:

`` `gráfico de terraform | dot -Tsvg> graph.svg```

---

# fmt

O comando terraform fmt é usado para reescrever os arquivos de configuração do Terraform para um formato e estilo canônicos. Este comando aplica um subconjunto das convenções de estilo da linguagem Terraform, junto com outros pequenos ajustes para facilitar a leitura.

Outros comandos do Terraform que geram a configuração do Terraform produzirão arquivos de configuração que estão de acordo com o estilo imposto pelo terraform fmt, portanto, usar esse estilo em seus próprios arquivos garantirá a consistência.

O formato canônico pode mudar de forma secundária entre as versões do Terraform, portanto, após atualizar o Terraform, recomendamos executar proativamente o Terraform fmt em seus módulos junto com quaisquer outras alterações que você esteja fazendo para adotar a nova versão.

## Notas

* Leitura extra:
  * https://www.terraform.io/docs/commands/fmt.html
  * https://www.terraform.io/docs/configuration/style.html

---

# validate

O comando terraform validate valida os arquivos de configuração em um diretório, referindo-se apenas à configuração e não acessando quaisquer serviços remotos como estado remoto, APIs de provedor, etc.

Validate executa verificações que verificam se uma configuração é sintaticamente válida e internamente consistente, independentemente de quaisquer variáveis ​​fornecidas ou estado existente. Portanto, é principalmente útil para verificação geral de módulos reutilizáveis, incluindo a exatidão de nomes de atributos e tipos de valores.

## Notas

* Muito útil para rodar em CI
* Leitura extra:
  * https://www.terraform.io/docs/commands/validate.html