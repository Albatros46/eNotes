# eNotes
E-Notes Project – Real Time Project
-------------------------------------------------------------------------------------
Technology Stack:
Backend – Spring Boot REST, JPA, AOP, Logging, Actuator, Security, OAuth Login, Caching, Junit & Mockito, Sonar cube, JMeter, Swagger, Schedular, Docker, GitHub 
Frontend – Angular / React
DB – MySQL 
Tools – GitHub, STS, Figma
Deploy Server- AWS 

Functionality & Features:
    1. User Authentication and Authorization:
    • User Registration (with email verification).
    • User Login (JWT-based token authentication).
    • Role-based access control (Admin, User)

    2. Notes Management

    • Create, update, and delete categories.
    • View and filter notes by category.
    • Create, edit, and delete notes.
    • Save notes with file attachments (PDF, images, etc.)
    • Display or download attached files within notes.
    • Paginated view for notes.
    • Search for notes (search by title, content, category, etc.)
    • Mark notes as favorite.
    • View a list of favorite notes.
    • Copy Notes
    • Export All Notes and Single Notes in Excel or PDF format

    -- Veritabanı oluşturma
--USING eNotes;

-- Veritabanına bağlanma
--\c eNotes;

-- User tablosu
CREATE TABLE AppUser (
    id INTEGER PRIMARY KEY GENERATED ALWAYS AS IDENTITY,
    firstName VARCHAR(50),
    lastName VARCHAR(50),
    email VARCHAR(100) UNIQUE NOT NULL,
    password VARCHAR(100) NOT NULL,
    mobNu VARCHAR(15),
    roles VARCHAR(100)
);

-- Category tablosu
CREATE TABLE Category (
    id INTEGER PRIMARY KEY GENERATED ALWAYS AS IDENTITY,
    name VARCHAR(100) NOT NULL,
    isActive BOOLEAN DEFAULT TRUE,
    isDelete BOOLEAN DEFAULT FALSE,
    createdBy INTEGER REFERENCES AppUser(id),
    createdDate TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updatedBy INTEGER REFERENCES AppUser(id),
    updatedDate TIMESTAMP
);

-- File tablosu
CREATE TABLE File (
    id INTEGER PRIMARY KEY GENERATED ALWAYS AS IDENTITY,
    originalName VARCHAR(255),
    uploadFileName VARCHAR(255),
    displayFileName VARCHAR(255),
    fileSize BIGINT,
    path VARCHAR(255)
);

-- ToDo tablosu
CREATE TABLE ToDo (
    id INTEGER PRIMARY KEY GENERATED ALWAYS AS IDENTITY,
    title VARCHAR(255) NOT NULL,
    description TEXT,
    priority INTEGER,
    status VARCHAR(50),
    publishDate TIMESTAMP,
    lastUpdateDate TIMESTAMP,
    userId INTEGER REFERENCES AppUser(id) -- User ile ilişkilendirme
);

-- Notes tablosu
CREATE TABLE Notes (
    id INTEGER PRIMARY KEY GENERATED ALWAYS AS IDENTITY,
    title VARCHAR(255) NOT NULL,
    description TEXT,
    category INTEGER REFERENCES Category(id),
    userId INTEGER REFERENCES AppUser(id), -- User ile ilişkilendirme
    publishDate TIMESTAMP,
    lastUpdateDate TIMESTAMP,
    fileId INTEGER REFERENCES File(id) -- File ile ilişkilendirme
);

