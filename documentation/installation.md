# Installation and Lab Environment

## Overview

This document describes the virtual environment used for the Linux Secure Jump Server and Network Security Lab.

## Hardware and Software

- Host computer: MacBook Air
- Host operating system: macOS
- Virtualization software: Oracle VirtualBox
- Server operating system: Ubuntu Server

## Virtual Machines

### Jump Server

- Hostname: jump
- Username: josh
- Role: Secure administrative gateway

### Internal Server

- Hostname: internal
- Username: josh
- IP address: 192.168.50.20
- Role: Protected internal server

## Network Access

The administrative connection follows this path:

MacBook Air → Jump Server → Internal Server

SSH is used to administer both Ubuntu servers.

## Installation Status

Both Ubuntu Server virtual machines have been installed and configured successfully.
