# SYN_Stealth_Port_Scanner
A SYN Python Stealth Scanner created to scan for open ports on your targets network address with their IP.
A seemless intigrated scanner with a loading bar and help menue.

Must run file with root privilages in Kali Linux.

Features include: 
# ----- Advanced Stealth SYN Scanner (single-file) ------------
# Description:
# Full-featured SYN scanner with:
# - heavy stealth defaults (random source ports/seq + decoys)
The scanner uses randomized TCP source ports and unpredictable initial sequence numbers for every SYN packet it sends. This makes traffic patterns significantly harder to correlate by intrusion detection systems. The tool also supports decoy packets—spoofed SYN packets appearing to come from fake IP addresses—making it difficult for a target to determine which host initiated the real scan. These stealth defaults reduce the scanner’s detectability and mimic the behavior of advanced security scanners.

# - decoy SYNs (spoofed IPs) -- decoys default = 5
For every real SYN sent, the scanner generates additional SYN packets that appear to originate from randomly generated IP addresses. These “decoys” are designed to obscure the origin of the actual scan by polluting the target’s logs with fake traffic sources. Targets receiving these packets cannot easily differentiate the legitimate probing host from the decoys. By default, five decoys are created, but the number is fully configurable.

# - optional IP fragmentation (--fragment)
With fragmentation enabled, the scanner splits SYN packets across multiple IP fragments before sending them. This technique attempts to evade basic packet-inspection firewalls or IDS systems that do not properly reassemble fragmented traffic or do not inspect every fragment. Since the target system reassembles the fragments before processing, the scan proceeds normally from the target’s perspective while potentially bypassing filtering rules.

# - banner grabbing for open ports
When a port responds with a SYN/ACK (indicating the port is open), the scanner attempts a lightweight TCP connection to retrieve the service banner. Many network services, such as SSH or FTP, automatically send a greeting string when a client connects. Capturing these banners allows the scanner to identify software versions or infer service configurations, improving scan accuracy and enabling more detailed reporting.

# - simple OS fingerprinting (TTL/window heuristics)
The scanner uses basic passive fingerprinting techniques based on the TTL (Time To Live) value and TCP window size observed in SYN/ACK responses. Different operating systems use characteristic defaults—for example, Windows commonly uses a TTL of 128 and Linux often uses 64. These heuristics are quick, lightweight, and require no additional traffic. While not as advanced as full fingerprinting tools, they provide practical OS guesses for each detected open port. 

# - progress bar + per-target ETA (tqdm)
A real-time progress bar is displayed for each target, showing how many ports have been scanned and how many remain. It updates as each thread completes a port probe. The tool also calculates an estimated time remaining (ETA) based on scanning speed and current progress. This makes long scans more transparent and user-friendly by giving continuous visual feedback.

# - colorized terminal output (termcolor)
Results printed to the terminal use colored text to improve readability and convey scan states at a glance. Open ports are shown in green, warnings in yellow, headings in cyan/magenta, and critical errors in red. This visual enhancement makes it easier to interpret large scan results and quickly identify important findings.

# - open-only results printed and saved in file
The scanner filters out all closed or filtered ports, showing only confirmed open ports in the terminal output. This dramatically reduces noise and focuses attention on actionable findings. Only open ports are saved to output files as well, reducing unnecessary clutter and ensuring clean reports suitable for analysis or documentation.

# - grouped-by-service output
Open ports are organized by service category (e.g., SSH, HTTP, DNS) rather than a flat list. Results are grouped under human-readable service names with each port listed underneath. This makes the output easier to analyze, enabling quick identification of which services are exposed and how many instances are running.

# - JSON output (timestamp in UTC, timezone-aware)
The scanner can export all open-port findings to a JSON file containing the port, service, banner, OS guess, decoys used, handshake status, and a correctly formatted timestamp in UTC. Using timezone-aware timestamps ensures compatibility with log systems, SIEM tools, and forensic analysis workflows. The JSON structure is clean, standards-friendly, and easy to parse programmatically.

# - CSV log of open ports
Alongside JSON export, the scanner can write results to a CSV file for easy import into spreadsheet tools, dashboards, or security analysis software. The CSV contains one row per open port and includes the timestamp, target, port, service, OS guess, handshake information, decoys used, and captured banners. This provides a lightweight reporting format useful for audits and documentation.

# - thread pool and concurrency control
To accelerate scanning, the tool uses a thread pool that probes multiple ports in parallel. The maximum number of threads is user-configurable, allowing fine tuning based on network conditions and system capabilities. Threading is implemented safely, with locks ensuring consistent shared data and preventing race conditions. This design keeps the scanner fast, stable, and scalable.
# - help section via argparse (--help)
The script includes a comprehensive command-line help menu using Python’s argparse. Running the script with --help displays a detailed description of every feature, supported flags, default settings, and usage examples. This makes the scanner self-documenting and easy to use, even for users unfamiliar with its full range of options.

---------------------------------------------
---------------------------------------------
# - Includes "--help" options after typing "sudo (file name) --help" to activate settings to change outputs.
# "--help" includes:
"-t", "--targets",   "Comma to separate targets (IP or hostnames)"
"-p", "--ports",     "Ports like '22,80,443' or ranges '1-1024' or mix"
"--decoys",          "Number of decoys (default 5)"
"--fragment",        "Fragment IP packets"
"--timeout",         "SYN timeout seconds"
"--banner-timeout",  "Banner grabbing timeout seconds"
"--min-delay",       "Min jitter delay seconds"
"--max-delay",       "Max jitter delay seconds"
"--max-threads",     "Max concurrent threads"
"-f", "--format",    choices=["table", "json"], default="table", help="Output format for terminal"
"-o", "--output",    "Write open-only results to JSON (and CSV alongside) if provided"
"-v", "--verbose",   "prints extra info"
