# PROJECT Funky Swarm — VM Architecture

```mermaid
flowchart LR
    User["Paulie + ChatGPT<br/>strategy, task design, review"] --> TG["Telegram Bot<br/>Funky-Swarm control plane"]
    TG --> H["VM 105: Hermes-Lab<br/>10.0.0.102<br/>autonomous execution agent"]

    subgraph P["Proxmox Host — 10.0.0.200"]
        H
        PL["VM 101: Paulie-Lab<br/>10.0.0.88<br/>canonical workspace + restored projects"]
        U["VM 100: Ubuntu-main<br/>general Linux workspace"]
        K["VM 102: Kali-Lab<br/>security tooling"]
        M["VM 103: Metasploitable<br/>safe vulnerable target"]
        SOC["VM 104: Onion SOC<br/>monitoring + telemetry"]
        B["Backup / external storage<br/>SBA hard drive + old Linux files"]
    end

    H -. "SSH / rsync / read-only discovery" .-> PL
    H -. "sandbox project recovery" .-> B
    K -. "approved lab testing only" .-> M
    SOC -. "logs / telemetry" .-> H
    SOC -. "logs / telemetry" .-> K

    classDef control fill:#6d28d9,stroke:#c4b5fd,color:#fff
    classDef hermes fill:#2563eb,stroke:#93c5fd,color:#fff
    classDef canonical fill:#059669,stroke:#6ee7b7,color:#fff
    classDef security fill:#dc2626,stroke:#fecaca,color:#fff
    classDef soc fill:#334155,stroke:#cbd5e1,color:#fff
    classDef storage fill:#f59e0b,stroke:#fde68a,color:#111827

    class User,TG control
    class H hermes
    class PL canonical
    class K,M security
    class SOC soc
    class B storage
```

## Role Summary

| Component | Role |
|---|---|
| **Paulie + ChatGPT** | Strategy, task decomposition, governance, review |
| **Telegram Bot** | Human-in-the-loop control plane for Hermes |
| **Hermes-Lab VM 105** | Autonomous execution agent, sandbox runner, memory, reports |
| **Paulie-Lab VM 101** | Canonical workspace and restored project files |
| **Ubuntu-main VM 100** | General Linux workspace / legacy helper environment |
| **Kali-Lab VM 102** | Security tooling for approved lab testing |
| **Metasploitable VM 103** | Safe vulnerable target for internal testing |
| **Onion SOC VM 104** | Monitoring, telemetry, SOC lab |
| **Backup / SBA HDD** | Historical project backups and old Linux recovery files |

## Operating Principle

Hermes-Lab performs risky or iterative execution inside sandboxes. Paulie-Lab preserves canonical project state. Proxmox remains stable infrastructure.
