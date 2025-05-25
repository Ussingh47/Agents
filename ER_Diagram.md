# Entity-Relationship Diagram (ERD) - Collaborative Coding Platform

## Overview

This document presents the Entity-Relationship Diagram for the Collaborative Coding Platform following traditional ER diagram notation rules. The ERD uses proper symbols: rectangles for entities, diamonds for relationships, ellipses for attributes, and parallelograms for weak entities.

## ER Diagram

```
                    ┌─────────────┐
                    │   user_id   │ ◄─── Primary Key
                    └──────┬──────┘
                           │
                    ┌──────▼──────┐
                    │             │
                    │    USER     │ ◄─── Strong Entity
                    │             │
                    └──────┬──────┘
                           │
        ┌──────────────────┼──────────────────┐
        │                  │                  │
   ┌────▼────┐       ┌─────▼─────┐      ┌────▼────┐
   │  email  │       │ username  │      │password │
   │(unique) │       │           │      │  hash   │
   └─────────┘       └───────────┘      └─────────┘

                           │
                           │ 1
                    ┌──────▼──────┐
                    │             │
                    │   HAS       │ ◄─── Relationship
                    │             │
                    └──────┬──────┘
                           │ M
                    ┌──────▼──────┐
                    │             │
                    │   SESSION   │ ◄─── Strong Entity
                    │             │
                    └──────┬──────┘
                           │
        ┌──────────────────┼──────────────────┐
        │                  │                  │
   ┌────▼────┐       ┌─────▼─────┐      ┌────▼────┐
   │session  │       │jwt_token  │      │expires  │
   │   id    │       │           │      │   at    │
   └─────────┘       └───────────┘      └─────────┘


                    ┌─────────────┐
                    │ project_id  │ ◄─── Primary Key
                    └──────┬──────┘
                           │
                    ┌──────▼──────┐
                    │             │
                    │   PROJECT   │ ◄─── Strong Entity
                    │             │
                    └──────┬──────┘
                           │
        ┌──────────────────┼──────────────────┐
        │                  │                  │
   ┌────▼────┐       ┌─────▼─────┐      ┌────▼────┐
   │project  │       │description│      │is_public│
   │  name   │       │           │      │         │
   └─────────┘       └───────────┘      └─────────┘

                           │
                           │ M
                    ┌──────▼──────┐
                    │             │
                    │  MEMBER_OF  │ ◄─── Relationship (M:N)
                    │             │
                    └──────┬──────┘
                           │ N
                           │
                    ┌──────▼──────┐
                    │             │
                    │    USER     │ ◄─── (Connected above)
                    │             │
                    └─────────────┘

                    ┌─────────────┐
                    │    role     │ ◄─── Relationship Attribute
                    └──────┬──────┘
                           │
                    ┌──────▼──────┐
                    │             │
                    │  MEMBER_OF  │
                    │             │
                    └─────────────┘


                    ┌─────────────┐
                    │   file_id   │ ◄─── Primary Key
                    └──────┬──────┘
                           │
                    ┌──────▼──────┐
                    │             │
                    │    FILE     │ ◄─── Strong Entity
                    │             │
                    └──────┬──────┘
                           │
        ┌──────────────────┼──────────────────┐
        │                  │                  │
   ┌────▼────┐       ┌─────▼─────┐      ┌────▼────┐
   │file_name│       │file_path  │      │file_type│
   │         │       │           │      │         │
   └─────────┘       └───────────┘      └─────────┘

                           │
                           │ 1
                    ┌──────▼──────┐
                    │             │
                    │  CONTAINS   │ ◄─── Relationship
                    │             │
                    └──────┬──────┘
                           │ M
                           │
                    ┌──────▼──────┐
                    │             │
                    │   PROJECT   │ ◄─── (Connected above)
                    │             │
                    └─────────────┘


                    ┌─────────────┐
                    │ version_id  │ ◄─── Partial Key
                    └──────┬──────┘
                           │
                   ╔═══════▼═══════╗
                   ║               ║
                   ║ FILE_VERSION  ║ ◄─── Weak Entity
                   ║               ║
                   ╚═══════┬═══════╝
                           │
        ┌──────────────────┼──────────────────┐
        │                  │                  │
   ┌────▼────┐       ┌─────▼─────┐      ┌────▼────┐
   │version  │       │content    │      │commit   │
   │ number  │       │   diff    │      │message  │
   └─────────┘       └───────────┘      └─────────┘

                           │
                           │ 1
                   ╔═══════▼═══════╗
                   ║               ║
                   ║   VERSIONED   ║ ◄─── Identifying Relationship
                   ║               ║
                   ╚═══════┬═══════╝
                           │ M
                    ┌──────▼──────┐
                    │             │
                    │    FILE     │ ◄─── (Connected above)
                    │             │
                    └─────────────┘


                    ┌─────────────┐
                    │ message_id  │ ◄─── Primary Key
                    └──────┬──────┘
                           │
                    ┌──────▼──────┐
                    │             │
                    │   MESSAGE   │ ◄─── Strong Entity
                    │             │
                    └──────┬──────┘
                           │
        ┌──────────────────┼──────────────────┐
        │                  │                  │
   ┌────▼────┐       ┌─────▼─────┐      ┌────▼────┐
   │message  │       │ content   │      │timestamp│
   │  type   │       │           │      │         │
   └─────────┘       └───────────┘      └─────────┘

                           │
                           │ 1
                    ┌──────▼──────┐
                    │             │
                    │ GENERATES   │ ◄─── Relationship
                    │             │
                    └──────┬──────┘
                           │ 1
                    ┌──────▼──────┐
                    │             │
                    │ AI_REQUEST  │ ◄─── Strong Entity
                    │             │
                    └──────┬──────┘
                           │
        ┌──────────────────┼──────────────────┐
        │                  │                  │
   ┌────▼────┐       ┌─────▼─────┐      ┌────▼────┐
   │ prompt  │       │ai_response│      │ status  │
   │         │       │           │      │         │
   └─────────┘       └───────────┘      └─────────┘
```

