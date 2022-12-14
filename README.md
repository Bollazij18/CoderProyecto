# CoderProyecto
Entregas .sql del proyecto Coder_SQL_Bollazzi
Este Repositorio de Github se centrará para compartir todos los códigos SQL correspondientes al proyecto del curso. 

---- ENTREGAS COMPLETAS VERSION V.0 --

-- Creation of Database and tables (More tables to come next) --

IF DATABASE e_commerce IS NULL
CREATE DATABASE e_commerce;

USE e_commrce;

CREATE TABLE Clientes(
Usuario	VarChar(21) NOT NULL,
Nombre	VarChar(21) NOT NULL,
Apellido	VarChar(21) NOT NULL,
Direccion	VarChar(60) NOT NULL,
Telefono	VarChar(15) NOT NULL,
Edad	TinyInt NOT NULL,
Tarjeta_1	ShortInt NOT NULL,
Tarjeta_2	ShortInt,
Tarjeta_3	ShortInt,
RFC	VarChar (20),

PRIMARY KEY (Usuario)
);

CREATE TABLE Pedidos(
ID_Pedido	VarChar(30) AUTO_INCREMENT,
Usuario	VarChar(21) NOT NULL,
Monto	Money NOT NULL,
Fecha	DateTime NOT NULL,
Direccion	VarChar(60) NOT NULL,
Nombre_Articulo	VarChar(21) NOT NULL,
Cantidad	TinyInt NOT NULL,

PRIMARY KEY (ID_Pedido),
FOREIGN KEY (Usuario) REFERENCES Clientes(Usuario)
);

CREATE TABLE Productos(
SKU	VarChar(30) NOT NULL,
Nombre_Articulo	VarChar(21) NOT NULL,
Precio	Money NOT NULL,
Talla	TinyInt,
Genero	VarChar(10) NOT NULL,
Color	VarChar(10) NOT NULL,
Tipo	VarChar(15) NOT NULL,
Disponibilidad	TinyInt NOT NULL,
Almacen	VarChar(10) NOT NULL,

PRIMARY KEY (SKU),
FOREIGN KEY (Nombre_Articulo) REFERENCES Almacen(Nombre_Articulo)
);

CREATE TABLE Almacen(
ID_Almacen	VarChar(10) NOT NULL,
Direccion	VarChar(60) NOT NULL,
Telefono	VarChar(15) NOT NULL,
Zona_distribucion	VarChar(10) NOT NULL,
Disponibilidad	TinyInt NOT NULL,
Capacidad	SmallInt NOT NULL,

PRIMARY KEY (ID_Almacen)
);

CREATE TABLE Proveedores(
ID_Proveedor	VarChar(30) NOT NULL,
RFC	VarChar(20) NOT NULL,
Direccion Varchar(60),
Contacto VarChar(30),
Tipo	VarChar(15) NOT NULL,

PRIMARY KEY (ID_Proveedor)
);

CREATE TABLE Cambios_Clientes(
Usuario	VarChar(21) NOT NULL,
Nombre	VarChar(21) NOT NULL,
Apellido	VarChar(21) NOT NULL,
Direccion	VarChar(60) NOT NULL,
Telefono	VarChar(15) NOT NULL,
Edad	TinyInt NOT NULL,
Tarjeta_1	ShortInt NOT NULL,
Tarjeta_2	ShortInt,
Tarjeta_3	ShortInt,
RFC	VarChar (20),
Fecha_de_Cambio Date NOT NULL,
Tiempo_Actualizacion Time NOT NULL,
ID_Cambio Integer AUTO_INCREMENT NOT NULL,
Tipo_Cambio Var_Char(15) NOT NULL,

FOREIGN KEY (Usuario) REFERENCES Clientes(Usuario)
);

CREATE TABLE Movimientos(
ID_Ops VarChar (40) NOT NULL,
ID_Almacen	VarChar(10) NOT NULL,
Direccion	VarChar(60) NOT NULL,
Telefono	VarChar(15) NOT NULL,
Direccion_Envio	VarChar(10) NOT NULL,
Tiempo_Entrega	Date NOT NULL,

PRIMARY KEY (ID_Ops),
FOREIGN KEY (Usuario) REFERENCES Clientes(Usuario),
FOREIGN KEY (ID_Almacen) REFERENCES Almacen(ID_Almacen)
);

