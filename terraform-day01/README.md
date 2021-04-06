# Introdução

Infraestrutura como código (IaC) é o processo de gerenciamento e provisionamento de data centers de computador por meio de arquivos de definição legíveis por máquina, em vez de configuração de hardware físico ou ferramentas de configuração interativas.

Terraform é uma ferramenta para criar, alterar e criar versões de infraestrutura com segurança e eficiência. Terraform pode gerenciar provedores de serviços existentes e populares, bem como soluções internas personalizadas.

Infraestrutura como código
A infraestrutura é descrita usando uma sintaxe de configuração de alto nível. Isso permite que um projeto de seu datacenter seja versionado e tratado como você faria com qualquer outro código. Além disso, a infraestrutura pode ser compartilhada e reutilizada.

### Planos de Execução
O Terraform possui uma etapa de "planejamento" onde gera um plano de execução. O plano de execução mostra o que o Terraform fará quando você chamar apply. Isso permite que você evite surpresas quando o Terraform manipular a infraestrutura.

### Gráfico de recursos
O Terraform cria um gráfico de todos os seus recursos e paraleliza a criação e modificação de quaisquer recursos não dependentes. Por causa disso, o Terraform cria a infraestrutura da forma mais eficiente possível e os operadores obtêm informações sobre as dependências em sua infraestrutura.

### Mudança de automação
Mudanças complexas podem ser aplicadas à sua infraestrutura com o mínimo de interação humana. Com o plano de execução e o gráfico de recursos mencionados anteriormente, você sabe exatamente o que o Terraform mudará e em que ordem, evitando muitos possíveis erros humanos.

## Notas do dia

* Resumindo, Terraform (bin) lê o arquivo de definição (HCL), compara com o estado e gera ou modifica os recursos para espelhar o arquivo de configuração.
* O Terraform funciona de forma descritiva, como em: você define como deseja que seus recursos sejam configurados e o Terraform garante que os recursos "cheguem lá"

## Leitura extra

* https://www.terraform.io/intro/index.html
* https://www.hashicorp.com/resources/what-is-mutable-vs-immutable-infrastructure

--- 

# Compreendendo a HCL (linguagem de configuração HashiCorp)

Tópicos abordados:
* Sintaxe de bloco
   * Argumentos
* Identificadores
* Fornecedor

## Leitura Extra

* https://www.terraform.io/docs/configuration/syntax.html

--- 

# Comandos básicos

Tópicos abordados:
* o arquivo * .tfstate contém informações importantes, que não devem ser contidas localmente, porque outros membros da equipe precisam trabalhar com você. Por isso, é recomendável usar um back-end remoto (e seguro). Neste curso, usaremos AWS S3

## Comandos

