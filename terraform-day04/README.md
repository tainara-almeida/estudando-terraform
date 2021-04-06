# Condições

Um operador é um tipo de expressão que transforma ou combina uma ou mais outras expressões. Os operadores combinam dois valores de alguma forma para produzir um terceiro valor de resultado ou transformam um único valor fornecido para produzir um único resultado.

Os operadores que trabalham com dois valores colocam um símbolo de operador entre os dois valores, semelhante à notação matemática: 1 + 2. Os operadores que trabalham com apenas um valor colocam um símbolo de operador antes desse valor, como! True.

A linguagem Terraform possui um conjunto de operadores para aritmética e lógica, que são semelhantes aos operadores em linguagens de programação como JavaScript ou Ruby.

## Notas

* Leitura Extra:
  * https://www.terraform.io/docs/configuration/expressions.html#arithmetic-and-logical-operators
* Exemplo de uso:
  * count = var.environment == "production"? 2 + var.extra: 1
* count.index pode ajudar você a fornecer diferentes recursos com base no parâmetro "count"

---

# Tipo de restrições

Os autores do módulo Terraform e os desenvolvedores do provedor podem usar restrições de tipo detalhadas para validar os valores fornecidos pelo usuário para suas variáveis ​​de entrada e argumentos de recursos. Isso requer algum conhecimento adicional sobre o sistema de tipos do Terraform, mas permite que você crie uma interface de usuário mais resiliente para seus módulos e recursos.

## Notas

* Leitura extra:
  * https://www.terraform.io/docs/configuration/types.html

---

# Loop for_each

Por padrão, um bloco de recursos configura um objeto de infraestrutura real. (Da mesma forma, um bloco de módulo inclui o conteúdo de um módulo filho na configuração uma vez.) No entanto, às vezes você deseja gerenciar vários objetos semelhantes (como um conjunto fixo de instâncias de computação) sem escrever um bloco separado para cada um. O Terraform tem duas maneiras de fazer isso: count e for_each.

Se um recurso ou bloco de módulo inclui um argumento for_each cujo valor é um mapa ou um conjunto de strings, o Terraform criará uma instância para cada membro desse mapa ou conjunto.

## Notas

* Leitura extra:
  * https://www.terraform.io/docs/configuration/meta-arguments/for_each.html