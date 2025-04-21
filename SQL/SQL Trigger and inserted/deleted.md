# SQL Trigger and inserted/deleted

BEGIN TRAN

CREATE TABLE dbo.MyCustomer (
ID int IDENTITY
,[NAME] varchar(50)
,[AccountId] varchar(50)
);
GO

CREATE TRIGGER dbo.CustomerAccountId ON dbo.MyCustomer
AFTER INSERT

AS

IF (ROWCOUNT_BIG() = 0) RETURN;

if exists (select * from inserted) BEGIN
UPDATE c SET [AccountId] = concat('NZ','-',[c.ID](http://c.id/))
FROM dbo.MyCustomer AS c
JOIN inserted AS i ON [c.ID](http://c.id/) = [i.ID](http://i.id/)
END

GO

INSERT INTO dbo.MyCustomer ([Name],[AccountId]) SELECT 'Joe', 'DefaultValue'
INSERT INTO dbo.MyCustomer ([Name],[AccountId]) Values ('Jim', 'DefaultValue')
INSERT INTO dbo.MyCustomer ([Name],[AccountId]) Values ('JIll', 'DefaultValue')

INSERT INTO dbo.MyCustomer ([Name],[AccountId])
SELECT 'Joe', 'DefaultValue' UNION
SELECT 'Jim','DefaultValue' UNION
SELECT 'JIll','DefaultValue';

SELECT  ident_current('dbo.MyCustomer') AS [LastID_1]
,@@IDENTITY AS [LastID_2]
,scope_identity() AS [LastID_3];

select * from dbo.MyCustomer

ROLLBACK TRAN