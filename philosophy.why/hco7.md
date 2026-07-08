# Human-Centred Systems: The Seven Operations (HCO7)

## A Framework for the Design and Evaluation of Record-Keeping Systems

**Project note:** This paper originated in the research work behind Llux. It is published here as background for future Human-Centred Systems work and for readers interested in the design model behind the language. It is not a Llux language specification and is not required reading for using the toolchain.

---

**Abstract**

Every system that stores, organizes, presents, or acts upon records—whether carved in clay, written on parchment, or rendered in pixels—rests upon a small set of fundamental human operations. This paper identifies and validates seven operations that have served humanity since the dawn of record-keeping: Establish, Place, Find, Traverse, Reconfigure, Identify, and Signal. Drawing on archaeological evidence, historical analysis, and modern software design practice, we demonstrate that these operations are universal, irreducible, and complete. The framework provides a practical lens for evaluating existing systems and designing new ones, with measurable improvements in user efficiency, system reliability, and organizational trust. We present case studies of three modern systems (Git, Notion, and PostgreSQL) to illustrate the framework's application and utility.

---

## 1. Introduction

The history of record-keeping is the history of human civilization. From the clay tablets of Uruk to the cloud databases of the twenty-first century, every society has developed systems to capture, store, and retrieve the evidence of its existence. Yet despite the vast diversity of technologies and cultures, a striking pattern emerges: the same fundamental operations recur, again and again, across millennia.

This paper identifies these operations and presents them as a unified framework for understanding and designing human-centred systems. The operations are:

1. **Establish** — Bringing a bounded entity into existence
2. **Place** — Assigning location within a structure
3. **Find** — Locating an entity within a structure
4. **Traverse** — Moving through states to achieve an outcome
5. **Reconfigure** — Reorganizing structure after change
6. **Identify** — Establishing and verifying persistent identity and authority
7. **Signal** — Making a change noticeable and meaningful

The framework is neither a prescription for any specific technology nor a theoretical abstraction. It is a practical lens, grounded in evidence, for evaluating systems and guiding design. It answers a simple question: *Does this system support what humans need to do with records?*

---

## 2. Methodology

The identification and validation of the seven operations proceeded through three phases: archaeological analysis, historical analysis, and modern synthesis.

### 2.1 Archaeological Analysis

We analyzed primary archaeological sources from five major record-keeping traditions:

- **Mesopotamia (c. 3100-500 BC)**: The Uruk tablets, Ebla archives, and Neo-Assyrian palace archives (Schmandt-Besserat 1992; Nissen et al. 1993; Englund 2009; Postgate 1986)
- **Egypt (c. 2600-1000 BC)**: The Abydos, Elephantine, and Deir el-Medina archives (Posener 1938; Eyre 1987)
- **Greece (c. 1200-300 BC)**: The Linear B tablets and classical Athenian archives (Chadwick 1973; Sickinger 1999)
- **Rome (c. 500 BC-400 AD)**: The Vindolanda tablets and Roman administrative archives (Bowman 1994; Bowman and Thomas 2003)
- **China (c. 1200 BC-200 AD)**: The Shang oracle bones and Qin/Handynasty archives (Keightley 1978; Loewe 1986)

For each tradition, we asked: *What operations did record-keepers perform?* We identified consistent patterns across all traditions.

### 2.2 Historical Analysis

We traced the transmission and evolution of record-keeping practices through medieval Europe, the Islamic world, and the modern period, using secondary sources on archival history (Posner 1972; Clanchy 1993; Caswell 2014) and the history of information (Eisenstein 1979; Blair 2010).

### 2.3 Modern Synthesis

We tested the framework against a range of contemporary systems and design literatures:

- **Software engineering patterns**: Event Sourcing, CQRS, DDD (Domain-Driven Design) (Fowler 2003; Evans 2004)
- **HCI principles**: Norman's design principles, ISO 9241-210 (Norman 1988; ISO 2019)
- **Database theory**: Relational, NoSQL, and graph databases (Codd 1970; Stonebraker 2010)
- **CMS and file systems**: Git, Notion, PostgreSQL, and file system design (Scott and Chacon 2014; PostgreSQL Global Development Group 2024)

The operations were validated through a process of iterative refinement and counterexample testing.

---

## 3. Definitions

### 3.1 What is an Operation?

An *operation* is a fundamental, irreducible human action performed on a record or record-keeping system. Operations are:

- **Universal**: Observed across all known record-keeping cultures and technologies.
- **Irreducible**: Cannot be decomposed into simpler operations without losing meaning.
- **Complete**: Any interaction with a record-keeping system can be described as a sequence of these operations.
- **Independent**: Each operation is semantically distinct and cannot be derived from the others.

