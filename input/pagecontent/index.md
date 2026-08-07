### Introduction {#intro}

This IG provides guidance on how fact-of-death notifications can be sent to providers and potentially other clinical systems using FHIR. For example, Vital Records Offices can use this IG to send fact-of-death notifications to EHRs where that patient was seen. By enabling providers to learn promptly and reliably that a patient has died, these fact of death notifications will support active coordination of care and discontinuation of outreach.

### Technical Overview {#technical}

This implementation guide defines the FHIR resources, profiles, and exchange patterns used by parties like Vital Records Offices to communicate a registered death event back to providers that previously cared for the decedent or other interested parties. This IG is a complement to the existing Vital Records Death Reporting (VRDR) and Vital Records Common Library (VRCL) FHIR IGs. If a patient's death isn't recorded at a given healthcare facility with that patient's records, there are many compounding negative effects including communication with families, chart accuracy, and resource allocation.

The artifacts available in the guide include profiles for a notification bundle conveying the identity of the patient decedent, the fact and date/time of death, place of death, and patient matching demographics sufficient for receiving systems to match the notification to a patient record. It reuses decedent demographic profiles from the Vital Records Common Library and event profiles from VRDR.

Many electronic exchanges including this one do necessitate the need to ensure appropriate patient identification so that information is being sent to the correct locations and matched to any pre-existing records. The specific details of that patient identification or source of identification information is out of scope for this work item, though we will ensure that the breadth of common demographics required for safe nationwide matching will be considered as the IG is put together.

The main sections of this IG are:
{: #walkthrough}

- [Background](background.html) - business context implementers should be familiar with before reading
  the remainder of the IG.
- [Detailed Specification](spec.html) - the actors, message events, notification content, and
  conformance expectations implementers are expected to implement.
- [Artifact Index](artifacts.html) - the profiles, terminology, message definitions, and examples
  defined by this guide.
- [Downloads](downloads.html) - a downloadable copy of this implementation guide and other useful
  information.

### Authors

| Name | Email/URL |
|---|---|
| HL7 International - Public Health | [http://www.hl7.org/Special/committees/pher](http://www.hl7.org/Special/committees/pher) |
| Natan Shpringman, Epic | [nshpring@epic.com](mailto:nshpring@epic.com) |