CREATE TABLE Operaciones_Almacen(
ID_Ops VarChar (40) NOT NULL,
ID_Almacen	VarChar(10) NOT NULL,
Direccion	VarChar(60) NOT NULL,
Telefono	VarChar(15) NOT NULL,
Direccion_Envio	VarChar(10) NOT NULL,
Tiempo_Entrega	Date NOT NULL,
Fecha_Actualizacion Date NOT NULL,
Tiempo_Actualizacion Time NOT NULL,
ID_Actualizacion  AUTO_INCREMENT NOT NULL,
Tipo_Actualizacion Var_Char(15) NOT NULL,

PRIMARY KEY (ID_Ops),
FOREIGN KEY (Usuario) REFERENCES Clientes(Usuario),
FOREIGN KEY (ID_Almacen) REFERENCES Almacen(ID_Almacen)
);

CREATE TABLE Pruebas_Varias(
ID_Test VarChar (40) NOT NULL,
Test_Text VarChar (100), 
Fecha_Actualizacion Date NOT NULL,
Tiempo_Actualizacion Time NOT NULL,
Tipo_Actualizacion Var_Char(15) NOT NULL,

PRIMARY KEY (ID_Test),
);

CREATE TABLE Test_01(
ID_Test01 VarChar (40) NOT NULL,
Test_Field VarChar (20),
Test_Text VarChar (100),
Fecha_Actualizacion Date NOT NULL,
Tiempo_Actualizacion Time NOT NULL,

PRIMARY KEY (ID_Test01),
);

-- Insertion of data (More tables and data to come next)-- 

