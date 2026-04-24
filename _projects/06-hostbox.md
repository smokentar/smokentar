---
title: "Hostbox"
excerpt: "is a single-tenant booking engine built with Next.js and SQLite, enabling direct reservations, payments, and fully branded websites for short-term rental operators."
collection: projects
tags:
  - Next.js
  - SQLite
  - Stripe
  - Docker
---

_View live at [luxeambra.com](https://luxeambra.com)._<br>

## Overview

Hostbox is a self-hosted booking engine for short-term rentals.<br/>
Run your own direct booking website. No marketplace fees. Full control.

## Features

**Direct payments** allow guided onboarding through Stripe Connect. Funds are transferred directly to the host's account.

**Reservation management** provides a unified interface for creating, updating, and cancelling reservations.

**Dynamic views** allow the frontend to automatically adapt between single or multi-property modes based on the number of properties.

**Automated emails** are sent automatically when a transaction occurs (e.g. booking confirmations, cancellations, notifications).

**Calendar integration** periodically pulls remote calendars and exposes its own feeds in iCal format.

## Architecture

The system is monolithic and single-tenant. It runs in a Docker container including the Next.js application and a file-based SQLite database.<br/>

Low complexity, simple backups, horizontal scaling.

### Frontend

A public-facing property booking interface is paired with a secure admin dashboard for user-friendly management of listings, reservations, pricing, and more.

The UI dynamically switches between single- and multi-property modes depending on the number of listings.

### Backend

Server-side logic and API routes are used to handle:

- Booking lifecycle management
- Payment orchestration (via Stripe)
- Calendar synchronisation jobs
- Property setup (image uploads, pricing, taxes, rules, etc.)
- Automated emails to both guests and hosts

### Security

Authentication is handled via HTTP-only cookies for admin sessions, with token generation and validation. Payment operations are delegated to Stripe to minimise PCI scope.

### Storage

Each container requires a dedicated SQLite database stored as a file on disk.<br>
File storage (e.g. images) is handled in a specific directory, attached to the container's persistent volume.<br>
Images are automatically compressed before being stored.

### Containers & Deployment

The entire application comes in a single Docker container. An Nginx service can be used as a front to one or multiple containers, terminatign SSL and distributing traffic based on host header.
SSl certificates can be generated with Let's Encrypt.

## Summary

Hostbox is not a marketplace replacement, but a complementary system that provides a direct booking channel.
