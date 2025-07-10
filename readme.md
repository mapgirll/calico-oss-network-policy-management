# Calico Open Source 3.30: Kubernetes Network Policy Management Workshop

## Welcome

In this Calico Open Source focused workshop, you will work with Calico, Calico Whisker, and Calico Cloud Free Tier to learn how implement network security for workloads to reduce the attack surface of applications.  

Cloud-native applications require a modern approach based on the zero-trust principles of identity-based access, least privilege access, and proactively detecting threats and reducing the blast radius in case of a breach.

Calico enables fine-grained, secure workload access controls between your microservices and external databases, cloud services, APIs, and other applications. It also prevents the lateral movement of threats with identity-aware segmentation that works across all of your workload environments, including hosts, VMs, Kubernetes components, and services.

You will come away from this workshop with an understanding of how others in your industry are securing and observing cloud-native applications with Calico, along with best practices that you can implement in your organization.

### Time Requirements

The estimated time to complete this workshop is 60-90 minutes.

### Target Audience

- Cloud Professionals
- DevSecOps Professional
- Site Reliability Engineers (SRE)
- Solutions Architects
- Anyone interested in Calico Cloud :)

### Learning Objectives

1. Learn how to deploy zero-trust workload access controls
2. Learn how to use Calico Whisker to identify network traffic flows
3. Visualize all cluster traffic with Calico Cloud Free Tier
4. Understand how network policy tiers, network sets can enhance and speed up network security and network policy organization.

## Workshop Environment Preparation

> [!WARNING]
> **For this workshop, you are expected to have access to a previously created Calico Open Source cluster.**

If you need to set up a Calico cluster, please refer to the [Calico quickstart guide](https://docs.tigera.io/calico/latest/getting-started/kubernetes/quickstart).

[Module 1 - Getting Started with Whisker](../modules/module-1-getting-started-with-whisker.md) 
[Module 2 - Introducing Tiers](../modules/module-2-introducingtiers.md) 
[Module 3 - Writing Network Policy](../modules/module-3-writing-network-policy.md)  
[Module 4 - Network Policy Best Practices](../modules/module-4-network-policy-best-practices.md) 
[Module 5 - Calico Cloud Free Tier](../modules/module-5-calico-cloud-free-tier.md) 

---

### Useful links

- [Project Calico](https://www.tigera.io/project-calico/)
- [Calico Academy - Get Calico Certified!](https://academy.tigera.io/)
- [O’REILLY EBOOK: Kubernetes security and observability](https://www.tigera.io/lp/kubernetes-security-and-observability-ebook)
- [Calico Users - Slack](https://slack.projectcalico.org/)

### Follow us on social media

- [LinkedIn](https://www.linkedin.com/company/tigera/)
- [Twitter](https://twitter.com/tigeraio)
- [YouTube](https://www.youtube.com/channel/UC8uN3yhpeBeerGNwDiQbcgw/)
- [Slack](https://calicousers.slack.com/)
- [Github](https://github.com/tigera-solutions/)
- [Discuss](https://discuss.projectcalico.tigera.io/)

> **Note**: The examples and sample code provided in this workshop are intended to be consumed as instructional content. These will help you understand how Calico Cloud can be configured to build a functional solution. These examples are not intended for use in production environments.