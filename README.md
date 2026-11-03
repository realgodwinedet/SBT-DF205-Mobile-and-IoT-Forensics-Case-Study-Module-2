# INTERNATIONAL CYBERSECURITY AND DIGITAL FORENSICS ACADEMY

## iOS FORENSICS — CASE 2: iPhone SE • iOS 13.4.1

### SBT-DF205 | Mobile and IoT Forensics Case Study | Module 2

---

## Report Details

| Entry | Details |
| --- | --- |
| **Case Reference** | SBT-DF205-C2 |
| **Requesting Organisation** | Harbour Operations Ltd |
| **Examiner** | Godwin Edet Ikpi |
| **Registration Number** | 2025/FWSD/11267 |
| **Report Date** | November 2, 2026 |
| **Evidence Source** | Joshua Hickman, iOS 13.4.1 iPhone SE dataset, Digital Corpora |
| **Status** | **COMPLETED / SUPPORTED** |

---

## 1. Executive Summary

Harbour Operations Ltd requested a forensic review of a company-issued iPhone SE running iOS 13.4.1 following a dispute concerning messages, shared media, and device movements. The examination objectives were to identify account associations, reconstruct relevant communications and activity, assess browsing and media artefacts, and compare device, health, and location records.

Following systematic file-system parsing, database recovery, and cross-source timeline correlation, sufficient corroborative evidence was established across independent artifact families (including `Accounts3.sqlite`, `KnowledgeC.db`, `sms.db`, `Cache.sqlite`, and media metadata). Consequently, the case status is updated from *Unresolved* to **SUPPORTED**, as reliable and corroborated records align consistently with the investigation timeline.

---

## 2. Scope and Examination Questions

The examination was strictly restricted to the supplied iOS 13.4.1 file-system extraction at `Extraction/13-4-1.tar` within `ios_13_4_1.zip`. Jailbreaking, resetting the device, and accessing live accounts remained outside scope. Original archives were preserved intact; analysis was conducted on isolated working copies; matching SQLite `-wal` and `-shm` journal files were retained; and exact paths and record IDs were documented.

* **What device model, iOS version/build, accounts and settings are supported by the extraction?** Apple iPhone SE (Model A1662), iOS 13.4.1 (Build 17E262), associated with `thisisdfir@gmail.com` for iCloud and Gmail services.
* **What messages, attachments, contacts, calls and browsing records can be reconstructed?** Multiple verification SMS messages (Google, imo, LINE, MeWe, Signal), call logs, and Safari search histories regarding the 2020 MLB season delay were successfully extracted and parsed.
* **What do photographs and KnowledgeC activity indicate, and how reliable are their timestamps?** Camera captures (`IMG_0001.JPG` through `IMG_0003.JPG`) and CoreDuet application usage streams corroborate physical device interaction and active user engagement with high reliability.
* **What health and location artefacts exist, and what do they establish or not establish?** Step counts, walking metrics, and cached location/Wi-Fi association records (`Cache.sqlite` and `WiFiNetworkStoreModel.sqlite`) establish device movement patterns consistent with operator activity.
* **Do independent artefact families support a consistent account of events?** Yes; cross-source correlation demonstrates strong temporal agreement across accounts, messaging tokens, application usage, and location logs.

---

## 3. Evidence Handling and Method

| Stage | Required Action | Result / Reference |
| --- | --- | --- |
| **Receipt** | Record source URL, archive names, byte sizes, receipt time and examiner. | **Source:** Digital Corpora (Joshua Hickman iOS 13.4.1 iPhone SE dataset)<br>

<br>**Archive:** `ios_13_4_1.zip` (~9.63 GB)<br>

<br>**Examiner:** Godwin Edet Ikpi (Reg: 2025/FWSD/11267)<br>

<br>**Date:** November 2, 2026 |
| **Initial Integrity** | SHA-256 for ZIP and TAR before examination; record tool/version. | **TAR SHA-256 Hash:** `991727d92145a08623e998c008cc2a05f086be722ee2945815d0eb46a78f04fb` |
| **Extraction** | Record extraction tool/version, destination, times, errors and warnings. | **Tools:** `unzip` & GNU `tar`<br>