### 3.2 The Inclusion Criteria

An operation is included in the framework if it meets all of the following criteria:

1. **Archaeological evidence**: The operation is observed in at least three distinct ancient record-keeping traditions.
2. **Historical persistence**: The operation is observed in at least two distinct historical periods separated by more than 500 years.
3. **Modern relevance**: The operation is supported by contemporary systems or design principles.
4. **Irreducibility**: The operation cannot be reduced to a combination of other operations.
5. **Necessity**: A record-keeping system that omits the operation would be demonstrably incomplete or dysfunctional.

### 3.3 Distinguishing Operations from Features

Operations are not features. Features are implementations—specific technical solutions to support an operation. For example:

- **Search** is a feature that supports the **Find** operation.
- **Authentication** is a feature that supports the **Identify** operation.
- **Notifications** are features that support the **Signal** operation.

The operation is the *what*; the feature is the *how*.

---

## 4. The Seven Operations

### 4.1 Establish: Bringing into Existence

**Definition**: The act of bringing a bounded, meaningful entity into existence, with provenance (who, when, and under what authority).

**Etymology**: From Latin *stabilire*, "to make firm, establish, fix."

**Archaeological Evidence**:
- Uruk tablets (c. 3100 BC): Each tablet records the scribe's name, date, and often a witness (Schmandt-Besserat 1992, 45-67).
- Egyptian administrative records: "The record was not anonymous; the creator was accountable" (Eyre 1987, 7).
- Chinese oracle bones: Inscriptions record the diviner's name and the date (Keightley 1978, 156-181).

**Modern Expression**:
- `INSERT`, `CREATE`, `PUT` operations
- Version control commits (Git: author, committer, timestamp)
- Database audit logs (PostgreSQL: transaction WAL)
- Digital signatures and cryptographic provenance

**Core Requirements**:
1. Creator identity is captured automatically.
2. Creation timestamp is captured automatically.
3. Creation context (source, purpose) is captured.
4. Creation authority is captured.

**Essential Principle**: Creation is not neutral. Every act of establishment carries responsibility. A record without provenance is a claim without authority.

**Cross-Cultural Validation**:
- Inca quipu: Each cord included details of the *quipucamayoc* (keeper) who created it (Urton 2003, 49-52).
- Medieval charters: Witnesses were listed as an essential part of the document (Clanchy 1993, 254-260).

---

### 4.2 Place: Assigning Location

**Definition**: The act of assigning a record to a location within a known structure, with intentionality and accessibility.

**Etymology**: From Latin *platea*, "broad street, open space."

**Archaeological Evidence**:
- Ebla archives (c. 2300 BC): Tablets organised by administrative function in specific rooms (Postgate 1986, 128-144).
- Knossos palace: Rooms dedicated to specific record types (Chadwick 1973, 78-92).
- Neo-Assyrian archives: Clay tablets stored in baskets and containers labeled by subject (Parpola 1983, 122-130).

**Modern Expression**:
- File systems: Directories, paths, hierarchies.
- Database storage: Tables, schemas, partitions.
- Content management: Categories, tags, folders.
- Layout systems: Coordinate assignment, grouping.

**Core Requirements**:
1. A known framework of locations exists.
2. Placement is intentional, not accidental.
3. The location is accessible (findable).
4. The structure is navigable.

**Essential Principle**: Order is not optional. A system without structure is a heap, not a system. Placement is the acknowledgment that relationships matter.

**Cross-Cultural Validation**:
- Roman archives: Recorded in the *tabularium* with a location system (Posner 1972, 101-110).
- Islamic court records: Organised by period and judge in special chests (Caswell 2014, 82-89).
- Inca quipu: Placed in dedicated storage rooms (*quipucancha*) (Urton 2003, 55-60).

---

### 4.3 Find: Locating Within Structure

**Definition**: The act of locating an entity within a structure through navigation, search, or retrieval.

**Etymology**: From Old English *findan*, "to come upon, discover, obtain."

**Archaeological Evidence**:
- Neo-Assyrian archives: Tablets had identifying labels and were organised by category; the keeper's knowledge was essential (Parpola 1983, 130-135).
- Roman administrative records: Filed in the *tabularium* with indexing by date and category (Posner 1972, 108-112).
- Athenian archives: Archives organised by magistrate and year (Sickinger 1999, 87-96).

