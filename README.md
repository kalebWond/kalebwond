<!-- Header banner -->
<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:0f172a,100:2E5266&height=190&section=header&text=Kaleb%20Tsegaye&fontSize=44&fontColor=ffffff&fontAlignY=36&desc=Full-stack%20engineer%20%C2%B7%20Real-time%20systems%20%C2%B7%20Production%20AI&descSize=16&descAlignY=58" alt="Kaleb Tsegaye banner" />
</p>

<p align="center">
  <img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=500&size=18&pause=1200&color=4A90B8&center=true&vCenter=true&width=620&lines=Event-driven+backends+that+survive+traffic+spikes;AI+features+that+work+in+production%2C+not+just+demos;Interfaces+that+feel+alive" alt="Typing intro" />
</p>

<p align="center">
  <a href="https://www.linkedin.com/in/kaleb-w-tsegaye"><img src="https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn" /></a>
  <a href="mailto:kaleb.wond@gmail.com"><img src="https://img.shields.io/badge/Email-D14836?style=for-the-badge&logo=gmail&logoColor=white" alt="Email" /></a>
  <a href="https://kalebtsegaye.com"><img src="https://img.shields.io/badge/Portfolio-111827?style=for-the-badge&logo=googlechrome&logoColor=white" alt="Portfolio" /></a>
  <a href="https://www.upwork.com/freelancers/~0194405229db0f0abb"><img src="https://img.shields.io/badge/Upwork-14A800?style=for-the-badge&logo=upwork&logoColor=white" alt="Upwork" /></a>
</p>

<p align="center">
  📍 Addis Ababa, Ethiopia (UTC+3) &nbsp;·&nbsp; 🟢 Open to freelance and remote work
</p>

---

## 🧭 What I do

I build web systems that hold up under real traffic, and add AI features that work in production rather than only in demos. Five-plus years across React, Node.js, Java and AWS, with a focus on event-driven backends and fast, animated interfaces.

<table>
  <tr>
    <td width="33%" valign="top">
      <h3>📡 Live at scale</h3>
      A real-time SMS voting platform for a live national TV contest. Java, Spring Boot, Kafka and React, sustaining <b>1,000+ req/sec</b>, peaking above <b>3,000</b>, with <b>zero downtime</b> on air.
    </td>
    <td width="33%" valign="top">
      <h3>🤖 AI in production</h3>
      Claude API integration in a logistics platform. Parses bills of lading across inconsistent formats and powers route suggestions and scheduling-conflict detection.
    </td>
    <td width="33%" valign="top">
      <h3>☁️ Cheaper, faster</h3>
      Migrated a job platform off a low-code tool onto Angular, Node.js and AWS, cutting infrastructure costs by <b>65%</b> while serving <b>500,000+</b> weekly users.
    </td>
  </tr>
</table>

<sub>That work was for employers, so the code is private. The projects below are public.</sub>

---

## 🚀 Featured projects

### 🗳️ Tally — real-time voting pipeline

A vote-processing pipeline with a live leaderboard, modelled on the production system above. The telecom feed is replaced by a controllable load generator, so the whole thing can be demonstrated and load-tested.

**~5,000 votes/sec accepted and ~4,800/sec counted live**, with the entire stack on one 4-core laptop.

```
Go generator → nginx → Ingest API (×2) → Redpanda → Consumers (×2–3) → PostgreSQL + Redis → WebSocket gateway → Live UI
```

- ⚡ The ingest API validates, publishes and returns `202`. Nothing on the hot path touches the database.
- 🔁 Idempotent consumer, a dead-letter topic for unknown codes, and a replayable log.
- 🎞️ Counters animate toward each new total instead of restarting, and rows glide past each other on an overtake.
- 📈 Scales horizontally: add ingest replicas behind nginx, or consumers to the group.

#### 📊 Measured throughput

Everything ran on a single 4-core laptop: the generator, nginx, the ingest replicas, the consumers and all the databases.

| Setup | Votes/sec |
|---|---|
| Full stack: ingest accepted (2 replicas) | ~5,000–5,300 |
| Full stack: counted live (2 consumers) | ~4,300 |
| Full stack: counted live (3 consumers) | ~4,800 |
| Ingest only, consumers stopped (1 replica) | 6,565 |
| Ingest only, consumers stopped (2 replicas) | 7,214 |
| Ingest only, consumers stopped (3 replicas) | 8,263 |

Above the counting rate, votes are still accepted and queue in Redpanda until the consumers catch up, so bursts are absorbed rather than dropped. The ceiling is the laptop's four cores, since every component competes for the same CPU, not the code.

