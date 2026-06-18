# TinyAuth - Self-Hosted Authentication Server

**Category**: Software  
**Added**: 2026-06-12  
**Status**: Active  
**Tags**: authentication, authorization, self-hosted, security, identity-management

## Overview

TinyAuth is a lightweight authentication server suitable for self-hosted infrastructure. Could provide centralized auth for various homelab services.

## Problem/Motivation

May be handy for self-hosting scenarios where multiple services need centralized authentication and authorization. Could simplify access management for homelab infrastructure.

## Key Features

- Lightweight auth server
- Self-hosted option
- API-based authentication
- User management
- Suitable for small deployments

## Use Cases

1. **Single Sign-On**: Centralized login for multiple services
2. **Homelab Services**: Auth for internal applications
3. **API Protection**: Secure APIs with token-based auth
4. **User Management**: Centralized user directory

## Potential Integrations

1. **Jellyfin**: Centralized authentication
2. **Open-WebUI**: User management
3. **Frigate**: Secure NVR access
4. **Terax**: IDE authentication
5. **Reverse Proxy**: Protected access to services

## Relevant Resources

- [tinyauthapp/tinyauth](https://github.com/tinyauthapp/tinyauth) — Official repository
- Related topics: [[Security]], [[Self-Hosted Services]], [[Proxmox VE Homelab]], [[Identity Management]]

## Deployment Strategy

### In Proxmox

- [ ] Deploy TinyAuth LXC container
- [ ] Configure database
- [ ] Set up initial users
- [ ] Configure service integrations
- [ ] Test authentication flow
- [ ] Set up backup strategy

### Configuration

- [ ] Admin user creation
- [ ] User groups and roles
- [ ] API token generation
- [ ] LDAP/OAuth integration (if supported)
- [ ] Rate limiting
- [ ] Session management

## Security Considerations

- [ ] TLS encryption for all connections
- [ ] Strong password policies
- [ ] Regular backups
- [ ] Access logging
- [ ] Rate limiting for failed attempts
- [ ] Secure credential storage

## Learning Path

- [ ] Review documentation
- [ ] Test locally in LXC
- [ ] Plan integration architecture
- [ ] Configure service connectors
- [ ] Implement in homelab
- [ ] Document setup and maintenance

---

*See [[AGENTIC_NOTES.md]] for structuring conventions and [[Resources/Links.md]] for link repository.*