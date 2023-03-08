+++ 
draft = false
date = 2023-03-05T21:23:13Z
title = "sc-100 mindmap"
description = ""
slug = ""
authors = ["dan"]
tags = ["azure", "cybersecurity", "mermaid"]
categories = ["azure", "certification"]
externalLink = ""
series = []
+++

OK, so this mindmap is mental (unless you enjoy a good zoom in-and-out) - but i'll break down each exam objective into sections, which may make it more consumable...


{{<mermaid>}}
mindmap
  root((Azure SC-100 Exam Objectives))
    Design a Zero Trust strategy and architecture
        Build an overall security strategy and architecture
            Identify the integration points in a security architecture by using Microsoft Cybersecurity Reference Architecture MCRA
            Translate business goals into security requirements
            Translate security requirements into technical capabilities, including security services, security products, and security processes
            Design security for a resiliency strategy
            Integrate a hybrid or multitenant environment into a security strategy
            Develop a technical governance strategy for security
        Design a security operations strategy    
            Design a logging and auditing strategy to support security operations
            Develop security operations to support a hybrid or multicloud environment
            Design a strategy for SIEM and SOAR
            Evaluate security workflows
            Evaluate a security operations strategy for incident management lifecycle
            Evaluate a security operations strategy for sharing technical threat intelligence
        Design an identity security strategy
            Design a strategy for access to cloud resources
            Recommend an identity store e.g tenants, B2B, B2C, hybrid
            Recommend an authentication strategy
            Recommend an authorization strategy
            Design a strategy for conditional access
            Design a strategy for role assignment and delegation
            Design security strategy for privileged role access to infrastructure including identity based firewall rules and Privileged Identity Management PIM in Microsoft Azure Active Directory Azure AD, part of Microsoft Entra
            Design security strategy for privileged activities including PAM, entitlement management, cloudtenant administration
    Evaluate Governance Risk Compliance technical strategies and security operations strategies
        Design a regulatory compliance strategy
            Interpret compliance requirements and translate into specific technical capabilities new or existing
            Evaluate infrastructure compliance by using Microsoft Defender for Cloud
            Interpret compliance scores and recommend actions to resolve issues or improve security
            Design implementation of Azure Policy
            Design for data residency requirements
            Translate privacy requirements into requirements for security solutions
        Evaluate security posture and recommend technical strategies to manage risk
            Evaluate security posture by using Azure Security Benchmark
            Evaluate security posture by using Microsoft Defender for Cloud
            Evaluate security posture by using Secure Scores
            Evaluate security posture of cloud workloads
            Design security for an Azure Landing Zone
            Interpret technical threat intelligence and recommend risk mitigations
            Recommend security capabilities or controls to mitigate identified risks
    Design security for infrastructure
        Design a strategy for securing server and client endpoints
            Specify security baselines for server and client endpoints
            Specify security requirements for servers, including multiple platforms and operating systems
            Specify security requirements for mobile devices and clients, including endpoint protection, hardening, and configuration
            Specify requirements to secure Active Directory Domain Services
            Design a strategy to manage secrets, keys, and certificates
            Design a strategy for secure remote access
            Design a strategy for securing privileged access
        Design a strategy for securing SaaS, PaaS, and IaaS services
            Specify security baselines for SaaS, PaaS, and IaaS services
            Specify security requirements for IoT workloads
            Specify security requirements for data workloads, including SQL Server, Azure SQL, Azure Synapse, and Azure Cosmos DB
            Specify security requirements for web workloads, including Azure App Service
            Specify security requirements for storage workloads, including Azure Storage
            Specify security requirements for containers
            Specify security requirements for container orchestration
    Design a strategy for data and applications
        Specify security requirements for applications
            Specify priorities for mitigating threats to applications
            Specify a security standard for onboarding a new application
            Specify a security strategy for applications and APIs
        Design a strategy for securing data
            Specify priorities for mitigating threats to data
            Design a strategy to identify and protect sensitive data
            Specify an encryption standard for data at rest and in motion
    Recommend security best practices and priorities 
        Recommend security best practices by using the Microsoft Cybersecurity Reference Architecture and Azure Security Benchmarks
            Recommend best practices for cybersecurity capabilities and controls
            Recommend best practices for protecting from insider and external attacks
            Recommend best practices for Zero Trust security
            Recommend best practices for Zero Trust Rapid Modernization Plan
        Recommend a secure methodology by using the Cloud Adoption Framework
            Recommend a DevSecOps process
            Recommend a methodology for asset protection
            Recommend strategies for managing and minimizing risk
        Recommend a ransomware strategy by using Microsoft Security Best Practices
            Plan for ransomware protection and extortion based attacks i.e., backup and recovery, limit scope
            Protect assets from ransomware attacks
            Recommend Microsoft ransomware best practices
{{</mermaid>}}