CREATE TABLE Articles (
    ArticleId INT PRIMARY KEY IDENTITY(1,1),
    Title VARCHAR(255) NOT NULL,
    Abstract TEXT,
    Keywords VARCHAR(255),
    FullText TEXT,
    PublicationDate DATE,
    DOI VARCHAR(100),
    Url VARCHAR(255)
);

-- Создание таблицы для авторов
CREATE TABLE Authors (
    AuthorId INT PRIMARY KEY IDENTITY(1,1),
    FirstName VARCHAR(50) NOT NULL,
    LastName VARCHAR(50) NOT NULL
);

-- Создание таблицы для журналов
CREATE TABLE Journals (
    JournalId INT PRIMARY KEY IDENTITY(1,1),
    ISSN VARCHAR(10) NOT NULL,
    Name VARCHAR(255) NOT NULL,
    Publisher VARCHAR(255)
);

-- Создание таблицы для связей "Статья-Автор"
CREATE TABLE ArticleAuthors (
    ArticleId INT NOT NULL,
    AuthorId INT NOT NULL,
    PRIMARY KEY (ArticleId, AuthorId),
    FOREIGN KEY (ArticleId) REFERENCES Articles(ArticleId),
    FOREIGN KEY (AuthorId) REFERENCES Authors(AuthorId)
);

-- Создание таблицы для связей "Статья-Журнал"
CREATE TABLE ArticleJournals (
    ArticleId INT NOT NULL,
    JournalId INT NOT NULL,
    PRIMARY KEY (ArticleId, JournalId),
    FOREIGN KEY (ArticleId) REFERENCES Articles(ArticleId),
    FOREIGN KEY (JournalId) REFERENCES Journals(JournalId)
);

-- Пример добавления статьи
INSERT INTO Articles (Title, Abstract, PublicationDate, DOI) VALUES
('New Insights into the Structure of DNA', 'This article presents groundbreaking research...', '2023-03-15', '10.1038/s41586-023-05879-x');

-- Пример добавления автора
INSERT INTO Authors (FirstName, LastName) VALUES
('John', 'Smith');

-- Пример добавления журнала
INSERT INTO Journals (ISSN, Name, Publisher) VALUES
('0028-0836', 'Nature', 'Springer Nature');

-- Пример добавления связи "Статья-Автор"
INSERT INTO ArticleAuthors (ArticleId, AuthorId) VALUES
(1, 1);

-- Пример добавления связи "Статья-Журнал"
INSERT INTO ArticleJournals (ArticleId, JournalId) VALUES
(1, 1);
