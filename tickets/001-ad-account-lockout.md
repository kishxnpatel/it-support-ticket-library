# TKT-001 - AD Account Lockout (repeated lockouts)

## Symptoms
- User reports: “My password is correct but it keeps locking me out.”
- Account locks again shortly after unlock/password reset.
- Sign-in failures across Outlook/Teams/VPN (depending on environment).

## Environment
- Device/OS: Windows 10/11
- Identity: Active Directory (on-prem)
- Common triggers: cached credentials, mapped drives, scheduled tasks, mobile mail client

## Triage (what I checked first)
- Confirmed user identity and impact (can they sign in anywhere?).
- Verified the account is currently locked and captured timestamp of last lockout.
- Checked whether user recently changed password (common trigger for cached creds).

## Diagnostics (commands/logs)
```txt
# On a management workstation / DC (requires RSAT + permissions)

# 1) Check lockout status and last logon attributes
Get-ADUser -Identity <username> -Properties LockedOut,BadPwdCount,LastBadPasswordAttempt,LastLogonDate |
  Select-Object LockedOut,BadPwdCount,LastBadPasswordAttempt,LastLogonDate

# 2) Find locked out accounts (useful if user unsure which account)
Search-ADAccount -L
