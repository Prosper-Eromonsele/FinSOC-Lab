# Active Response Block Screenshot Placeholder

**File to replace with:** `active-response-block.png`

**Description of what the screenshot should show:**
- Terminal output on Linux Endpoint showing `iptables -L -n -v` with DROP rule for attacker IP
- OR log excerpt from `/var/ossec/logs/active-responses.log` showing:
  - "Successfully blocked IP xxx.xxx.xxx.xxx using iptables"
  - Rule ID that triggered it (e.g., 100102)
- Bonus: Before/after comparison if possible

**Purpose in portfolio:** Visual proof that automated containment actually worked.
