This page provides the business context an implementer should have before reading the
[Detailed Specification](spec.html). It is a shell awaiting content from the work group.

### Why fact-of-death notification matters {#why}

*To be written.* When a patient's death is not recorded at a facility that holds their chart, the
consequences compound: outreach and recall letters continue to be sent to the deceased, families
receive appointment reminders and bills, the chart is inaccurate for anyone who later reads it, and
panel and resource planning are computed against patients who are no longer living.

### Relationship to VRDR and VRCL {#relationship}

*To be written.* This guide is a complement to the Vital Records Death Reporting (VRDR) and Vital
Records Common Library (VRCL) implementation guides rather than a replacement for either. VRDR
describes reporting a death *to* vital records; this guide describes notifying providers *from*
vital records. Decedent demographics are reused from VRCL and the death event profiles from VRDR, so
that a jurisdiction is not maintaining two incompatible representations of the same decedent.

### Current state and what it costs {#current-state}

*To be written.* Describe how providers learn of deaths today, the delay involved, and what is
missed.

### Scope {#scope}

*To be written.* State plainly what is in scope and what is not. In particular, the specific
mechanism and source of patient identification is out of scope, though the guide does constrain the
breadth of demographics carried so that safe nationwide matching is possible.