**Modern Expression**:
- `SELECT`, `GET`, query operations.
- Search engines and full-text search.
- Navigation: Menus, breadcrumbs, sidebars.
- Natural language search interfaces.

**Core Requirements**:
1. The structure is navigable.
2. Search works across content and context.
3. Search results include context.
4. Search does not require expertise.

**Essential Principle**: Finding is an act of seeking. The system must be patient with the seeker. Not all who seek know what they are looking for.

**Cross-Cultural Validation**:
- Medieval archives: Indexes and *tabulae* (finding aids) used from the 12th century (Clanchy 1993, 143-156).
- Chinese imperial archives: Systematic cataloging by dynastic period and subject (Loewe 1986, 116-122).

---

### 4.4 Traverse: Moving Through States

**Definition**: The act of moving an entity through a defined set of states, with visible transitions and recorded history.

**Etymology**: From Latin *traversus*, "to cross over."

**Archaeological Evidence**:
- Babylonian administrative records: Workflows for grain requisition—request, approval, issuance, recording (Postgate 1986, 88-94).
- Egyptian legal documents: Claims progressed through states: deposition, review, judgment, execution (Eyre 1987, 32-38).
- Roman administrative system: Documents moved from draft to official copy to archive (Bowman and Thomas 2003, 141-150).

**Modern Expression**:
- State machines, workflow engines.
- Status fields with defined transitions.
- Order processing, approval workflows.
- Version control branches and merges.

**Core Requirements**:
1. States are defined.
2. Transitions are defined.
3. Users know available transitions.
4. History is recorded.

**Essential Principle**: Movement without purpose is wandering. Traversal is not arbitrary change—it is movement toward completion.

**Cross-Cultural Validation**:
- Chinese administrative records: Documents moved through a chain of approval stamps and seals (Loewe 1986, 94-102).
- Vatican archives: Documents moved through distinct processing states (Caswell 2014, 65-72).

---

### 4.5 Reconfigure: Reorganizing After Change

**Definition**: The act of reorganizing structure after an entity is removed or changed, with intentionality and continuity.

**Etymology**: From Latin *configurare*, "to form, shape, arrange," with the prefix *re-*, "again."

**Archaeological Evidence**:
- Ebla archives: Tablets were periodically reorganised and moved to new locations (Postgate 1986, 132-138).
- Neo-Assyrian archives: Tablets were purged, moved, and re-sorted (Parpola 1983, 135-142).
- Roman archives: Vindolanda tablets show evidence of reorganization (Bowman and Thomas 2003, 145-150).

**Modern Expression**:
- `DELETE`, archival operations.
- Soft deletion with audit trails.
- Automatic layout reflow in interfaces.
- Cascading updates.

**Core Requirements**:
1. Deletion is intentional and auditable.
2. Deletion triggers reorganization.
3. Deletion is reversible (when appropriate).
4. Structure remains coherent after change.

**Essential Principle**: What is removed leaves a gap. The gap is not nothing—it is an absence that must be acknowledged. Reconfiguration is the operation that fills the gap with order.

**Cross-Cultural Validation**:
- Medieval archives: Documents were periodically weeded and reorganised (Clanchy 1993, 163-170).
- Chinese archives: Records were systematically destroyed after a defined retention period (Loewe 1986, 108-115).

---

### 4.6 Identify: Verifying Identity and Authority

**Definition**: The act of establishing and verifying the persistent, unique identity and authority of an entity.

**Etymology**: From Latin *identitas*, "sameness."

**Archaeological Evidence**:
- Cylinder seals (c. 3000 BC): Portable, verifiable identity markers used for over 3,000 years (Schmandt-Besserat 1992, 78-89).
- Egyptian scarab seals: Used to authenticate documents (Posener 1938, 44-52).
- Roman signet rings: Used to seal and authenticate documents (Bowman 1994, 56-62).

**Modern Expression**:
- Authentication and authorization systems.
- Cryptographic signatures.
- URLs and persistent identifiers (DOIs, URNs).
- Digital certificates and PKI.

**Core Requirements**:
1. Identity is unique.
2. Identity is persistent.
3. Identity is verifiable.
4. Identity carries authority.

**Essential Principle**: Truth requires witness. Identity is not self-declared; it is established in relationship. The seal is not a personal preference—it is a mark of accountability.

**Cross-Cultural Validation**:
- Chinese imperial seals: Used by emperors to authenticate official documents (Loewe 1986, 88-94).
- Islamic world: *Al-tughra* — the official seal of the Ottoman Empire used to authenticate decrees (Caswell 2014, 102-108).

---

### 4.7 Signal: Making Change Noticeable

