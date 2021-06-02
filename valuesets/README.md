# Valuesets

The defined valuesets are based on the schema [valueset.json](https://github.com/eu-digital-green-certificates/ehn-dgc-schema/blob/main/valueset.json) published by the EU ([GitHub Repo](https://github.com/eu-digital-green-certificates/ehn-dgc-schema)).

## disease-agent-targeted

The disease-agent-targeted (key `tg` inside the `v`, `t` and `r` objects) is always the SNOMED CT code for COVID-19. The valueset can be found on the GitHub Repository of the `eu-digital-green-certificates` in the `ehn-dgc-schema` project under following [link](https://github.com/eu-digital-green-certificates/ehn-dgc-schema/blob/main/valuesets/disease-agent-targeted.json).

### Mapping

There is no mapping needed for the disease-agent-target valueset. Use the [original file](https://github.com/ehn-digital-green-development/ehn-dgc-schema/blob/main/valuesets/disease-agent-targeted.json).

## vaccine-prophylaxis

The vaccination-prophylaxis (key `vp` inside the `v` object) is the SNOMED CT or ATC classification code for one of the covid-19 vaccine types. Following types are defined:

- `1119349007` --> SARS-CoV-2 mRNA vaccine (SNOMED CT)
- `1119305005` --> SARS-CoV-2 antigen vaccine (SNOMED CT)
- `J07BX03` --> covid-19 vaccines (ATC)

Use the ATC code, when the vaccine is neither an antigen nor a mRNA or the information is missing.
The valueset definition can be found on the GitHub Repository of the `eu-digital-green-certificates` in the `ehn-dgc-schema` project under following [link](https://github.com/eu-digital-green-certificates/ehn-dgc-schema/blob/main/valuesets/vaccine-prophylaxis.json).

### Mapping

There is no mapping needed for the vaccine-prophylaxis valueset. Use the [original file](https://github.com/ehn-digital-green-development/ehn-dgc-schema/blob/main/valuesets/vaccine-prophylaxis.json).

## vaccine-medicinal-product

The vaccine-medicinal-product (key `mp` inside the `v` object) is the code of the Union Register of medicinal products or [Vaccine medicinal products not centrally authorized in the EU](https://webgate.ec.europa.eu/fpfis/wikis/x/ZYg-L).

> **NOTE:** The valueset contains more vaccines than validated for Switzerland. This should be the whole list of the approved vaccines from the EU.

### Mapping

There is no mapping needed for the vaccine-prophylaxis valueset. Use the [original file](https://github.com/ehn-digital-green-development/ehn-dgc-schema/blob/main/valuesets/vaccine-medicinal-product.json).
The merged vaccine file inside the ../cumulated folder then should only contain the accepted vaccines from Switzerland. Accepted means NOT the approved ones in Switzerland, but those that are accepted when crossing the border!

## vaccines-mah-manf

The vaccine manufacturer (key `ma` inside the `v` object) is the organisation id of the manufacturer.

### Mapping

There is no need for a mapping. Use the [original valueset](https://github.com/ehn-digital-green-development/ehn-dgc-schema/blob/main/valuesets/vaccine-mah-manf.json).

## test-result

The test result valueset contains the snomed ct codes for detected and not detected.

### Mapping

There is no mapping needed for the test-result valueset. Use the [original file](https://github.com/ehn-digital-green-development/ehn-dgc-schema/blob/main/valuesets/test-result.json).

## test-type

The test type valueset contains two different type of covid-19 test types. The Rapid immunoassay and te NAAT.

### Mapping

There is the newly created [original file](https://github.com/ehn-digital-green-development/ehn-dgc-schema/blob/main/valuesets/test-type.json) to get the data from. There are no differences between the two files.

## test-manf

The test manufacturer and name file (test-manf) contains the list with all allowed test kits, containing the product and the manufacturer name.

> **NOTE:** The valueset contains more tests than validated for Switzerland. This should be the whole list of the approved tests from the EU. For a list of approved tests in Switzerland, consult the [SARS-CoV-2-Schnelltests für die Fachanwendung](https://www.bag.admin.ch/dam/bag/de/dokumente/biomed/heilmittel/COVID-19/validierte-schnelltests-covid.pdf.download.pdf/Validierte%20SARS-CoV-2-Schnelltests%20FA.pdf) file.

### Mapping

The [original valueset](https://github.com/ehn-digital-green-development/ehn-dgc-schema/blob/main/valuesets/test-manf.json).

The display name of the `valueSetValues` contains the manufacturer and the product name comma sepparated. Therefore, split the file into the two files `test-manufacturer` and `test-name`, where the display should then contain only the manufacturer or the test name.
