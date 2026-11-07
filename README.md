# Disk Forensic Analysis Using Autopsy

## Project Overview

This project demonstrates a practical digital forensic investigation using **Autopsy**, an open-source digital forensics platform built on The Sleuth Kit (TSK).

The project walks through the examination of digital storage media to identify, recover, analyze, and document digital evidence. It covers the forensic examination of disk images, file-system structures, deleted files, user activities, browser artifacts, metadata, and other potentially relevant evidence.

The objective is to demonstrate how a digital forensic investigator can examine a storage device systematically while preserving the integrity and evidential value of the acquired data.

This repository is designed for cybersecurity students, digital forensic beginners, SOC analysts, incident responders, and anyone interested in practical digital forensic investigations.

## 1. Learning Objectives

By completing this practical exercise, learners should be able to:

1. Explain the fundamentals of digital forensics and disk forensic analysis.
2. Understand forensic imaging and why it is necessary.
3. Explain the importance of evidence integrity and chain of custody.
4. Install and configure Autopsy.
5. Create and manage forensic investigation cases.
6. Add disk images and logical data sources to an Autopsy case.
7. Configure and execute Autopsy ingest modules.
8. Examine file-system structures and directory contents.
9. Identify and recover deleted files where recovery is possible.
10. Perform keyword searches across acquired evidence.
11. Examine file metadata and timestamps.
12. Analyze browser artifacts and user activities.
13. Identify suspicious files and file-extension mismatches.
14. Generate forensic timelines.
15. Calculate and verify cryptographic hashes.
16. Generate and interpret forensic investigation reports.

## 2. What Is Disk Forensic Analysis?

Disk forensic analysis is the process of acquiring, preserving, examining, and interpreting digital evidence stored on computer storage media.

These storage devices may include:

- Hard Disk Drives (HDDs).
- Solid State Drives (SSDs).
- USB flash drives.
- External storage devices.
- Memory cards.
- Virtual machine disk images.
- Other digital storage media.

During an investigation, an examiner may look for:

- Deleted documents and photographs.
- Recently accessed files.
- Browser history and downloaded files.
- User-created documents.
- Suspicious executable files.
- Evidence of unauthorized access.
- Hidden files and directories.
- File-system metadata.
- Evidence of data exfiltration.
- Potential indicators of malicious activity.

### Why Is Disk Forensics Important?

Disk forensic analysis is useful in:

- Cybercrime investigations.
- Incident response.
- Insider-threat investigations.
- Malware investigations.
- Data theft investigations.
- Corporate security investigations.
- Legal and regulatory investigations.
- Recovery of deleted or lost information.

## 3. Tools and Technologies

The following tools are used or referenced in this project.

| Tool | Purpose |
|---|---|
| Autopsy | Digital forensic examination and analysis |
| The Sleuth Kit (TSK) | File-system forensic analysis framework |
| FTK Imager | Forensic image acquisition and examination |
| WinHex / HxD | Hexadecimal examination of files and storage data |
| PowerShell | Hash calculation and file verification |
| SHA-256 | Cryptographic integrity verification |
| Windows / Linux | Forensic laboratory operating systems |

### Primary Tool: Autopsy

Autopsy provides a graphical interface for investigating disk images and other digital evidence.

Its capabilities include:

- File-system analysis.
- Deleted-file identification.
- Keyword searching.
- Hash calculation and lookup.
- File-type identification.
- Browser artifact extraction.
- Timeline analysis.
- Metadata examination.
- Evidence tagging.
- Forensic report generation.

Official resources:

- Autopsy website: https://www.autopsy.com/
- Autopsy downloads: https://www.autopsy.com/download/
- Autopsy documentation: https://www.sleuthkit.org/autopsy/docs/
- The Sleuth Kit: https://www.sleuthkit.org/

## 4. Laboratory Environment and Requirements

### Hardware Requirements

Recommended laboratory specifications:

| Component | Minimum Recommendation |
|---|---|
| Processor | Dual-core processor |
| RAM | 8 GB |
| Storage | 50 GB available space |
| Operating System | Windows 10/11 or supported Linux |
| Display | 1366 × 768 or higher |

For larger forensic images, 16 GB RAM or more and additional SSD storage are recommended.

### Software Requirements

1. Autopsy.
2. A supported operating system.
3. A forensic disk image or controlled sample evidence.
4. A hashing utility.
5. Optional: FTK Imager.

### Laboratory Safety

Only investigate storage devices and forensic images that you own or have explicit authorization to examine.

**Important forensic principles:**

