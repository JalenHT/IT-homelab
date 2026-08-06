# Lab 2 — MFA & Authentication Methods in Entra ID

## Objective
Configure and test Multi-Factor Authentication for users in Microsoft Entra ID to simulate real enterprise MFA enforcement.

## Environment
- Microsoft Entra ID Free tier
- Personal lab tenant: jalenthomas1216gmail.onmicrosoft.com

## What I did

### Security defaults
- Verified Security Defaults were enabled on the tenant
- Confirmed all users are required to register MFA on next login

### MFA registration
- Logged in as Alex Turner in a private browser window
- Completed MFA registration using Microsoft Authenticator app
- Scanned QR code and verified push notification worked

### MFA testing
- Signed out and back in as Alex Turner
- Approved MFA prompt and confirmed successful login
- Denied MFA prompt and confirmed access was blocked

### Per-user MFA
- Located the Per-user MFA page in Entra ID
- Observed that Security Defaults shows users as Disabled on Per-user MFA page
- Manually set Alex Turner to Enforced to test legacy MFA method
- Confirmed status changed to Enforced

### Sign-in log review
- Pulled sign-in logs filtered to Alex Turner
- Identified Success, Interrupted, and Failure entries
- Confirmed MFA enforcement is working correctly

## What I observed
- Security Defaults enforces MFA for all users automatically at the policy level
- Per-user MFA shows Disabled even when Security Defaults is on because they are two separate systems
- Per-user MFA is the legacy method and Microsoft recommends migrating away from it
- Denying the MFA prompt results in a Failure entry in the sign-in logs
- Sign-in logs are the best way to confirm MFA is actually working

## Skills demonstrated
- MFA configuration and enforcement
- Authentication method registration
- Security defaults management
- Per-user MFA configuration
- Sign-in log analysis and interpretation
- Understanding of legacy vs modern MFA systems

## Tools used
- Microsoft Entra ID
- Microsoft Authenticator app
- Entra ID Sign-in logs
- Per-user MFA portal

## Screenshots
![Security Defaults](security-defaults.png)
![Sign-in Logs](signin-logs.png)
![Per-user MFA Status](per-user-mfa.png)
