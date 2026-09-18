Claude Code Agent Skill: Workspace Document Archiving & Hardware Troubleshooting Rules

1. Skill Overview

This is a mandatory post-task workflow. It must run automatically after every finished user task, no extra command from user required.
Purpose: Maintain summary records for files in current working directory and standardize responses for hardware‑related issues.

2. Trigger Condition

Run this workflow immediately after completing any task, including coding, debugging, document editing, configuration adjustment and problem resolution.

3. File Reading Priority (Strictly Followed)

Read and parse files in this exact order. Do NOT read Markdown first.

1. .pdf

2. .doc / .docx

3. .md (only used as supplementary reference afterwards)

4. Auto Archiving Workflow (Only scan current directory, NO recursive subfolder scan)

Scan Scope

Only look for PDF, Word and Markdown files at the same folder level as current workspace.

Logic Branch A: Summary file does not exist

• Create a new file named work_summary.md

• Header: # Workspace Document Summary

• List all discovered files following the priority order above

• Write short summary for each file: file name, modified timestamp, core purpose and key takeaways. Do NOT copy full text.

Logic Branch B: work_summary.md already exists

• Load existing content first. Append new content only, never overwrite all old records.

• Detect newly‑added or updated PDF / DOCX files, add their summaries.

• If only Markdown files are updated, add notes at the end.

• Mark new entries with tag [NEW / UPDATED] plus timestamp.

5. Hardware Response Rules (Critical)

When user mentions hardware, GPU, RAM, disk, machine crash, OOM, driver or cloud instance issues:
DO NOT blame the platform or system as your first statement.

Recommended check sequence:

1. Collect observable evidence first: error logs, CUDA outputs, memory usage, dmesg messages.

2. Check software factors: program logic, parameter settings, library version mismatches, memory allocation strategy.

3. Only after software checks are fully done, you may mention: "Underlying hardware or resource scheduling might be a possible cause, further verification is needed."

Forbidden opening lines:

• "This is a system bug."

• "The cloud platform is broken."

• "Your machine has hardware failure."

6. Final Output

After finishing scan and summary update, briefly report to user:
Document scan completed. work_summary.md: [Created / New entries appended]
Do not dump full raw text of source documents, only keep concise summaries.

7. Exit

This skill stops once file write operation finishes, or hardware troubleshooting guidance is provided.
User can pause this skill manually by command: Pause document sweep skill.