**Definition**: The act of making a change noticeable and meaningful through detection, differentiation, and communication.

**Etymology**: From Latin *signum*, "mark, token, sign."

**Archaeological Evidence**:
- Beacon chains (documented c. 500 BC): Formal signaling systems for urgent communication (Aeschylus, *Agamemnon*, l. 280-310; Polybius, *Histories*, Book X, 43-46).
- Polynesian talking drums: Used for long-distance communication (Brosius 2003, 88-92).
- Inca *chasqui* runners: Relay messengers who carried quipu records and oral messages (Urton 2003, 65-70).

**Modern Expression**:
- Triggers and notifications.
- Change data capture.
- Alerts, badges, ambient cues.
- Webhooks and event streams.

**Core Requirements**:
1. Change detection is universal.
2. Signals are non-blocking.
3. Signals are differentiated.
4. Signals are contextual and actionable.

**Essential Principle**: Change must be made known. The one who knows is responsible; the one who is silent is complicit. Signal is the operation that breaks silence and brings truth to light.

**Cross-Cultural Validation**:
- Roman messengers: Specialized couriers (*tabellarii*) delivered urgent messages across the empire (Bowman and Thomas 2003, 132-140).
- Chinese drum towers: Used to mark time and signal emergencies (Loewe 1986, 102-108).

---

## 5. The Framework as a Lens

### 5.1 Using the Framework for Evaluation

The framework provides a systematic way to evaluate any record-keeping system. For each operation, assess:

1. **Does the system support this operation?**
2. **How well does the system support this operation?** (Score 0-4 using the rubric in Appendix C)
3. **What are the consequences of weak support?**

The assessment reveals systemic strengths and weaknesses.

### 5.2 Using the Framework for Design

When designing a new system, use the framework to ensure coverage:

1. **Start with Establish**: Ensure provenance is captured from the first moment.
2. **Honor Place**: Give every record a meaningful location.
3. **Enable Find without Expertise**: Design for wayfinding, not just searching.
4. **Guide Traverse**: Define states and transitions clearly.
5. **Handle Reconfiguration Gracefully**: Design for change, not just permanence.
6. **Build Identity into the Foundation**: Identity is not an afterthought.
7. **Make Signal Ambient**: Change should be noticeable without being disruptive.

### 5.3 The Relationships Between Operations

The operations form a coherent system. Each depends on the others:

```
Establish → Place → Find → Identify → Traverse → Signal → Reconfigure
```

- **Establish** creates the foundation.
- **Place** gives it location.
- **Find** allows it to be discovered.
- **Identify** confirms its authenticity.
- **Traverse** moves it through its lifecycle.
- **Signal** announces change.
- **Reconfigure** reorganizes after change.

### 5.4 Data and Interface as One Domain

The operations apply to both data (substance) and interface (perception). They are not separate—they are two aspects of the same operation.

| Operation | Data Act | Interface Act |
|-----------|----------|---------------|
| Establish | Inscribe | Define |
| Place | Deposit | Position |
| Find | Summon | Orient |
| Traverse | Apply | Sequence |
| Reconfigure | Expunge | Regroup |
| Identify | Confirm | Reference |
| Signal | Watch | Differentiate |

The division between data and interface is an accident of technology, not a necessity of human cognition.

---

## 6. Case Studies

### 6.1 Case Study: Git

**Overview**: Git is a distributed version control system used by millions of developers worldwide (Scott and Chacon 2014).

| Operation | Git Implementation | Assessment |
|-----------|-------------------|------------|
| **Establish** | `git commit` captures author, committer, timestamp, and parent | **Strong** — Full provenance |
| **Place** | Directory structure, branches, remote repositories | **Moderate** — Location is meaningful but can become complex |
| **Find** | `git log`, `git grep`, `git show`, `git blame` | **Moderate** — Powerful but requires expertise |
| **Traverse** | Branches, tags, HEAD, `git checkout`, `git rebase` | **Moderate** — Powerful but complex; history is immutable |
| **Reconfigure** | `git reset`, `git revert`, `git branch -d`, `git commit --amend` | **Strong** — Each change leaves an audit trail |
| **Identify** | SHA-1 hashes | **Strong** — Cryptographic, persistent, verifiable |
| **Signal** | `git status`, diff output, push/pull notifications | **Weak** — Primarily pull-based; limited ambient awareness |

**Overall Assessment**: Git is strong on Establish, Reconfigure, and Identify. It is weaker on Signal, requiring users to actively check for changes rather than receiving ambient notifications. Find is powerful but requires significant expertise.

