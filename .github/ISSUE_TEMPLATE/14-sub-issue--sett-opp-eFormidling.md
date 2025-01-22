---
name: 'Sub-issue: Sett opp eFormidling'
about: Sub-issue mal for oppsett av eFormidling.
title: Sett opp eFormidling
labels: ''
assignees: ''

---

## Oppgaver

<!-- [eFormidling dokumentasjon](https://docs.altinn.studio/altinn-studio/guides/development/eformidling/). -->

- [ ] Legg til en ny Maskinportenklient i samarbeidsportalen.
  - [ ] [Opprett nøklene](https://docs.altinn.studio/nb/authentication/getting-started/maskinportenclient/#opprette-jwk).
  - [ ] Legg til riktig scopes for eFormidling.
  - [ ] Legg til secrets i Azure Key Vault.
- [ ] Sett opp eFormidling i applicationmetadata.json.
- [ ] Sett opp eFormidling i appsettings.json.
- [ ] Legg til `IEventSecretCodeProvider`.
- [ ] Legg til `IEFormidlingMetadata`.
- [ ] Legg til `IEFormidlingReceivers`.
- [ ] Legg til et feedback steg.
- [ ] Legg til validering på filnavn.

### Huskeliste

- Navnene på secrets burde følge denne syntaksen: `navn-på-apprepoet-NavnPåSettings`.
- Organisasjonsnummeret i maskinporten klienten må være [TE sitt organisasjonsnummer](https://github.com/Altinn/altinn-cdn/blob/master/orgs/altinn-orgs.json).