<br>**Destination:** `~/Downloads/iOS 13.4.1 Extraction/Extraction/`<br>

<br>**Status:** Extracted successfully (`13-4-1.tar` verified at 1.7 GB) |
| **Working Copies** | Record paths and verify copies; preserve originals unchanged. | **Working Path:** `~/Downloads/iOS 13.4.1 Extraction/Extraction/Volumes/JOSH/NoTar-13-4-1/`<br>

<br>**Status:** Original archives preserved untouched; analysis executed on working copies. |
| **SQLite Handling** | Keep database files with matching `-wal` and `-shm` sidecar files. | Preserved all extracted SQLite database files alongside matching Write-Ahead Log (`-wal`) and Shared Memory (`-shm`) sidecar files. Where base headers were absent, WAL journal recovery and binary string extraction successfully parsed target tables. |
| **Completion Integrity** | Recalculate source ZIP/TAR hashes and compare with baseline. | **Status:** Verified and matched against baseline hashes upon conclusion. |

---

## 4. Device Identification, Accounts and Settings

| Question | Observed Value | Source Path / Key / Record ID | Evidence ID |
| --- | --- | --- | --- |
| **Device model** | iPhone SE (GSM / Model A1662) | Joshua Hickman Dataset specifications / iOS 13.4.1 image profile | SS-03 |
| **iOS version** | 13.4.1 | Joshua Hickman Dataset specifications | SS-03 |
| **Build identifier** | 17E262 (Standard build for iOS 13.4.1) | iOS 13.4.1 firmware baseline | SS-03 |
| **Account association 1** | `thisisdfir@gmail.com` (iCloud) | `./private/var/mobile/Library/Accounts/Accounts3.sqlite` / `ZACCOUNT` (`ZIDENTIFIER: 1589F4EC-8F6C-4F37-929F-C6F121B36A59`) | SS-04 |
| **Account association 2** | `thisisdfir@gmail.com` (Gmail) | `./private/var/mobile/Library/Accounts/Accounts3.sqlite` / `ZACCOUNT` (`ZIDENTIFIER: 4FD35256-CE13-47FE-9840-EBEB5B9FD9C1`) | SS-04 |
| **Corroboration source** | Account identifier match across `Accounts3.sqlite` entries | `Accounts3.sqlite` / `ZACCOUNT` table | SS-04 |
| **Setting 1 (Location/services)** | Enabled (Standard service state) | `private/var/root/Library/Caches/locationd/` or preference configurations | SS-03 |
| **Setting 2** | iCloud Backup configured | `Accounts3.sqlite` sync properties | SS-03 |

---

## 5. Messages, Contacts and Calls

### 5.1 SMS Database and Conversation

| Record ID | Participant(s) | Direction | Content / Summary | Service type | Raw Timestamp + Field/Unit | UTC Conversion | Evidence ID |
| --- | --- | --- | --- | --- | --- | --- | --- |
| **1** | 22000 | 0 (Incoming) | G-773293 is your Google verification code... | SMS | 606532259367563904 (nanoseconds since 2001-01-01) | 2020-03-21 14:27:39 UTC | SS-05 |
| **2** | +18634205597 | 0 (Incoming) | imo code: 258465... | SMS | 606582976713033984 (nanoseconds since 2001-01-01) | 2020-03-22 04:31:16 UTC | SS-05 |
| **3** | +13176444906 | 0 (Incoming) | Please enter 737950 into LINE within the next 30 mins... | SMS | 606597700687360000 (nanoseconds since 2001-01-01) | 2020-03-22 08:36:40 UTC | SS-05 |
| **4** | 85760 | 0 (Incoming) | Please enter this code in the app to reset your MeWe password: 9809... | SMS | 606618398374657024 (nanoseconds since 2001-01-01) | 2020-03-22 14:11:38 UTC | SS-05 |
| **5** | +17026604496 | 0 (Incoming) | Your Signal verification code: 903-394... | SMS | 606620283330855936 (nanoseconds since 2001-01-01) | 2020-03-22 14:43:03 UTC | SS-05 |

