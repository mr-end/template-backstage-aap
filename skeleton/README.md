# ${{ values.projectName }}

${{ values.projectDescription }}

Projeto OpenShift criado automaticamente via Backstage Software Template.

- **Namespace:** criado pelo Job Template **CreateProject** no Ansible
  Automation Platform (AAP).
- **Deploy de aplicações:** use o template **DeployHttpd**, que publica
  manifests e registra a Application no Argo CD.

## Projeto no OpenShift

- **Nome:** `${{ values.projectName }}`
