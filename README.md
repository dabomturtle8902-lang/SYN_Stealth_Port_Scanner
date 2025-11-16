# SYN_Stealth_Port_Scanner
A SYN Python Stealth Scanner created to scan for open ports on your targets network address with their IP.
A seemless intigrated scanner with a loading bar and help menue.

Must run file with root privilages in Kali Linux.

Features include: 
# ----- Advanced Stealth SYN Scanner (single-file) ------------
# Description:
# Full-featured SYN scanner with:
# - heavy stealth defaults (random source ports/seq + decoys)
# - decoy SYNs (spoofed IPs) -- decoys default = 5
# - optional IP fragmentation (--fragment)
# - banner grabbing for open ports
# - simple OS fingerprinting (TTL/window heuristics)
# - progress bar + per-target ETA (tqdm)
# - colorized terminal output (termcolor)
# - open-only results printed and saved
# - grouped-by-service output
# - JSON output (timestamp in UTC, timezone-aware)
# - CSV log of open ports
# - thread pool and concurrency control
# - help section via argparse (--help)


Includes "--help" options after typing "sudo (file name) --help" to activate settings to change outputs.
#"--help" includes:
parser = argparse.ArgumentParser(description="Advanced Stealth SYN Scanner (open-only outputs)"
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