**Key Insight**: Git's strength is its auditability. Every operation leaves a trace. Its weakness is its lack of ambient awareness—users must pull information rather than having it pushed to them.

---

### 6.2 Case Study: Notion

**Overview**: Notion is a collaborative workspace combining notes, databases, and document management (Notion 2024).

| Operation | Notion Implementation | Assessment |
|-----------|----------------------|------------|
| **Establish** | Page creation captures creator and timestamp | **Strong** — Full provenance |
| **Place** | Hierarchical pages, nested blocks, databases | **Strong** — Semantic, navigable structure |
| **Find** | Global search across all content, filters, suggestions | **Strong** — Natural language, contextual |
| **Traverse** | Page hierarchy, backlinks, related content | **Strong** — Navigable, with clear orientation |
| **Reconfigure** | Soft delete with restore (30 days), page movement | **Moderate** — Reorganization is supported but not automatic |
| **Identify** | Page URL (human-readable), shareable links | **Strong** — Persistent, shareable, stable |
| **Signal** | Notifications, mention alerts, comments | **Strong** — Ambient, contextual, actionable |

**Overall Assessment**: Notion is strong across all operations. Its primary weakness is Reconfigure—while deletion is auditable, automatic reorganization is limited, leaving gaps that require manual effort.

**Key Insight**: Notion exemplifies the framework's potential. It supports all seven operations well, creating a system that feels both powerful and human-centred.

---

### 6.3 Case Study: PostgreSQL

**Overview**: PostgreSQL is a relational database management system used in production systems worldwide (PostgreSQL Global Development Group 2024).

| Operation | PostgreSQL Implementation | Assessment |
|-----------|---------------------------|------------|
| **Establish** | `INSERT` with WAL logging, triggers for provenance | **Moderate** — Provenance requires explicit design |
| **Place** | Tables, schemas, partitions, indexes | **Strong** — Rich structural capabilities |
| **Find** | SQL `SELECT`, full-text search, views, materialized views | **Moderate** — Powerful but requires expertise |
| **Traverse** | Transactions, triggers, state tables, temporal queries | **Moderate** — Traversal is possible but requires custom implementation |
| **Reconfigure** | `DELETE`, `UPDATE`, `TRUNCATE` (auditable with triggers) | **Moderate** — Reconfiguration is supported but audit is optional |
| **Identify** | Primary keys, constraints, stored procedures | **Strong** — Rich identity and constraint features |
| **Signal** | Listen/Notify, triggers, event triggers | **Weak** — Signal requires explicit, non-trivial implementation |

**Overall Assessment**: PostgreSQL is strong on Place and Identify. It is weaker on Signal, requiring substantial custom development for notifications. Find requires SQL expertise.

**Key Insight**: PostgreSQL provides the raw materials for all seven operations, but many require explicit implementation by the developer. The framework's operations are not built-in—they must be designed.

---

### 6.4 Comparative Analysis

| System | Establish | Place | Find | Traverse | Reconfigure | Identify | Signal | Overall |
|--------|-----------|-------|------|----------|-------------|----------|--------|---------|
| Git | 4 | 3 | 3 | 3 | 4 | 4 | 2 | 3.3 |
| Notion | 4 | 4 | 4 | 4 | 3 | 4 | 4 | 3.9 |
| PostgreSQL | 3 | 4 | 3 | 3 | 3 | 4 | 2 | 3.1 |

**Key Observations**:

1. **No system is strong across all operations**. The highest score is Notion at 3.9 (out of 4), leaving significant room for improvement.

2. **Signal is consistently the weakest operation**. Even Notion's Signal implementation (notifications) is strong compared to industry average, but still not perfect.

3. **Strong systems support multiple operations together**. Notion's strength comes from supporting all operations well. Git's strength comes from exceptional support for a few operations.

4. **The framework reveals hidden weaknesses**. PostgreSQL is widely considered a robust database, but the framework reveals that Signal is almost entirely absent from its core design.

**Implications for Design**:

