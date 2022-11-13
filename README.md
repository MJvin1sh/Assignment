# Assignment

CREATE TABLE Instruments (
                Name VARCHAR(30) NOT NULL,
                Pitch INTEGER NOT NULL,
                CONSTRAINT name PRIMARY KEY (Name)
);


CREATE TABLE Address (
                AddressID INTEGER NOT NULL,
                Number INTEGER NOT NULL,
                Street1 VARCHAR(50) NOT NULL,
                ZIP Code INTEGER NOT NULL,
                State VARCHAR(20) NOT NULL,
                City VARCHAR(20) NOT NULL,
                Street2 VARCHAR(50) NOT NULL,
                CONSTRAINT addressid PRIMARY KEY (AddressID)
);


CREATE TABLE Musician (
                SSN INTEGER NOT NULL,
                AddressID INTEGER NOT NULL,
                Title VARCHAR(30) NOT NULL,
                Name VARCHAR(30) NOT NULL,
                AlbumID INTEGER NOT NULL,
                CONSTRAINT ssn PRIMARY KEY (SSN, AddressID, Title, Name, AlbumID)
);


CREATE TABLE Song (
                Title VARCHAR(30) NOT NULL,
                Name VARCHAR(30) NOT NULL,
                SSN INTEGER NOT NULL,
                AddressID INTEGER NOT NULL,
                Length INTEGER NOT NULL,
                AlbumID INTEGER NOT NULL,
                CONSTRAINT title PRIMARY KEY (Title, Name, SSN, AddressID)
);


CREATE TABLE Album (
                AlbumID INTEGER NOT NULL,
                SSN INTEGER NOT NULL,
                AddressID INTEGER NOT NULL,
                Title VARCHAR(30) NOT NULL,
                Name VARCHAR(30) NOT NULL,
                Release_Date TIMESTAMP NOT NULL,
                Format VARCHAR(30) NOT NULL,
                Age INTEGER NOT NULL,
                CONSTRAINT albumid PRIMARY KEY (AlbumID, SSN, AddressID, Title, Name)
);


CREATE TABLE Musician_instrument (
                AddressID VARCHAR NOT NULL,
                SSN INTEGER NOT NULL,
                Musician_AddressID INTEGER NOT NULL,
                Name VARCHAR(30) NOT NULL,
                CONSTRAINT addressid__ssn PRIMARY KEY (AddressID, SSN)
);


ALTER TABLE Musician_instrument ADD CONSTRAINT musician_instrument_instruments_fk
FOREIGN KEY (Name)
REFERENCES Instruments (Name)
ON DELETE NO ACTION
ON UPDATE NO ACTION
NOT DEFERRABLE;

ALTER TABLE Song ADD CONSTRAINT instruments_song_fk
FOREIGN KEY (Name)
REFERENCES Instruments (Name)
ON DELETE NO ACTION
ON UPDATE NO ACTION
NOT DEFERRABLE;

ALTER TABLE Musician ADD CONSTRAINT address_musician_fk
FOREIGN KEY (AddressID)
REFERENCES Address (AddressID)
ON DELETE NO ACTION
ON UPDATE NO ACTION
NOT DEFERRABLE;

ALTER TABLE Musician_instrument ADD CONSTRAINT musician_musician_instrument_fk
FOREIGN KEY (SSN, Musician_AddressID)
REFERENCES Musician (SSN, AddressID)
ON DELETE NO ACTION
ON UPDATE NO ACTION
NOT DEFERRABLE;

ALTER TABLE Song ADD CONSTRAINT musician_song_fk
FOREIGN KEY (SSN, AddressID)
REFERENCES Musician (SSN, AddressID)
ON DELETE NO ACTION
ON UPDATE NO ACTION
NOT DEFERRABLE;

ALTER TABLE Album ADD CONSTRAINT musician_album_fk
FOREIGN KEY (SSN, AddressID, Title, Name)
REFERENCES Musician (SSN, AddressID, Title, Name)
ON DELETE NO ACTION
ON UPDATE NO ACTION
NOT DEFERRABLE;

ALTER TABLE Musician ADD CONSTRAINT song_musician_fk
FOREIGN KEY (Name, AddressID, Title, SSN)
REFERENCES Song (Name, AddressID, Title, SSN)
ON DELETE NO ACTION
ON UPDATE NO ACTION
NOT DEFERRABLE;

ALTER TABLE Album ADD CONSTRAINT song_album_fk
FOREIGN KEY (Name, AddressID, Title, SSN)
REFERENCES Song (Name, AddressID, Title, SSN)
ON DELETE NO ACTION
ON UPDATE NO ACTION
NOT DEFERRABLE;

ALTER TABLE Song ADD CONSTRAINT album_song_fk
FOREIGN KEY (SSN, AddressID, Title, AlbumID, Name)
REFERENCES Album (SSN, AddressID, Title, AlbumID, Name)
ON DELETE NO ACTION
ON UPDATE NO ACTION
NOT DEFERRABLE;

ALTER TABLE Musician ADD CONSTRAINT album_musician_fk
FOREIGN KEY (SSN, AddressID, Title, AlbumID, Name)
REFERENCES Album (SSN, AddressID, Title, AlbumID, Name)
ON DELETE NO ACTION
ON UPDATE NO ACTION
NOT DEFERRABLE;
