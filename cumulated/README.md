# :warning: Rapid-tests value-sets are available until December 31, 2021. They will be removed from the repository after this date. The data will be available through our api. For more information, consult the [api-doc](https://github.com/admin-ch/CovidCertificate-Apidoc#generation-revocation-and-value-set-api-doc). A version of the cumulated value-set will be updated through the file cumulated_value-sets_YYYYMMDD.json at the root of this repository :warning:
# Cumulated

## Mapping

This chapter discribes the mapping of the cumulated arrays into the certificate content.

### Vaccines

The file "covid-19-vaccines.json" shall be used as whitelist for the valid vaccines.

| Cumulated JSON path | Certificate JSON path |
| ------------------- | --------------------- |
| entries[n].prophylaxis_code | v[0].vp |
| entries[n].code | v[0].mp |
| entries[n].auth_holder_code | v[0].ma |

> Where "n" is the array pos of the corresponding vaccination entry.

### Tests

The file "covid-19-tests.json" shall be used as whitelist for the valid test kits.

| Cumulated JSON path | Certificate JSON path |
| ------------------- | --------------------- |
| entries[n].type_code | t[0].tt |
| entries[n].manufacturer_code_eu | v[0].ma<sup>1</sup> |
| entries[n].type | v[0].nm<sup>2</sup> |

> Where `n` is the array pos of the corresponding test kit entry.
> <sup>1</sup>: Use `.ma` when the test type is "Rapid immunoassay" (type code LP217198-3)
> <sup>2</sup>: Use `.nm` when the test type is "Nucleic acid amplification with probe detection" (type code LP6464-4). This field is not in the tested example.

## Structure

Following two chapters shortly describe the structures of the whitelist files.

### Vaccines structure

The structure of the "covid-19-vaccines.json":

```javascript
{
    // Id of the list
    "Id": "Covid 19 Vaccines",
    // Last modified date
    "Date": "2021-05-05",
    // Version code
    "Version": "1.0.0",
    // Entries array, where all acceppted vaccines are listed
    "entries": [
        // Object containing merged information of a vaccine
        {
            // Name of vaccination as string
            // Current source: "display" value of ../valuesets/vaccine-medical-product.json "valueSetValues" entries.
            "name": "Comirnaty",
            // Code of vaccination as string
            // Current source: key of ../valuesets/vaccine-medical-product.json "valueSetValues" entries.
            "code":"EU/1/20/1528",
            // Name of prophylaxos type as string
            // Current source: "display" value of ../valuesets/vaccine-prophylaxis.json "valueSetValues" entries.
            "prophylaxis": "COVID-19 mRNA vaccine",
            // Code of prophylaxos type as string
            // Current source: key of ../valuesets/vaccine-prophylaxis.json "valueSetValues" entries.
            "prophylaxis_code": "1119349007",
            // Name of authorization holder as string
            // Current source: "display" value of ../valuesets/vaccine-mah-manf.json "valueSetValues" entries.
            "auth_holder": "BioNTech Manufacturing GmbH",
            // Code of authorization holder as string
            // Current source: key of ../valuesets/vaccine-mah-manf.json "valueSetValues" entries.
            "auth_holder_code": "ORG-100030215",
            // If authorization is active
            // Current source: "active" value of ../valuesets/vaccine-medical-product.json "valueSetValues" entries.
            "active": "true"
        }
    ]
}

```

#### Maintenance

Following table shows the mapping from the value sets to the cumulated files:
| Cumulated JSON path | vaccine-medical-product.json | vaccine-prophylaxis.json | vaccines-mah-manf.json |
| ------------------- | ---------------------------- | ------------------------ | -------------------------- |
| entries[n].name | valueSetValues.x<sup>3</sup>.display | - | - |
| entries[n].code | valueSetValues.x<sup>3</sup> | - | - |
| entries[n].prophylaxis | - | valueSetValues.y<sup>4</sup>.display | - |
| entries[n].prophylaxis_code | - | valueSetValues.y<sup>4</sup> | - |
| entries[n].auth_holder | - | - | valueSetValues.z<sup>5</sup>.display |
| entries[n].auth_holder_code | - | - | valueSetValues.z<sup>5</sup> |
| entries[n].active | valueSetValues.x<sup>3</sup>.active | - | - |

