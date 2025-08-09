# Distributed Denial of Service (DDoS) – Detailed Notes

---

## 1. Introduction
- In **Information Security**, every domain has **unique risks and threats** based on:
  - **Scope**: What the domain covers
  - **Functions**: What it does
  - **Objectives**: What it aims to achieve
  - **Technology**: The systems it uses
  - **Data Sensitivity**: Type and importance of the data it handles
  - **Vulnerabilities**: Weak points in design or operation
- **DDoS** is one of the key threats in the *availability* domain of cybersecurity.

---

## 2. What is a DDoS Attack?
- **Definition**:  
  A **malicious attempt** to disrupt the normal functioning of a website, server, or online service by **flooding it with massive amounts of internet traffic**.
- **Difference from DoS**:
  - **DoS**: Single source of attack
  - **DDoS**: Multiple sources attacking simultaneously
- **Source of Traffic**:  
  Usually from a **botnet** — a network of compromised devices infected with malware.
- **Real-World Analogy**:  
  - Imagine you open a bakery.
  - A huge crowd shows up, blocking entrances and filling the shop, preventing real customers from entering.
  - They don’t want to buy anything — just cause chaos.
  - **Attacker** = The person who gathered and sent the crowd.
  - **Botnet** = The crowd.
  - **Victim** = Your bakery.

---

## 3. Key Components of a DDoS Attack
1. **The Attacker**
   - Coordinates and controls the attack
   - Goal: Overload the target to disrupt service

2. **The Botnet (Amplification Network)**
   - A distributed network of compromised devices:
     - Personal computers
     - Servers
     - IoT devices (smart cameras, thermostats, routers)
   - Owners are often unaware their devices are infected.

3. **The Victim**
   - The server, service, or network targeted for disruption
   - Overwhelmed by incoming traffic

---

## 4. How a DDoS Works
- Attacker sends **commands** to the botnet.
- All compromised devices send **huge volumes of requests** to the target at the same time.
- This:
  - Consumes **bandwidth** (network overload)
  - Consumes **processing power** (CPU overload)
  - Causes **delays or crashes**
- Legitimate users:
  - Experience **slow response times**
  - Sometimes **cannot connect at all**

---

## 5. Real Example – Dyn Attack (2016)
- **Target**: Dyn, a DNS service provider.
- **Effect**:
  - Major sites like **Twitter, Netflix, Reddit** went offline for hours.
  - Impacted parts of **US** and **Europe**.
- **Botnet Used**: Mirai
  - Exploited IoT devices (cameras, routers) to launch the attack.
- **Lesson Learned**:
  - Everyday devices can be hijacked for massive cyberattacks.

---

## 6. Impact of DDoS Attacks
- **Financial Losses**:
  - E-commerce downtime → lost sales
  - Banking services → lost transactions
- **Reputation Damage**:
  - Customer trust eroded
  - Users may move to competitors
- **Operational Disruption**:
  - Essential services interrupted
  - Dependency chain effects (users affected indirectly)
- **Distraction for Other Attacks**:
  - While defending against DDoS, attackers may:
    - Steal data
    - Install malware
    - Create backdoors

---

## 7. Summary
- **DDoS = Distributed attack from multiple sources**
- Uses **botnets** to flood a target
- Goal: Make services **unavailable** to real users
- Can cause **financial**, **reputational**, and **operational** damage
- Sometimes used as a **cover** for deeper intrusions
