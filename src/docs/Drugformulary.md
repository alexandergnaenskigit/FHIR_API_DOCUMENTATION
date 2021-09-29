---
title: '5. Drug formulary API'
---

# Drug formulary API

Drug formulary API follows [DaVinci PDEX US Drug Formulary Implementation Guide](http://hl7.org/fhir/us/davinci-drug-formulary/index.html)

This implementation guide defines a FHIR interface to a health insurer's drug formulary information for patients/consumers. A drug formulary is a list of brand-name and generic prescription drugs a health insurer agrees to pay for, at least partially, as part of health insurance coverage. Drug formularies are developed based on the efficacy, safety and cost of drugs. The primary use cases for this FHIR interface enable consumers/members/patients to understand the costs and alternatives for drugs that have been prescribed, and to compare their drug costs across different insurance plans

<b>*Permissions are required to get access to this api</b>

This API uses the same principles as described in [Overview](../ParamountInteroperabilityAPIs/basic.html) section and adds the following main resources:

- [Medication Knowledge](../../profiles/MedicationKnowledge/DaVinci-PDEX-US-Drug-Formulary.html)


## Additinal samples:

 - Get MedicationKnowledge by code</br>
[https://portal.aidbox.myparamount.org/MedicationKnowledge?code=75987011110](https://portal.aidbox.myparamount.org/MedicationKnowledge?code=75987011110)