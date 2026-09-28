# Phone -- Physical --- Investigation Summary

## Evidence Files Investigated

  -------------------------------------------------------------------------------------------------------------------
  File                           Analyst         Hash
  ------------------------------ --------------- --------------------------------------------------------------------
  `tracy-phone-2012-07-05.E01`   Khushi Matin    `7410EB756ED1AF9E12D8D8873F9FAA164076214A62A042D1B93B3D935E7333B7`
                                 Shaikh          

  -------------------------------------------------------------------------------------------------------------------

------------------------------------------------------------------------

## Summary Statistics

-   **Number of evidence files:** 1
-   **Total size:** 753 MB (78,97,26,745 bytes)
-   **Number of files/artefacts examined:** The generated Autopsy report
    contains multiple artefact result sets; exact unique-file count is
    not established from the report summary.
-   **Relevant artefacts identified:** 49 EXIF metadata records, 49 User
    Content Suspected records, 30 web-cookie records, and keyword-search
    hits including email-related remnants.
-   **Suspicious artefacts identified:** No artefact can be conclusively
    classified as malicious from the phone report alone. Email-related
    remnants in unallocated space and web/application artefacts are
    relevant for further correlation.

------------------------------------------------------------------------

## Files / Artefacts Investigated

### 1. Operating System Information

**Source:** `tracy-phone-2012-07-05.E01`

**Investigation:**\
Autopsy's Operating System Information result was examined. The report
identifies `Mac OS X` through the artefact:

`/img_tracy-phone-2012-07-05.E01/vol_vol4/System/Library/CoreServices/SystemVersion.plist`

**Finding:**\
An Apple operating-system artefact was identified within the physical
image. This establishes the presence of a Mac OS X system environment in
the examined image. The operating-system artefact should be considered
together with the other device and application artefacts before making a
definitive hardware-identification statement.

------------------------------------------------------------------------

### 2. EXIF Metadata and Recovered Images

**Source:** `tracy-phone-2012-07-05.E01`

**Investigation:**\
Autopsy's EXIF Metadata result identified **49 records**. Multiple JPEGs
were recovered from `$CarvedFiles` and contained embedded metadata. Many
records identify **Apple iPhone 3G** as the device model and include
capture timestamps. Several records also contain latitude, longitude
and, in some cases, altitude.

Examples include:

-   `2011-05-04 12:47:53 IST` --- Apple iPhone 3G ---
    `18.583833333333335, 73.82383333333334`
-   `2011-05-10 08:51:18 IST` --- Apple iPhone 3G ---
    `18.583833333333335, 73.82383333333334`
-   `2011-06-16 17:59:14 IST` --- Apple iPhone 3G ---
    `18.6075, 73.78533333333333`
-   `2012-06-23 14:15:32 IST` --- Apple iPhone 3G ---
    `38.89083333333333, -77.02333333333333`, with altitude recorded
-   `2012-06-23 14:24:25 IST` --- Apple iPhone 3G ---
    `38.89833333333333, -77.02`
-   `2012-06-23 14:44:22 IST` --- Apple iPhone 3G ---
    `38.89833333333333, -77.02`

An additional EXIF record identifies an `OLYMPUS OPTICAL CO.,LTD E-10`
image dated `2003-06-01 13:22:52 IST`.

**Finding:**\
The physical image contains recovered photographic artefacts retaining
EXIF information. The EXIF records provide timestamps and, for a subset
of photographs, geographic coordinates and device-model information.
Because many of these files are under `$CarvedFiles`, the photographs
appear to have been recovered through file carving rather than only from
normal allocated paths.

------------------------------------------------------------------------

### 3. User Content Suspected

**Source:** `tracy-phone-2012-07-05.E01`

**Investigation:**\
Autopsy's User Content Suspected result identified **49 JPEG records**,
each annotated with the comment:

`EXIF metadata data exists for this file.`

The records correspond to carved image files across the two identified
volumes.

**Finding:**\
The User Content Suspected result independently identifies a set of
recovered image artefacts containing EXIF metadata. This supports the
relevance of the recovered photographs for timeline and location
analysis, although the metadata alone does not establish the purpose of
the photographs or the identity of the person who operated the device.

------------------------------------------------------------------------

### 4. Web Categories and Browser/Application Cookies

**Source:** `tracy-phone-2012-07-05.E01`

**Investigation:**\
Autopsy identified web-category artefacts for:

-   `facebook.com` from an application cookie database
-   `live.com` from the phone's Safari cookie database

The Web Cookies result contains **30 cookie records**, including records
for `facebook.com`, `live.com`, `.examiner.com`, and `.article.wn.com`.

Examples:

