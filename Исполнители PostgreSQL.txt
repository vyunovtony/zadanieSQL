-- Создание таблицы жанров
CREATE TABLE genres (
    id SERIAL PRIMARY KEY,
    name VARCHAR(255) NOT NULL
);

-- Создание таблицы исполнителей
CREATE TABLE performers (
    id SERIAL PRIMARY KEY,
    name VARCHAR(255) NOT NULL
);

-- Создание таблицы связей между исполнителями и жанрами
CREATE TABLE performer_genres (
    performer_id INTEGER NOT NULL,
    genre_id INTEGER NOT NULL,
    PRIMARY KEY (performer_id, genre_id),
    FOREIGN KEY (performer_id) REFERENCES performers(id),
    FOREIGN KEY (genre_id) REFERENCES genres(id)
);

-- Создание таблицы альбомов
CREATE TABLE albums (
    id SERIAL PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    release_date DATE NOT NULL
);

-- Создание таблицы связей между исполнителями и альбомами
CREATE TABLE performer_albums (
    performer_id INTEGER NOT NULL,
    album_id INTEGER NOT NULL,
    PRIMARY KEY (performer_id, album_id),
    FOREIGN KEY (performer_id) REFERENCES performers(id),
    FOREIGN KEY (album_id) REFERENCES albums(id)
);

-- Создание таблицы треков
CREATE TABLE tracks (
    id SERIAL PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    duration INTERVAL NOT NULL,
    album_id INTEGER NOT NULL,
    FOREIGN KEY (album_id) REFERENCES albums(id)
);

-- Создание таблицы сборников
CREATE TABLE collections (
    id SERIAL PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    release_year INTEGER NOT NULL
);

-- Создание таблицы связей между треками и сборниками
CREATE TABLE track_collections (
    track_id INTEGER NOT NULL,
    collection_id INTEGER NOT NULL,
    PRIMARY KEY (track_id, collection_id),
    FOREIGN KEY (track_id) REFERENCES tracks(id),
    FOREIGN KEY (collection_id) REFERENCES collections(id)
);