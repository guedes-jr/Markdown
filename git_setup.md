# Git Hooks – Validação de Mensagens de Commit (Conventional Commits)

Esse hook força que todas as mensagens de commit sigam o padrão.

## Configuração

1. Crie na raiz do projeto o diretório `.githooks` e adicione o arquivo `commit-msg`.
2. Configure o Git para usar o diretório de hooks: `git config core.hooksPath .githooks`
3. Coloque o código abaixo no arquivo `commit-msg`.

```bash
#!/bin/sh

MSG_FILE="$1"

pattern='^(init|feat|docs|style|refact|perf|test|chore|build|ci)(\([a-z0-9_-]+\))?: [A-Z].+'

if ! grep -Eq "$pattern" "$MSG_FILE"; then
  echo
  echo "Commit inválido!"
  echo
  echo "Formato esperado: type(scope?): Descrição"
  echo
  echo "  type       : init, feat, docs, style, refactor,"
  echo "               perf, test, chore, build, ci"
  echo "  scope?     : opcional, ex.: (api), (ui-component)"
  echo "  Descrição  : deve iniciar com letra maiúscula"
  echo
  echo "Exemplo válido:"
  echo "  feat(auth): Adiciona endpoint de login com JWT"
  echo
  exit 1
fi

exit 0
```
