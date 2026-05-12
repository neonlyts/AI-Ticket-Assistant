# NeonAssist – AI Ticket Triage Assistant

## Overview
This project demonstrates how AI (Claude) can be used to automate IT support ticket triage. It is a part of my hands-on exploration into practical AI adoption within enterprise workflows.

## Problem
Manual triage of tickets is time-consuming and inconsistent.

## Solution
Used Claude prompts to:
- Summarise tickets
- Identify urgency
- Suggest next actions

## Example 1

Input:
"User unable to access VPN..."

Output:
Summary: Remote user is unable to connect to VPN due to an authentication failure, blocking access to all internal systems.
Priority: High
Likely Root Cause: Expired or incorrect credentials are the most likely culprit — this could be a recently changed/expired Active Directory or RADIUS password, an MFA token issue, or a locked-out account following failed login attempts.
Suggested Next Steps:

Verify account status — Check AD/LDAP to confirm the account isn't locked, disabled, or past its password expiry date.
Reset credentials if needed — Unlock the account or prompt a password reset and have the user retry.
Check MFA/2FA — If MFA is enforced on the VPN, confirm the user's authenticator app is in sync and tokens are valid.
Review VPN gateway logs — Pull auth logs from the VPN server (e.g. Cisco ASA, Fortinet, Palo Alto) to identify the exact failure reason and any repeated attempts.
Confirm VPN client config — Ensure the client hasn't been updated or misconfigured on the user's end (correct server address, authentication profile, etc.).
Escalate if systemic — If multiple users are reporting the same issue, escalate immediately as it may indicate a broader auth server (RADIUS/LDAP) outage.

## Example 2

Input:
"Teams not working. App launches, doesn't log in..."

Output:
Summary: Microsoft Teams launches successfully but fails to complete the login process, preventing the user from accessing the application.
Priority: Medium
Likely Root Cause: Most commonly a corrupted local Teams cache or an expired/broken authentication token. Could also be related to a conditional access policy change, SSO/Azure AD issue, or a recent Teams/OS update that's broken the sign-in flow.
Suggested Next Steps:

Clear the Teams cache — Close Teams fully via Task Manager, then delete the contents of %appdata%\Microsoft\Teams and relaunch.
Sign out and back in — If the app allows it, sign out and attempt a fresh login to force a new token request.
Check credentials — Confirm the user's Microsoft 365 account is active, not locked, and the password hasn't recently expired.
Try Teams on the web — Have the user attempt login at teams.microsoft.com to determine if the issue is client-specific or account-wide.
Reinstall the Teams client — If cache clearing doesn't resolve it, do a clean uninstall/reinstall of the Teams app.
Check Azure AD / Conditional Access — Review any recent policy changes in Entra ID that may be blocking authentication for this user or device.
Check for widespread issues — Verify the Microsoft 365 Service Health Dashboard for any active incidents affecting Teams sign-in.



## Practical Implementation

This solution can be implemented as:
- A Copilot Studio chatbot for IT teams
- A ServiceNow/Jira integration for automated ticket triage
- A Teams-based assistant for support engineers

This demonstrates how AI can move from concept to operational use within existing enterprise tools.



## Tools Used
- Claude (Anthropic)
- Prompt Engineering