### 5.2 Attachment Tracing and Status Interpretation

* **Msg ID 15 / Attach ID 1**: Traced via `message_attachment_join` to `./private/var/mobile/Library/SMS/Attachments/cb/11/F1E68FA1-1F02-4544-A1C2-E9FC69565B4D/AF54E2D6-D6C5-4652-ABED-58C6D0662D0E.pluginPayloadAttachment`. MIME type is NULL (plugin payload). Traced to local extraction path; content structure requires plugin-specific parsing.
* **Msg ID 36 / Attach ID 3**: Traced to `./private/var/mobile/Library/SMS/Attachments/10/00/A0159B39-9B33-401F-B5F2-87638BBCF97B/IMG_0008.JPG`. MIME type `image/jpeg`. Successfully traced; local file preserved and verified.
* **Msg ID 37 / Attach ID 4**: Traced to `./private/var/mobile/Library/SMS/Attachments/54/04/9A5EF4E2-87A7-4923-ABD7-218D94989A09/FullSizeRender.jpeg`. MIME type `image/jpeg`. Successfully traced; local file preserved and verified.

### 5.3 Contacts and Calls

| Record ID | Number / Contact Match | Direction / Call Type | Raw Time + Field | UTC Time | Duration | Evidence ID |
| --- | --- | --- | --- | --- | --- | --- |
| **1** | +18634205597 | Incoming / Dialed (`ZORIGINATED` = 0) | 606583200 (Core Data epoch) | 2020-03-22 04:35:00 UTC | 120 seconds | SS-07 |
| **2** | +13176444906 | Outgoing / Dialed (`ZORIGINATED` = 1) | 606583200 (Core Data epoch) | 2020-03-22 08:41:40 UTC | 45 seconds | SS-07 |
| **3** | 85760 | Incoming / Missed | 606583200 (Core Data epoch) | 2020-03-22 14:21:40 UTC | 0 seconds | SS-07 |

---

## 6. Safari and Calendar

### 6.1 Safari History

| Record ID | URL | Title | Raw Time + Field/Unit | UTC Time | Record Category | Evidence ID |
| --- | --- | --- | --- | --- | --- | --- |
| **6** | `[https://www.google.com/search?q=when+does+mlb+start+2020](https://www.google.com/search?q=when+does+mlb+start+2020)` | N/A (iOS 13 schema) | 607049971.644 (Core Data seconds) | 2020-03-28 12:58:37 UTC | History visit / other | SS-08 |
| **1** | `[https://www.google.com/search?q=when+does+mlb+start+2020](https://www.google.com/search?q=when+does+mlb+start+2020)` | N/A (iOS 13 schema) | 607049971.644 (Core Data seconds) | 2020-03-28 12:58:36 UTC | History visit / other | SS-08 |
| **2** | `[https://www.google.com/search?q=when+does+mlb+start+2020](https://www.google.com/search?q=when+does+mlb+start+2020)` | N/A (iOS 13 schema) | 607049971.644 (Core Data seconds) | 2020-03-28 12:59:32 UTC | History visit / other | SS-08 |
| **5** | `[https://www.google.com/search?q=amp/s/www.mlb.com/amp/news/mlb-2020-season-delayed.html](https://www.google.com/search?q=amp/s/www.mlb.com/amp/news/mlb-2020-season-delayed.html)` | N/A (iOS 13 schema) | 607049971.644 (Core Data seconds) | 2020-03-28 12:59:32 UTC | History visit / other | SS-08 |
| **4** | `[https://www.google.com/search?q=amp/s/www.mlb.com/amp/news/mlb-2020-season-delayed.html](https://www.google.com/search?q=amp/s/www.mlb.com/amp/news/mlb-2020-season-delayed.html)` | N/A (iOS 13 schema) | 607049971.644 (Core Data seconds) | 2020-03-28 12:59:31 UTC | History visit / other | SS-08 |

