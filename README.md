# Hello World Caixa — Backstage + Ansible Automation Platform

Template do Backstage para disparar o Job Template **Hello World Caixa** no Ansible Automation Platform (AAP).

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

## Pré-requisitos

1. **Backstage** com o plugin [`@janus-idp/backstage-scaffolder-backend-module-aap`](https://github.com/janus-idp/backstage-plugins/tree/main/plugins/aap-backend) instalado e configurado.

2. **Ansible Automation Platform** acessível pelo Backstage com credenciais configuradas no `app-config.yaml`:

   ```yaml
   aap:
     baseUrl: https://aap.example.com
     authorization: "Bearer <token>"
   ```

3. O Job Template **Hello World Caixa** deve existir no AAP.

## Como registrar no Backstage

Adicione a referência ao `catalog-info.yaml` no seu `app-config.yaml`:

```yaml
catalog:
  locations:
    - type: url
      target: https://github.com/<org>/<repo>/blob/main/catalog-info.yaml
```

Ou importe manualmente via **Backstage UI → Register Existing Component**.

## Parâmetros disponíveis

| Parâmetro         | Tipo    | Padrão          | Descrição                                    |
|-------------------|---------|-----------------|----------------------------------------------|
| `inventory`       | string  | Demo Inventory  | Inventário a ser utilizado                   |
| `verbosity`       | number  | 0               | Nível de verbosidade (0-4)                   |
| `extraVariables`  | string  | —               | Variáveis extras em YAML para o playbook     |

## Estrutura do repositório

```
.
├── catalog-info.yaml   # Registro do template no catálogo Backstage
├── template.yaml       # Definição do template Scaffolder
└── README.md           # Este arquivo
```