- Never modify original evidence unnecessarily.
- Always work from a forensic image or verified working copy.
- Record the source and acquisition details.
- Calculate cryptographic hashes.
- Preserve original evidence separately.
- Document every important investigative action.
- Do not interpret an automated finding as proof of criminal activity without corroboration.

## 5. Project Directory Structure

A recommended directory structure for this practical exercise is:

```text
Disk-Forensic-Analysis/
│
├── README.md
│
├── evidence/
│   ├── original/
│   ├── working-copy/
│   └── sample-data/
│
├── acquisition/
│   ├── acquisition-notes.md
│   └── hash-verification.txt
│
├── autopsy-case/
│   └── CASE-001/
│
├── screenshots/
│   ├── 01-autopsy-dashboard.png
│   ├── 02-case-creation.png
│   ├── 03-data-source.png
│   ├── 04-ingest-configuration.png
│   ├── 05-file-analysis.png
│   ├── 06-deleted-files.png
│   ├── 07-keyword-search.png
│   ├── 08-timeline-analysis.png
│   └── 09-forensic-report.png
│
├── reports/
│   ├── autopsy-report/
│   └── investigation-summary.md
│
└── documentation/
    ├── chain-of-custody.md
    └── investigation-notes.md
```

*Note: The evidence directories and screenshots are placeholders for the actual laboratory files. Do not commit confidential evidence, private personal information, or large forensic disk images to a public GitHub repository.*

---

# 6. Practical Walkthrough: Disk Forensic Investigation

The practical investigation follows the standard digital forensic workflow:

**Evidence identification → Acquisition → Preservation → Examination → Analysis → Reporting**

## Phase 1: Preparing the Forensic Laboratory

### Step 1: Install Autopsy

1. Visit https://www.autopsy.com/download/.
2. Download the supported Autopsy installer for your operating system.
3. Run the installer.
4. Follow the installation wizard.
5. Launch Autopsy after installation.
6. Confirm that the application opens successfully.

On Windows, Autopsy may request administrator privileges for certain acquisition and disk-access operations.

**Expected outcome:** Autopsy launches and displays its welcome screen.

### Step 2: Prepare Your Evidence

For this exercise, obtain a controlled forensic disk image or create a sample image from a storage device you are authorized to examine.

Common forensic image formats include:

- RAW/DD (`.dd`, `.img`, `.raw`).
- Expert Witness Format (`.E01`).

A forensic image should preserve the relevant data and structure of the source storage medium.

You can obtain educational forensic datasets from:

- NIST Computer Forensic Reference Data Sets (CFReDS): https://cfreds.nist.gov/
- Digital Forensics Tool Testing: https://www.dfrws.org/

Keep the original evidence in a protected directory and use a separate working copy for examination.

### Step 3: Calculate the Evidence Hash

A cryptographic hash helps establish whether evidence has changed between acquisition and examination.

On Windows PowerShell:

```powershell
Get-FileHash "C:\Evidence\sample.dd" -Algorithm SHA256
```

On Linux:

```bash
sha256sum sample.dd
```

Record the resulting hash in your evidence documentation.

Example:

```text
Evidence ID: EVD-001
Evidence Name: sample.dd
Hash Algorithm: SHA-256
Hash Value: [INSERT ACTUAL HASH]
Date Acquired: [INSERT DATE]
Examiner: [INSERT NAME]
```

Do not use an invented hash value in your investigation report.

For segmented forensic images, preserve and verify the complete image set according to the acquisition tool's procedure.

## Phase 2: Creating a Forensic Case in Autopsy

### Step 4: Launch Autopsy

1. Open Autopsy.
2. Select **Create New Case**.
3. The New Case Information wizard will appear.

### Step 5: Enter Case Information

Provide the following details:

| Field | Example |
|---|---|
| Case Name | Disk_Forensic_Investigation |
| Base Directory | C:\ForensicCases |
| Case Type | Single-user |
| Case Number | CASE-001 |
| Examiner | Your Name |
| Organization | Cybersecurity Training Laboratory |

Use a unique case number for every investigation.

Click **Next** and complete the additional case information fields available in your installed version.

Click **Finish**.

**Expected outcome:** Autopsy creates the investigation case and prepares the environment for evidence examination.

## Phase 3: Adding the Evidence Source

### Step 6: Add a Data Source

After creating the case:

1. Select **Add Data Source**.
2. Choose the appropriate data source type.
3. For a forensic image, select **Disk Image or VM File**.
4. Browse to the location of your forensic image.
5. Select the image.
6. Confirm the relevant time-zone setting.
7. Complete the wizard.

