# tools

Magicorn DevOps araç seti — Docker imajları ve Azure Pipelines agent.

## Imajlar

| Imaj | Açıklama |
|------|----------|
| **tools-deploy** | Ubuntu (glibc) tabanlı: awscli, kubectl, helm, jq, git, ssh. Hem genel deploy hem azp-agent base. |
| **tools-debug** | Alpine tabanlı debug araçları. |
| **tools-maven** | Maven + Eclipse Temurin (Java build). |
| **tools-azp-agent** | `tools-deploy` üzerine agent katmanı; Node (externals/node24) çalışır. |

## Build

- **buildspec.yml** — amd64 imajları build/push, multi-arch manifest oluşturur.
- **buildspec-arm64.yml** — arm64 imajları build/push (manifest amd64 pipeline’da oluşturulur).

Tag: `git describe --tags --abbrev=0` (örn. `0.1.4`); imaj tag’leri `0.1.4-amd64` / `0.1.4-arm64`.

## ECR Public repoları

Build/push öncesi **public.ecr.aws/magicorn** altında şu repolar tanımlı olmalı:

- `tools-deploy`
- `tools-debug`
- `tools-maven`
- `tools-azp-agent`

Yeni repo: `aws ecr-public create-repository --repository-name <ad>`
