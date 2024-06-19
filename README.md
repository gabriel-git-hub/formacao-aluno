# Como utilizar

No diretório imediatamente acima do seu módulo, execute:

`git clone https://github.com/Danielbano1/formacao-aluno`

Depois você pode utilizar as funções de formacao-aluno com o import:

```Python
from .. import formacao-aluno

formacao-aluno.get_formatura(25)
```

**OBS:** Para utilizar imports relativos, seu módulo também precisa fazer parte de um package, ou seja, o diretório do módulo deve possuir um arquivo `__init__.py` assim como o nosso.

Alternativamente, se o diretório acima do seu módulo também for um repositório, como o principal, você pode adicionar formacao-aluno como submódulo:

`git submodule add https://github.com/Danielbano1/formacao-aluno`

## Dependências

Python 3.9+

# Documentação adicional

O módulo possui um endereço de um arquivo fixo para registro da base de dados em memória persistente, inacessivel ao cliente.
O módulo usa um espaço em memória de acesso rápido para guardar o banco de dados para o uso das funcionalidades do módulo. Esta posição de memória também é inacessível ao cliente.

## inicializar

Esta função realiza a leitura da base de dados na memória persistente para um espaço de acesso rápido a ser usado pelas outras funções. A memória de acesso rápido acessada é fixa e qualquer informação previamente armazenada será perdida.

### Requisitos

- Retorna ARQUIVO_NAO_ENCONTRADO caso não encontre o arquivo de leitura
- Retorna ARQUIVO_EM_FORMATO_INVALIDO caso encontre o arquivo de leitura, mas não seja capaz de fazer a leitura
- Retorna OPERACAO_REALIZADA_COM_SUCESSO caso faça a leitura com sucesso
- Não avalia a integridade do conteudo lido e sua compatibilidade com as aplicações que o usarão

## finalizar

Esta função realiza o registro da base de dados em memória de acesso rápido sendo usada pelo módulo no arquivo resignado pelo módulo. Qualquer conteudo prévio no arquivo será sobrescrito.

### Requisitos

- Retorna ERRO_NA_ESCRITA_DO_ARQUIVO caso não seja capaz de fazer a escrita
- Retorna OPERACAO_REALIZADA_COM_SUCESSO caso faça a escrita com sucesso

## add_formatura

Esta função recebe em seus parâmetros um inteiro representantdo o id do aluno e um inteiro representando o id de formacao, em sequência. Esta função cria um novo registro de formatura de tal aluno, tal formacao, zero cursos concluidos. Retorna uma tupla com uma mensagem de erro e um dicionario com tais informaçoes da nova formatura, em sequência.

### Requisitos

- Retorna uma tupla com a mensagem OPERACAO_REALIZADA_COM_SUCESSO e um dicionario com as informações da nova formatura

### Acoplamento

- id_aluno: int
  inteiro identificador do aluno a ser matriculado na formatura
- id_formacao: int
  inteiro identificador da formacao a ser matriculada na formatura

## notify_curso_concluido

Esta função recebe nos parâmetros um inteiro repersentando o id do aluno e um inteiro representando o id do curso, em sequência. Ela busca no banco de dados por uma formatura cuja id de aluno seja a informada e adiciona o novo curso aos cursos concluidos por esse aluno nessa formatura. A função retorna uma mensagem de erro

### Requisitos

- Retorna FORMATURA_NAO_ENCONTRADA caso não encontre uma formatura com o id de aluno fornecido
- Retorna OPERACAO_REALIZADA_COM_SUCESSO caso encontre uma formatura com o id de aluno, adicionando o curso aos cursos concluidos pelo aluno nesta formatura


### Acoplamento

- id_aluno: int
  inteiro identificador do aluno que concluiu um curso
- id_curso: int
  inteiro identificador do curso concluido pelo aluno

## get_formaturas_by_aluno

Esta função recebe em seus parâmetros um inteiro representando o id de um aluno. Ela retorna uma tupla com uma mensagem de erro seguida por uma lista todas as ids formacoes desse aluno.

### Requisitos

- Retorna uma tupla com a mensagem OPERACAO_REALIZADA_COM_SUCESSO e uma lista com todas as ids de formacoes registradas em formaturas com o id do aluno informada, em sequência

### Acoplamento

- id_aluno: int
  inteiro identificador do aluno a ser consultado

## get_formaturas

Retorna uma tupla com uma mensagem de erro e uma lista com todas as formaturas registradas, em sequência.

### Requisitos

- Retorna uma tupla com a mensagem OPERACAO_REALIZADA_COM_SUCESSO e uma lista com todas as formatursas registradas, em sequência

## get_alunos_by_formatura

Esta função recebe em seus parâmetros um inteiro identificador de uma formacao. Esta função retorna uma tupla com uma mensagem de erro e uma lista com todas os ids dos alunos registrados em formaturas com a formacao informada, em sequência.

### Requisitos

- Retorna uma tupla com a mensagem OPERACAO_REALIZADA_COM_SUCESSO e uma lista com todas os ids dos alunos registrados em formaturas com a formacao informada, em sequência

### Acoplamento

- id_formacao: int
  inteiro identificador da formacao a ser pesquisada

## is_concluida

Esta função recebe em seus parâmetros um inteiro que representa um id de aluno e im inteiro que representa um id de formacao, em sequencia. A função busca na base de dados e retorna uma tupla com uma mensagem de erro seguida por um valor booleano indicando se o aluno informado concluiu a formacao informada.

### Requisitos

- Retorna uma tupla com a mensagem FORMATURA_NAO_ENCONTRADA e o valor booleano False, em sequência, caso não seja encontrada uma formatura com o id do aluno e o id da formacao informados no banco de dados
- Retorna uma tupla com a mensagem OPERACAO_REALIZADA_COM_SUCESSO e o valor booleano False, em sequência, caso seja encontrada uma formatura com o id do aluno e o id da formacao informados no banco de dados e seus cursos concluidos não abranjam todos os cursos da formacao
- Retorna uma tupla com a mensagem OPERACAO_REALIZADA_COM_SUCESSO e o valor booleano True, em sequência, caso seja encontrada uma formatura com o id do aluno e o id da formacao informados no banco de dados e seus cursos concluidos abranjam todos os cursos da formacao

### Acoplamento

- id_aluno: int
  inteiro identificador do aluno consultado
- id_formacao: int
  inteiro identificador da formacao consultada







