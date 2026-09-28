# Phone Content -- Logical Extract: Analysis

## 1. Scope

This examination covers the logical phone extraction contained in:

`D:\DF2`

The original logical evidence archive was:

`D:\tracy-phone-2012-07-05.tar`

SHA-256:

`aa8ac5304f5f12cf1eecb8462bd7aac5225f05ac42115bfebf5ad56befe86005`

`D:\DF2` was treated as the original extracted evidence source. Database
copies in `D:\DF\Phone_Logical_Analysis\Database_Analysis` were used as
working copies for database examination.

## 2. Examination approach

The examination included:

-   filesystem and directory review;
-   SQLite database examination using DB Browser for SQLite;
-   SMS/message analysis;
-   call-history analysis;
-   contacts/address-book review;
-   Notes, Mail, Calendar, Voicemail, Maps and media review;
-   Safari review;
-   application-data review;
-   system/log artifact review;
-   strings examination;
-   filesystem metadata/timestamp review;
-   cross-artifact correlation.

The analysis distinguishes direct observations from interpretations and
correlations. System timestamps are not treated as proof of a user's
intent or manual action unless the artifact itself supports that
conclusion.

## 3. SMS / Messages

### Observation

The `sms.db` database contained 8 records in the `message` table.

The records involved these telephone numbers:

-   `+15713083236`
-   `+17038296071`
-   `+12027252124`

The message contents included discussions concerning weekend plans,
going out for pizza, school arrangements, affordability of Prufrock, and
meeting at Bubba's Grill.

The `group_member` table associated the three principal telephone
numbers with message groups. `msg_pieces` contained no rows.

Raw message timestamps were stored as integer date values. The examined
records correspond to dates in June and July 2012, including July 5,
2012.

### Interpretation

The structured `message` table is the primary source for message count
and message-record interpretation. The strings extraction from `sms.db`
corroborated the presence of message text, phone numbers, SQLite schema
information, and database metadata.

### Finding

The logical extraction contains eight structured SMS message records
involving three principal telephone numbers.

### Caution

Strings output should not be used to count messages independently
because the same text may appear more than once in raw database storage.

## 4. Call History

### Observation

`call_history.db` contained four records in the `call` table.

The recorded addresses were:

-   `6508870260`
-   `7038296191`
-   `+15713083236`
-   `5712458517`

The recorded durations were 20 seconds, 56 seconds, 0 seconds, and 0
seconds respectively.

The `data` table contained four rows, and all recorded byte counters
were zero.

### Interpretation

The call database records four calls. The zero values in the `data`
table indicate that no byte-transfer statistics were recorded in those
rows.

### Finding

Call-history evidence is present and provides an independent
communication artifact. `+15713083236` is recorded in both the
call-history database and the SMS database.

## 5. Contacts / Address Book

### Observation

The Address Book database contained contact records including names such
as Pat, Tracy, Apple Inc., Terry and Carry.

### Interpretation

The Address Book provides contact information stored on the device.

### Finding

Address-book data was successfully identified and examined. No identity
assignment to the SMS telephone numbers is made unless directly
supported by the examined contact fields.

## 6. Notes, Mail, Calendar, Voicemail, Maps and Media

### Observation

These application/content areas were examined during the logical
extraction review.

-   Notes: examined.
-   Mail: examined.
-   Calendar: examined.
-   Voicemail: blank.
-   Maps: empty.
-   Photos/media: examined.

### Finding

No additional finding from the empty Voicemail or Maps areas was
identified. Other reviewed areas were recorded as examined without
making unsupported conclusions about user behavior.

## 7. Safari

### Observation

The Safari folder reviewed in the logical extraction was empty.

### Finding

No Safari browser-history artifact was identified in the examined Safari
folder.

## 8. Application Data

Several application directories were examined.

### FlashLight

The FlashLight application was identified as
`com.ihandysoft.flashlight.free`.

The application contained a `googleanalytics.sql` database with tables
including `events`, `hits`, `session`, `referrer`, and
`custom_var_cache`.

Observed analytics values included application/user categories such as
`OldUser`, `NewUser`, and `NormalUser`, together with application event
information.

The FlashLight preferences also contained application
configuration/state keys and version information.

### Facebook

The Facebook application contained:

-   `Cookies.binarycookies`;
-   WebKit local-storage databases;
-   an application preferences plist.

The preferences contained Facebook application state/navigation fields,
including account/session-related fields and a Facebook user identifier.
Authentication/session credential material was present in the artifact,
but credential values were not reproduced in this report.

### Instagram

The Instagram application was identified as version 2.4.0 from its
preferences.

Its cache contained Instagram-hosted JPG files. These establish cached
application content but do not by themselves establish who created or
viewed the underlying media.

### Great Solitaire iPhone

The application contained preference data and several `.gg` document
files, including `achievement.gg`, `goodsdatabuy.gg`, `mymoney.gg`,
`nowapplygoods.gg`, and `writereview.gg`.

`achievement.gg` was identified as a binary/serialized application file
and was not further analyzed.

### Finding

Application artifacts demonstrate stored application state,
configuration, cache, analytics and document data within the logical
extraction. Their presence alone should not be treated as proof of a
particular user action.

