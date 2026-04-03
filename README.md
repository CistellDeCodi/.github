# 🧺 CistellDeCodi | Operations Center

Centralized management for the **@srustullet** ecosystem. Designed for logical efficiency and automated auditing.

## 🚀 The Master Command
To run the entire synchronization and auditing flow with a single entry point, use the orchestrator:
`~/cistell_orchestrator.sh`

## 🛠️ Infrastructure & Fleet Components

| Script | Role | Context |
| :--- | :--- | :--- |
| **`cistell_orchestrator.sh`** | **The Brain.** | Coordinates Setup, Sync, and Audit stages in sequence. |
| **`cistell_setup.sh`** | **Provisioning.** | Creates organization repos, clones missing folders, and sets git aliases. |
| **`cistell_sync_all.sh`** | **Execution.** | Mass synchronization of code (pull/push) across all managed repositories. |
| **`issues_to_cistell.sh`** | **Auditing.** | Automatically syncs open issues to the [Project 4 Board](https://github.com/orgs/CistellDeCodi/projects/4). |

## ⚙️ Global Aliases
This ecosystem enables the `git basket` command globally to handle multi-remote pushes:
`git config --global alias.basket '!git pull origin main && git push origin main && git push org main'`

---
*Built for Minimum Friction & Maximum Logical Efficiency | @srustullet*
