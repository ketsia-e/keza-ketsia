# DESCRIPTIONS

## CODES
```SQL
-- Create Users Table
CREATE TABLE Users (
    UserID INT PRIMARY KEY,
    UserName VARCHAR(100),
    Email VARCHAR(100)
);
```SQL
-- Create Roles Table
CREATE TABLE Roles (
    RoleID INT PRIMARY KEY,
    RoleName VARCHAR(100)
);
````SQL
-- Create UserRoles Table (Associative Table)
CREATE TABLE UserRoles (
    UserRoleID INT PRIMARY KEY,
    UserID INT,
    RoleID INT,
    FOREIGN KEY (UserID) REFERENCES Users(UserID),
    FOREIGN KEY (RoleID) REFERENCES Roles(RoleID)
);
```SQL
-- Insert Users
INSERT INTO Users (UserID, UserName, Email) VALUES (1, 'Alice', 'alice@example.com');
INSERT INTO Users (UserID, UserName, Email) VALUES (2, 'Bob', 'bob@example.com');
```SQL
-- Insert Roles
INSERT INTO Roles (RoleID, RoleName) VALUES (1, 'Admin');
INSERT INTO Roles (RoleID, RoleName) VALUES (2, 'User');
```SQL
-- Insert UserRoles
INSERT INTO UserRoles (UserRoleID, UserID, RoleID) VALUES (1, 1, 1); -- Alice as Admin
INSERT INTO UserRoles (UserRoleID, UserID, RoleID) VALUES (2, 1, 2); -- Alice as User
INSERT INTO UserRoles (UserRoleID, UserID, RoleID) VALUES (3, 2, 2); -- Bob as User
```SQL
-- Update User Email
UPDATE Users SET Email = 'alice_new@example.com' WHERE UserID = 1;
````SQL
-- Update Role Name
UPDATE Roles SET RoleName = 'Administrator' WHERE RoleID = 1;
-- Delete a User
DELETE FROM Users WHERE UserID = 2; -- Deleting Bob
````SQL
-- Delete a Role
DELETE FROM Roles WHERE RoleID = 2; -- Deleting User Role
```SQL
-- Retrieve Users with their Roles
SELECT u.UserName, r.RoleName
FROM Users u
JOIN UserRoles ur ON u.UserID = ur.UserID
JOIN Roles r ON ur.RoleID = r.RoleID;
````SQL
-- Example of granting privileges
GRANT SELECT ON Users TO public;
```SQL
-- Example of transaction control
BEGIN;
INSERT INTO Users (UserID, UserName, Email) VALUES (3, 'Charlie', 'charlie@example.com');
COMMIT; -- Save the changes
```SQL
-- Find users with a specific role
SELECT UserName FROM Users
WHERE UserID IN (SELECT UserID FROM UserRoles WHERE RoleID = 1); -- Users with Admin role