## 9. System and Log Artifacts

### `private\var\log`

Observed:

-   `kernel.log` --- 0 KB / empty.
-   `asl\SweepStore` --- 1 KB and approximately 8 bytes of content.
-   `ppp` --- empty.
-   `sa` --- empty.

### `private\var\logs`

#### `keybagd.log`

The log contains repeated entries stating:

`System Keybag loaded`

Events were recorded from June 6 through July 5, 2012. Several entries
occur on July 5, including approximately 12:18:46, 14:27:40, 14:30:06
and 14:40:12.

These are system-level keybag events. They are not, by themselves, proof
of a manual unlock or a particular user action.

#### `lockdownd.log`

The log contains device startup and SIM/activation processing.

On July 5, 2012, startup sequences occurred around:

-   12:18;
-   14:27;
-   14:30;
-   14:40.

The log also records the device hostname as "Tracy Sumtwelve's iPhone"
during one of these sequences.

The log records SIM-status and activation-state processing. These
entries are interpreted as device/service events rather than evidence of
user intent.

#### `AppleSupport\general.log`

The file identifies:

-   OS: iPhone OS 4.2.1 (8C148)
-   Model: iPhone1,2
-   Created: June 6, 2012 at 12:03:28, UTC−0700

It contains dated diagnostic/system records extending through July 5,
2012.

The report intentionally omits the device serial number.

#### CrashReporter

The `Baseband` and `Panics` directories were empty.

### Finding

The substantive system-log artifacts provide a useful device-level
timeline. Multiple independent logs show system activity on the same
dates, particularly July 5, 2012. They do not independently establish
the reason for each event or the user's actions.

## 10. Strings Analysis

A strings extraction from `sms.db` recovered:

-   SQLite database schema;
-   triggers and indexes;
-   telephone numbers;
-   message text;
-   group and database metadata.

The strings output corroborated the structured SQLite examination.

Because raw SQLite strings may occur multiple times in different
database structures or pages, strings output was not used as an
independent message count.

## 11. File Metadata

### Original evidence `sms.db`

Location:

`D:\DF2\private\var\mobile\Library\SMS\sms.db`

Observed filesystem metadata:

-   Size: 48.0 KB (49,152 bytes)
-   Windows Created: September 26, 2026 11:02:00 PM
-   Windows Modified: July 6, 2012 12:10:44 AM
-   Windows Accessed: September 26, 2026 11:02:00 PM

The 2026 Created/Accessed timestamps are treated as extraction/computer
timestamps and are not interpreted as phone activity.

The July 6, 2012 Modified timestamp is recorded as filesystem metadata.
It is not automatically interpreted as the creation or sending time of
an SMS.

### Extracted `private` directory

Observed:

-   Size: 95.3 MB (99,958,697 bytes)
-   Size on disk: 101 MB (106,192,896 bytes)
-   Contents: 3,785 files and 362 folders
-   Windows Created: September 26, 2026 11:01:54 PM

Again, the 2026 timestamp reflects the extracted working environment
rather than the original phone activity.

## 12. Cross-Correlation

### Direct communication correlation

`+15713083236` appears in both:

-   the SMS database; and
-   the call-history database.

This is a direct cross-database correlation of the same telephone
number.

### System timeline correlation

On July 5, 2012, several system artifacts record activity in the same
general period:

-   `keybagd.log` records keybag loads;
-   `lockdownd.log` records startup/SIM/activation processing;
-   `AppleSupport\general.log` records a diagnostic event;
-   SMS records occur later that day.

These artifacts establish temporal correlation but do not establish
causation or user intent.

### Database timestamp correlation

The original `sms.db` has a July 6, 2012 filesystem modification
timestamp, while the latest identified SMS records are dated July 5,
2012. This is a timeline relationship, but the filesystem timestamp
cannot be assumed to represent the time of a specific message operation.

## 13. Overall Findings

1.  The logical extraction contains structured SMS, call-history,
    address-book, calendar, notes, mail, application and system-log
    artifacts.
2.  Eight structured SMS records were identified.
3.  Four call-history records were identified.
4.  `+15713083236` is independently recorded in both SMS and
    call-history evidence.
5.  System logs provide a device-level timeline spanning June and July
    2012, including several July 5 events.
6.  Application artifacts from Facebook, Instagram, FlashLight and Great
    Solitaire were identified and examined.
7.  Safari was empty in the examined folder, and no voicemail or Maps
    data was identified in the examined locations.
8.  Strings analysis corroborated the structured SQLite findings.
9.  Filesystem metadata was documented while distinguishing
    extraction/computer timestamps from artifact-internal timestamps.
10. No finding in this examination should be interpreted as proof of
    user intent unless directly supported by the artifact.

## 14. Evidence Handling Notes

The original extracted evidence at `D:\DF2` was treated as read-only.
Working database copies were maintained separately under:

`D:\DF\Phone_Logical_Analysis\Database_Analysis`

The original archive SHA-256 recorded for integrity verification is:

`aa8ac5304f5f12cf1eecb8462bd7aac5225f05ac42115bfebf5ad56befe86005`
