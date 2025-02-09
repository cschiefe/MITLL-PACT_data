MIT-LL ASDF Exposure Notification Service Dataset 1
====================================================

Data was generated by the Exposure Notification Service (ENS) on Android mobile phones during tests in the Autonomous Systems Development Facility (ASDF) at MIT-LL from August 2020 through December 2020. The ENS software is written and distributed by Google LLC.

Data collection was performed in the Autonomous Systems Development Facility using RF-analogous mannequins in lieu of humans. The phones were placed in the front shirt pockets, rear pants pockets, or in a nylon bag hung from the mannequins' necks. The mannequins were placed at various distances and each of 3 orientations (facing each other, facing away from each other, or facing the same direction). The "large room" is a hangar bay approximately 100'w x 70'd x 33' h; the "small room" is an office approximately 12.5'w x 13.75'd x 8.5'h. Some tests used 2 phones and some used 3; the summary data sheet is organized by pairs of phones.

Data consists of phone logs of Bluetooth ENS messages, Temporary Exposure Keys, and test metadata (distances, timestamps,
phone IDs). Format is CSV and text files.

The system logs from the phones do not record ENS v2 data structures (both because we were using a v1 app and because the ENS service had not provided that level of logging in production). To compute ScanInstances and ExposureWindows, we ported the open source ENS internals code to run on a desktop, and fed in the beacons and timestamps from the phones' system logs. The ScanInstance and ExposureWindow data for each pair of phone exposures is formatted as CSV files under exposure_windows*/. Those CSVs have one row per ScanInstance; the data for the ExposureWindow is repeated in each row of its constituent ScanInstances.

On 2020-12-15, Google released an update to the calibration values for Android. Our tests on 2020-12-22 and 2020-12-23 showed the new values in use on the phones.


Test metadata / input to postprocessing step:
----------------------------------------------

- MITLL_ASDF_TestSummary.csv
    - Timestamps for begin/end of test, and clock offsets
    - Phone hardware IDs
    - Physical configuration (locations, distances, orientations)
    - Expect detection (just a boolean indicator of whether phones were < 6' apart for >= 15 min)

- MITLL_ASDF_TestSummary_Combo.csv -- same format as 1., but with time-consecutive fixed-distance tests "rolled up" into longer exposures at varying distances, either greater or less than 6 feet.

- ENS "dumpsys" file
    - Service-level configuration at runtime
    - History of Temporary Exposure Keys used by ENS
    - History of Bluetooth message contents sent by ENS
    - History of Bluetooth message contents received by ENS

- ENS Service log file from bugreport
    - Timestamps and contents of Bluetooth message contents received by ENS
    - Timestamps and contents of ENS data structures and matching events

For more information, please contact Curran Schiefelbein, curran.schiefelbein@ll.mit.edu.


DISTRIBUTION STATEMENT A. Approved for public release. Distribution is unlimited.
----------------------------------------------------------------------------------

This material is based upon work supported under Air Force Contract No. FA8702-15-D-0001. Any opinions, findings, conclusions or recommendations expressed in this material are those of the author(s) and do not necessarily reflect the views of the U.S. Air Force.

© 2021 Massachusetts Institute of Technology.

Delivered to the U.S. Government with Unlimited Rights, as defined in DFARS Part 252.227-7013 or 7014 (Feb 2014). Notwithstanding any copyright notice, U.S. Government rights in this work are defined by DFARS 252.227-7013 or DFARS 252.227-7014 as detailed above. Use of this work other than as specifically authorized by the U.S. Government may violate any copyrights that exist in this work.