* terraform plan - O comando plano de terraform é usado para criar um plano de execução. O Terraform realiza uma atualização, a menos que seja explicitamente desativado, e então determina quais ações são necessárias para atingir o estado desejado especificado nos arquivos de configuração.
  * O argumento opcional -out pode ser usado para salvar o plano gerado em um arquivo para execução posterior com a aplicação do terraform, que pode ser útil ao executar o Terraform em automação [https://learn.hashicorp.com/tutorials/terraform/automate- terraform]
  * https://www.terraform.io/docs/commands/plan.html
  * terraform plan [opções] [dir]
* terraform apply - O comando terraform apply é usado para aplicar as alterações necessárias para alcançar o estado desejado da configuração ou o conjunto pré-determinado de ações gerado por um terraform plan excutando o plan
  * https://www.terraform.io/docs/commands/apply.html
  * terraform apply [opções] [dir-or-plan]
* terraform destroy - A infraestrutura gerenciada pelo Terraform será destruída. Isso pedirá confirmação antes de destruir.
  * https://www.terraform.io/docs/commands/destroy.html
  * terraform destroy [opções] [dir]

---

# Expressões e console

As expressões são usadas para referir-se ou calcular valores dentro de uma configuração. As expressões mais simples são apenas valores literais, como "hello" ou 5, mas a linguagem Terraform também permite expressões mais complexas, como referências a dados exportados por recursos, aritmética, avaliação condicional e várias funções internas.

## Notas

* Leitura extra:
   * https://www.terraform.io/docs/configuration/expressions.html


536 / 5000
Resultados de tradução
## Comandos

* console terraform
   * Este comando fornece um console de linha de comando interativo para avaliar e experimentar expressões. Isso é útil para testar interpolações antes de usá-las nas configurações e para interagir com quaisquer valores atualmente salvos no estado. Se o estado atual estiver vazio ou ainda não tiver sido criado, o console pode ser usado para experimentar a sintaxe da expressão e funções integradas.
   * https://www.terraform.io/docs/commands/console.html
   * console terraform [opções] [dir]


--- 

# Dados

As fontes de dados permitem que os dados sejam buscados ou calculados para uso em outro lugar na configuração do Terraform. O uso de fontes de dados permite que uma configuração do Terraform use informações definidas fora do Terraform ou definidas por outra configuração separada do Terraform.

Cada provedor pode oferecer fontes de dados junto com seu conjunto de tipos de recursos.

## Notas

* Leitura extra:
   * https://www.terraform.io/docs/configuration/data-sources.html

---

# Funções

A linguagem Terraform inclui várias funções integradas que você pode chamar de dentro de expressões para transformar e combinar valores. A sintaxe geral para chamadas de função é um nome de função seguido por argumentos separados por vírgula entre parênteses

A linguagem do Terraform não oferece suporte a funções definidas pelo usuário e, portanto, apenas as funções integradas à linguagem estão disponíveis para uso. A navegação para esta seção inclui uma lista de todas as funções integradas disponíveis.

## Notas:

* Leitura Extra:
   * https://www.terraform.io/docs/configuration/expressions.html#function-calls
   * https://www.terraform.io/docs/configuration/functions.html

---

# Provedores

Terraform é usado para criar, gerenciar e atualizar recursos de infraestrutura, como máquinas físicas, VMs, switches de rede, contêineres e muito mais. Quase qualquer tipo de infraestrutura pode ser representado como um recurso no Terraform.

Um provedor é responsável por entender as interações da API e expor recursos. A maioria dos provedores configura uma plataforma de infraestrutura específica (nuvem ou auto-hospedada). Os provedores também podem oferecer utilitários locais para tarefas como gerar números aleatórios para nomes de recursos exclusivos.

Cada provedor Terraform tem sua própria documentação, descrevendo seus tipos de recursos e seus argumentos.

Terraform depende de plug-ins chamados "provedores" para interagir com sistemas remotos.

As configurações do Terraform devem declarar quais provedores são exigidos, para que o Terraform possa instalá-los e usá-los. Além disso, alguns provedores exigem configuração (como URLs de endpoint ou regiões de nuvem) antes de serem usados.

## Notas

* Leitura Extra:
  * https://www.terraform.io/docs/configuration/providers.html
  * https://www.terraform.io/docs/configuration/providers.html#alias-multiple-provider-configurations

---

# Variáveis

As variáveis ​​de entrada servem como parâmetros para um módulo Terraform, permitindo que aspectos do módulo sejam personalizados sem alterar o código-fonte do próprio módulo e permitindo que os módulos sejam compartilhados entre diferentes configurações.

Ao declarar variáveis ​​no módulo raiz de sua configuração, você pode definir seus valores usando opções CLI e variáveis ​​de ambiente. Quando você os declara em módulos filho, o módulo de chamada deve passar valores no bloco de módulo.

Se você estiver familiarizado com as linguagens de programação tradicionais, pode ser útil comparar os módulos do Terraform com as definições de função:

* Variáveis ​​de entrada são como argumentos de função.
* Os valores de saída são como os valores de retorno da função.
* Os valores locais são como as variáveis ​​locais temporárias de uma função.

## Notas

* Leitura Extra:
  * https://www.terraform.io/docs/configuration/variables.html

---

# Provisioners

Os provisionadores podem ser usados para modelar ações específicas na máquina local ou em uma máquina remota para preparar servidores ou outros objetos de infraestrutura para o serviço.

## Notas

* Leitura Extra:
   * https://www.terraform.io/docs/provisioners/index.html
   * https://www.terraform.io/docs/provisioners/remote-exec.html
   * https://www.terraform.io/docs/provisioners/local-exec.html
   * https://www.terraform.io/docs/provisioners/connection.html
* Atenção ao objeto "self"
* Deve ser usado como último recurso
* TO-DO
   * Revisores de fornecedores