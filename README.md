# sbom-data

Programvaruförteckningar (SBOM) i SPDX-format för Sundsvalls kommuns
webbkatalog och API-katalog på
[ekosystemet.sundsvall.dev](https://ekosystemet.sundsvall.dev/).

```
api/<slug>.spdx.json        API-katalogen  →  /api/<slug>-sbom.html
tjanster/<slug>.spdx.json   Webbkatalogen  →  /tjanster/<slug>-sbom.html
```

## Varför ett eget repo

Förteckningarna är tillsammans drygt 90 MB och skrivs om varje vecka. Låg de
kvar i webbplatsens repo
([dev-web](https://github.com/Public-Service-as-a-Service/dev-web)) fick varje
utcheckning, byggkontext och deploy bära dem. Webbplatsens bygge hämtar dem
härifrån med `git clone --depth 1`, så bara den senaste versionen laddas ned.

## Genererad data – redigera inte för hand

Filerna skrivs av `.github/workflows/refresh-sbom.yml` i `dev-web`, som varje
måndag 05:00 UTC checkar ut varje tjänsts källkodsrepo, kör Trivy och
normaliserar resultatet. En handskriven ändring skrivs över vid nästa körning.

Fältet `documentNamespace` i en del filer namnger katalogernas gamla domäner.
Det är en SPDX-identifierare, inte en länk, och lämnas orörd för att bevara
kontinuiteten mot tidigare förteckningar.
