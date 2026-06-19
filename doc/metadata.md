# Metadados essenciais do superbadge

Este pacote SFDX contem apenas os metadados relevantes para evidenciar as configuracoes do superbadge **User Authentication Settings**.

## Arquivos principais

| Requisito | Arquivo |
| --- | --- |
| Politicas globais de senha e trusted IP | `force-app/main/default/settings/Security.settings-meta.xml` |
| Restricao de apps conectados aprovados por admin | `force-app/main/default/settings/ConnectedApp.settings-meta.xml` |
| IPs e horarios do Call Center | `force-app/main/default/profiles/Call Center Profile.profile-meta.xml` |
| IPs do Inside Sales | `force-app/main/default/profiles/Inside Sales Profile.profile-meta.xml` |
| Politica de senha para administrador | `force-app/main/default/profilePasswordPolicies/PT1_profilePasswordPolicy1652814767705.profilePasswordPolicy-meta.xml` |
| Politica de senha adicional de administrador | `force-app/main/default/profilePasswordPolicies/Break_Glass_Administrator_profilePasswordPolicy1654105698038.profilePasswordPolicy-meta.xml` |

## Evidencias recuperadas

### Politicas globais de senha

Arquivo: `Security.settings-meta.xml`

- Complexidade: `UpperLowerCaseNumericSpecialCharacters`
- Minimo: `12`
- Tentativas invalidas: `ThreeAttempts`
- Bloqueio: `ThirtyMinutes`
- Resposta secreta ocultada: `true`
- Rede confiavel: `13.108.0.0`

### Perfil Inside Sales

Arquivo: `Inside Sales Profile.profile-meta.xml`

- Corporate Office: `13.108.0.0`
- VPN: `22.0.0.1 - 22.0.255.0`
- Sem restricao de horario recuperada no perfil.

### Perfil Call Center

Arquivo: `Call Center Profile.profile-meta.xml`

- Corporate Office: `13.108.0.0`
- Horario permitido: segunda a sexta, `480` a `1020` minutos.
- Equivalencia: `08:00` a `17:00`.
- Sabado e domingo bloqueados: `0` a `0`.

### Apps conectados

Arquivo: `ConnectedApp.settings-meta.xml`

- `enableAdminApprovedAppsOnly`: `true`
- `enableAdminApprovedAppsOnlyForExternalUser`: `true`

### Politica de senha de administrador

Arquivo: `PT1_profilePasswordPolicy1652814767705.profilePasswordPolicy-meta.xml`

- Perfil: `admin`
- Minimo: `15`
- Complexidade: `4`
- Tentativas invalidas: `3`
- Bloqueio: `30`
- Resposta secreta ocultada: `true`

## Comandos usados

```powershell
sf org login web --alias user-auth-settings --instance-url https://login.salesforce.com --set-default --browser chrome
sf project retrieve start --target-org user-auth-settings --manifest manifest/package.xml --ignore-conflicts --wait 10
sf project retrieve start --target-org user-auth-settings --metadata ProfilePasswordPolicy --ignore-conflicts --wait 10
```
