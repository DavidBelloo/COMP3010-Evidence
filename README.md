# AI logs – COMP3010 CW1

AI use level: **P1 Partnered Work**. Two tools were used:

|Tool|Where it ran|Used for|
|-|-|-|
|Claude (Anthropic)|claude.ai|Evidence-file safety check, analysis scripts, quiz support, report drafting and review|
|Qwen3.6-35B-A3B|Locally via Ollama|Independent check that the analysis steps were reproducible|

## Log of AI use and validation

|#|Task|AI output|Problem found|How it was checked|
|-|-|-|-|-|
|1|Quiz Q7: hash of the .js file|`c19c2ddc…` from a walkthrough, flagged as unconfirmed|Wrong: a 1.15 KB corrupt partial copy of gerv.gun|DLE quiz checker rejected it; VirusTotal lookup|
|2|Payload extraction and hashing|SHA-256 of gerv.gun, trow.exe, wp.exe|None|Sizes match Content-Length; gerv.gun matches Hybrid Analysis|
|3|First full analysis|Missed the SMTP burst and t64.bin|Incomplete|Second full pass over all files|
|4|Decoy POST count|"637 requests"|My count was 662|662 packets = 637 requests + 25 TCP retransmissions (A9)|
|5|SMTP connection count|475, then 290|Both wrong|My count: 239 attempts (unique server + source port); 475 SYNs include retries (A11)|
|6|Decoy response count|563 responses, 275 errors (tshark 4.2.2)|My Wireshark: 570 − 6 = 564, 276 errors|Older tshark does not parse the gerv.gun response (frame 204) (A10)|
|7|Extraction method|"Export Objects does not list gerv.gun"|Wrong for my Wireshark version|Export Objects screenshot (A8)|
|8|NBNS traffic|Initially described as name registration|Wrong: all 684 NBNS packets are queries|Wireshark filter `nbns`|
|9|Malware family of each stage|Pushdo for the whole infection|Refined: gerv.gun is Shiotob; trow.exe is Pushdo|VirusTotal and Hybrid Analysis (A15)|
|10|Detection rules|Two Suricata rules|–|Suricata 7.0.3 test, each fired once (A13)|