Autopsy supports common forensic image formats, including RAW and E01.

For a physical disk examination, use the appropriate acquisition and write-protection procedures rather than treating an ordinary live disk connection as equivalent to a forensic image.

### Step 7: Configure the Ingest Modules

Autopsy uses ingest modules to automate different aspects of forensic examination.

The available modules depend on the installed Autopsy version and configuration.

For this laboratory, enable relevant modules where available:

| Ingest Module | Investigation Purpose |
|---|---|
| Recent Activity | Extract browser and operating-system activity |
| Hash Lookup | Compare files against configured hash databases |
| File Type Identification | Identify actual file types |
| Extension Mismatch Detector | Identify files whose extensions do not match their contents |
| Keyword Search | Search indexed evidence for specified terms |
| Embedded File Extractor | Examine supported embedded and archive content |
| Picture Analyzer | Analyze supported image information |
| Encryption Detection | Identify potential encrypted files |
| Interesting Files Identifier | Identify files matching configured criteria |

Select the modules relevant to the exercise.

Avoid enabling every available module indiscriminately, particularly when investigating large disk images or working with limited hardware resources.

Click **Next** or **Finish**, depending on the wizard.

### Step 8: Allow Ingest Processing to Complete

Autopsy begins processing the evidence.

Monitor the ingest progress indicator.

The duration depends on:

- Disk image size.
- Number of files.
- Number of enabled modules.
- Available RAM.
- Processor performance.
- Storage speed.

Do not assume that the absence of immediate findings means there is no evidence.

**Expected outcome:** Autopsy processes the data source and populates the results tree with available forensic findings.

## Phase 4: File-System Examination

### Step 9: Examine the File-System Structure

Expand the data source in the left-hand navigation panel.

Explore the available file-system structures and directories.

Pay particular attention to:

- User directories.
- Desktop.
- Documents.
- Downloads.
- Pictures.
- Videos.
- Recycle Bin.
- Temporary directories.
- Application data directories.

Examine the following:

1. File names.
2. File extensions.
3. File sizes.
4. File locations.
5. Creation timestamps.
6. Modification timestamps.
7. Access timestamps, where available.

Record potentially relevant files and their original paths.

### Step 10: Examine File Metadata

Select a file and inspect the available details.

Depending on the file and its format, Autopsy may display:

- File name.
- File path.
- File size.
- MIME type.
- File-system timestamps.
- Hash values.
- Metadata attributes.
- Associated artifacts.

For image files, examine available EXIF information, including:

- Camera manufacturer.
- Camera model.
- Date and time information.
- GPS coordinates, if present.
- Image dimensions.

**Investigation objective:** Determine whether the file metadata provides useful context about the origin, handling, or relevance of the evidence.

Remember that timestamps can be affected by file-system behavior, copying, time-zone settings, and other factors. Do not treat a timestamp as conclusive proof of when a person performed an action.

## Phase 5: Deleted File Analysis

### Step 11: Identify Deleted Files

Deleted files can contain important forensic evidence.

In Autopsy:

1. Expand the data source.
2. Navigate to the deleted-files view or the relevant file-system listing.
3. Apply the deleted-file filter where available.
4. Review the identified deleted entries.
5. Select potentially relevant files.
6. Examine their metadata and available contents.

Depending on the file system, storage medium, and extent of overwriting, some deleted files may be recoverable while others may not.

### Step 12: Recover and Examine Deleted Files

Where supported:

1. Select the deleted file.
2. Use the available extraction or export option.
3. Save the recovered file into a separate examination directory.
4. Record the original file path.
5. Calculate the recovered file's SHA-256 hash.
6. Examine its content without altering the original evidence.

Example:

```text
Recovered Evidence ID: REC-001
Original Filename: confidential.docx
Original Location: /Users/John/Documents/
Status: Deleted
Recovery Status: Successfully extracted
SHA-256: [INSERT ACTUAL HASH]
```

**Important:** A file appearing in a deleted-files listing does not automatically mean its complete contents are recoverable. Distinguish deleted directory entries, recoverable content, and partially overwritten data.

## Phase 6: Keyword Search and Evidence Discovery

### Step 13: Configure Keyword Searches

Keyword searching helps identify potentially relevant information in a large collection of files.

In Autopsy:

1. Locate the Keyword Search functionality.
2. Configure the relevant search terms or lists.
3. Run the search against the indexed evidence.
4. Review the returned matches.
5. Identify the files containing relevant terms.
6. Examine the context surrounding each match.

