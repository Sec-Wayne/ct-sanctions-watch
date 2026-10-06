# Unrevoked Sanctioned Domains

Detected sanctioned domains off of CT logs.<br>
Only shows certificates where the CA's legal jurisdiction is within a sanctions list.<br>
Revocation checks performed regularly.<br>
Any queries see Wayne.

A listing is not a finding that anyone broke the law.<br>
Licenses and exemptions may apply. They are not checked here.<br>
Each row shows what the certificate and the cited list entries say.

## How a certificate is listed

1. The domain belongs to a website that an official sanctions list, or an
   official page, ties to a sanctioned entity.
2. The certificate was issued by a certificate authority (CA) whose country,
   as recorded in [CCADB](https://www.ccadb.org/), is covered by that list:
   an EU member state for `EU`, the United States for `US`, the United
   Kingdom for `UK`, Switzerland for `CH`, Canada for `CAN`.
3. The certificate is unexpired, and neither the CA's CRL nor its OCSP
   responder reports it revoked. It leaves the list once it is revoked or
   expires.

## Last updated

All times are UTC.

<!--STATUS-->

- List refreshed: 2026-10-06T18:50:32Z
- Sanctions lists read: 2026-10-06T15:44:19Z
- Revocation last checked: 2026-10-06T16:22:07Z
- CRLs read were issued between 2026-10-05T18:10:38Z and 2026-10-06T16:08:44Z

<!--/STATUS-->

## Files

| File | What it holds |
|---|---|
| `index.html` | The list as a web page, grouped by CA and then by entity. |
| `sanctions.csv` | One row per certificate, domain and entity. |
| `sanctions.json` | The same rows, with the update times and sources. |

A certificate may be logged as a precertificate, as the final certificate,
or both. Where both are logged they share a serial number and appear as
separate rows; counts on the page count them once. One certificate can
appear under more than one entity when the entities share a website.

The key of a row is `sha256`, `domain` and `entity_list_id`.

## Columns

| Column | Meaning |
|---|---|
| `ca` | The CA that issued the certificate. |
| `ca_country` | The CA's country, as recorded in CCADB. |
| `sanctions_list` | The list covering the CA's country: `EU`, `US`, `UK`, `CH` or `CAN`. |
| `entity` | The sanctioned person or organization. |
| `entity_list`, `entity_list_id` | The list entry that designates the entity, for example `ofac` and `35137`. |
| `listed_on` | When the list entry was made, where the list gives it. |
| `programs` | The list's sanctions programs for the entry, separated by `; `. |
| `domain` | The name in the certificate. |
| `listed_domain` | The listed website that name belongs to. |
| `domain_list`, `domain_list_id` | Where the website comes from. Often another list's entry for the same entity, since lists differ in which websites they record. `official-page` means a government page, given in `domain_source_url`. |
| `domain_source_url` | The page that names the website: the list entry's page, or the official page for `official-page`. Empty where the list has no page per entry. |
| `entry_type` | `precertificate` or `certificate`. |
| `not_before`, `not_after` | When the certificate is valid. |
| `serial`, `sha256` | The certificate's serial number and SHA-256 fingerprint. |
| `crt_sh`, `censys` | The certificate on crt.sh and Censys. |
| `validation` | `DV`, `OV`, `IV` or `EV`. DV means the CA checked only control of the domain. OV, IV and EV mean it also checked the organization or individual. |
| `crl_this_update` | The issue date of the CRL the certificate was checked against. |
| `revocation_checked_at` | When that CRL was read. |
| `ocsp_status` | `good`, or `no_ocsp` where the certificate names no OCSP responder. |
| `ocsp_checked_at` | When OCSP was asked. OCSP is asked less often than CRLs are read, so this can be older than `revocation_checked_at`. |

Dates are ISO 8601 in UTC. An empty CSV cell is `null` in the JSON.

## Sources

Each `entity_list` and `domain_list` is one of these IDs. Published is the
publisher's date. Fetched is when the file was read.

<!--SOURCES-->

| ID | Source | Use | Published | Fetched |
|---|---|---|---|---|
| `fr-gels` | [EU and French national asset freezes (French Treasury register)](https://gels-avoirs.dgtresor.gouv.fr/ApiPublic/api/v1/publication/derniere-publication-fichier-json) | Sanctions list | 2026-10-05 | 2026-10-06 |
| `ofac` | [US OFAC Specially Designated Nationals](https://www.treasury.gov/ofac/downloads/sanctions/1.0/sdn_advanced.xml) | Sanctions list | none | 2026-10-06 |
| `uk` | [UK Sanctions List (FCDO)](https://sanctionslist.fcdo.gov.uk/docs/UK-Sanctions-List.xml) | Sanctions list | 2026-10-06 | 2026-10-06 |
| `seco` | [Switzerland SECO sanctions](https://www.sesam.search.admin.ch/sesam-search-web/pages/downloadXmlGesamtliste.xhtml?lang=de&action=downloadXmlGesamtlisteAction) | Sanctions list | 2026-09-28 | 2026-10-06 |
| `un` | [UN Security Council Consolidated List](https://scsanctions.un.org/resources/xml/en/consolidated.xml) | Sanctions list | 2026-10-06 | 2026-10-06 |
| `canada` | [Canada Consolidated Autonomous Sanctions List](https://www.international.gc.ca/world-monde/assets/office_docs/international_relations-relations_internationales/sanctions/sema-lmes.xml) | Sanctions list | none | 2026-10-06 |
|  | [CCADB](https://www.ccadb.org/resources) | CA operator and country | none | 2026-10-05 |
|  | Certificate Transparency logs | Certificates and their DNS names, read continuously | none | 2026-10-06 |
|  | Issuer CRLs | Revocation | none | 2026-10-06 |
|  | OCSP | Revocation, where the certificate names a responder | none | 2026-10-06 |

<!--/SOURCES-->
