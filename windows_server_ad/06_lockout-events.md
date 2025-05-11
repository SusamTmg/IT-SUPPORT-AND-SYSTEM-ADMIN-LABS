# Lab 06 – Account Lockout & Event Viewer

## Objective
Simulate and investigate account lockout scenarios.

## Steps
- Locked user account by typing wrong password 5 times
- Unlocked user from ADUC (Account tab > Unlock)
- Checked Event Viewer for Event ID 4740
- Enabled auditing using `auditpol` and local security policy

## Purpose
Account lockout monitoring is crucial for security and user support.

## Learnings
- Account lockout policies are critical for security
- Auditing must be enabled to track login issues

## Real-World Relevance
Helps IT support investigate brute force attacks and login issues.