For demonstration purposes, use the following search terms:

```text
password
confidential
bank
transaction
admin
secret
database
backup
```

These are illustrative search terms, not evidence of malicious activity.

### Step 14: Analyze Keyword Search Results

For every relevant match:

- Record the keyword.
- Record the filename.
- Record the file path.
- Examine the surrounding content.
- Record the matching location where available.
- Determine whether the match is relevant to the investigation.

A keyword match is a lead, not a conclusion. Validate it against the surrounding evidence.

## Phase 7: Browser and User Activity Analysis

### Step 15: Examine Recent Activity

If the Recent Activity ingest module was enabled, navigate to the extracted results.

Depending on the available data, examine:

- Browser history.
- Bookmarks.
- Cookies.
- Download records.
- Search activity.
- Operating-system artifacts.
- Relevant user-account information.

Look for activity that may help reconstruct events.

For example:

- Was a particular website visited?
- Was a file downloaded?
- Are there records of access to a particular resource?
- Do browser artifacts correlate with other evidence?

Document relevant findings with their associated timestamps and source artifacts.

**Important:** Browser artifacts may be incomplete or absent because of private browsing, deleted data, unsupported browser formats, or other technical limitations.

## Phase 8: File-Type and Suspicious File Analysis

### Step 16: Identify File Types

Navigate to the File Types section.

Review available categories, such as:

- Documents.
- Images.
- Videos.
- Archives.
- Executables.
- Audio files.

Examine files with unusual names, extensions, or locations.

### Step 17: Investigate Extension Mismatches

A file extension does not necessarily represent the actual content of a file.

For example:

```text
document.jpg
```

may contain executable or archive data rather than a JPEG image.

Use Autopsy's Extension Mismatch Detector, where available, to identify potential discrepancies.

For each result:

1. Record the filename.
2. Record the original location.
3. Examine the identified file type.
4. Compare the extension with the actual format.
5. Investigate the surrounding files and context.

Do not automatically classify every mismatch as malware. Renamed files can have legitimate explanations.

## Phase 9: Timeline Analysis

### Step 18: Generate a Forensic Timeline

A forensic timeline helps reconstruct the sequence of events using available timestamped evidence.

In Autopsy:

1. Locate the Timeline feature.
2. Open the timeline interface.
3. Select the relevant date range.
4. Filter the available event categories.
5. Examine significant timestamps.
6. Correlate file-system events with browser and other extracted artifacts.

Look for:

- File creation.
- File modification.
- File access, where supported.
- Downloads.
- Application activity.
- Other timestamped artifacts.

### Step 19: Correlate Timeline Events

Suppose the investigation identifies:

| Time | Event | Evidence |
|---|---|---|
| 09:00 | Document created | File-system metadata |
| 09:15 | Website visited | Browser history |
| 09:30 | File downloaded | Browser download artifact |
| 10:00 | Document modified | File-system metadata |

These are illustrative events, not actual findings from the sample evidence.

Correlate multiple independent artifacts before drawing conclusions.

## Phase 10: Hash Verification and Evidence Integrity

### Step 20: Examine Hash Information

Autopsy can calculate file hashes and, when configured, compare them against known hash databases.

Hash analysis is useful for:

- Identifying known files.
- Detecting identical file contents.
- Supporting evidence integrity checks.
- Identifying known malicious files when suitable reference databases are configured.

Use SHA-256 as the preferred integrity hash for this exercise.

For a forensic image:

```powershell
Get-FileHash "C:\Evidence\sample.dd" -Algorithm SHA256
```

For a recovered file:

```powershell
Get-FileHash "C:\Recovered\confidential.docx" -Algorithm SHA256
```

Record the results separately.

A matching hash supports the conclusion that two files have identical contents with extremely high confidence. A hash mismatch does not, by itself, establish why the files differ.

---

# 7. Evidence Documentation and Reporting

## Step 21: Tag Relevant Evidence

During analysis, identify and tag relevant files and artifacts.

Useful categories include:

- Interesting.
- Notable.
- Suspicious.
- Potentially Relevant.
- Exculpatory.
- Requires Further Investigation.

Use comments or examiner notes to explain why an item was tagged.

Avoid describing an item as malicious or incriminating without sufficient supporting evidence.

## Step 22: Generate an Autopsy Report

After reviewing the findings:

1. Select **Generate Report**.
2. Choose an appropriate report module.
3. Select the relevant report format.
4. Configure the report contents.
5. Include relevant tagged files and available artifacts.
6. Generate the report.
7. Save the report in the project reporting directory.

