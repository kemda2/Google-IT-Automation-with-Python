# Postmortem

Imagine this: You are a software developer for a banking company, and your development team has been informed of a security breach that exposed sensitive client data. Your team immediately conducts a postmortem, or incident analysis. A postmortem examines the impact the breach caused, including the vulnerability of the application; determines updates needed to ensure security best practices for protection from future attacks; and determines a process to protect clients’ data.

In this reading, you will learn more about postmortem, the role it plays in understanding and learning from system failures and incidents, its key components, and its use in software development and infrastructure operations.

## Postmortem

Postmortem is a term typically used in the medical field, but it is also commonly used in the programming world as well. As the name implies, postmortem generally means something bad happened. You might hear other developers call this “putting out a dumpster fire.” It’s a thorough analysis process used after a major incident has occurred—like a system outage or significant disruption. The analysis includes determining what caused the disruption, establishing steps to resolve the problem, and setting plans to prevent future disruptions. For example, a software developer pushes out poorly written code into production. The software developer failed to have the code undergo a peer review. As a result, the database connection misconfiguration broke, which resulted in outages. A postmortem is written up to explain what went wrong and how software developers can prevent the same issue from occuring in the future.

A postmortem process allows teams to understand and learn from system failures and incidents. The purpose of the postmortem process is to understand what happened, why it happened, and how to avoid it again in the future rather than assigning blame to an individual or team.

## Key components

A postmortem report provides clear details of the incident to all team members and promotes a culture of continuous improvement. Key components of a postmortem include:
* Incident timeline: This describes what happened and when it happened. 
* Root cause analysis: This includes details of why the incident happened.
* Impact analysis: This includes details of who and what was affected by the incident. 
* Mitigation and recovery: This includes the steps taken to correct the incident.
* Action items for improvement: This describes the steps to take to prevent a future incident.

Let’s use our banking incident as an example to further explain the components. The incident timeline details the sequence of events from when an application or program was launched to when the disruption occurred. This would be the events that led up to when the security breach occurred. The root cause analysis investigates why the security breach occurred. The impact analysis is an assessment of the number of customers that were impacted by the breach, how their data was exposed, and any potential reputational and financial damages that occurred. Mitigation and recovery are the actions that are taken to stop the breach and to update the code for better security and performance. Action items for improvement explain the strategies the bank will take to prevent similar security breaches from occuring in the future.

A postmortem analysis informs developers which areas of the code need to be updated to create a stronger application. In infrastructure operations, a postmortem analysis is used to learn from a system’s disruption. It identifies weaknesses in the infrastructure and guides the measures to improve resilience.

## Key takeaways

A postmortem or incident analysis provides developers with insights into an unexpected software incident that has occurred. The analysis provides the necessary details needed to determine the root cause of the disruption, why and how it occurred, and who was impacted. These details also allow developers to create a plan to strengthen the software so a disruption will not happen again in the future.
