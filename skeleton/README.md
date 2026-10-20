# ${{ values.projectName }}

${{ values.projectDescription }}

Projeto OpenShift criado automaticamente via Backstage Software Template.

- **Namespace:** criado pelo Job Template **CreateProject** no Ansible
  Automation Platform (AAP).
- **Httpd (opcional):** manifests em `manifests/httpd/`; a Application
  no Argo CD é registrada pelo template (GitOps) — não pelo AAP.

## Projeto no OpenShift

- **Nome:** `${{ values.projectName }}`