HTML is a convenient format for reviewing findings in a browser. Other supported formats may include XLS and other report types, depending on the installed version and modules.

Review the generated report to confirm that it contains the intended evidence and relevant examination details.

## Step 23: Prepare an Investigation Summary

The final investigation summary should contain:

### A. Case Information

- Case number.
- Investigation title.
- Examiner.
- Organization.
- Examination date.
- Evidence identification.

### B. Investigation Objective

Explain the purpose of the examination.

### C. Evidence Description

Document the source, format, size, acquisition information, and cryptographic hash.

### D. Examination Methodology

Describe the tools, techniques, and Autopsy modules used.

### E. Findings

Document the relevant evidence discovered.

### F. Evidence Correlation

Explain how the different findings relate to one another.

### G. Limitations

Identify technical limitations, missing artifacts, unsupported file types, and any other factors that affect the conclusions.

### H. Conclusion

Provide an objective summary of the findings without making unsupported assumptions.

---

# 8. Chain of Custody

Chain of custody is the chronological documentation of evidence handling from collection through examination, storage, transfer, and reporting.

It helps establish accountability and supports the integrity of the investigation.

Use the following template:

| Field | Description |
|---|---|
| Evidence ID | Unique evidence identifier |
| Evidence Description | Description of the storage device or image |
| Collected By | Name of the collecting examiner |
| Date Collected | Date and time of collection |
| Source | Original device or evidence source |
| Acquisition Method | Tool and method used |
| Hash Algorithm | SHA-256 |
| Hash Value | Actual calculated hash |
| Storage Location | Protected evidence storage location |
| Transfer History | Record of evidence transfers |
| Examination Date | Date examination commenced |

Every transfer or handling event should be documented, including the person responsible, date, time, purpose, and relevant integrity checks.

# 9. Expected Learning Outcomes

At the end of this project, learners should have demonstrated the ability to:

- Create and manage an Autopsy forensic case.
- Add and examine a forensic disk image.
- Configure and run ingest modules.
- Identify relevant files and directories.
- Examine deleted files.
- Perform forensic keyword searches.
- Investigate browser artifacts.
- Examine file metadata.
- Identify suspicious file characteristics.
- Construct and interpret a forensic timeline.
- Verify evidence using cryptographic hashes.
- Tag relevant evidence.
- Generate an investigation report.
- Document the chain of custody.

# 10. Ethical and Legal Considerations

Digital forensic investigations must be conducted within applicable legal and organizational frameworks.

The following principles should guide every examination:

1. Obtain proper authorization before accessing digital devices.
2. Preserve original evidence.
3. Maintain an accurate chain of custody.
4. Protect sensitive personal information.
5. Avoid unauthorized disclosure of collected information.
6. Maintain detailed investigation notes.
7. Report findings objectively.
8. Distinguish observations from interpretations and conclusions.

This project is intended for educational and authorized forensic investigations.

# 11. References and Further Learning

### Official Documentation

- [Autopsy Official Website](https://www.autopsy.com/)
- [Autopsy Documentation](https://www.sleuthkit.org/autopsy/docs/)
- [The Sleuth Kit](https://www.sleuthkit.org/)
- [Autopsy Quick Start Guide](https://www.sleuthkit.org/autopsy/docs/user-docs/4.19.1/quick_start_guide.html)
- [Autopsy Ingest Modules](https://www.sleuthkit.org/autopsy/docs/user-docs/4.5.0/ingest_page.html)

### Forensic Practice Resources

- [NIST Computer Forensic Reference Data Sets](https://cfreds.nist.gov/)
- [Digital Forensics Research Workshop](https://www.dfrws.org/)
- [NIST Computer Security Resource Center](https://csrc.nist.gov/)

---

## 12. Project Conclusion

Disk forensic analysis is an essential component of digital investigations and incident response.

Through this practical project, learners gain experience using Autopsy to examine digital storage evidence, identify relevant artifacts, recover available deleted data, reconstruct user activities, and produce structured forensic reports.

The exercise reinforces the importance of evidence integrity, systematic examination, accurate documentation, and objective interpretation of digital evidence.

**Project:** Disk Forensic Analysis Using Autopsy

**Domain:** Cybersecurity / Digital Forensics and Incident Response (DFIR)

**Primary Tool:** Autopsy

**Level:** Beginner to Intermediate

**Practical Focus:** Evidence Acquisition, Preservation, Examination, Analysis, and Reporting
