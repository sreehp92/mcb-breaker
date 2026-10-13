# ⚡ Server MCB Circuit Breaker Dashboard

> **Mobile-First Linux Circuit Breaker Distribution Board & Self-Healing Sentinel**  
> டெர்மினல் கட்டளைகள் இல்லாமலேயே செல்போன் வழியாக சர்வர் மவுண்ட்கள், இணையதளங்கள், மற்றும் சிஸ்டம் சேவைகளை நேரடியாக ஆன்/ஆஃப் செய்து நிர்வகிக்கும் நவீன டாஷ்போர்டு.

---

## 📌 கண்ணோட்டம் (Overview)

வீடுகளில் உள்ள மின்வாரிய MCB (Miniature Circuit Breaker) விநியோகப் பலகை போன்று, லினக்ஸ் சர்வரில் இயங்கும் சேவைகள், சேமிப்பக மவுண்ட்கள் (Mounts), மற்றும் 13-க்கும் மேற்பட்ட இணையதளங்களை இயற்பியல் விசை வடிவில் (Tactile Levers) கட்டுப்படுத்த இந்த அமைப்பு உருவாக்கப்பட்டுள்ளது.

* **Frontend:** தனித்தன்மை வாய்ந்த இன்டஸ்ட்ரியல் UI (HTML5, Tailwind CSS, Web Audio API).
* **Backend Agent:** பாதுகாப்பான REST API கொண்ட Python 3 Flask டெமான் (`server_agent.py`).
* **Networking:** Cloudflare Zero Trust Tunnel (`cloudflared`) வழியே பாதுகாப்பான இணைப்பு.
* **Authentication:** Bearer Token பாதுகாப்பு நெறிமுறை.

---

## 🛠️ கட்டமைப்பு (Architecture)

```text
[ மொபைல் / பிரவுசர் UI ]
       │
       ▼ (HTTPS)
[ Cloudflare Tunnel: breaker.corepulse.in ]
       │
       ▼ (Local Port Forwarding)
[ 127.0.0.1:5005 (Flask Daemon: mcb-agent.service) ]
       │
       ├──► Storage Mounts (/mnt/storage, /mnt/backup)
       ├──► Nginx Reverse Proxy & 13+ Virtual Hosts
       ├──► Systemd Daemons (Tailscale, Docker, PostgreSQL)
       └──► Live Telemetry (CPU, RAM, Disk I/O)