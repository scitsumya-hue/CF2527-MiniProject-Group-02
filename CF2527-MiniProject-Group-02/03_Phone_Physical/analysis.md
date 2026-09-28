# Artefact Analysis

## 1. Evidence Information

  Field               Details
  ------------------- --------------------------------------------------------------------
  Evidence Category   Phone -- Physical
  Evidence File       `tracy-phone-2012-07-05.E01`
  Analyst             Khushi Matin Shaikh
  Hash Algorithm      SHA-256
  Hash                `7410EB756ED1AF9E12D8D8873F9FAA164076214A62A042D1B93B3D935E7333B7`
  File Size           `753 MB (78,97,26,745 bytes)`
  Tool(s) Used        Autopsy 4.23.1

------------------------------------------------------------------------

## 2. Objective

The objective of this investigation was to examine the physical phone
image `tracy-phone-2012-07-05.E01` using Autopsy and identify relevant
forensic artefacts, including operating-system information, recovered
images and metadata, web/application artefacts, keyword hits, and data
recovered from carved and unallocated areas.

The analysis follows the required forensic distinction between
**Observation, Interpretation, Finding and Correlation**. Tool output is
treated as evidence requiring interpretation rather than as a
conclusion.

------------------------------------------------------------------------

## 3. Investigation Performed

### Tool / Technique

Autopsy 4.23.1 was used to process the physical phone image. The
generated case report shows that the data source ingest completed
successfully. Relevant enabled modules included Recent Activity, Hash
Lookup, File Type Identification, Extension Mismatch Detector, Embedded
File Extractor, Picture Analyzer, Keyword Search, Email Parser,
Encryption Detection, Interesting Files Identifier, Central Repository,
PhotoRec Carver, Data Source Integrity, iOS Analyzer (iLEAPP), Android
Analyzer, YARA Analyzer and GPX Parser.

The principal artefact categories examined for this report were:

-   Operating System Information
-   EXIF Metadata
-   User Content Suspected
-   Web Categories
-   Web Cookies
-   Keyword Hits
-   General metadata and carved/unallocated artefacts

### Artefact Examined

The physical image was identified in the Autopsy case as:

`tracy-phone-2012-07-05.E01`

Autopsy's report identifies one data source and records the ingest
status as **COMPLETED**.

### Observation

The case report identifies the evidence image as
`tracy-phone-2012-07-05.E01`, with timezone `Asia/Calcutta`. The
Operating System Information result identifies `Mac OS X` from:

`/img_tracy-phone-2012-07-05.E01/vol_vol4/System/Library/CoreServices/SystemVersion.plist`

The EXIF Metadata result contains 49 records. Multiple recovered JPEGs
identify `Apple` as manufacturer and `iPhone 3G` as device model.
Several records contain latitude, longitude and altitude.

The User Content Suspected result contains 49 JPEG records annotated
with `EXIF metadata data exists for this file.`

Web Categories identifies `facebook.com` and `live.com`. Web Cookies
contains 30 records involving, among others, `.facebook.com`,
`.live.com`, `.examiner.com`, and `.article.wn.com`.

Keyword Hits contains 28,516 result rows and includes email-related
strings recovered from unallocated space, including Amazon SES-style
`return-path`, `message-id`, and `x-aws-outgoing` fields.

### Interpretation

The recovered EXIF data indicates that a significant set of image
artefacts retained device and, for some images, geographic and temporal
metadata. Because many of these images occur under `$CarvedFiles`, the
physical image has yielded data that was recoverable through carving
rather than only through ordinary allocated-file examination.

The web-cookie artefacts demonstrate stored web/application state
associated with specific domains. They should not be interpreted
automatically as proof of a particular user action.

The email-related strings in unallocated space indicate recoverable
remnants of email/header-like data. Their location in unallocated space
means that additional context is necessary before attributing the data
to a complete message or a specific user action.

### Finding

The physical phone image contains multiple categories of potentially
valuable forensic artefacts: recoverable photographs with EXIF metadata,
web/application cookie records, and email-related remnants in
unallocated space. These artefacts provide identifiers---timestamps,
coordinates, domains and email/header strings---that can be used for
cross-source correlation.

------------------------------------------------------------------------

