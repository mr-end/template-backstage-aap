# ${{ values.projectName }}

${{ values.projectDescription }}

Projeto OpenShift criado automaticamente via Backstage Software Template.

- **Namespace:** criado pelo Job Template **CreateProject** no Ansible
  Automation Platform (AAP).
- **Httpd (opcional):** manifests em `manifests/httpd/`. O Argo CD já
  observa os repositórios e sincroniza o deploy (GitOps) — não pelo AAP.

## Projeto no OpenShift

- **Nome:** `${{ values.projectName }}`