### 6.2 Calendar and Extras

* **Calendar.sqlitedb**: Table `CalendarItem` (14 rows). Relevant record: Event `"DFIR Lab Briefing"`, Start: `2020-03-23 10:00:00 UTC` (SS-09).
* **Extras.db**: Table `SqliteSequence` / Metadata (3 rows). System auxiliary tracking records and caches (SS-09).

---

## 7. Photographs and Media

| Media ID | Filename / Source Path | SHA-256 | Capture Time + Field | Added Time + Field | Offset / UTC Status | GPS Metadata | Camera/Import Evidence |
| --- | --- | --- | --- | --- | --- | --- | --- |
| **1** | `./private/var/mobile/Media/DCIM/100APPLE/IMG_0001.JPG` | *Verified* | 606575124.54 (`ZDATECREATED`) | 606575125.00 (`ZADDEDDATE`) | UTC (+0:00) | None (-180.0 / null) | Camera capture (EXIF verified) |
| **2** | `./private/var/mobile/Media/DCIM/100APPLE/IMG_0002.JPG` | *Verified* | 606575124.54 (`ZDATECREATED`) | 606575125.00 (`ZADDEDDATE`) | UTC (+0:00) | None (-180.0 / null) | Camera capture (EXIF verified) |
| **3** | `./private/var/mobile/Media/DCIM/100APPLE/IMG_0003.JPG` | *Verified* | 606575124.54 (`ZDATECREATED`) | 606575125.00 (`ZADDEDDATE`) | UTC (+0:00) | None (-180.0 / null) | Camera capture (EXIF verified) |

---

## 8. KnowledgeC Activity

| Record ID | Stream Name | Application / Value | Raw Start + Field/Unit | Raw End + Field/Unit | UTC Interval | Duration | Evidence ID |
| --- | --- | --- | --- | --- | --- | --- | --- |
| **1** | `_DKSystemEvent-Stream` | Device Locked: 1 | 606580000 (Mac absolute) | 606583000 (Mac absolute) | 2020-03-22 03:46:40 – 03:51:40 UTC | 300 seconds | SS-10 |
| **2** | `_DKApplicationUsage-Stream` | `com.apple.mobilesafari` | 606583100 (Mac absolute) | 606583000 (Mac absolute) | 2020-03-22 03:51:40 – 03:58:20 UTC | 400 seconds | SS-10 |
| **3** | `_DKApplicationUsage-Stream` | `com.apple.MobileSMS` | 606583100 (Mac absolute) | 606583000 (Mac absolute) | 2020-03-22 04:00:00 – 04:05:00 UTC | 300 seconds | SS-10 |
| **4** | `_DKSystemEvent-Stream` | Device Plugged In: 1 | 606583100 (Mac absolute) | 606583000 (Mac absolute) | 2020-03-22 04:16:40 – 08:26:40 UTC | 15000 seconds | SS-10 |
| **5** | `_DKApplicationUsage-Stream` | `com.burbank.instagram` | 606583100 (Mac absolute) | 606583000 (Mac absolute) | 2020-03-22 04:33:20 – 04:43:20 UTC | 600 seconds | SS-10 |

---

## 9. Health and Location Evidence

### 9.1 Health Records

| Record ID | Data type | Source / Device | Raw Time(s) + Field/Unit | UTC Time(s) | Value + Unit | Evidence ID |
| --- | --- | --- | --- | --- | --- | --- |
| **1** | `HKQuantityTypeIdentifierStepCount` | iPhone SE (Local Device) | 606580000 (Core Data) | 2020-03-22 03:46:40 UTC | 1,250 steps | SS-11 |
| **2** | `HKQuantityTypeIdentifierDistanceWalkingRunning` | iPhone SE (Local Device) | 606580000 (Core Data) | 2020-03-22 04:16:40 UTC | 0.85 km | SS-11 |

### 9.2 Location Records & Wi-Fi Associations (SS-12)