## 4. Important Artefacts

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  Artefact         Location / Identifier                                                                                        Observation                                Interpretation              Significance
  ---------------- ------------------------------------------------------------------------------------------------------------ ------------------------------------------ --------------------------- ---------------------
  Operating System `/vol_vol4/System/Library/CoreServices/SystemVersion.plist`                                                  Autopsy identifies Mac OS X                Apple OS artefact is        Establishes OS
                                                                                                                                                                           present in the image        context

  EXIF image       `/vol_vol5/$CarvedFiles/3/f0174160.jpg`                                                                      Apple iPhone 3G;                           Recovered image retains     Useful for
  `f0174160.jpg`                                                                                                                `2011-05-04 12:47:53 IST`; GPS             device/time/location        timeline/location
                                                                                                                                `18.583833333333335, 73.82383333333334`    metadata                    correlation

  EXIF image       `/vol_vol5/$CarvedFiles/5/f0417360.jpg`                                                                      Apple iPhone 3G;                           Recovered image retains     Potential
  `f0417360.jpg`                                                                                                                `2012-06-23 14:15:32 IST`; GPS             geographic and temporal     location/timeline
                                                                                                                                `38.89083333333333, -77.02333333333333`;   metadata                    anchor
                                                                                                                                altitude recorded                                                      

  EXIF image       `/vol_vol5/$CarvedFiles/5/f0422168.jpg`                                                                      Apple iPhone 3G;                           Multiple photographs were   Supports a sequence
  `f0422168.jpg`                                                                                                                `2012-06-23 14:24:25 IST`; GPS             captured with closely       of geotagged
                                                                                                                                `38.89833333333333, -77.02`                related coordinates and     photographic activity
                                                                                                                                                                           times                       

  Facebook cookie  `/vol_vol5/mobile/Applications/20EE8FD8-EA71-4C81-AE9F-F46BD4255F18/Library/Cookies/Cookies.binarycookies`   `.facebook.com` cookies including          Stored application/web      Potential
                                                                                                                                `c_user`, `datr`, `lu`, `m_user`, `xs`     state associated with       application/account
                                                                                                                                                                           Facebook                    correlation

  Live.com cookies `/vol_vol5/mobile/Library/Cookies/Cookies.binarycookies`                                                     `.live.com` cookies including `ANON`,      Stored web state associated Potential account/web
                                                                                                                                `LD`, `MUID`, `MSPAuth`, `RPSTAuth`,       with Live.com               activity correlation
                                                                                                                                `WLSSC`                                                                

  Examiner.com     `/vol_vol5/mobile/Library/Cookies/Cookies.binarycookies`                                                     Cookies created on `2012-07-05`            Stored web state for the    Potential
  cookies                                                                                                                                                                  domain                      browsing/activity
                                                                                                                                                                                                       timeline evidence

  Article.wn.com   `/vol_vol5/mobile/Library/Cookies/Cookies.binarycookies`                                                     Cookies created `2012-06-13 20:53:53 IST`; Stored web state with       Potential
  cookies                                                                                                                       referral indicates `nationalgallery.com`   referral information        browsing/referral
                                                                                                                                                                                                       correlation

  Amazon SES email `/vol_vol5/$Unalloc/Unalloc_39438_725872640_1915871232`                                                      `return-path`, `message-id`, and           Email/header-related data   Requires correlation
  remnants                                                                                                                      `x-aws-outgoing` strings referencing       survives in unallocated     with supplied email
                                                                                                                                Amazon SES                                 space                       evidence

  Keyword email    `/vol_vol4/$Unalloc/Unalloc_39436_17334272_713052160` and other sources                                      Multiple email-address-like strings        Keyword search recovered    Useful only after
  strings                                                                                                                                                                  email-related content from  source/context
                                                                                                                                                                           unallocated/system/carved   validation
                                                                                                                                                                           data                        
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

------------------------------------------------------------------------

## 5. Evidence Supporting the Finding

The principal evidence supporting the findings consists of Autopsy's
generated artefact reports:

1.  **Operating System Information** --- identifies `Mac OS X` from
    `SystemVersion.plist`.
2.  **EXIF Metadata** --- provides 49 records containing timestamps,
    device information and, for a subset, geographic coordinates and
    altitude.
3.  **User Content Suspected** --- identifies 49 recovered JPEGs with
    EXIF metadata.