## ER Diagram Notation Legend

### Symbols Used:
- **Rectangles** (┌─┐): Strong Entities
- **Double Rectangles** (╔═╗): Weak Entities
- **Diamonds** (◊): Relationships
- **Double Diamonds** (◊◊): Identifying Relationships
- **Ellipses** (○): Attributes
- **Underlined**: Primary Key attributes
- **Dashed Ellipses**: Derived attributes

## Entity Descriptions

### 1. USER (Strong Entity)
- **Primary Key**: user_id
- **Attributes**:
  - email (unique)
  - username
  - password_hash
- **Purpose**: Stores user account information

### 2. SESSION (Strong Entity)
- **Primary Key**: session_id
- **Attributes**:
  - jwt_token
  - expires_at
- **Purpose**: Manages user authentication sessions

### 3. PROJECT (Strong Entity)
- **Primary Key**: project_id
- **Attributes**:
  - project_name
  - description
  - is_public
- **Purpose**: Stores project information

### 4. FILE (Strong Entity)
- **Primary Key**: file_id
- **Attributes**:
  - file_name
  - file_path
  - file_type
- **Purpose**: Stores file information within projects

### 5. FILE_VERSION (Weak Entity)
- **Partial Key**: version_id
- **Attributes**:
  - version_number
  - content_diff
  - commit_message
- **Purpose**: Tracks file version history
- **Depends on**: FILE entity

### 6. MESSAGE (Strong Entity)
- **Primary Key**: message_id
- **Attributes**:
  - message_type
  - content
  - timestamp
- **Purpose**: Stores communication messages

### 7. AI_REQUEST (Strong Entity)
- **Primary Key**: request_id
- **Attributes**:
  - prompt
  - ai_response
  - status
- **Purpose**: Tracks AI assistance requests

## Relationships

### 1. HAS (USER → SESSION)
- **Type**: One-to-Many (1:M)
- **Description**: One user can have multiple active sessions

### 2. MEMBER_OF (USER ↔ PROJECT)
- **Type**: Many-to-Many (M:N)
- **Attributes**: role
- **Description**: Users can be members of multiple projects

### 3. CONTAINS (PROJECT → FILE)
- **Type**: One-to-Many (1:M)
- **Description**: Each project contains multiple files

### 4. VERSIONED (FILE → FILE_VERSION)
- **Type**: Identifying Relationship (1:M)
- **Description**: Files have multiple versions, versions cannot exist without files

### 5. GENERATES (MESSAGE → AI_REQUEST)
- **Type**: One-to-One (1:1)
- **Description**: AI requests are generated from specific messages

## Key Features

✅ **Proper ER Notation**: Uses standard symbols and conventions
✅ **Weak Entity**: FILE_VERSION depends on FILE
✅ **Identifying Relationship**: VERSIONED relationship
✅ **Many-to-Many**: USER and PROJECT relationship
✅ **Relationship Attributes**: Role attribute on MEMBER_OF
✅ **Primary Keys**: Clearly identified for all entities

This simplified ER diagram follows traditional ER modeling rules and captures the core entities and relationships needed for the collaborative coding platform based on the DFD requirements.

