# ci-templates-homelab

Reusable workflows do GitHub Actions reutilizáveis por qualquer aplicação do ambiente de laboratório.

## Templates disponíveis

| Arquivo | O que faz |
|---|---|
| `java-gradle-build.yml` | Build e testes com Gradle, upload do JAR como artefato |
| `docker-build-push.yml` | Build e push de imagem Docker no ghcr.io, expõe SHA curto como output |
| `gitops-update.yml` | Atualiza campo em manifest YAML via yq e commita no k8s-gitops |

## Como usar

Os templates são chamados via `workflow_call` a partir do repositório `ci-homelab`:

```yaml
jobs:
  build:
    uses: rodrigomsr2/ci-templates-homelab/.github/workflows/java-gradle-build.yml@main
    with:
      working-directory: '.'
      artifact-name: minha-app-jar
      artifact-path: build/libs/minha-app-*.jar
```

## Convenções

- Todos os inputs obrigatórios declarados com `required: true` — sem defaults implícitos
- Templates agnósticos — nenhum valor de aplicação hardcoded
- `yq` para atualização de manifests YAML — nunca `sed`
- Imagens tagueadas com SHA curto (`sha-xxxxxxx`) — imutável e rastreável