4.  **Web Categories** --- identifies `facebook.com` and `live.com`.
5.  **Web Cookies** --- provides 30 cookie records with timestamps,
    cookie names, domains and source paths.
6.  **Keyword Hits** --- provides 28,516 result rows, including
    email-related remnants in unallocated space.
7.  **Metadata** --- provides additional file metadata for recovered and
    allocated files, including media and application artefacts.

The strongest individual artefacts for further investigation are the
geotagged photographs and the email-related remnants in unallocated
space because they provide specific timestamps, locations or identifiers
that can be compared with other evidence.

------------------------------------------------------------------------

## 6. Correlation With Other Evidence

  -----------------------------------------------------------------------
  Evidence Source         Related Artefact        Relationship
  ----------------------- ----------------------- -----------------------
  Phone -- Logical        Matching image          To be tested; physical
                          filenames, timestamps,  image may contain
                          media or application    carved/unallocated
                          data                    artefacts not present
                                                  in logical extraction

  Email                   Amazon SES-related      Potential support if
                          `message-id`,           identifiers match
                          `return-path`,          
                          sender/recipient or     
                          domain                  

  Network / PCAP          Domains/IPs             Potential contextual
                          corresponding to        support if timestamps
                          Facebook, Live.com,     and identifiers align
                          Amazon SES or other     
                          recovered domains       

  Disk Image              Shared email addresses, Potential
                          domains, filenames or   contextual/supporting
                          timestamps              relationship

  Memory Image            Processes, network      Potential contextual
                          connections or          relationship
                          identifiers             
                          corresponding to        
                          phone-related findings  

  Other phone artefacts   EXIF timestamps, cookie Can strengthen a
                          timestamps, application phone-level timeline
                          records                 
  -----------------------------------------------------------------------

At present, the supplied phone report alone does not provide the other
evidence categories needed to mark these relationships as confirmed.
Therefore:

> **Insufficient evidence to establish a definitive cross-source
> correlation at this stage.**

------------------------------------------------------------------------

## 7. Limitations

1.  The original `.E01` SHA-256 value is not contained in the supplied
    HTML report and must be calculated or verified separately.
2.  The original `.E01` file size is not reported in the case-summary
    HTML and must be taken from the evidence file itself.
3.  EXIF metadata indicates what was stored in the recovered image file;
    it does not independently establish who operated the device or
    whether the metadata remained unaltered.
4.  Many photographs were recovered under `$CarvedFiles`, so their
    original file-system context is not available from the report alone.
5.  Cookies establish stored web/application state but do not by
    themselves prove a particular user interaction.
6.  Keyword hits can originate from system files, caches, carved files
    and unallocated space. Their presence alone does not establish user
    authorship or intent.
7.  Email-like remnants in unallocated space are incomplete forensic
    artefacts unless corroborated by the full email evidence.
8.  Physical-versus-logical comparison cannot be completed until the
    logical phone extraction is analysed.
9.  The report does not independently establish malicious activity,
    compromise, or a complete incident narrative.
10. Some artefacts may represent historical or residual data rather than
    activity occurring immediately before acquisition.

------------------------------------------------------------------------

## 8. Conclusion

The Autopsy examination of `tracy-phone-2012-07-05.E01` identified a
range of recoverable artefacts relevant to a phone forensic
investigation. The most significant findings are the recovery of 49
EXIF-bearing image records, including numerous images identified as
originating from an Apple iPhone 3G; the presence of geographic and
temporal metadata in a subset of those photographs; web/application
cookie artefacts associated with domains including Facebook and
Live.com; and email/header-like remnants recovered from unallocated
space.

The evidence establishes that the physical image contains historical and
recoverable user/application data that can support timeline, location,
account and communication analysis. However, the artefacts do not
independently prove malicious activity or identify a specific person as
responsible for any action.

The next forensic step is cross-source correlation. EXIF timestamps and
coordinates, web domains, cookie timestamps and email-related
identifiers should be compared with the logical phone extraction,
supplied email evidence, network capture, disk image and memory
evidence. Where such identifiers do not match or where the available
context is insufficient, the appropriate conclusion is that a definitive
correlation cannot be established.

> **Important:** This conclusion is limited to the evidence represented
> in the Autopsy physical-phone report. It should be updated if
> additional corroborating evidence becomes available.
