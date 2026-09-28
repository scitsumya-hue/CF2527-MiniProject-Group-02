# APPENDIX — COMPUTER FORENSICS PHONE PHYSICAL INVESTIGATION

## Supporting Screenshots and Evidence

This appendix contains the Autopsy 4.23.1 evidence-analysis screenshots captured during the physical (E01) phone image forensic examination.

### Appendix A — Evidence Source

This section documents the data source structure and volume/partition layout identified within the acquired physical image.

![Figure A1 - Autopsy listing of the data source and volumes](images/Phone_Physical_Figure_A1.png)

**Figure A1.** Autopsy “Listing” view of data source tracy-phone-2012-07-05.E01, showing the identified volumes: vol1 (Unallocated, sectors 0–5), vol4 (System, sectors 6–174085), vol5 (Data, sectors 174086–1982458), and vol6 (Unallocated, sectors 1982459–1982463).

### Appendix B — Operating System Information

The operating system running on the device was identified via a keyword search hit on the SystemVersion.plist file located within the System partition (vol4).

![Figure B1 - SystemVersion.plist keyword search result](images/Phone_Physical_Figure_B1.png)

**Figure B1.** Keyword search result and extracted text of SystemVersion.plist (path: /vol_vol4/System/Library/CoreServices/SystemVersion.plist), confirming ProductName “iPhone OS”, ProductVersion “4.2.1”, and ProductBuildVersion “8C148”.

### Appendix C — EXIF Metadata

Autopsy's EXIF Metadata analysis module identified 49 image files containing embedded metadata, including GPS coordinates and creation timestamps, recovered from the \$CarvedFiles directory of the System volume (vol4).

![Figure C1 - EXIF Metadata results](images/Phone_Physical_Figure_C1.png)

**Figure C1.** EXIF Metadata results (49 results) with carved image f0136568.jpg selected, showing embedded GPS coordinates (Latitude 18.588666666666667, Longitude 73.780666666666667), Date Created 2011-05-29 23:00:53 IST, file size 768664 bytes, MD5 a6eefa558167535ae222cc99d1fbb975, and SHA-256 3a779ade4846923562039506a79571632278ccd5b3069c158e75aa0db036fab1.

### Appendix D — Email Content and Header Information Recovered from Unallocated Space

A keyword search for “message-id” returned 8 results, including email artifacts carved directly from unallocated space on the Data volume (vol5), confirming recoverable email content and header metadata outside the active file system.

![Figure D1 - Keyword search results for message-id](images/Phone_Physical_Figure_D1.png)

**Figure D1.** Keyword search results for “message-id” (8 results) with item Unalloc_39438_725872640_1915871232 selected, located at /img_tracy-phone-2012-07-05.E01/vol_vol5/\$Unalloc/U... . The extracted text shows Message-ID: \<CAAOmep=onoKQwgzRtVtKaXCAAwXE18NJhHpd=5078Kf0OA_Kug@mail.gmail.com\>, From: Pat TeeSumTwelve \<patsumtwelve@gmail.com\>, To: TracySumtwelve@gmail.com, and body text beginning “Hey Sis, Thanks for the tickets. How are things going at home?”, recovered entirely from unallocated space.

### Appendix E — Evidence Reference

| Item | Reference |
|---|---|
| Case name | `CF_Phone_Physical_Investigation` |
| Evidence file | `tracy-phone-2012-07-05.E01` |
| Forensic tool | Autopsy 4.23.1 |
