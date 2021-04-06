# Blocos dinâmicos

Em construções de bloco de nível superior, como recursos, as expressões geralmente podem ser usadas apenas ao atribuir um valor a um argumento. Isso cobre muitos usos, mas alguns tipos de recursos incluem blocos aninhados repetíveis em seus argumentos, que não aceitam expressões.

Você pode construir blocos aninhados repetíveis dinamicamente, como a configuração usando um tipo de bloco dinâmico especial, que é compatível com blocos de recurso, dados, provedor e provisionador.

## Notas

* Leitura extra:
  * https://www.terraform.io/docs/configuration/expressions/dynamic-blocks.html

---

# String Template

Dentro das expressões de string entre aspas e heredoc, as sequências $ {e% {começam as sequências de modelo. Os modelos permitem incorporar expressões diretamente em um literal de string, para construir strings dinamicamente a partir de outros valores.

## Notas

* Leitura Extra:
  * https://www.terraform.io/docs/configuration/expressions/strings.html

---

# Terraform Cloud

Quando executado localmente, o Terraform gerencia cada coleção de infraestrutura com um diretório de trabalho persistente, que contém uma configuração, dados de estado e variáveis. Como o Terraform CLI usa conteúdo do diretório em que é executado, você pode organizar os recursos de infraestrutura em grupos significativos, mantendo suas configurações em diretórios separados.

Terraform Cloud gerencia coleções de infraestrutura com espaços de trabalho em vez de diretórios. Um espaço de trabalho contém tudo o que o Terraform precisa para gerenciar uma determinada coleção de infraestrutura, e espaços de trabalho separados funcionam como diretórios de trabalho completamente separados.

Observação: Terraform Cloud e Terraform CLI têm recursos chamados "espaços de trabalho", mas são um pouco diferentes. Os espaços de trabalho CLI são arquivos de estado alternativo no mesmo diretório de trabalho; eles são um recurso conveniente para usar uma configuração para gerenciar vários grupos de recursos semelhantes.
## Notas

* Leitura Extra:
  * https://www.terraform.io/docs/cloud/workspaces/index.html
  * https://www.terraform.io/docs/cloud/users-teams-organizations/api-tokens.html