<!-- SPDX-FileCopyrightText: 2026 The Aural Authors -->
<!-- SPDX-License-Identifier: LicenseRef-Fidenne-Freeware -->
<!-- Translated from SECURITY.md at commit 60083913fecff876c8e1725df00d19fcb559a621 -->

# Reporting a Security Issue — Fidenne

## Supported versions

| Version | Security fixes |
|---|---|
| The most recently published release | Received |
| Any other version | Not received — please upgrade to the latest release and check again |

Fidenne is still in beta (0.x). Fixes go out only in a new release, and we do not issue separately patched builds of past versions.

## How to report

**Please do not write it in a public issue.** If it becomes known before it is fixed, other users are put at risk.

1. If the **Security** tab of this repository shows **Report a vulnerability** (GitHub private vulnerability reporting), use that to report.
2. If it does not appear, report by email: **fidenne.support@gmail.com** — please put `[보안]` (Korean for "[Security]") at the start of the subject.

Helpful things to include:

- The app version and build (app menu › About Fidenne (Fidenne 에 관하여)), the macOS version, and the Mac model
- What you do and what happens — steps that can be repeated
- Impact: what becomes possible to read or change
- If you know it, how to fix it

When attaching a diagnostic file, please send only what falls within the boundary written in [Privacy](PRIVACY.en.md).

## What happens next

- Because this is a small project, **we do not promise a response time**. We will send an acknowledgment and do the fixing work as quickly as we can.
- Please do not disclose the details before a fixed release comes out. After the fix, we will write what was fixed in the release notes and, if you wish, include the reporter's name.
- Extensions (plugins) are managed separately by their authors. Please report problems in an extension itself to the person who made it.