-   `.facebook.com` --- `c_user` --- created `2012-06-14 00:46:36 IST`
-   `.facebook.com` --- `datr` --- created `2012-06-14 00:46:36 IST`
-   `.facebook.com` --- `xs` --- created `2012-06-14 00:46:37 IST`
-   `.live.com` --- `ANON` --- created `2012-07-05 21:57:12 IST`
-   `.live.com` --- `MUID` --- created `2012-07-05 21:57:36 IST`

**Finding:**\
Web-state artefacts associated with Facebook, Live.com and other domains
are present in the physical image. These records demonstrate the
presence of stored web/application state but do not, by themselves,
establish a specific user action, message, or malicious activity.

------------------------------------------------------------------------

### 5. Keyword Hits and Recovered Email-Related Data

**Source:** `tracy-phone-2012-07-05.E01`

**Investigation:**\
Autopsy's Keyword Hits result contains **28,516 result rows**. The
results include strings from allocated files, system artefacts, carved
files and unallocated space. Of particular relevance are email-like
strings recovered from unallocated data.

One unallocated object contains strings including:

-   `return-path: <...@amazonses.com>`
-   `message-id: <...@email.amazonses.com>`
-   `x-aws-outgoing`

The relevant source is:

`/img_tracy-phone-2012-07-05.E01/vol_vol5/$Unalloc/Unalloc_39438_725872640_1915871232`

Other keyword hits include email-address-like strings associated with
`packet-shaper.com` and other domains.

**Finding:**\
Email-related remnants are present in unallocated space within the
physical image. These artefacts indicate that remnants of
email/header-related data are recoverable, but the phone report alone
does not establish whether a complete message existed, whether it was
sent or received by the device user, or whether the remnants represent a
user-generated communication.

------------------------------------------------------------------------

## Consolidated Findings

1.  The physical image contains an Apple operating-system artefact
    identified by Autopsy as **Mac OS X** through `SystemVersion.plist`.
2.  Autopsy recovered **49 image artefacts with EXIF metadata**,
    including numerous records identifying an **Apple iPhone 3G** and,
    for a subset, GPS coordinates and capture timestamps.
3.  The recovered images include geographically tagged photographs from
    multiple dates and locations, making them useful for timeline and
    location correlation.
4.  Autopsy identified web/application cookie artefacts associated with
    **Facebook, Live.com, Examiner.com and article.wn.com**.
5.  Email-related strings, including Amazon SES-style header fields,
    were recovered from unallocated space. These require validation
    against the separate email evidence before any attribution or
    security conclusion is made.
6.  The available phone report does **not by itself establish a
    malicious action or a complete attack storyline**.

------------------------------------------------------------------------

## Correlations

-   **Timeline correlation:** EXIF timestamps can be compared with
    timestamps from the logical phone extraction, email evidence and
    network capture.
-   **Location correlation:** GPS coordinates embedded in recovered
    photographs can be compared with locations or network-related
    evidence from other sources.
-   **Domain correlation:** `facebook.com`, `live.com`, and other
    domains identified in phone cookies can be checked against
    URLs/domains found in the email, disk, and network evidence.
-   **Email correlation:** The Amazon SES-related remnants should be
    compared with the separately provided email sample for matching
    message identifiers, domains, timestamps or header fields.
-   **Physical vs logical comparison:** The physical image may contain
    carved images, unallocated remnants and historical artefacts that
    should be compared against the logical phone extraction.

At this stage, **insufficient evidence is available to establish a
definitive cross-source correlation** without the results from the other
evidence categories.

------------------------------------------------------------------------

## Unresolved Questions / Limitations

-   The SHA-256 hash of the original `.E01` must be inserted after
    verification against the original evidence file.
-   The total evidence-file size was not available in the generated HTML
    report and should be obtained from the original `.E01`.
-   EXIF metadata can be altered or preserved independently of the
    current physical location of the device; therefore, GPS metadata
    should be corroborated with other evidence.
-   A web cookie establishes stored web/application state, not
    necessarily a specific user action.
-   Keyword hits from system files and unallocated space require context
    and validation before attribution.
-   The recovered email-like strings do not establish sender, recipient,
    delivery status, or user interaction without additional evidence.
-   The physical-versus-logical phone comparison cannot be completed
    until the logical extraction is analysed.
-   No conclusion of malicious activity should be made solely from the
    Autopsy artefacts reported here.

------------------------------------------------------------------------

## Category Conclusion

The Autopsy examination of `tracy-phone-2012-07-05.E01` identified a
substantial set of recoverable phone artefacts, with the most
significant results being **EXIF-bearing recovered photographs,
web/application cookies, and email-related remnants in unallocated
space**. The EXIF records provide useful temporal and geographic
information, while the web and email artefacts provide identifiers that
can be tested against the other evidence categories.

The phone physical evidence therefore provides several strong
correlation points, but it does **not independently establish a
malicious incident or a complete user-action narrative**. Final
conclusions should be based on correlation with the logical phone
extraction, email, network, memory and disk evidence.
