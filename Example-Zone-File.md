```bash
$TTL 86400        ; Default time-to-live (TTL) for cached records (in seconds)
@   IN  SOA  ns1.example.com. admin.example.com. (
            2025031101  ; Serial number (YYYYMMDD##)
            3600        ; Refresh (1 hour)
            1800        ; Retry (30 minutes)
            1209600     ; Expire (2 weeks)
            86400       ; Minimum TTL (1 day)
)

; Nameserver records (NS)
@   IN  NS  ns1.example.com.
@   IN  NS  ns2.example.com.

; A records (IP addresses for the domain and subdomains)
@   IN  A   192.168.1.10  ; Main domain (example.com)
www IN  A   192.168.1.10  ; www.example.com
mail IN  A   192.168.1.20  ; Mail server (mail.example.com)

; MX records (Mail Exchange)
@   IN  MX  10 mail.example.com.

; CNAME records (Aliases)
ftp  IN  CNAME  www.example.com.

; TXT records (Custom text records, often used for SPF, DKIM, etc.)
@   IN  TXT  "v=spf1 mx -all"
```
---

### **Explanation of the Zone File**

- **SOA Record**: Defines the **Start of Authority**, including the primary nameserver and admin email (`admin@example.com`).
- **NS Records**: Lists the **authoritative nameservers** (`ns1.example.com` and `ns2.example.com`).
- **A Records**: Maps domain names (`example.com`, `www.example.com`, `mail.example.com`) to IP addresses.
- **MX Record**: Specifies the mail server (`mail.example.com`).
- **CNAME Record**: Creates an alias (`ftp.example.com` → `www.example.com`).
- **TXT Record**: Adds a text-based DNS record (e.g., SPF record for email security).

---
