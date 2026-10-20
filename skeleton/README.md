# ${{ values.projectName }}

${{ values.projectDescription }}

Projeto OpenShift criado automaticamente via Backstage Software Template.

- **Namespace:** criado pelo Job Template **CreateProject** no Ansible
  Automation Platform (AAP).
- **Deploy de aplicações:** template **DeployHttpd** (pode ser disparado
  junto com a criação do projeto) publica manifests em `manifests/httpd/`;
  o Argo CD sincroniza sozinho.

## Projeto no OpenShift

- **Nome:** `${{ values.projectName }}`
