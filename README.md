# Hello World Caixa — Backstage + Ansible Automation Platform

Template do Backstage (RHDH) para disparar o Job Template **Hello World Caixa** no Ansible Automation Platform (AAP), utilizando os plugins oficiais da Red Hat.

## Dados do Job Template no AAP

| Campo                   | Valor                          |
|-------------------------|--------------------------------|
| **Nome**                | Hello World Caixa              |
| **Descrição**           | Hello World Caixa              |
| **Tipo de Job**         | run                            |
| **Organização**         | CAIXA                          |
| **Inventário**          | Demo Inventory                 |
| **Projeto**             | CAIXA Project                  |
| **Playbook**            | linux_playbook.yml             |
| **Ambiente de Execução**| Default execution environment  |
| **Forks**               | 0                              |
| **Verbosidade**         | 0 (Normal)                     |
| **Timeout**             | 0                              |
| **Show changes**        | Off                            |
| **Job slicing**         | 1                              |

## Plugins utilizados

Este template utiliza os plugins oficiais do **Red Hat Ansible Automation Platform** para o RHDH:

| Plugin | Tipo | Função |
|--------|------|--------|
| `ansible-plugin-backstage-rhaap` | Frontend | Página "Ansible" no menu do Backstage |
| `ansible-plugin-backstage-self-service` | Frontend | Campos `AAPTokenField` e `AAPResourcePicker` no scaffolder |
| `ansible-backstage-plugin-catalog-backend-module-rhaap` | Backend | Sincroniza orgs, usuários, teams e job templates do AAP |
| `ansible-plugin-scaffolder-backend-module-backstage-rhaap` | Backend | Ação `ansible:jobTemplate:launch` no scaffolder |

### Configuração dos plugins (dynamic plugins)

```yaml
dynamicPlugins:
  - disabled: false
    package: >-
      oci://registry.redhat.io/ansible-automation-platform/automation-portal:2.2!ansible-plugin-backstage-rhaap
    pluginConfig:
      dynamicPlugins:
        frontend:
          ansible.plugin-backstage-rhaap:
            appIcons:
              - importName: AnsibleLogo
                name: AnsibleLogo
            dynamicRoutes:
              - importName: AnsiblePage
                menuItem:
                  icon: AnsibleLogo
                  text: Ansible
                path: /ansible

  - disabled: false
    package: >-
      oci://registry.redhat.io/ansible-automation-platform/automation-portal:2.2!ansible-plugin-backstage-self-service
    pluginConfig:
      dynamicPlugins:
        frontend:
          ansible.plugin-backstage-self-service:
            scaffolderFieldExtensions:
              - importName: AAPTokenFieldExtension
              - importName: AAPResourcePickerExtension

  - disabled: false
    package: >-
      oci://registry.redhat.io/ansible-automation-platform/automation-portal:2.2!ansible-backstage-plugin-catalog-backend-module-rhaap
    pluginConfig:
      catalog:
        providers:
          rhaap:
            development:
              orgs: "Default,CAIXA"
              sync:
                orgsUsersTeams:
                  schedule:
                    frequency: { minutes: 5 }
                    timeout: { minutes: 1 }
                jobTemplates:
                  enabled: true
                  schedule:
                    frequency: { minutes: 5 }
                    timeout: { minutes: 1 }

  - disabled: false
    package: >-
      oci://registry.redhat.io/ansible-automation-platform/automation-portal:2.2!ansible-plugin-scaffolder-backend-module-backstage-rhaap
    pluginConfig:
      dynamicPlugins:
        backend:
          ansible.plugin-scaffolder-backend-module-backstage-rhaap:
```

## Fluxo do template

```
┌─────────────────────┐     ┌──────────────────────┐     ┌─────────────────────┐
│  1. Token do AAP    │────▶│  2. Seleção de Job   │────▶│  3. Confirmação     │
│  (AAPTokenField)    │     │  Template, Inventário │     │                     │
│                     │     │  (AAPResourcePicker)  │     │                     │
└─────────────────────┘     └──────────────────────┘     └────────┬────────────┘
                                                                   │
                                                                   ▼
                                                         ┌─────────────────────┐
                                                         │  ansible:jobTemplate │
                                                         │  :launch            │
                                                         │  (Executa no AAP)   │
                                                         └─────────────────────┘
```

## Parâmetros disponíveis

| Parâmetro         | Tipo    | Campo UI           | Padrão          | Descrição                                    |
|-------------------|---------|--------------------|-----------------|----------------------------------------------|
| `aapToken`        | string  | AAPTokenField      | —               | Token de autenticação do AAP                 |
| `jobTemplate`     | string  | AAPResourcePicker  | Hello World Caixa | Job Template a executar                    |
| `inventory`       | string  | AAPResourcePicker  | Demo Inventory  | Inventário a ser utilizado                   |
| `verbosity`       | number  | select             | 0               | Nível de verbosidade (0-4)                   |
| `extraVariables`  | string  | textarea           | —               | Variáveis extras em YAML para o playbook     |

## Como registrar no Backstage / RHDH

Adicione a referência ao `catalog-info.yaml` no seu `app-config.yaml`:

```yaml
catalog:
  locations:
    - type: url
      target: https://github.com/<org>/<repo>/blob/main/catalog-info.yaml
```

Ou importe manualmente via **Backstage UI → Register Existing Component**.

## Estrutura do repositório

```
.
├── catalog-info.yaml   # Registro do template no catálogo Backstage
├── template.yaml       # Definição do template Scaffolder
└── README.md           # Este arquivo
```
