# Database Implementation

This document describes the database persistence layer implementation for the Mergington High School Management System.

## Overview

The application now uses SQLAlchemy ORM with SQLite for data persistence, replacing the previous in-memory storage.

## Database Schema

### Tables

#### `activities`
- `id` (Integer, Primary Key)
- `name` (String, Unique, Indexed)
- `description` (String)
- `schedule` (String)
- `max_participants` (Integer)

#### `participants`
- `id` (Integer, Primary Key)
- `email` (String, Unique, Indexed)

#### `activity_participants` (Association Table)
- `activity_id` (Foreign Key → activities.id)
- `participant_id` (Foreign Key → participants.id)

## Files Structure

```
src/
├── database.py      # Database configuration and session management
├── models.py        # SQLAlchemy models (Activity, Participant)
├── init_db.py       # Database initialization with seed data
└── app.py           # FastAPI endpoints (updated to use database)
```

## Setup Instructions

1. **Install Dependencies**
   ```bash
   pip install -r requirements.txt
   ```

2. **Run the Application**
   The database will be automatically initialized on startup:
   ```bash
   uvicorn src.app:app --reload
   ```

3. **Database File**
   - Database file: `mergington_school.db`
   - Location: Project root directory
   - Automatically created on first run

## Features

### Data Persistence
- All activities and participants are stored in SQLite database
- Data persists across application restarts
- No data loss on server restart

### Seed Data
- Automatically populates database with initial activities on first run
- Includes 9 default activities with sample participants
- Only seeds data if database is empty

### Database Operations
- **Create**: Add new participants when signing up
- **Read**: Retrieve all activities and participants
- **Update**: Modify activity participants
- **Delete**: Remove participants from activities

## Benefits

✅ **Data Persistence** - No data loss on restart
✅ **Data Integrity** - Enforced by database constraints
✅ **Scalability** - Easy to migrate to PostgreSQL for production
✅ **Foundation** - Ready for user authentication and advanced features

## Future Enhancements

- Add Alembic for database migrations
- Implement user authentication tables
- Add indexes for performance optimization
- Support PostgreSQL for production deployment