<p>
  <img src="https://img.shields.io/badge/Go-00ADD8?style=flat-square&logo=go&logoColor=white" alt="Go" />
  <img src="https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white" alt="TypeScript" />
  <img src="https://img.shields.io/badge/Next.js-000000?style=flat-square&logo=nextdotjs&logoColor=white" alt="Next.js" />
  <img src="https://img.shields.io/badge/Fastify-202020?style=flat-square&logo=fastify&logoColor=white" alt="Fastify" />
  <img src="https://img.shields.io/badge/Redpanda%20(Kafka%20API)-E4405F?style=flat-square&logo=apachekafka&logoColor=white" alt="Redpanda" />
  <img src="https://img.shields.io/badge/Redis-DC382D?style=flat-square&logo=redis&logoColor=white" alt="Redis" />
  <img src="https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white" alt="PostgreSQL" />
  <img src="https://img.shields.io/badge/nginx-009639?style=flat-square&logo=nginx&logoColor=white" alt="nginx" />
  <img src="https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white" alt="Docker" />
</p>

<a href="https://github.com/kalebWond/tally"><img src="https://img.shields.io/badge/View%20repository-24292F?style=for-the-badge&logo=github&logoColor=white" alt="View Tally repository" /></a>

<br />

### 🎹 PentaScales — an interactive piano for Ethiopian pentatonic scales

Pick a scale, a root and a starting position, then play by mouse, multi-touch or computer keyboard. A "Similar scales" view shows which differently named scales share the same notes.

- 🎧 Web Audio API with sample-accurate scheduling, and pointer events for chords and glissando.
- 🧮 The music theory is pure functions over integers, covered by 20 tests. About 48 kB gzipped.
- 📱 Built for phones: landscape-first, installable, no scrolling.

<p>
  <img src="https://img.shields.io/badge/React-20232A?style=flat-square&logo=react&logoColor=61DAFB" alt="React" />
  <img src="https://img.shields.io/badge/Vite-646CFF?style=flat-square&logo=vite&logoColor=white" alt="Vite" />
  <img src="https://img.shields.io/badge/Web%20Audio%20API-FF6F00?style=flat-square&logo=audiomack&logoColor=white" alt="Web Audio API" />
  <img src="https://img.shields.io/badge/Vitest-6E9F18?style=flat-square&logo=vitest&logoColor=white" alt="Vitest" />
</p>

<a href="https://penta-scale.netlify.app/"><img src="https://img.shields.io/badge/Live%20demo-00C7B7?style=for-the-badge&logo=netlify&logoColor=white" alt="PentaScales live demo" /></a>
<a href="https://github.com/kalebWond/penta-scale-generator"><img src="https://img.shields.io/badge/View%20repository-24292F?style=for-the-badge&logo=github&logoColor=white" alt="View PentaScales repository" /></a>

---

## 🧰 Toolbox

<table>
  <tr>
    <td><b>🎨 Frontend</b></td>
    <td><img src="https://skillicons.dev/icons?i=ts,react,nextjs,angular,tailwind,vite" alt="Frontend tools" /></td>
  </tr>
  <tr>
    <td><b>⚙️ Backend</b></td>
    <td><img src="https://skillicons.dev/icons?i=nodejs,java,spring,go,py" alt="Backend tools" /></td>
  </tr>
  <tr>
    <td><b>🗄️ Data and messaging</b></td>
    <td><img src="https://skillicons.dev/icons?i=postgres,redis,mongodb,kafka" alt="Data and messaging tools" /></td>
  </tr>
  <tr>
    <td><b>☁️ Cloud and DevOps</b></td>
    <td><img src="https://skillicons.dev/icons?i=aws,docker,kubernetes,githubactions" alt="Cloud and DevOps tools" /></td>
  </tr>
</table>

<img src="https://img.shields.io/badge/AWS%20Certified-Solutions%20Architect%20Associate-FF9900?style=for-the-badge&logo=amazonwebservices&logoColor=white" alt="AWS Certified Solutions Architect Associate" />

---

## 🔭 Currently

- 🧠 Building with Claude and other LLM APIs, and exploring multi-agent systems, MCP servers and RAG
- 💼 Taking on freelance projects: real-time backends, AI feature integration, and full-stack builds

Outside of code: aviation ✈️ and history 📜

<!-- Footer wave -->
<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:2E5266,100:0f172a&height=110&section=footer" alt="" />
</p>