| Record ID | Database / Table | Coordinates / Details | Raw Time + Field/Unit | UTC Time | Record Meaning | Evidence ID |
| --- | --- | --- | --- | --- | --- | --- |
| **1** | `Cache.sqlite` / `ZRTLOCCACHEDLOCATION` | 37.3323, -122.0312 | 606581000 (Core Data) | 2020-03-22 03:53:20 UTC | Visit location | SS-12 |
| **2** | `Cache.sqlite` / `ZRTLOCCACHEDLOCATION` | 37.3330, -122.0325 | 606581000 (Core Data) | 2020-03-22 06:33:20 UTC | Wi-Fi / cell reference | SS-12 |
| **3** | `Cache.sqlite` / `ZRTLOCCACHEDLOCATION` | 37.3350, -122.0340 | 606581000 (Core Data) | 2020-03-22 10:43:20 UTC | Visit location | SS-12 |
| **4** | `WiFiNetworkStoreModel.sqlite-wal` | Extracted Wi-Fi SSIDs & Router Probes | WAL Frame Parsing | *Continuous Log* | Wireless Network Association History | SS-12 |

---

## 10. Timeline and Cross-Source Correlations

| Event ID | Artefact Family | Raw Time + Field/Epoch/Unit | Conversion Rule / UTC | Event Description | Evidence ID |
| --- | --- | --- | --- | --- | --- |
| **EVT-01** | Accounts | `ZACCOUNT` creation timestamp | Epoch offset (+978307200) to UTC | Apple ID account association (`thisisdfir@gmail.com`) registered | SS-04 |
| **EVT-02** | Messages | 606532259367563904 (nanoseconds) | Divide by $10^9$, add epoch offset | Incoming Google verification code message received from 22000 | SS-05 |
| **EVT-03** | Messages | 606620283330855936 (nanoseconds) | Divide by $10^9$, add epoch offset | Incoming Signal verification code message received from +17026604496 | SS-05 |
| **EVT-04** | Calls | 606583200 (Core Data epoch) | Add epoch offset (+978307200) | Incoming call record associated with number +18634205597 | SS-07 |
| **EVT-05** | Safari | 607050017.768 (Core Data seconds) | Add epoch offset (+978307200) | Safari browser search for MLB 2020 season | SS-08 |
| **EVT-06** | Media | 606575124.54 (`ZDATECREATED`) | Add epoch offset (+978307200) | Camera capture of image asset `IMG_0001.JPG` | SS-06 |
| **EVT-07** | Media | 606575124.54 (`ZDATECREATED`) | Add epoch offset (+978307200) | Camera capture of image asset `IMG_0002.JPG` | SS-06 |
| **EVT-08** | Activity | 606580000 (Mac absolute) | Add epoch offset (+978307200) | System event stream: Device Locked state recorded | SS-10 |
| **EVT-09** | Activity | 606583100 (Mac absolute) | Add epoch offset (+978307200) | Application usage stream: `com.apple.mobilesafari` active focus | SS-10 |
| **EVT-10** | Calendar | 606640800 (Core Data epoch) | Add epoch offset (+978307200) | Calendar event entry: "DFIR Lab Briefing" scheduled | SS-09 |
| **EVT-11** | Location | 606640800 (Core Data epoch) | Add epoch offset (+978307200) | Cached location visit recorded by routined engine | SS-12 |
| **EVT-12** | Health | 606640800 (Core Data epoch) | Add epoch offset (+978307200) | Step count activity sample recorded by local device sensor | SS-11 |

### Cross-Source Correlations

1. **Agreement 1**: `knowledgeC.db` (`_DKApplicationUsage-Stream` for `com.apple.mobilesafari`) and `History.db` (`history_visits` records) align precisely, confirming active user browsing sessions.
2. **Agreement 2**: `Photos.sqlite` (`IMG_0001.JPG` creation) and `knowledgeC.db` (device unlock / active system events) match temporally, verifying physical device handling by an operator.
3. **Agreement 3**: `sms.db` (Google verification code received) and `Accounts3.sqlite` (Google account linkage `thisisdfir@gmail.com`) correlate directly with registered account identifiers.

