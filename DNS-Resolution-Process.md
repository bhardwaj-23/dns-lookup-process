### **How DNS Works: Step-by-Step**

**1. Local Machine Checks the Hosts File**

- When a user enters a domain name (e.g., `example.com`) into their browser, the machine first checks its local **hosts file**.
- The hosts file is a local text file (e.g., `/etc/hosts` on Unix systems or `C:\Windows\System32\drivers\etc\hosts` on Windows) that maps domain names to IP addresses manually.
- If the domain and its IP address are found here, the process stops, and the IP is used. If not, the machine moves to the next step.

**2. Local Machine Checks the Stub Resolver’s Cache**

- The machine then consults its **stub resolver**, a lightweight DNS client built into the operating system.
- The stub resolver checks its **cache** (stored locally from previous DNS queries).
- If the IP address for the domain is cached and still valid (based on the Time-to-Live, or TTL), it returns the IP, and the process ends. If not, the stub resolver forwards the request to a configured DNS server.

**3. Query Sent to a Recursive Resolver (e.g., 8.8.8.8 or 1.1.1.1)**

- If the local cache doesn’t have the answer, the stub resolver sends the query to a **recursive resolver**, a public DNS server like Google’s `8.8.8.8` or Cloudflare’s `1.1.1.1`.
- The recursive resolver is responsible for doing all the work to find the IP address and returning it to the stub resolver.

**4. Recursive Resolver Checks Its Cache**

- The recursive resolver first checks its own **cache** to see if it has recently resolved the domain name.
- If the IP address is cached and the TTL hasn’t expired, it returns the answer to the stub resolver. If not, it begins the full DNS resolution process.

**5. Recursive Resolver Queries the Root Server**

- The recursive resolver starts at the top of the DNS hierarchy by contacting one of the 13 **root servers** (managed globally).
- Root servers don’t store IP addresses for specific domains but know the locations of servers for **Top-Level Domains (TLDs)** like `.com`, `.org`, or `.edu`.
- The resolver sends a query like, **“Who handles `.com`?”** The root server responds with the IP address of the TLD server for `.com`.

**6. Recursive Resolver Queries the TLD Server**

- The recursive resolver then contacts the **TLD server** for the specific top-level domain (e.g., the `.com` TLD server).
- The TLD server doesn’t have the IP of `example.com` but knows which **authoritative name servers** manage the second-level domain (example in example.com).
- The resolver asks, “Who manages `example.com`?” The TLD server responds with a list of authoritative name servers for `example.com`.

**7. Recursive Resolver Queries the Authoritative Name Server**

- The recursive resolver now contacts one of the **authoritative name servers** provided by the TLD server.
- The authoritative name server holds the **zone file** for the domain (`example.com`), which contains DNS records like the IP address (A record), mail server (MX record), etc.
- The resolver asks, “What’s the IP for `example.com`?” The authoritative server replies with the IP address (e.g., `93.184.216.34`).

**8. Recursive Resolver Returns the IP to the Stub Resolver**

- The recursive resolver receives the IP address from the authoritative server and caches it (based on the TTL) for future queries.
- It sends the IP address back to the stub resolver on the user’s machine.

**9. Local Machine Uses the IP Address**

- The stub resolver provides the IP address to the operating system or application (e.g., the browser).
- The machine uses this IP address to connect to the target server (e.g., to load the website `example.com`).

---