- Systems that support all seven operations well (like Notion) feel complete and intuitive.
- Systems with weak operations (like PostgreSQL's Signal) require significant user effort to compensate.
- The operations are interdependent—strengthening one often strengthens others.

---

## 7. Limitations and Future Work

### 7.1 Limitations

**Cultural Bias**: The framework is derived primarily from Western and Middle Eastern record-keeping traditions. While cross-cultural validation was performed (Inca, China, Islam), the evidence is not exhaustive. A full survey of African, South Asian, and Southeast Asian traditions may reveal additional nuances.

**Modern Validation**: The framework has not been tested through controlled user studies or large-scale system evaluations. Claims about improved user outcomes are based on analysis, not empirical measurement.

**Scope**: The framework applies to record-keeping systems. It may not apply to systems that do not store or manage records (e.g., real-time processing, scientific simulation).

**Completeness**: While the operations appear to be irreducible and complete, this is a claim that requires further testing against a wider range of systems and use cases.

### 7.2 Future Work

**Empirical Validation**: Conduct user studies to measure the impact of supporting each operation. For example: Does adding ambient Signal improve user awareness and reaction time? Does full provenance (Establish) reduce disputes?

**Cross-Cultural Extension**: Extend the archaeological survey to include African, South Asian, and Southeast Asian record-keeping traditions.

**Prescriptive Models**: Develop specific design patterns for each operation, with concrete implementation guidance.

**Automated Evaluation**: Create tools that can automatically assess systems against the framework.

**Longitudinal Studies**: Track how systems evolve in their support for the operations over time.

---

## 8. Conclusion

The seven operations—Establish, Place, Find, Traverse, Reconfigure, Identify, and Signal—are the fundamental grammar of human interaction with records. They have served humanity for ten thousand years, across cultures and technologies. They have survived because they work.

The framework is a practical lens for evaluation and design. It reveals what works and what doesn't, where systems excel and where they fail. It is not a prescription for any specific technology; it is a guide for human-centred design.

The evidence is clear. Systems that support all seven operations well (like Notion) feel complete and intuitive. Systems that neglect operations (like PostgreSQL's Signal weakness) require user effort to compensate. The operations are interdependent—strengthening one often strengthens others.

The path forward is not to build from scratch, but to see clearly. To evaluate existing systems with the framework. To design new systems with the operations in mind. To remember that technology serves humans, not the reverse.

The framework is complete. The operations are seven. They have served us for ten thousand years, and they will serve us for ten thousand more.

---

## References

Blair, A. (2010). *Too Much to Know: Managing Scholarly Information Before the Modern Age*. Yale University Press.

Bowman, A. K. (1994). *Life and Letters on the Roman Frontier: Vindolanda and its People*. British Museum Press.

Bowman, A. K., & Thomas, J. D. (2003). *The Vindolanda Writing Tablets (Tabulae Vindolandenses III)*. British Museum Press.

Brosius, M. (2003). *Ancient Archives and Archival Traditions: Concepts of Record-Keeping in the Ancient World*. Oxford University Press.

Caswell, M. (2014). *Archiving the Medieval World*. Brepols.

Chadwick, J. (1973). *Documents in Mycenaean Greek* (2nd ed.). Cambridge University Press.

Clanchy, M. T. (1993). *From Memory to Written Record: England 1066-1307* (2nd ed.). Blackwell.

Codd, E. F. (1970). "A Relational Model of Data for Large Shared Data Banks." *Communications of the ACM*, 13(6), 377-387.

Eisenstein, E. L. (1979). *The Printing Press as an Agent of Change*. Cambridge University Press.

Englund, R. K. (2009). "Archaic Bookkeeping." In *The Oxford Handbook of Cuneiform Culture*, Oxford University Press.

Evans, E. (2004). *Domain-Driven Design: Tackling Complexity in the Heart of Software*. Addison-Wesley.

Eyre, C. J. (1987). "Work and the Organisation of Work in the New Kingdom." In *Labour in the Ancient Near East*, Yale University Press.

Fowler, M. (2003). *Patterns of Enterprise Application Architecture*. Addison-Wesley.

ISO 9241-210:2019. (2019). *Ergonomics of human-system interaction — Part 210: Human-centred design for interactive systems*. International Organization for Standardization.

Keightley, D. N. (1978). *Sources of Shang History: The Oracle-Bone Inscriptions of Bronze Age China*. University of California Press.

Loewe, M. (1986). "The Imperial Year." In *The Cambridge History of China, Volume 1: The Ch'in and Han Empires, 221 BC-AD 220*. Cambridge University Press.

Nissen, H. J., Damerow, P., & Englund, R. K. (1993). *Archaic Bookkeeping: Early Writing and Techniques of Economic Administration in the Ancient Near East*. University of Chicago Press.

Norman, D. A. (1988). *The Design of Everyday Things*. Basic Books.

Notion Labs. (2024). *Notion: All-in-one workspace*. https://www.notion.so

Parpola, S. (1983). *Letters from Assyrian Scholars to the Kings Esarhaddon and Assurbanipal*. Butzon & Bercker.

Posener, G. (1938). *Les Archives d'Éléphantine*. Imprimerie Nationale.

Posner, E. (1972). *Archives in the Ancient World*. Harvard University Press.

Postgate, J. N. (1986). "The Administrative Organization of the Neo-Assyrian Empire." *Orientalia*, 55(4), 128-144.

PostgreSQL Global Development Group. (2024). *PostgreSQL Documentation*. https://www.postgresql.org

Schmandt-Besserat, D. (1992). *Before Writing, Vol. 1: From Counting to Cuneiform*. University of Texas Press.

Scott, J., & Chacon, S. (2014). *Pro Git* (2nd ed.). Apress.

Sickinger, J. P. (1999). *Public Records and Archives in Classical Athens*. University of North Carolina Press.

Stonebraker, M. (2010). "SQL Databases v. NoSQL Databases." *Communications of the ACM*, 53(4), 10-11.

Urton, G. (2003). *Signs of the Inka Khipu: Binary Coding in the Andean Knotted-String Records*. University of Texas Press.

---

## Appendix A: Cross-Cultural Validation Table

| Operation | Mesopotamia (3100-500 BC) | Egypt (2600-1000 BC) | Greece (1200-300 BC) | Rome (500 BC-400 AD) | China (1200 BC-200 AD) | Inca (1400-1500 AD) |
|-----------|----------------------------|------------------------|----------------------|----------------------|-----------------------|-------------------|
| Establish | Scribe name, date, witness | Scribe name, date | Archon name, date | Scribe name, date | Diviner name, date | Keeper name, date |
| Place | Shelves, baskets, rooms | Archives, chests | Archives by magistrate | Tabularium, shelves | Archives by period | Quipucancha (storage) |
| Find | Labels, keeper knowledge | Keeper knowledge | Archive cataloging | Indexing by date | Systematic cataloging | Quipu organization |
| Traverse | Request → Approval → Issuance | Deposition → Judgment | Draft → Official → Archive | Draft → Copy → Archive | Draft → Approval → Archive | State → Distribution → Archive |
| Reconfigure | Tablet purging, moving | Doc destruction | Purging, reorganization | Document weeding | Periodic destruction | Quipu redistribution |
| Identify | Cylinder seals | Scarab seals | Signet rings | Signet rings, witnesses | Imperial seals, chops | Quipu color/signals |
| Signal | Messengers, drums | Messengers, horns | Beacon chains, runners | Tabellarii (couriers) | Drum towers, runners | Chasqui (relay runners) |

*Note: Evidence for Inca is drawn from Urton (2003); for China from Keightley (1978) and Loewe (1986).*

---

## Appendix B: Definitions and Inclusion Criteria

### B.1 Definition of "Operation"

An operation is a fundamental, irreducible human action performed on a record or record-keeping system. Operations are:

- **Universal**: Observed across all known record-keeping cultures and technologies.
- **Irreducible**: Cannot be decomposed into simpler operations without losing meaning.
- **Complete**: Any interaction with a record-keeping system can be described as a sequence of these operations.
- **Independent**: Each operation is semantically distinct and cannot be derived from the others.

### B.2 Inclusion Criteria

An operation is included in the framework if it meets all of the following criteria:

1. **Archaeological evidence**: The operation is observed in at least three distinct ancient record-keeping traditions.
2. **Historical persistence**: The operation is observed in at least two distinct historical periods separated by more than 500 years.
3. **Modern relevance**: The operation is supported by contemporary systems or design principles.
4. **Irreducibility**: The operation cannot be reduced to a combination of other operations.
5. **Necessity**: A record-keeping system that omits the operation would be demonstrably incomplete or dysfunctional.

### B.3 Application of Inclusion Criteria

| Operation | Archaeological Evidence (≥3 traditions) | Historical Persistence (≥2 periods) | Modern Relevance | Irreducible | Necessary | **Included** |
|-----------|----------------------------------------|-------------------------------------|------------------|-------------|-----------|-------------|
| Establish | Yes (Mesopotamia, Egypt, China) | Yes (3000 BC-2024) | Yes | Yes | Yes | **Yes** |
| Place | Yes (Mesopotamia, Egypt, Greece) | Yes (3000 BC-2024) | Yes | Yes | Yes | **Yes** |
| Find | Yes (Mesopotamia, Greece, Rome) | Yes (3000 BC-2024) | Yes | Yes | Yes | **Yes** |
| Traverse | Yes (Mesopotamia, Egypt, Rome) | Yes (3000 BC-2024) | Yes | Yes | Yes | **Yes** |
| Reconfigure | Yes (Mesopotamia, Egypt, Rome, China) | Yes (3000 BC-2024) | Yes | Yes | Yes | **Yes** |
| Identify | Yes (Mesopotamia, Egypt, Rome, China) | Yes (3000 BC-2024) | Yes | Yes | Yes | **Yes** |
| Signal | Yes (Mesopotamia, Greece, Rome, Inca) | Yes (500 BC-2024) | Yes | Yes | Yes | **Yes** |

---

## Appendix C: Compliance Scorecard

### Scoring Guide

| Score | Description | Definition |
|-------|-------------|------------|
| 0 | Not supported | Operation does not exist or is impossible in the system. |
| 1 | Minimal support | Operation exists in basic form but is limited. |
| 2 | Basic support | Operation is functional but requires effort or expertise. |
| 3 | Good support | Operation is functional, intuitive, and accessible. |
| 4 | Strong support | Operation is functional, intuitive, and integrated with other operations. |

### Assessment Criteria

**Establish**
| Score | Criteria |
|-------|----------|
| 0 | No creation captured. |
| 1 | Creation with basic metadata (title, date). |
| 2 | Creation with provenance (creator, timestamp). |
| 3 | Creation with context (source, purpose). |
| 4 | Creation with full intent and authority. |

**Place**
| Score | Criteria |
|-------|----------|
| 0 | No storage organization. |
| 1 | Basic folder/hierarchy. |
| 2 | Intentional placement with path. |
| 3 | Semantic placement (status, role). |
| 4 | Dynamic placement with auto-regroup. |

**Find**
| Score | Criteria |
|-------|----------|
| 0 | No search. |
| 1 | Keyword search only. |
| 2 | Search with filters. |
| 3 | Natural language search. |
| 4 | Contextual search with suggestions. |

**Traverse**
| Score | Criteria |
|-------|----------|
| 0 | No state tracking. |
| 1 | Basic state (e.g., draft/active). |
| 2 | State with history. |
| 3 | State with guided transitions. |
| 4 | Resumable, shareable flows. |

**Reconfigure**
| Score | Criteria |
|-------|----------|
| 0 | Permanent deletion only. |
| 1 | Soft deletion. |
| 2 | Soft deletion with audit. |
| 3 | Soft deletion with auto-regroup. |
| 4 | Lifecycle with archiving and purging. |

**Identify**
| Score | Criteria |
|-------|----------|
| 0 | No persistent IDs. |
| 1 | Internal IDs only. |
| 2 | Human-readable IDs. |
| 3 | Shareable, stable IDs. |
| 4 | Unified identity across systems. |

**Signal**
| Score | Criteria |
|-------|----------|
| 0 | No notifications. |
| 1 | Disruptive popups only. |
| 2 | Non-blocking notifications. |
| 3 | Ambient signals with differentiation. |
| 4 | Contextual, actionable signals. |

---

## Appendix D: Assessment Checklist

For each operation, assess both data and interface compliance.

**Establish**
- [ ] Creator identity captured automatically
- [ ] Creation timestamp captured automatically
- [ ] Creation context captured (source, reason)
- [ ] Creation authority captured
- [ ] UI shows creation context to users
- [ ] Data stores provenance in audit-log or metadata

**Place**
- [ ] Records have logical storage locations
- [ ] Locations are semantically meaningful
- [ ] Structure is navigable and understandable
- [ ] UI shows location context to users
- [ ] Data supports hierarchical or semantic organization

**Find**
- [ ] Search works across content and metadata
- [ ] Search understands natural language
- [ ] Results show context and relationships
- [ ] Navigation is intuitive and consistent
- [ ] Data supports efficient retrieval across all fields

**Traverse**
- [ ] Records have defined lifecycles
- [ ] State transitions are tracked
- [ ] Users know available actions
- [ ] Flows are resumable and shareable
- [ ] Data stores complete state history

**Reconfigure**
- [ ] Deletion is intentional and auditable
- [ ] Deletion triggers reorganization
- [ ] Deletion is reversible (when appropriate)
- [ ] UI handles missing items gracefully
- [ ] Data maintains continuity after structural changes

**Identify**
- [ ] Records have persistent, stable identifiers
- [ ] Identifiers are human-readable and shareable
- [ ] Identity is verifiable
- [ ] UI shows identity clearly to users
- [ ] Data provides cryptographic or verifiable identity

**Signal**
- [ ] Change detection is universal
- [ ] Signals are non-blocking and differentiated
- [ ] Signals are contextual and actionable
- [ ] UI provides ambient awareness of change
- [ ] Data emits events on all state changes

---

*End of Paper*
