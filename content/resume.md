+++
title = "Resume"
path = "resume"
template = "page.html"
[extra]
eyebrow = "Resume"
printable = true
+++

<div class="role" style="justify-content: space-between;">
  <div>
    <h2 style="margin: 0; border: none; padding: 0;">Vinicius Santos</h2>
    <p style="margin: 0.25rem 0 0; color: var(--fg-muted);">
      Backend Engineer · São Paulo, Brazil ·
      <a href="https://www.linkedin.com/in/vinicius-santana-santos/">LinkedIn</a> ·
      <a href="https://github.com/ViniciussSantos">GitHub</a>
    </p>
  </div>
</div>

## Summary

Backend engineer specializing in data infrastructure and performance-critical
systems. I build production tooling in Python and Rust, from analytics pipelines
and security agents to high-throughput data processing, with a focus on
correctness and observable systems.

## Experience

<div class="role">
Software Developer — MixRank
<span class="when">May 2024 — Present</span>
</div>

- Architected a ClickHouse analytics system from the ground up on NixOS, writing custom Nix modules and automated ingestion agents in Python to provide self-serve data access for sales and marketing teams.
- Designed a proactive security monitoring agent in Python to replace legacy auditd alerts, using `/proc` scanning and a custom suppression ruleset to provide fleet-wide visibility with high-trust, curated alerting.
- Overhauled APK download pipelines in Python with concurrent split processing and geo-aware proxy selection, reducing errors and improving data throughput for revenue-driving products.
- Optimized critical data paths using Rust and PyO3 (Rust–Python FFI), including a high-performance Bloom filter and a LinkedIn URL normalization module that corrected long-standing slug truncation bugs across terabytes of data.
- Reduced PostgreSQL resource consumption by 30% by migrating legacy aggregation agents to native `MERGE` commands (PostgreSQL 18), significantly decreasing WAL churn and transaction timeouts.
- Managed complex data lifecycle tasks, including the multi-year deprecation of legacy database tables and the maintenance of Grafana/Graphite clusters for 99.9% dashboard uptime.

<div class="role">
Software Developer Intern — Tokenlab
<span class="when">Aug 2021 — Aug 2023</span>
</div>

- Delivered full-stack and mobile features across multiple client projects using Node.js, GraphQL, React, Angular, and Flutter on AWS, from greenfield builds to legacy maintenance.

## Skills

- **Languages:** Python, Rust, Java, Go, JavaScript/TypeScript, C#, SQL
- **Technologies:** Node.js, React, Angular, GraphQL, Docker, Kubernetes, AWS, PostgreSQL, Redis, Nix/NixOS, ClickHouse, Grafana

## Education

<div class="role">
B.Sc. Computer Science (Dual Degree Program) — Universidade Federal do ABC, Brazil
<span class="when">Dec. 2025</span>
</div>

<div class="role">
B.Sc. Science and Technology (Dual Degree Program) — Universidade Federal do ABC, Brazil
<span class="when">Nov. 2024</span>
</div>

## Projects

- **[UFABC Next](https://github.com/ufabc-next)** — Co-maintainer of a campus application helping 5,000+ students at Universidade Federal do ABC organize class schedules and review professors. Modernized the legacy codebase from ES3 to ES6/TypeScript, improving maintainability and developer experience, and built new features.
- **[RocksDB compaction](https://github.com/ViniciussSantos/rocksdb)** — Developed an adaptive compaction picker within the RocksDB codebase to monitor PMem latency.