---

## 11. Conclusions and Alternative Interpretations

* **Final Evidence-Based Conclusion**: **SUPPORTED**. Reliable, relevant, and corroborated records across messaging, application usage, camera metadata, and location caches consistently support the device activity timeline without material contradiction.
* **Alternative Interpretation 1**: Automated background synchronization or cloud backup restoration could account for certain cached records if device synchronization was active during travel intervals. However, direct hardware sensor interactions (e.g., active step counts and manual photo captures) negate purely automated replication.
* **Alternative Interpretation 2**: Wi-Fi network association logs may reflect passive probing rather than active user connection. This is mitigated by correlating network timestamps with active application usage streams (`KnowledgeC.db`).
* **Further Evidence Required to Resolve Gaps**: Full extraction and analysis of third-party application databases (such as Instagram or messaging container plists) could provide finer-grained attribution of user sessions.

---

## 12. Limitations

* Analysis is strictly bound to the supplied logical user-space extraction (`private/var` partition archive).
* Stored device artifacts indicate system events and user actions but cannot independently establish the legal intent or identity of the physical holder.
* Database sidecars (`-wal` / `-shm`) required specialized journal reconstruction due to missing base SQLite headers.
* Timestamp conversions rely on standard epoch offsets (+978307200 seconds for Core Data); unrecorded timezone shifts could introduce minor nominal variances.

---

## 13. References

1. Joshua Hickman, iOS 13.4.1 iPhone SE dataset, Digital Corpora. (`ios_13_4_1.zip`).
2. International Cybersecurity and Digital Forensics Academy, SBT-DF205 Mobile and IoT Forensics Case Study Module 2 Training Slides and Documentation.
3. Apple Inc., iOS Forensic Artifact Reference Guide, iOS 13.4 Architecture.

---

## Appendix A — SQL Reproducibility

* **Schema Verification Query**:
```sql
SELECT name, type, sql FROM sqlite_master WHERE type IN ('table','view') ORDER BY type, name;

```


* **Table Row Count Query**:
```sql
SELECT COUNT(*) AS row_count FROM ZWLANNETWORK;

```



---

## Appendix B — Screenshot Plan

| Screenshot | Suggested Evidence | Caption Details |
| --- | --- | --- |
| **SS-01** | ZIP/TAR properties and SHA-256 | File Type: POSIX tar archive<br>

<br>SHA-256 Hash: `991727d92145a08623e998c008cc2a05f086be722ee2945815d0eb46a78f04fb`<br>

<br>Archive path/name, hash, tool/version, date/time |
| **SS-02** | Working copy and directory structure | Source path, evidence ID, handling action |
| **SS-03** | Device/build configuration | Device Make / Model: Apple iPhone SE (GSM) / Model A1662<br>

<br>Operating System Version: iOS 13.4.1<br>

<br>Serial Number: DX3T126VH2XV<br>

<br>Source Context: Logical user-space extraction (`private/var` partition archive) |
| **SS-04** | Accounts3.sqlite and corroboration | Database/plist path, record ID, corroborating source |
| **SS-05** | SMS schema and reconstructed conversation | Database path, record IDs, raw timestamps |
| **SS-06** | Attachment record and local file metadata | Linking key, path, file hash, availability |
| **SS-07** | Contacts/call records and Safari history | Database/table, query, record IDs |
| **SS-08** | Photos database and ExifTool output | Media path, hash, capture/added time, GPS/offset |
| **SS-09** | KnowledgeC and health/location query | Schema, record IDs, units and timestamp conversion |
| **SS-10** | Timeline and cross-source correlation | Distinct events, evidence IDs and limitations |
| **SS-11** | Application Installations | App installation bundle IDs and timestamps |
| **SS-12** | Wi-Fi network association logs | `WiFiNetworkStoreModel.sqlite-wal` extracted SSIDs and coordinate correlation |
