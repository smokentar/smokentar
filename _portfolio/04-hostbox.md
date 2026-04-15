---
title: "Hostbox"
excerpt: "is a single-tenant booking engine built with Next.js and SQLite, enabling direct reservations, payments, and fully branded websites for short-term rental operators."
collection: portfolio
tags:
  - Next.js
  - SQLite
  - Stripe
  - Docker
---

_View live at [luxeambra.com](https://luxeambra.com)._<br>
_View code and admin dashboard on request._

## Overview

Hostbox is a full-stack booking engine designed to provide short-term rental operators with a self-hosted alternative to marketplaces such as Airbnb and Booking.com.

This system follows a single-tenant container model, where each client runs in an isolated Docker container. Each instance includes a Next.js application and a file-based SQLite database. Low complexity, simple backups, easy horizontal scaling.

## Features

**Direct payments** allow guided onboarding through Stripe Connect. Funds are transferred directly to the host's account.

**Reservation management** provides a unified interface for creating, updating, and cancelling reservations.

**Dynamic views** allow the frontend to automatically adapt between single or multi-property modes based on the number of properties.

**Automated emails** are sent automatically when a transaction occurs (e.g. booking confirmations, cancellations, notifications).

**Calendar integration** periodically pulls remote calendars and exposes its own feeds in iCal format.

## Architecture

### Frontend

The application comprises a monolithic public booking interface and a password-protected admin dashboard. The frontend uses server actions to handle read / write operations.

The website will dynamically switch between single and multi-property views, based on the number of properties added by the user.

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

Each tenant uses a dedicated SQLite database stored as a file on disk.<br>
File storage (e.g. images) is handled in a tenant-specific directory, attached to the container's persistent volume.<br>
Images are automatically compressed before being stored.

### Containers & Deployment

Each client is deployed as an isolated Docker container containing the full application stack.<br>
An Nginx service fronts all containers, terminates SSL and distributes traffic based on host header.<br>
SSL certificates are generated with Let's Encrypt.

## Summary

Hostbox is not a marketplace replacement, but a complementary system that provides a direct booking channel.
