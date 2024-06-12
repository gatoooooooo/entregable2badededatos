# ENTREGABLE 2
#### **crear base de datos**
crear base de datos
```sql
CREATE DATABASE Clinica;
GO
```
uso de bade de datos
```sql
USE Clinica
GO
```
---
#### **crear tablas**
paciente
```sql
CREATE TABLE Paciente (
    PacienteID INT PRIMARY KEY IDENTITY(1,1),
    Nombre NVARCHAR(100) NOT NULL,
    Apellido NVARCHAR(100) NOT NULL,
    FechaNacimiento DATE NOT NULL,
    Genero CHAR(1) CHECK (Genero IN ('M', 'F')),
    Telefono NVARCHAR(15),
    Direccion NVARCHAR(255),
    Email NVARCHAR(100)
);
GO
```
doctor
```sql
CREATE TABLE Doctor (
    DoctorID INT PRIMARY KEY IDENTITY(1,1),
    Nombre NVARCHAR(100) NOT NULL,
    Apellido NVARCHAR(100) NOT NULL,
    Especialidad NVARCHAR(100) NOT NULL,
    Telefono NVARCHAR(15),
    Email NVARCHAR(100),
    HorarioTrabajo NVARCHAR(100)
);
GO
```
habitacion
```sql
CREATE TABLE Habitacion (
    HabitacionID INT PRIMARY KEY IDENTITY(1,1),
    NumeroHabitacion NVARCHAR(10) NOT NULL,
    TipoHabitacion NVARCHAR(50),
    Estado NVARCHAR(50) CHECK (Estado IN ('Disponible', 'Ocupada', 'Mantenimiento')),
    PacienteID INT,
    FOREIGN KEY (PacienteID) REFERENCES Paciente(PacienteID)
);
GO
```
---
#### **insertar datos**
Insertar datos en la tabla Paciente
```sql
INSERT INTO Paciente (Nombre, Apellido, FechaNacimiento, Genero, Telefono, Direccion, Email)
VALUES 
('Gonzalo', 'Morante', '2004-03-04', 'M', '980647465', 'Calle Falsa 123', 'gonzalo@gmail.com'),
('Maria', 'Gonzalez', '1990-07-20', 'F', '963532674', 'Avenida Siempreviva 742', 'maria@gmail.com'),
('Carlos', 'Ramirez', '1985-02-10', 'M', '958465741', 'Calle Los Olivos 456', 'carlos@gmail.com'),
('Ana', 'Lopez', '1975-11-30', 'F', '995625745', 'Calle Las Flores 789', 'ana@gmail.com'),
('Luis', 'Martinez', '2000-04-25', 'M', '941657523', 'Avenida Las Palmas 101', 'luis@gmail.com');
GO
```
Insertar datos en la tabla Doctor
```sql
INSERT INTO Doctor (Nombre, Apellido, Especialidad, Telefono, Email, HorarioTrabajo)
VALUES 
('Ana', 'Gomez', 'Cardiología', '958647515', 'ana@gmail.com', 'Lunes a Viernes 9:00-17:00'),
('Pedro', 'Hernandez', 'Pediatría', '978585845', 'pedro@example.com', 'Lunes a Viernes 10:00-18:00'),
('Luisa', 'Mendez', 'Dermatología', '965278658', 'luisa@example.com', 'Martes a Sábado 8:00-16:00'),
('Juan', 'Ruiz', 'Neurología', '998963457', 'juan@example.com', 'Lunes a Jueves 11:00-19:00'),
('Elena', 'Torres', 'Ginecología', '974857458', 'elena@example.com', 'Miércoles a Domingo 9:00-17:00');
GO
```
habitacion
```sql
INSERT INTO Habitacion (NumeroHabitacion, TipoHabitacion, Estado)
VALUES 
('101', 'Individual', 'Disponible'),
('102', 'Doble', 'Ocupada'),
('103', 'Individual', 'Mantenimiento'),
('104', 'Suite', 'Disponible'),
('105', 'Doble', 'Ocupada');
GO
```
asignar habitaciones a pacientes
```sql
UPDATE Habitacion SET PacienteID = 1 WHERE NumeroHabitacion = '102';
UPDATE Habitacion SET PacienteID = 3 WHERE NumeroHabitacion = '105';
GO
```
---
#### **consultas simples**
1)  Seleccionar todos los pacientes
```sql
SELECT * FROM Paciente;
```
2) Seleccionar todos los doctores
 ```sql
SELECT * FROM Doctor;
```
3) Seleccionar todas las habitaciones
 ```sql
SELECT * FROM Habitacion;
```
4) Seleccionar todos los pacientes de género femenino
 ```sql
SELECT * FROM Paciente WHERE Genero = 'F';
```
5) Seleccionar habitaciones que están ocupadas
 ```sql
SELECT * FROM Habitacion WHERE Estado = 'Ocupada';
```
---
### **Consultas avanzadas**
1) Lista de pacientes y sus habitaciones asignadas
```sql
SELECT 
    p.PacienteID,
    p.Nombre,
    p.Apellido,
    h.NumeroHabitacion,
    h.TipoHabitacion,
    h.Estado
FROM Paciente p
LEFT JOIN Habitacion h ON p.PacienteID = h.PacienteID;
```
2) pacientes atendidos por cada especialidad médica
```sql
SELECT 
    d.Especialidad,
    COUNT(c.ConsultaID) AS NumeroPacientesAtendidos
FROM Doctor d
LEFT JOIN Consulta c ON d.DoctorID = c.DoctorID
GROUP BY d.Especialidad;
```
3) Pacientes que están asignados a habitaciones ocupadas
```sql
SELECT 
    p.PacienteID,
    p.Nombre,
    p.Apellido,
    h.NumeroHabitacion,
    h.TipoHabitacion
FROM Paciente p
JOIN Habitacion h ON p.PacienteID = h.PacienteID
WHERE h.Estado = 'Ocupada';
```
4) Doctores que trabajan en un horario específico
```sql
SELECT 
    d.DoctorID,
    d.Nombre,
    d.Apellido,
    d.Especialidad,
    d.HorarioTrabajo
FROM Doctor d
WHERE d.HorarioTrabajo LIKE '%Lunes%';
```
5) consulta varios campos de tres tablas diferentes:
```sql
SELECT 
    p.Nombre AS NombrePaciente,
    p.Apellido AS ApellidoPaciente,
    c.FechaConsulta,
    c.Diagnostico,
    d.Nombre AS NombreDoctor,
    d.Apellido AS ApellidoDoctor,
    d.Especialidad
FROM Consulta c
JOIN Paciente p ON c.PacienteID = p.PacienteID
JOIN Doctor d ON c.DoctorID = d.DoctorID
WHERE c.FechaConsulta BETWEEN '2023-01-01' AND '2023-12-31';
```
---
### **Insertar**
paciente
```sql
INSERT INTO Paciente (Nombre, Apellido, FechaNacimiento, Genero, Telefono, Direccion, Email)
VALUES ('María', 'López', '1992-08-20', 'F', '925323234', 'Calle Principal 123', 'lopez@gmail.com');
```
doctor
```sql
INSERT INTO Doctor (Nombre, Apellido, Especialidad, Telefono, Email, HorarioTrabajo)
VALUES ('Pedro', 'García', 'Oftalmología', '555-5678', 'pedro.garcia@example.com', 'Lunes a Viernes 10:00-18:00');
```
asigna habitacion a paciente
```sql
UPDATE Habitacion
SET PacienteID = 6, Estado = 'Ocupada'
WHERE NumeroHabitacion = '103';
```
consulta
```sql
SELECT 
    p.Nombre AS NombrePaciente,
    h.NumeroHabitacion
FROM 
    Paciente p
JOIN 
    Habitacion h ON p.PacienteID = h.PacienteID
WHERE 
    p.Nombre = 'María' AND p.Apellido = 'López';
```
---
### **Actualizar**
paciente
```sql
UPDATE Paciente
SET Telefono = '92657415', Direccion = 'Calle Segundaria 123', Email = 'lopezg@gmail.com'
WHERE PacienteID = 6;
```
doctor
```sql
UPDATE Doctor
SET Especialidad = 'Neurología'
WHERE DoctorID = 4;
```
habitacion
```sql
UPDATE Habitacion
SET Estado = 'Mantenimiento'
WHERE NumeroHabitacion = '103';
```
consulta
```sql
SELECT 
    Nombre,
    Telefono,
    Direccion,
    Email
FROM Paciente
WHERE PacienteID = 6;
```
---
### **Eliminar**
>paciente
```sql
DELETE FROM Paciente
WHERE PacienteID = 6;
```
doctor
```sql
DELETE FROM Doctor
WHERE DoctorID = 4;
```
habitacion
```sql
DELETE FROM Habitacion
WHERE NumeroHabitacion = '103';
```
---
### **Procedimiento**
procedimiento lista paciente
```sql
CREATE PROCEDURE ListarPacientesPorGenero
    @Genero CHAR(1)
AS
BEGIN
    SELECT *
    FROM Paciente
    WHERE Genero = @Genero;
END;
```
procedimioento actualizar informacion paciente
CREATE PROCEDURE ActualizarInformacionPaciente
```sql
    @PacienteID INT,
    @Telefono NVARCHAR(15),
    @Direccion NVARCHAR(255),
    @Email NVARCHAR(100)
AS
BEGIN
    UPDATE Paciente
    SET Telefono = @Telefono,
        Direccion = @Direccion,
        Email = @Email
    WHERE PacienteID = @PacienteID;
END;
```
