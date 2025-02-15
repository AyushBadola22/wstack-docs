---
id: database-schema
title: Database Schema
sidebar_label: Database Schema
---

# Database Schema

This document provides an overview of the database schema used in the project. The database schema defines the structure of the database, including tables, columns, and relationships between tables.

## Tables

### Users

- `id`: Primary key, integer
- `username`: Unique, string
- `email`: Unique, string
- `password`: String
- `created_at`: Timestamp
- `updated_at`: Timestamp

### Posts

- `id`: Primary key, integer
- `user_id`: Foreign key, integer
- `title`: String
- `content`: Text
- `created_at`: Timestamp
- `updated_at`: Timestamp

### Comments

- `id`: Primary key, integer
- `post_id`: Foreign key, integer
- `user_id`: Foreign key, integer
- `content`: Text
- `created_at`: Timestamp
- `updated_at`: Timestamp

## Relationships

- A user can have multiple posts.
- A post can have multiple comments.
- A comment belongs to a single post and a single user.