INSERT INTO 
Clientes(Usuario, Nombre, Apellido, Direccion, Telefono, Edad, Tarjeta_1, Tarjeta_2, Tarjeta_3, RFC)
VALUES
('JP29','Juan','Perez','12 Calle Lago, Interlomas, CDMX 77292','123-654-2345','25','1234567891234567', NULL, NULL,'JUPEZ1234H'),
('JJSuarez','Jose','Suarez','254 Calle Espino, Chapultepec, CDMX 53624','123-874-2843','45','1234567891234567', '1234567891234567', NULL,'JOSUZ5432Y'),
('MP002','Maria','Perez','222 Calle Juarez, Saltillo 12310','223-657-8954','18','1234567891234567', NULL, NULL,'MAPEZ64738J'),
('JMorales','Jorge','Morales','654 calle 42, Merida, Yucatan 11590','774-965-3884','36','1234567891234567', NULL, NULL,'JOMOL5896HG'),
('SofOrt','Sofia','Ortiz','172 calle Lago, Queretaro,Queretaro 61632','363-163-7921','43','1234567891234567', 1234567891234567, NULL,'SOORZ6839S'),
('RegJACK','Regina','Jackson','221 calle Durango, La Condesa, CDMX 19829','123-759-9821','67','1234567891234567', NULL, NULL,'REJN8579Q'),
('AlMol','Alexis','Molina','94 calle Londres, Chihuahua, CDMX 12256','123-167-8532',29','1234567891234567', 1234567891234567, 1234567891234567,'ALMO85943FS'),
('AlfCampos','Alfredo','Campos','64 calle Artemisa, Puebla,Puebla 83201','166-748-3421','34','1234567891234567', NULL, NULL,'ALCA8492NB');


INSERT INTO 
Pedidos(Usuario, Monto, Fecha, Direccion, Nombre_Articulo, Talla, Cantidad)
VALUES
('JP29','2500.00','12 Calle Lago, Interlomas, CDMX 77292','20/08/2022','Camisa_Hombre','M','2'),
('JP29','5000.00','12 Calle Lago, Interlomas, CDMX 77292','1/12/2021','Camisa_Hombre','M','4'),
('SofOrt','1900.00','172 calle Lago, Queretaro,Queretaro 61632','4/05/2022','Blusa_Mujer','S','2'),
('SofOrt','799.00','172 calle Lago, Queretaro,Queretaro 61632','18/02/2022','Pantalon_Mujer','S','1'),
('AlfCampos','1900.00','64 calle Artemisa, Puebla,Puebla 83201','18/02/2022','Pantalon_Hombre','M','2'),
('MP002','7200.00','222 Calle Juarez, Saltillo 12310','15/08/2021','Pulcera_Mujer',NULL,'10'),
('SofOrt','3800.00','172 calle Lago, Queretaro,Queretaro 61632','6/10/2022','Blusa_Mujer','M','4'),
('MP002','1598.00','222 Calle Juarez, Saltillo 12310','04/10/2022','Pantalon_Mujer','S','2'),
('JJSuarez','1600.00','254 Calle Espino, Chapultepec, CDMX 53624','18/02/2020','Playera_Hombre','L','4'),
('JJSuarez','350.00','254 Calle Espino, Chapultepec, CDMX 53624','18/02/2020','Cartera_Hombre',NULL,'1');

INSERT INTO 
Productos(SKU, Nombre_Articulo, Precio, Talla	, Genero, Color, Tipo, Disponibilidad, Almacen)
VALUES
('2022CAHOBS200','Camisa_Hombre','1250.00','S','H','BLANCA','TOP','200','A01'),
('2022CAHOBM200','Camisa_Hombre','1250.00','M','H','BLANCA','TOP','200','A01'),
('2022CAHOBL200','Camisa_Hombre','1250.00','L','H','BLANCA','TOP','200','A01'),
('2022PLHOBS500','Playera_Hombre','400.00','S','H','BLANCA','TOP','500','A01'),
('2022PLHOBM500','Playera_Hombre','400.00','M','H','BLANCA','TOP','500','A01'),
('2022PLHOBL500','Playera_Hombre','400.00','L','H','BLANCA','TOP','500','A01'),
('2022CAHOAZS200','Camisa_Hombre','1250.00','S','H','AZUL','TOP','200','A01'),
('2022CAHOAZM200','Camisa_Hombre','1250.00','M','H','AZUL','TOP','200','A01'),
('2022CAHOAZL200','Camisa_Hombre','1250.00','L','H','AZUL','TOP','200','A01'),
('2022PLHOAZS500','Playera_Hombre','400.00','S','H','AZUL','TOP','500','A01'),
('2022PLHOAZM500','Playera_Hombre','400.00','M','H','AZUL','TOP','500','A01'),
('2022PLHOAZL500','Playera_Hombre','400.00','L','H','AZUL','TOP','500','A01'),
('2022BLMUBS500','Blusa_Mujer','950.00','S','H','BLANCA','TOP','500','A01'),
('2022BLMUBM500','Blusa_Mujer','950.00','M','H','BLANCA','TOP','500','A01'),
('2022BLMUBL500','Blusa_Mujer','950.00','L','H','BLANCA','TOP','500','A01'),
('2022PAMUNS300','Pantalon_Mujer','799.00','S','M','NEGRO','BOT','300','A02'),
('2022PAMUNM300','Pantalon_Mujer','799.00','M','M','NEGRO','BOT','300','A02'),
('2022PAMUNL300','Pantalon_Mujer','799.00','L','M','NEGRO','BOT','300','A02'),
('2022PAHONS300','Pantalon_Hombre','799.00','S','H','NEGRO','BOT','300','A02'),
('2022PAHONM300','Pantalon_Hombre','799.00','M','H','NEGRO','BOT','300','A02'),
('2022PAHONL300','Pantalon_Hombre','799.00','L','H','NEGRO','BOT','300','A02'),
('2022CIHOS250','Cinturon_Mujer','350.00','S','M','NEGRO','ACC','250','A02'),
('2022CIHOS250','Cinturon Hombre','400.00','S','H','NEGRO','ACC','250','A02'),
('2022CAMUACC500','Cartera_Mujer','350.00',NULL,'M','NEGRO','ACC','500','A02'),
('2022CAHOACC500','Cartera_Hombre','350.00',NULL,'H','NEGRO','ACC','500','A02'),
('2022PUMUORO250','Pulcera_Mujer','720.00',NULL,'M','ORO','ACC','250','A02');

INSERT INTO 
Almacen(ID_Almacen, Direccion, Telefono, Zona_distribucion, Disponibilidad, Capacidad)
VALUES
('A01','123 Calle 42, Nucalpan, Edo Mex 65454','443-245-8658','CentroA','2000','10000'),
('A02','1748 Calle Irrigacion, Naucalpan, Edo Mex 65345','784-543-7584','CentroB','100','5000'),
('A03','64 Calle Obregon, Monterrey, Nuevo Leon 647832','223-455-8732','NorEste','10','1000'),
('A04','785 Calle Juarez, Tijuana, Baja California 98490','646-627-7854','NorOeste','0','5000'),
('A05','645 Calle 42, Nucalpan, Oaxaca, Oaxaca 65454','152-743-0988','Sur','2000','8000'),
('A06','124 Calle Carranza, Veracruz, Veracruz 1374','173-245-8658','Este','50','2000'),
('A07','32 Calle Tequila, Guadalajara, Jalisco 98675','229-245-8658','Oeste','20','3000'),
('A08','1748 Calle 50, Merida, Yucatan 74324','784-543-6748','Sur-Este','100','5000');

INSERT INTO 
Proveedores(ID_Proveedor, RFC, Direccion, Contacto, Tipo)
VALUES
('PROV01','PGTU6F8903HD','74 calle Lagos, Santa Fe,CDMX 65748','proveedor1@gmail.com','Telas'),
('PROV02','UE63F7829SRI','637 calle Cervantes, Cancun, Quintana Roo 867511','proveedor2@gmail.com','Piel'),
('PROV03','UN74784932RH','123 calle Sonora, Monterrey, Nuevo Leon 784234','proveedor3@gmail.com','Telas'),
('PROV04','HF8594387FG6','583 calle lagos, CDMX 65748','proveedor4@gmail.com','Accesorios');



-- Creation of Views --

CREATE VIEW [ROPA_CABALLERO_DISPONIBLE] AS 
SELECT SKU, Nombre_Articulo, Precio, Talla, Genero, Color, Tipo, Almacen
FROM Productos
WHERE Genero = 'H' AND Disponibilidad <> ['0',NULL];

SELECT * FROM [ROPA_CABALLEROS_DISPONIBLE];

CREATE VIEW [ROPA_DAMA_DISPONIBLE] AS 
SELECT SKU, Nombre_Articulo, Precio, Talla, Genero, Color, Tipo, Almacen
FROM Productos
WHERE Genero = 'M' AND Disponibilidad <> ['0',NULL];

SELECT * FROM [ROPA_DAMA_DISPONIBLE];

CREATE VIEW [ULIMOS_PEDIDOS] AS
SELECT *
FROM Pedidos
WHERE ID_Pedido IS NOT NULL 
ORDER BY Fecha DESC;

SELECT * FROM [ULTIMOS_PEDIDOS];

CREATE VIEW [ALMACEN_LLENO] AS
SELECT *
FROM Almacen
WHERE Disponibilidad = '0'

SELECT * FROM [ALMACEN_LLENO];

CREATE VIEW [USUARIOS_ACTIVOS] AS
SELECT DISTINCT C.Usuario, C.Nombre, C.Apellido, COUNT(P.ID_Pedido) AS Pedidos_Usuario
FROM Clientes C
JOIN Pedidos P ON C.Usuario = P.Pedidos
WHERE P.ID_Pedido IS NOT NULL
GROUP BY 1
ORDER BY Pedidos_Usuario DESC
LIMIT 10;

SELECT * FROM [USUARIOS_ACTIVOS];

-- Creation of Functions --

-- Esta funcion calcula el tiempo que ha pasado en dias, --
-- sera uilizado para regresar el tiempo ocurrido en dias de las compras realizadas--

DELIMITER //

CREATE FUNCTION no_de_dias (Fecha1 DATE) RETURNS int DETERMINISTIC

BEGIN
 DECLARE Fecha2 DATE;
  Select current_date()into Fecha2;
  RETURN (Fecha2)-(Fecha1);

END 

END; //

DELIMITER ;

-- Esta funcion determina si los usuarios son mayores de edad o no --

DELIMITER //

CREATE FUNCTION Mayor_Edad (Edad INTEGER) RETURNS VarChar(4) DETERMINISTIC

BEGIN
 IF Edad >= 21 THEN
 RETURN 'YES';
 ELSE
 RETURN 'NO';
 END IF;

END

END; //

DELIMITER ;

-- Creation of SPs -- 
-- Este SP ordena el campo seleccionado por el usuario y de una forma desc o Asc dependiendo si el usuario selecciona 1 o 0-- 

DELIMITER //
CREATE PROCEDURE Order_Campo (IN @campo VarChar(), IN @orden INTEGER)

BEGIN
 IF @order = 1
  THEN
   SELECT * FROM Pedidos
   ORDER BY @campo DESC
  ELSE
   SELECT * FROM Pedidos
   ORDER BY @campo ASC
 END IF
END;

//

-- Este SP permite insertar valores en la tabla de Clientes --

DELIMITER //
CREATE PROCEDURE Master_Insert (@Usuario	VarChar(21, @Nombre	VarChar(21), @Apellido	VarChar(21), @Direccion	VarChar(60), 
                                @Telefono	VarChar(15), Edad	TinyInt, @Tarjeta_1	ShortInt, @Tarjeta_2	ShortInt, @Tarjeta_3	ShortInt, @RFC	VarChar (20))
AS
  BEGIN
      IF @StatementType = 'Insert'
        BEGIN
            INSERT INTO Clientes (Usuario, Nombre, Apellido, Direccion, Telefono, Edad, Tarjeta_1, Tarjeta_2, Tarjeta_3, RFC)
            
            VALUES  (@Usuario, @Nombre, @Apellido, @Direccion, @Telefono, @Edad, @Tarjeta_1, @Tarjeta_2, @Tarjeta_3, @RFC)
        END
     END IF
END; 
//

-- Creation of Triggers --

--Estos dos triggers son para la tabla de operaciones de almacen--
--Este trigger 
DELIMITER //
CREATE TRIGGER
ON Movimientos
BEFORE INSERT, DELETE FOR EACH ROW
AS

BEGIN
DECLARE User VarChar (40);
SELECT USER() INTO aUser;
SET NEW.Modificado_Fecha = GETDATE();
SET NEW.Modificado_Tiempo = GETTIME();
SET NEW.Modificado_por = aUser;

END;
//
-- Este trigger inserta un registro nuevo de lo inserado o borrado en la tabla de movimientos --
DELIMITER//
CREATE TRIGGER 
ON Movimientos
AFTER INSERT, DELETE

AS

BEGIN
 SET NOCOUNT ON;

 INSERT INTO Operaciones_Almacen(
  ID_Ops, ID_Almacen, Direccion, Telefono, Direccion_Envio, Tiempo_Entrega, Fecha_Actualizacion,Tiempo_Actualizacion, ID_Actualizacion, Tipo_Actualizacion)

 SELECT
  i.ID_Ops, i.ID_Almacen, i.Direccion, i.Telefono, i.Direccion_Envio, i.Tiempo_Entrega, GETDATE(), GETTIME(), AUTO_INCREMENT(), 'INS'
 
 FROM
 Inserted AS i
 
    UNION ALL
    
 SELECT
  d.ID_Ops, d.ID_Almacen, d.Direccion, d.Telefono, d.Direccion_Envio, d.Tiempo_Entrega, GETDATE(), GETTIME(), AUTO_INCREMENT(),'DEL'
 
 FROM
 Deleted AS d;
END;
//

--Estos dos triggers son para la tabla de cambios en la base de clientes o usuarios--
DELIMITER //
CREATE TRIGGER
ON Clientes
BEFORE INSERT, DELETE FOR EACH ROW
AS

BEGIN
DECLARE User VarChar (40);
SELECT USER() INTO aUser;
SET NEW.Modificado_Fecha = GETDATE();
SET NEW.Modificado_Tiempo = GETTIME();
SET NEW.Modificado_por = aUser;

END;
//
-- Este trigger inserta un registro con los datos insertados o borrados en la tabla de clientes --
DELIMITER //
CREATE TRIGGER
ON Clientes
AFTER INSERT, DELETE
AS

BEGIN
 SET NOCOUNT ON;
 
 INSERT INTO Cambios_Clientes(
  Usuario, Nombre, Apellido, Direccion, Telefono, Edad, Tarjeta_1, Tarjeta_2, Tarjeta_3, RFC, Fecha_de_Cambio, Tiempo_Actualizacion, ID_Cambio, Tipo_Cambio)

 SELECT
  i.Usuario, i.Nombre, i.Apellido, i.Direccion, i.Telefono, i.Edad, i.Tarjeta_1, i.Tarjeta_2, i.Tarjeta_3, i.RFC, GETDATE(), GETTIME(), AUTO_INCREMENT(),'INS'
 
 FROM
 Inserted AS i
 
    UNION ALL
    
 SELECT
  d.Usuario, d.Nombre, d.Apellido, d.Direccion, d.Telefono, d.Edad, d.Tarjeta_1, d.Tarjeta_2, d.Tarjeta_3, d.RFC, GETDATE(), GETTIME(), d.AUTO_INCREMENT(),'DEL'
 
 FROM
 Deleted AS d;
END;
//

-- Creation of users and permissions --
-- "Sentencias" --
--Crear un usuario con habilidades de int y update y otro con solo update, No pueden eliminar --

CREATE LOGIN Jose_B
WITH PASSWORD = 'Pa$$word1';

CREATE LOGIN Juan_M
WITH PASSWORD = 'Pa$$word2';

CREATE ROLE Managers;
CREATE ROLE Supervisors;

CREATE USER Manager_1 FOR LOGIN Jose_B;
CREATE USER Supervisor_1 FOR LOGIN Juan_M;

ALTER ROLE Managers
ADD MEMBER Manager_1;

ALTER Supervisors
ADD MEMBER Supervisor_1;

GRANT SELECT, UPDATE, ALTER, INSERT TO Managers;
GRANT SELECT, ALTER, UPDATE TO Supervisors;
--

--TCL Commands --
--Transacciones y comandos para entrega de TLC--

Pruebas_Varias
INSERT INTO Pruebas_Varias
VALUES (1A, Primer prueba de la tabla, GETDATE(), GETTIME(), INS);
COMMIT;

INSERT INTO Pruebas_Varias
VALUES (2A, Segunda prueba de la tabla, GETDATE(), GETTIME(), INS);
COMMIT;

UPDATE Pruebas_Varias
SET Test_Text = 'Primera prueba actualizada' WHERE ID_Test = '1A';
SAVEPOINT A;

UPDATE Pruebas_Varias
SET Test_Text = 'Primer prueba de tabla' WHERE ID_Test = '2A';
SAVEPOINT B;

ROLLBACK to A;
COMMIT;

--Insertando 8 nuevos registros en la tabla de pedidos con un savepoint a los 4 registros y otro a los 8 registros--

INSERT INTO  Pedidos
VALUES (1234579637,Juan32,2000.00,74 Calle Boston, Ciudad de Mexico 78323, 10/20/2022,Pantalon_Hombre,H,2);
	
INSERT INTO Pedidos
VALUES ('SofOrt','3800.00','172 calle Lago, Queretaro,Queretaro 61632','6/10/2022','Blusa_Mujer','M','4');

INSERT INTO Pedidos
VALUES ('MP002','1598.00','222 Calle Juarez, Saltillo 12310','04/10/2022','Pantalon_Mujer','S','2');

INSERT INTO Pedidos
VALUES ('JJSuarez','1600.00','254 Calle Espino, Chapultepec, CDMX 53624','18/02/2020','Playera_Hombre','L','4');

SAVEPOINT A;

INSERT INTO Pedidos
VALUES ('JJSuarez','350.00','254 Calle Espino, Chapultepec, CDMX 53624','18/02/2020','Cartera_Hombre',NULL,'1');

INSERT INTO Pedidos
VALUES ('JP29','5000.00','12 Calle Lago, Interlomas, CDMX 77292','1/12/2021','Camisa_Hombre','M','4');

INSERT INTO Pedidos
VALUES ('SofOrt','1900.00','172 calle Lago, Queretaro,Queretaro 61632','4/05/2022','Blusa_Mujer','S','2');

INSERT INTO Pedidos
VALUES ('SofOrt','799.00','172 calle Lago, Queretaro,Queretaro 61632','18/02/2022','Pantalon_Mujer','S','1');

SAVEPOINT B;

ROLLBACK TO A;
COMMIT;

--
