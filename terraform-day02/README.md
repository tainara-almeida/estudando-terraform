# Módulos

Um módulo é um contêiner para vários recursos usados juntos. Os módulos podem ser usados para criar abstrações leves, para que você possa descrever sua infraestrutura em termos de arquitetura, em vez de diretamente em termos de objetos físicos.

## Notas

* Melhor deixar suas informações de provedor e terraform (backend) no arquivo main.tf na raiz do projeto
* Importante lembrar:
   * Se você precisar enviar os dados do módulo filho, eles precisam ser enviados ao módulo raiz e, em seguida, configurados novamente
* Leitura extra:
   * https://www.terraform.io/docs/configuration/modules.html

---

# Processo interno

Um "back-end" no Terraform determina como o estado é carregado e como uma operação como aplicar é executada. Essa abstração permite o armazenamento de estado de arquivo não local, execução remota, etc.

Por padrão, o Terraform usa o back-end "local", que é o comportamento normal do Terraform com o qual você está acostumado.

## Notas

* O Terraform detecta mudanças na configuração de estado e ajuda você a fazer a transição dessa mudança
* O Terraform deve inicializar qualquer back-end configurado antes de usar. Isso pode ser feito simplesmente executando o terraform init.
* Os back-ends são responsáveis ​​por armazenar o estado e fornecer uma API para bloqueio de estado. O bloqueio de estado é opcional. Apesar do estado ser armazenado remotamente, todos os comandos do Terraform, como o console do terraform, as operações do estado do terrenoform, contaminação do terreno e outros continuarão a funcionar como se o estado fosse local.
* State Locking é altamente recomendado durante o trabalho em equipe
* Leitura extra:
  * https://www.terraform.io/docs/backends/index.html
  * https://www.terraform.io/docs/configuration/backend.html
  * https://www.terraform.io/docs/backends/config.html
  * https://www.terraform.io/docs/backends/init.html
  * https://www.terraform.io/docs/backends/state.html

---

# Estado

O Terraform deve armazenar o estado sobre sua infraestrutura e configuração gerenciadas. Esse estado é usado pelo Terraform para mapear recursos do mundo real para sua configuração, controlar os metadados e melhorar o desempenho de grandes infraestruturas.

## Notas

* Análise:
  * tração do estado do terreno
  * empurrar o estado da terraform
* Ferramenta de verificação: jq
* Leitura Extra:
  * https://www.terraform.io/docs/state/index.html
  * https://www.terraform.io/docs/state/purpose.html
  * https://www.terraform.io/docs/commands/state/index.html

## Comando de Estado

O comando terraform state é usado para gerenciamento avançado de estado. Conforme o uso do Terraform se torna mais avançado, há alguns casos em que você pode precisar modificar o estado do Terraform. Em vez de modificar o estado diretamente, os comandos de estado do terreno podem ser usados ​​em muitos casos.

# Importar

O Terraform é capaz de importar a infraestrutura existente. Isso permite que você pegue recursos que você criou por algum outro meio e coloque-os sob o gerenciamento do Terraform.

Essa é uma ótima maneira de fazer a transição lenta da infraestrutura para o Terraform ou de ter certeza de que poderá usar o Terraform no futuro, caso ele potencialmente não seja compatível com todos os recursos de que você precisa hoje.

## Notas

* Verifique a documentação de cada recurso para saber a forma adequada de importá-los
* Leitura Extra:
  * https://www.terraform.io/docs/import/index.html

---

# Área de trabalho

Cada configuração do Terraform tem um back-end associado que define como as operações são executadas e onde os dados persistentes, como o estado do Terraform, são armazenados.

Os dados persistentes armazenados no back-end pertencem a um espaço de trabalho. Inicialmente, o back-end tem apenas um espaço de trabalho, denominado "padrão" e, portanto, há apenas um estado Terraform associado a essa configuração.

Certos back-ends suportam vários espaços de trabalho nomeados, permitindo que vários estados sejam associados a uma única configuração. A configuração ainda tem apenas um back-end, mas várias instâncias distintas dessa configuração devem ser implantadas sem configurar um novo back-end ou alterar as credenciais de autenticação.

O Terraform começa com um único espaço de trabalho denominado "default". Este espaço de trabalho é especial porque é o padrão e também porque nunca pode ser excluído. Se você nunca usou áreas de trabalho explicitamente, então você só trabalhou na área de trabalho "padrão".

Os espaços de trabalho são gerenciados com o conjunto de comandos do espaço de trabalho do terraform. Para criar um novo espaço de trabalho e alternar para ele, você pode usar o novo espaço de trabalho do terraform; para alternar entre os espaços de trabalho, você pode usar a seleção de espaço de trabalho do terraform; etc.

## Notas

* Usando condicionais, você pode simplesmente alternar os espaços de trabalho e implantar sua infraestrutura com diferentes perfis / contas / regiões
* Leitura Extra:
  * https://www.terraform.io/docs/state/workspaces.html

---

# Dados sensíveis no estado

O estado do Terraform pode conter dados confidenciais, dependendo dos recursos em uso e de sua definição de "confidencial". O estado contém IDs de recursos e todos os atributos de recursos. Para recursos como bancos de dados, pode conter senhas iniciais.

Ao usar o estado local, o estado é armazenado em arquivos JSON de texto simples.

Ao usar o estado remoto, o estado só é mantido na memória quando usado pelo Terraform. Ele pode ser criptografado em repouso, mas isso depende do back-end de estado remoto específico.

## Notas

* Mesmo que o back-end seja configurado remotamente, sempre criptografe os dados, se possível
* Leitura extra:
  * https://www.terraform.io/docs/state/sensitive-data.html
  * https://www.terraform.io/docs/backends/types/s3.html