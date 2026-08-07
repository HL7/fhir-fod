This page defines what implementers are expected to do. It is a shell: the structure and the
artifact inventory are in place, and the sections marked *To be written* still need content from the
work group.

### Actors {#actors}

| Actor | Role |
|---|---|
| [Death Record Source](ActorDefinition-fod-death-record-source.html) | Holds registered death records and originates notifications. Typically a jurisdictional Vital Records Office. |
| [Notification Intermediary](ActorDefinition-fod-notification-intermediary.html) | Optionally relays notifications from a source to one or more receivers. Routes on the message header alone. |
| [Notification Receiver](ActorDefinition-fod-notification-receiver.html) | Accepts notifications and attempts to match each one to a patient record. Typically an EHR. |

### Message Events {#events}

A notification is a FHIR message. `MessageHeader.event` carries one of three codes, which is all an
intermediary needs in order to route without inspecting decedent content.

| Event code | Message | Meaning |
|---|---|---|
| `fact-of-death-notification` | [Notification](MessageDefinition-fod-notification.html) | An initial assertion that a registered death occurred. |
| `fact-of-death-correction` | [Correction](MessageDefinition-fod-correction.html) | Revises content previously sent for the same death record. |
| `fact-of-death-void` | [Void](MessageDefinition-fod-void.html) | Retracts a notification previously sent. |

### Notification Content {#content}

The [Fact of Death Notification Bundle](StructureDefinition-fod-notification-bundle.html) is a
`Bundle` of type `message`. Its content slices deliberately mirror the VRDR Mortality Roster Bundle,
so a jurisdiction already producing roster content can reuse the same resource instances.

| Entry | Profile | Cardinality |
|---|---|---|
| MessageHeader | [FOD Message Header](StructureDefinition-fod-message-header.html) | 1..1, first entry |
| Decedent | [FOD Decedent](StructureDefinition-fod-decedent.html) | 1..1 |
| DeathDate | [FOD Death Date](StructureDefinition-fod-death-date.html) | 1..1 |
| SourceOrganization | [FOD Source Organization](StructureDefinition-fod-source-organization.html) | 1..1 |
| Provenance | [FOD Provenance](StructureDefinition-fod-provenance.html) | 1..1 |
| DeathLocation | [FOD Death Location](StructureDefinition-fod-death-location.html) | 0..1 |
| Certifier | VRDR Certifier | 0..1 |

Two points that are easy to get wrong:

- The **date and time of death** are carried by the Death Date observation, not by the Patient.
  `Patient.deceasedBoolean` is fixed to `true` and exists only so that a receiver can see the fact of
  death without dereferencing. Where the two ever disagree, the observation wins.
- The **place of death** is carried twice, deliberately. The coded `placeOfDeath` component on the
  observation is always present; the Death Location resource is optional and may carry a generalized
  address. A sender that cannot disclose a street address still conveys the kind of place.

### Patient Matching {#matching}

Matching is the receiver's responsibility. This guide does not specify an algorithm, and the source
or assurance level of the sender's identity information is out of scope.

What the guide does constrain is the *breadth* of demographics a notification must carry, so that
safe matching is possible at all. The `fod-decedent-matchable` invariant requires either a Social
Security Number, or a birth date together with an address or a telecom.

*To be written:* rationale for the invariant's threshold, guidance on what a receiver should do with a
low-confidence match, and whether the weighted element scheme from the Identity Matching IG should be
adopted in place of the current invariant.

### Corrections and Retractions {#lifecycle}

*To be written.* Needs to cover: that a correction carries complete current content rather than a
delta; that `Provenance.recorded` establishes ordering; that a void sets the Death Date observation's
status to `entered-in-error`; and what a receiver is expected to do when a void arrives for a
notification it never matched.

### Acknowledgement {#acknowledgement}

Receiver support for acknowledgement is optional, but without it a jurisdiction has no way to learn
whether its notifications are reaching a patient record. The
[Acknowledgement Bundle](StructureDefinition-fod-acknowledgement-bundle.html) reports a
[Match Outcome](StructureDefinition-fod-match-outcome.html) and deliberately carries no decedent
content back to the sender.

*To be written:* whether acknowledgement should be promoted from optional to required, and how a
receiver reports an outcome that changes after human review.

### Transport and Security {#transport}

Notifications are delivered by invoking `$process-message` at the receiver's server root.

*To be written:* authentication and authorization expectations, whether asynchronous delivery is
permitted, and how endpoints are discovered and trusted.

### Privacy and Minimum Necessary {#privacy}

A notification carries the fact of death, when and where it happened, and enough demographics to
match. It does not carry cause of death, manner of death, autopsy findings, pregnancy status, or
tobacco contribution, all of which VRDR defines and none of which a receiver needs in order to
coordinate care or stop outreach.

*To be written:* the reasoning behind this boundary in the terms the work group wants on record, and
guidance for jurisdictions whose statutes constrain what may be disclosed.

### Conformance {#conformance}

Expectations by actor are stated in the
[Sender](CapabilityStatement-fod-sender.html) and
[Receiver](CapabilityStatement-fod-receiver.html) capability statements.

As normative statements are written into the sections above, they should also be recorded in the
[Narrative Conformance Statements](Requirements-fromNarrative.html) resource for traceability. That
resource currently has no statements in it.