> <sup>3</sup>: `x` represents the key names (medical product number) of the objects in the valueSetValues object.
> <sup>4</sup>: `y` represents the key names (SNOMED CT or ATC code) of the objects in the valueSetValues object.
> <sup>5</sup>: `z` represents the key names (organisation id) of the objects in the valueSetValues object.

### Tests structure
The structure of the "covid-19-tests.json":

```javascript
{
    // Id of the list
    "Id": "Covid 19 Tests",
    // Last modified date
    "Date": "2021-05-07",
    // Version code
    "Version": "1.0.0",
    // Entries array, where all acceppted tests are listed
    "entries": [
        // Object containing merged information of a test
        {
            // Name of test as string
            // Current source: "display" value of ../valuesets/test-name.json "valueSetValues" entries.
            "name": "Panbio COVID-19 Ag Test",
            // Type of test as string
            // Type of test, as long as it is found in ../valuesets/test-manf.json the value is "Rapid immunoassay"
            // One object needs to contain the "Nucleic acid amplification with probe detection"
            // Current source: "display" value of ../valuesets/test-type.json "valueSetValues" entries.
            "type": "Rapid immunoassay",
            // Type code of test type as string
            // If type of test is "Rapid immunossay" and found in ../valuesets/test-manf.json, key of array pos [0]
            // If type of test is "Nucleic acid amplification with probe detection", key of array pos [1]
            // Current source: key of ../valuesets/test-type.json "valueSetValues" entries.
            "type_code": "LP217198-3",
            // Manufacturer name of test as string
            // Current source: "display" value of ../valuesets/test-manufacturer.json "valueSetValues" entries.
            "manufacturer": "Abbott Rapid Diagnostics",
            // Swiss testkit code of test as string
            // Current source: TestKitCode of table entry from the document "Listen der validierten SARS-CoV-2-Schnelltests1.pdf" published by FOPH
            // Only set value, if "name" and "manufacturer" matches
            "swiss_test_kit": "2",
            // EU code of manufacturer as string
            // Current source: key of ../valuesets/test-manufacturer.json "valueSetValues" entries.
            "manufacturer_code_eu": "1232",
            // If authorization is active
            // Current source: "active" value of ../valuesets/test-name.json "valueSetValues" entries.
            "active": "true"
        }
    ]
}

```

#### Maintenance

Before the cumulated file can be manipulated, the original test-manufacturer-and-name.json has to be split in two file:

- test-manufacturer.json
- test-name.json

Following table shows the mapping from the value sets to the cumulated files:
| Cumulated JSON path | test-name.json | test-manufacturer.json | test-type.json |
| ------------------- | ---------------------------- | ------------------------ | -------------------------- |
| entries[n].name | valueSetValues.x<sup>6</sup>.display OR "PCR"<sup>7</sup> | - | - |
| entries[n].type | - | - | valueSetValues.[0].display<sup>8</sup> OR valueSetValues.[1].display<sup>7</sup> |
| entries[n].type_code | - | - | valueSetValues.y<sup>9</sup> |
| entries[n].manufacturer | - | valueSetValues.x<sup>6</sup> | - |
| entries[n].swiss_test_kit | - | - | - |
| entries[n].manufacturer_code_eu | - | valueSetValues.x<sup>6</sup> | - |
| entries[n].active | valueSetValues.x<sup>6</sup>.active | - | - |

> <sup>6</sup>: `x` represents the key names (manufacturer code) of the objects in the valueSetValues object.
> <sup>7</sup>: One object needs to contain the "Nucleic acid amplification with probe detection" test.
> <sup>8</sup>: If test is found in ../valuesets/test-manufacturer-and-name.json, use array pos [0] as fixed value.
> <sup>9</sup>: `y` represents the key names (test type code) of the objects in the valueSetValues object.
