##  Issues Faced and Fixes

| Issue | Solution |
|-------|----------|


| Time mismatch with DC | Synced time on Ubuntu, set timezone manually; disabled internet time on DC |

| Account disabled | Fixed from Active Directory: enabled user |

| `wbinfo -u` returns nothing | Restarted `winbind`, confirmed join, and re-synced time |

| Ubuntu login stuck | Increased RAM + CPU allocation, enabled Virtualization in BIOS |