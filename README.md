<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0F2027,50:203A43,100:2C5364&height=230&section=header&text=Naju&fontSize=60&fontColor=ffffff&fontAlignY=35&desc=Backend%20Developer%20%C2%B7%20AI%2FLLM%20Systems%20%C2%B7%20Security%20Enthusiast%20%C2%B7%20Kerala,%20India&descSize=16&descAlignY=58&animation=fadeIn" />

<br>

<a href="https://naju.me"><img src="https://img.shields.io/badge/portfolio-naju.me-2C5364?style=for-the-badge" /></a>
<a href="mailto:kcnajwan7@gmail.com"><img src="https://img.shields.io/badge/email-kcnajwan7%40gmail.com-D14836?style=for-the-badge&logo=gmail&logoColor=white" /></a>
<a href="https://github.com/najuaircrack"><img src="https://img.shields.io/badge/github-najuaircrack-181717?style=for-the-badge&logo=github&logoColor=white" /></a>

<br><br>

<img src="https://komarev.com/ghpvc/?username=najuaircrack&style=flat-square&color=2C5364&label=profile+views" />

</div>

<br>

### About

I'm a backend developer in Kerala, India. Most of my day-to-day is APIs, databases, and the Linux boxes underneath them — the unglamorous work of keeping things online when traffic spikes or something upstream falls over.

