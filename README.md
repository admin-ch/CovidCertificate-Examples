# Swiss Covid Certificate - Examples

Examples for the swiss covid certificate

*Please note that the schema files can be invalid or outdated due to the work in progress of the project.*

*Look up the newest Schema Version online, published by the EU ([GitHub Repo](https://github.com/eu-digital-green-certificates/ehn-dgc-schema)). The example .json files are based on the Document `Guidelines on Value Sets for Digital Green Certificates Version 1.0 2021-04-21` [Link](https://ec.europa.eu/health/sites/health/files/ehealth/docs/digital-green-certificates_dt-specifications_en.pdf)*

## Cetificate Content

The chapter [generic](#generic) describes the generic vaccination certificate part using the examlpe.
The chapters [vaccination](#vaccination), [tested](#tested) and [recovery](#recovery) describe the specific entries for the different kinds of the certificate.

### Generic

There is a general part, all covid certificate types must include.

```javascript
{
    // Version of the schema, according to Semantic versioning (ISO, https://semver.org/ version 2.0.0 or newer)
    // Type string with pattern "^\\d+.\\d+.\\d+$", defined in "DGC.schema.json"
    "ver": "1.0.0",
    // Surname(s), forename(s) - in that order 
    // Objects, defined in "DGC.schema.json"
    "nam": 
        // Object person_name as defined in "DGC.Core.Types.schema.json"
        // Only required "fnt" other values are optional
        {
            // Family name
            // String max length 50 chars
            "fn": "d'Arsøns - van Halen",
            // Given name
            // String max length 50 chars
            "gn": "François-Joan",
            // Standardised family name
            // String max length 50 chars with pattern "^[A-Z<]*$"
            "fnt": "DARSONS<VAN<HALEN",
            // Standardised given name
            // String max length 50 chars with pattern "^[A-Z<]*$"
            "gnt": "FRANCOIS<JOAN"
        },
    // Date of Birth, ISO 8601
    // String format date with pattern "(19|20)\\d{2}-\\d{2}-\\d{2}", defined dob in "DGC.schema.json"
    "dob": "1987-03-22",
    // Next elements would be the type spesific. Definition in separat chapters.
    ...
}

```

Followed by one of the elements `v`, `t` or `r`.

### Vaccination

The vaccination part is defined as followed:

```javascript
{
    // Previous elements are the generic ones. Definition above.
    ...
    // Vaccination group
    // Array of objects, defined in "DGC.schema.json"
    "v": [
        // Object vaccination_entry as defined in "DGC.Types.schema.json"
        {
            // disease or agent targeted
            // Value Sets for Digital Green Certificates. version 1.0, 2021-04-16, section 2.1
            // Type string according disease-agent-targeted in "DGC.ValueSets.schema.json"
            "tg": "840539006",
            // vaccine or prophylaxis
            // Value Sets for Digital Green Certificates. version 1.0, 2021-04-16, section 2.2
            // Type string according vaccine-prophylaxis in "DGC.ValueSets.schema.json"
            // SHALL contain one of the values "prophylaxis_code" defined in ./cumulated/covid-19-vaccines.json
            "vp": "1119349007",
            // vaccine medicinal product
            // Value Sets for Digital Green Certificates. version 1.0, 2021-04-16, section 2.3
            // Type string according vaccine-medicinal-product in "DGC.ValueSets.schema.json"
            // SHALL contain one of the values "code" defined in ./cumulated/covid-19-vaccines.json
            "mp": "EU/1/20/1528",
            // Marketing Authorization Holder - if no MAH present, thenmanufacturer
            // Value Sets for Digital Green Certificates. version 1.0, 2021-04-16, section 2.3
            // Type string vaccine-mah-manf in "DGC.ValueSets.schema.json"
            // SHALL contain one of the values "auth_holder_code" defined in ./cumulated/covid-19-vaccines.json
            "ma": "ORG-100030215",
            // Dose number
            // Int min 1, max 9 according dose_posint in "DGC.Core.Types.schema.json"
            "dn": 1,
            // Total Series of Doses
            // Int min 1, max 9 according dose_posint in "DGC.Core.Types.schema.json"
            "sd": 2,
            // Date of Vaccination, ISO 8601
            // String containing date according dt in "DGC.Types.schema.json"
            "dt": "2021-04-22",
            // Country of Vaccination, ISO 3166 (where possible)
            // String with pattern [A-Z]{1,10} according country_vt in "DGC.Core.Types.schema.json"
            "co": "CH",
            // Certificat Issuer
            // String with max length 50 according issuer in "DGC.Core.Types.schema.json"
            // In CH the value shall be fixed to BAG/OFSP/FOPH --> do not forget the translations/languages (EN/DE/FR/IT)
            "is": "Bundesamt für Gesundheit (BAG)",
            // Unique Certificate Identifier: UVCI
            // Unique string maxLength 50 according certification_id in "DGC.Core.Types.schema.json"
            // Example according definition in https://ec.europa.eu/health/sites/health/files/ehealth/docs/vaccination-proof_interoperability-guidelines_en.pdf ANNEX 2
            // Additional Info in the eHN Disscusion https://github.com/ehn-digital-green-development/ehn-dgc-schema/issues/15
            "ci": "01:CH:PlA8UWS60Z4RZVALl6GAZ:12"
        }
    ],
}

```

### Tested

The tested part is defined as followed:

```javascript
{
    // Previous elements are the generic ones. Definition above.
    ...
    // Testing group
    // Array of objects, defined in "DGC.schema.json"
    "t": [
        // Object testing_entry as defined in "DGC.Types.schema.json"
        {
            // disease or agent targeted
            // Value Sets for Digital Green Certificates. version 1.0, 2021-04-16, section 2.1
            // Type string, required code according disease-agent-targeted in "DGC.ValueSets.schema.json"
            "tg": "840539006",
            // Type of test
            // Value Sets for Digital Green Certificates. version 1.0, 2021-04-16, section 2.7
            // Type string, according tt in "DGC.Types.schema.json"
            "tt": "LP217198-3",
            // Test Result
            // "EU eHealthNetwork: Value Sets for Digital Green Certificates. version 1.0, 2021-04-16, section 2.9
            // Type string, required code according test-reslut in "DGC.ValueSets.schema.json"
            "tr": "260415000",
            // Test Manufacturer
            // Value Sets for Digital Green Certificates. version 1.0, 2021-04-16, section 2.8
            // IF key tt is with the value LP217198-3 then the ma field SHALL be set.
            // Type string, SHALL contain one of the values "manufacturer_code_eu" defined in ./cumulated/covid-19-tests.json
            "ma": "1232",
            // Date/Time of Sample Collection
            // Type string, format date-time ISO 8601 according sc in "DGC.Types.schema.json"
            "sc": "2021-04-13T14:20:00+00:00",
            // Date/Time of Test Result
            // Type string, format date-time ISO 8601 according dr in "DGC.Types.schema.json"
            "dr": "2021-04-13T14:40:01+00:00",
            // Testing Centre
            // String with a maxLength of 50 according tc in "DGC.Types.schema.json"
            "tc": "Amavita Apotheke Bahnhof Bern",  
            // Country of Vaccination, ISO 3166 (where possible)
            // String with pattern [A-Z]{1,10} according country_vt in "DGC.Core.Types.schema.json"
            "co": "CH",
            // Certificat Issuer
            // String with max length 50 according issuer in "DGC.Core.Types.schema.json"
            // In CH the value shall be fixed to BAG/OFSP/FOPH --> do not forget the translations/languages (EN/DE/FR/IT)
            "is": "Bundesamt für Gesundheit (BAG)",
            // Unique Certificate Identifier: UVCI
            // Unique string maxLength 50 according certification_id in "DGC.Core.Types.schema.json"
            // Example according definition in https://ec.europa.eu/health/sites/health/files/ehealth/docs/vaccination-proof_interoperability-guidelines_en.pdf ANNEX 2
            // Additional Info in the eHN Disscusion https://github.com/ehn-digital-green-development/ehn-dgc-schema/issues/15
            "ci": "01:CH:PlA8UWS60Z4RZVALl6GAZ:12"
        }
    ]
}
```

### Recovery

The recovery part is defined as followed:

```javascript
{
    // Previous elements are the generic ones. Definition above.
    ...
    // Recovery group
    // Array of objects, defined in "DGC.schema.json"
    "r": [
        // Object recovery_entry as defined in "DGC.Types.schema.json"
        {
            // disease or agent targeted
            // Value Sets for Digital Green Certificates. version 1.0, 2021-04-16, section 2.1
            // Type string, requires code disease-agent-targeted in "DGC.ValueSets.schema.json"
            "tg": "840539006",
            // Date of First Positive Test Result, ISO 8601
            // String with date content according fr in "DGC.Types.schema.json" 
            "fr": "2021-04-22",
            // Country of Vaccination, ISO 3166 (where possible)
            // String with pattern [A-Z]{1,10} according country_vt in "DGC.Core.Types.schema.json"
            "co": "CH",
            // Certificat Issuer
            // String with max length 50 according issuer in "DGC.Core.Types.schema.json"
            // In CH the value shall be fixed to BAG/OFSP/FOPH --> do not forget the translations/languages (EN/DE/FR/IT)
            "is": "Bundesamt für Gesundheit (BAG)",
            // Certificate Valid From, ISO 8601
            // String with date content according df in "DGC.Types.schema.json" 
            "df": "2021-05-01",
            // Certificate Valid Until, ISO 8601
            // String with date content according du in "DGC.Types.schema.json"
            // MAX duration is df + 180 days according https://ec.europa.eu/health/sites/health/files/ehealth/docs/digital-green-certificates_dt-specifications_en.pdf
            "du": "2021-10-21",
            // Unique Certificate Identifier: UVCI
            // Unique string maxLength 50 according certification_id in "DGC.Core.Types.schema.json"
            // Example according definition in https://ec.europa.eu/health/sites/health/files/ehealth/docs/vaccination-proof_interoperability-guidelines_en.pdf ANNEX 2
            // Additional Info in the eHN Disscusion https://github.com/ehn-digital-green-development/ehn-dgc-schema/issues/15
            "ci": "01:CH:PlA8UWS60Z4RZVALl6GAZ:12"
        }
    ]
}

```

## Mapping

For the specified values (like test manufacturer) use the mapping description in the [readme](./cumulated) of the cumulated folder.

## Valuesets

The valuesets are documented and defined in the ./valueset folder. There the [readme](./valuesets) describes the mapping from the original valuesets published the EU to our. Then we use the valueset to get the ./cumulated files. These files should then contain the merged lists that can be used. More infomration and a mapping can be found in the [readme](./cumulated) of the cumulated folder.

## Validation

Use a json validator (ex: [JSON Schema Validator](https://www.jsonschemavalidator.net/)).
Copy and paste in the "Select schema" field the DGC.schema.json file and in the "Input JSON" one of the example files.
