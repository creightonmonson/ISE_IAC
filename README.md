# Cisco ISE: Security as Code Framework 
### *Automating Network Access Control with Ansible and CI/CD*

This repository demonstrates the transition from manual, GUI-driven administration of **Cisco Identity Services Engine (ISE)** to a modern, version-controlled **Infrastructure as Code (IaC)** workflow. 

By leveraging the `cisco.ise` Ansible collection, we treat our security policy, network inventory, and identity tags as data—enabling rapid deployment, auditability, and consistency across the enterprise.



---

## 🎯 Demo Use Cases

This project showcases three high-value automation pillars in under 5 minutes:

1.  **Network Device Onboarding:** Zero-touch provisioning of switches and routers into the ISE inventory with correct Location and Device Type categorization.
2.  **Identity Micro-segmentation (SGTs):** Defining Scalable Group Tags (TrustSec) as code, allowing for identity-based policy without reliance on IP addresses.
3.  **Policy & Authorization Profiles:** Building Downloadable ACLs (dACLs) and binding them to Authorization Profiles, creating a "set-and-forget" security posture.

---

## 🛠 Project Structure

The repo follows an **modular design**, separating configuration data from the automation logic. This ensures that the playbooks remain generic while the variables define the environment. This allows for built in scalability - the variable files are the source of truth and future changes are handled by changing variable files

```text
.
├── ISE_hosts.yml           # Inventory file (Source of Truth)
├── ansible.cfg             # Optimized runtime settings 
├── group_vars/
│   └── ise_hosts.yml       # Credential management 
├── host_vars/
│   └── ise_host1           # host and role specifc variables
│       └── network_device_variables.yml 
│       └── authorization_policy_variables.yml
│       └── security_group_tag_variables.yml
└── roles/
    ├── network_devices/    # Use Case 1: Infrastructure Onboarding
    │   └── tasks/main.yml
    ├── security_groups/    # Use Case 2: Identity (SGTs)
    │   └── tasks/main.yml
    └── auth_profiles/      # Use Case 3: Policy (dACLs/profiles)
        └── tasks/main.yml
```
## 🚀 Getting Started

### 1. Prerequisites
Ensure you have the required Python SDK and Ansible collection installed on your control node:

```bash
pip install ciscoisesdk
ansible-galaxy collection install cisco.ise:3.0.1 --force
```
### 2. Configure Credentials
Update group_vars/ise_hosts.yml with your ISE node details. Note: Ensure to have configured API settings on your ISE node and enable ERS

### 3. Run the Playbook
```bash
ansible-playbook network_devices_deploy.yml
```

## Why Automate ISE?
Eliminate Human Error: Stop "fat-fingering" dACLs and shared secrets. If it's in the YAML, it's in the network.

Auditability: Every change is tracked in Git. You know who changed a policy and why through commit history.

Scalability: Onboard 1 or 1,000 devices in the same amount of time.

Infrastructure as Code: Move security away from a "black box" and into a peer-reviewed, documented workflow.

## 📈 Roadmap to CI/CD
[x] Stage 1: Basic Task Automation (Current Demo)

[ ] Stage 2: Git-based Pull Requests (Policy Peer Review)

[ ] Stage 3: Automated Linting and Pre-flight checks

[ ] Stage 4: Full Pipeline Integration (GitHub Workflows, MCP integration, AWX)