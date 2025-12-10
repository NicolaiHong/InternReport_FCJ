---
title: "Blog 1"
date: "2025-10-10"
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# How We Built a Flywheel to Steadily Improve Security for Amazon RDS

> by Joshua Brindle

This blog details the process an AWS security team undertook to secure a new feature, **PL/Rust**, on **Amazon Relational Database Service (Amazon RDS)**. The author, a principal security engineer, explains how the team moved beyond a simple implementation to build a comprehensive, self-improving security system—a "flywheel"—that combines technology, process, and testing to protect customers.

---

## The Pieces of the System

The project's central component was **PL/Rust**, an extension that allows users to write custom PostgreSQL functions in **Rust** that are then compiled into highly performant native machine code. The core of this extension is a library called **postgrestd**, which was designed to prevent database escapes. However, at the time, the library was new and had not yet been hardened for the realities of a large-scale production environment.
<br><br>
The primary security challenge arose from the fact that PL/Rust compiles these extensions directly on the database instance itself. This design requires a full development toolchain to be locally available, significantly increasing the potential risk. A poorly constructed extension could destabilize the database or its host instance, and attackers could use various techniques to try and bypass security controls like the **write xor execute (W^X)** model. This context made it clear that a series of robust mitigations were necessary to provide this functionality to customers safely.

---

## Challenging the Approach

The AWS culture of obsessing over operational excellence—with a focus on automation, resilience, and simplicity—heavily influenced the search for a solution. The team considered **SELinux (Security-Enhanced Linux)**, which was described as a long-debated option. SELinux is a set of kernel features that enforces **mandatory access control (MAC)**, adding a powerful layer of protection on top of the standard authorization system. Using SELinux policies, an administrator can be extremely specific about what is allowed on a system, for instance, by preventing a process from writing to a file even if its ownership permissions would normally permit it.
<br><br>
This level of deterministic control can greatly increase an operating system's security. The trade-off, however, is reduced flexibility and the significant effort required to configure the access controls to meet specific security requirements. After a thorough internal debate, which involved senior leaders challenging the idea to anticipate future issues, the team agreed that for the PL/Rust use case, the benefits of SELinux outweighed the downsides. The decision was made to proceed with this approach.

---

## Building the Security Flywheel

Simply implementing a tool wasn't enough; the team built a complete, constantly improving process around it.

1.  **Enforce and Monitor**: They built the SELinux environment and created policies to lock down the system. Crucially, they configured these policies to send any **denial messages** to their internal telemetry systems for analysis.
2.  **Respond**: Working with the internal blue team, they developed specific **incident response playbooks** for the Amazon RDS team to investigate these denial messages.
3.  **Test and Refine**: The team began running quarterly **"game days"**. During these exercises, the red team would stage exploits against the system, and the service team would respond using their playbooks. Afterwards, all teams would analyze the response to find bottlenecks and areas for improvement.

This cycle of enforcement, monitoring, response, and testing created a strong, well-oiled security machine.

---

## The Flywheel in Action: A Real-World Example

The effectiveness of this system was validated in a production environment. An SELinux denial message automatically generated a high-severity ticket for the service team. The system had worked as expected—it successfully blocked an unauthorized activity, acting as a proactive intrusion detection system.
<br><br>
Even though the immediate risk was neutralized, the team's process required them to investigate the root cause to see if the system could be improved further. The investigation eventually revealed that the activity was initiated by the research team at Varonis Threat Labs. AWS security then reached out to them to collaborate, demonstrating how a security event can lead to positive engagement with the research community. This incident provided a concrete and rewarding example of how the team's work directly benefited customers.

> For the security engineers involved, this was deeply validating, as it provided a concrete example of how their proactive work directly benefited customers by preventing a potential issue.