Outside of that I've been chasing two things that don't usually sit on the same resume. One is understanding language models properly, from the matrix multiplications up, instead of just wiring up someone else's API — that's what [Nanoforge](https://github.com/najuaircrack/Nanoforge) is for. The other is offensive security. I've spent years on the defensive side — firewalls, rate limits, service hardening — and at some point I realized I couldn't reason well about defense without understanding how attacks actually work, so I'm now working through CTFs and the tooling that goes with them.

<br>

**Right now:**
- Shipping backend systems, and pushing [Nanoforge](https://github.com/najuaircrack/Nanoforge) further as a from-scratch transformer/LLM framework
- Hand-writing firewall rules, rate limits, and service isolation on the Linux servers I run
- Working through Nmap, Burp Suite, and Wireshark on HTB/THM boxes to build up the offensive side properly

Say hi at [kcnajwan7@gmail.com](mailto:kcnajwan7@gmail.com).

<br>

## Tech Stack

<table>
<tr>
<td valign="top" width="20%"><b>Languages</b></td>
<td><img src="https://skillicons.dev/icons?i=py,js,ts,php,c,cpp,bash,rust" /></td>
</tr>
<tr>
<td valign="top"><b>Backend</b></td>
<td><img src="https://skillicons.dev/icons?i=nodejs,express,fastapi,django,laravel,nginx" /></td>
</tr>
<tr>
<td valign="top"><b>Web / Frontend tooling</b></td>
<td><img src="https://skillicons.dev/icons?i=nextjs,vite" /></td>
</tr>
<tr>
<td valign="top"><b>Data</b></td>
<td><img src="https://skillicons.dev/icons?i=mysql,postgres,mongodb,redis,sqlite" /></td>
</tr>
<tr>
<td valign="top"><b>Infra</b></td>
<td><img src="https://skillicons.dev/icons?i=linux,ubuntu,debian,docker,cloudflare,githubactions,aws,git" /></td>
</tr>
<tr>
<td valign="top"><b>Tools</b></td>
<td><img src="https://skillicons.dev/icons?i=postman" /></td>
</tr>
</table>

<br>

## Security Focus

Defense is where I've actually shipped things. Offense is newer, and I'm deliberately building it the slow way — real boxes and real tools, not just reading write-ups.

<table>
<tr>
<td valign="top" width="50%">

**🛡️ Defensive (hands-on)**
- Netfilter rules (iptables/nftables) written and maintained by hand, not left on defaults
- Rate limiting to stop abuse before it reaches the application layer
- Port hardening and service isolation
- Sandboxed testing before anything touches production

</td>
<td valign="top" width="50%">

**⚔️ Offensive (learning, active)**
- CTFs on HackTheBox and TryHackMe
- Network scanning and enumeration with Nmap
- Web app testing with Burp Suite
- Traffic analysis with Wireshark

</td>
</tr>
</table>

Not trying to collect buzzwords here — the point is understanding both sides well enough to build things that fail safely.

<br>

## Featured Projects

### 🧠 [Nanoforge](https://github.com/najuaircrack/Nanoforge)

A GPT-style decoder-only transformer built from raw Python and NumPy — no framework doing the hard parts for me. This is where I actually learn how attention, backprop, and tokenization work, by implementing them rather than importing them.

What's in it: rotary position embeddings, RMSNorm, SwiGLU/GEGLU feed-forward blocks, grouped-query attention with KV caching, sliding-window attention, and an optional mixture-of-experts path, with Flash Attention through PyTorch's SDPA when it's available. Training supports mixed precision, gradient accumulation and checkpointing, AdamW with cosine/linear/constant schedules, EMA, early stopping, and NaN/Inf health checks, plus a small local dashboard so I can watch loss curves without leaving the terminal. Tokenization covers a byte tokenizer (with an optional Rust backend for speed), HuggingFace BPE, a dependency-free pure-Python BPE fallback, and SentencePiece — all feeding into packed memmap datasets with boundary-aware packing for chat data. On the inference side there's streaming generation, a chat CLI, and the usual sampling toolbox: top-k, top-p, temperature, repetition penalties, mirostat.

It's still pre-alpha and the APIs shift often — that's the deal with a project whose whole point is learning by building, not chasing benchmarks against vLLM or Megatron.

<img src="https://img.shields.io/github/stars/najuaircrack/Nanoforge?style=flat-square&color=2C5364&label=stars" /> <img src="https://img.shields.io/github/languages/top/najuaircrack/Nanoforge?style=flat-square&color=2C5364" />

<br>

### 🗄️ [pterodactyl-mysql-backup](https://github.com/najuaircrack/pterodactyl-mysql-backup)

A MySQL backup manager for Pterodactyl game panels, built as a Blueprint extension — because cron scripts bolted onto a panel are exactly the kind of thing that silently breaks. Backups run through Laravel's queue system rather than an external cron job, and a backup record is created the moment it's queued, so both scheduled and manual runs show up in the panel immediately instead of appearing only once they finish. `mysqldump` output streams straight into a compressed `.sql.gz`, with optional AES-256-GCM encryption on top.

The part I spent the most time on is storage. Users get one-click OAuth for Google Drive, Dropbox, and OneDrive — the admin registers a single app per provider, so end users never see a client secret, they just click Connect. Beyond that there's native WebDAV, S3-compatible storage, FTP/FTPS/SFTP, and rclone-backed support for Box, MEGA, pCloud, and Yandex Disk for anyone who wants full control. Storage quotas are checked in three places — before a backup is even queued, after the dump but before upload, and again after upload with automatic pruning of the oldest backups — so nothing quietly fills a disk. Retention, restore with an automatic safety backup, per-server policies, and admin-side audit logs round out the rest.

Security-wise: credentials and OAuth tokens are encrypted at rest, OAuth state is validated against the session CSRF token, webhook/WebDAV URLs are blocked from resolving to private or link-local IPs unless explicitly allowed, and rclone is restricted to named remotes only — the `local` rclone type is blocked entirely so it can't be used to reach the panel's own filesystem.

<img src="https://img.shields.io/github/stars/najuaircrack/pterodactyl-mysql-backup?style=flat-square&color=2C5364&label=stars" /> <img src="https://img.shields.io/github/languages/top/najuaircrack/pterodactyl-mysql-backup?style=flat-square&color=2C5364" />

<br>

### 🎮 [AKRP V5](https://github.com/najuaircrack/AKRP-V5)

An Open.mp/SA-MP roleplay gamemode built and maintained for the All Kerala Roleplay community. Tuned to comfortably run around 70 concurrent players on a mid-range VPS, and released publicly to keep the codebase transparent after attempted leaks.

<img src="https://img.shields.io/github/stars/najuaircrack/AKRP-V5?style=flat-square&color=2C5364&label=stars" /> <img src="https://img.shields.io/github/languages/top/najuaircrack/AKRP-V5?style=flat-square&color=2C5364" />

<br>

### 📡 [Nettop](https://github.com/najuaircrack/Nettop)

A lightweight, Linux-first network monitoring TUI with a scriptable CLI controller. Captures live traffic, ranks source IPs, tracks packet and byte rates, shows MAC activity, and resolves IP geolocation.

<img src="https://img.shields.io/github/stars/najuaircrack/Nettop?style=flat-square&color=2C5364&label=stars" /> <img src="https://img.shields.io/github/languages/top/najuaircrack/Nettop?style=flat-square&color=2C5364" />

<br>

## GitHub Stats

<div align="center">
<img height="165" src="https://github-readme-stats.vercel.app/api?username=najuaircrack&show_icons=true&theme=tokyonight&count_private=true&hide_border=true&border_radius=10" />
<img height="165" src="https://github-readme-stats.vercel.app/api/top-langs/?username=najuaircrack&layout=compact&theme=tokyonight&hide_border=true&langs_count=6&border_radius=10" />
</div>

<br>

## Let's Talk

<div align="center">

<a href="https://naju.me"><img src="https://img.shields.io/badge/Portfolio-000000?style=for-the-badge&logo=About.me&logoColor=white" /></a>
<a href="mailto:kcnajwan7@gmail.com"><img src="https://img.shields.io/badge/Email-D14836?style=for-the-badge&logo=gmail&logoColor=white" /></a>

</div>

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:2C5364,100:0F2027&height=100&section=footer" />
