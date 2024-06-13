# EmpresaDB
**Crear base de datos**
```sql
CREATE DATABASE EmpresaDB;
GO
```
**uso de bade de datos**
```sql
USE EmpresaDB;
GO
```
### Crear tablas
**Crear tabla Departamento**
```sql
CREATE TABLE Departamento (
    IDDepartamento INT IDENTITY(1,1) PRIMARY KEY,
    NombreDepartamento VARCHAR(50) NOT NULL,
    Ubicacion VARCHAR(50) NOT NULL
);
```
**Crear tabla Empleado**
```sql
CREATE TABLE Empleado (
    IDEmpleado INT IDENTITY(1,1) PRIMARY KEY,
    NombreEmpleado VARCHAR(50) NOT NULL,
    Puesto VARCHAR(50) NOT NULL,
    IDJefe INT,
    FechaContratacion DATE NOT NULL,
    Salario DECIMAL(10, 2) NOT NULL,
    Comision DECIMAL(10, 2),
    IDDepartamento INT NOT NULL,
    FOREIGN KEY (IDJefe) REFERENCES Empleado(IDEmpleado),
    FOREIGN KEY (IDDepartamento) REFERENCES Departamento(IDDepartamento)
);
```
**Crear tabla Proyecto**
```sql
CREATE TABLE Proyecto (
    IDProyecto INT IDENTITY(1,1) PRIMARY KEY,
    NombreProyecto VARCHAR(50) NOT NULL,
    Ubicacion VARCHAR(50) NOT NULL,
    IDDepartamento INT NOT NULL,
    FOREIGN KEY (IDDepartamento) REFERENCES Departamento(IDDepartamento)
);
```
**Crear tabla EmpleadoProyecto**
```sql
CREATE TABLE EmpleadoProyecto (
    IDEmpleado INT NOT NULL,
    IDProyecto INT NOT NULL,
    HorasTrabajadas INT NOT NULL,
    PRIMARY KEY (IDEmpleado, IDProyecto),
    FOREIGN KEY (IDEmpleado) REFERENCES Empleado(IDEmpleado),
    FOREIGN KEY (IDProyecto) REFERENCES Proyecto(IDProyecto)
);
```
### Insertar registros
**Isertar registros en la tabla Departamento**
```sql
INSERT INTO Departamento (NombreDepartamento, Ubicacion) VALUES ('ACCOUNTING', 'NEW YORK');
INSERT INTO Departamento (NombreDepartamento, Ubicacion) VALUES ('RESEARCH', 'DALLAS');
INSERT INTO Departamento (NombreDepartamento, Ubicacion) VALUES ('SALES', 'CHICAGO');
INSERT INTO Departamento (NombreDepartamento, Ubicacion) VALUES ('OPERATIONS', 'BOSTON');
```
**Insertar registros en la tabla Empleado sin jefes**
```sql
INSERT INTO Empleado (NombreEmpleado, Puesto, IDJefe, FechaContratacion, Salario, Comision, IDDepartamento) VALUES ('KING', 'PRESIDENT', NULL, '1981-11-17', 5000, NULL, 1);
```
**Insertar registros en la tabla Empleado con jefes ya insertados**
```sql
INSERT INTO Empleado (NombreEmpleado, Puesto, IDJefe, FechaContratacion, Salario, Comision, IDDepartamento) VALUES ('JONES', 'MANAGER', 1, '1981-04-02', 2975, NULL, 2);
INSERT INTO Empleado (NombreEmpleado, Puesto, IDJefe, FechaContratacion, Salario, Comision, IDDepartamento) VALUES ('BLAKE', 'MANAGER', 1, '1981-05-01', 2850, NULL, 3);
INSERT INTO Empleado (NombreEmpleado, Puesto, IDJefe, FechaContratacion, Salario, Comision, IDDepartamento) VALUES ('CLARK', 'MANAGER', 1, '1981-06-09', 2450, NULL, 1);
```
**Insertar registros en la tabla Empleado con jefes ya insertados**
```sql
INSERT INTO Empleado (NombreEmpleado, Puesto, IDJefe, FechaContratacion, Salario, Comision, IDDepartamento) VALUES ('SCOTT', 'ANALYST', 2, '1987-04-19', 3000, NULL, 2);
INSERT INTO Empleado (NombreEmpleado, Puesto, IDJefe, FechaContratacion, Salario, Comision, IDDepartamento) VALUES ('FORD', 'ANALYST', 2, '1981-12-03', 3000, NULL, 2);
```
**Insertar registros en la tabla Empleado con jefes ya insertados**
```sql
INSERT INTO Empleado (NombreEmpleado, Puesto, IDJefe, FechaContratacion, Salario, Comision, IDDepartamento) VALUES ('SMITH', 'CLERK', 3, '1980-12-17', 800, NULL, 2);
INSERT INTO Empleado (NombreEmpleado, Puesto, IDJefe, FechaContratacion, Salario, Comision, IDDepartamento) VALUES ('ALLEN', 'SALESMAN', 4, '1981-02-20', 1600, 300, 3);
INSERT INTO Empleado (NombreEmpleado, Puesto, IDJefe, FechaContratacion, Salario, Comision, IDDepartamento) VALUES ('WARD', 'SALESMAN', 4, '1981-02-22', 1250, 500, 3);
INSERT INTO Empleado (NombreEmpleado, Puesto, IDJefe, FechaContratacion, Salario, Comision, IDDepartamento) VALUES ('MARTIN', 'SALESMAN', 4, '1981-09-28', 1250, 1400, 3);
INSERT INTO Empleado (NombreEmpleado, Puesto, IDJefe, FechaContratacion, Salario, Comision, IDDepartamento) VALUES ('TURNER', 'SALESMAN', 4, '1981-09-08', 1500, 0, 3);
INSERT INTO Empleado (NombreEmpleado, Puesto, IDJefe, FechaContratacion, Salario, Comision, IDDepartamento) VALUES ('ADAMS', 'CLERK', 5, '1987-05-23', 1100, NULL, 2);
INSERT INTO Empleado (NombreEmpleado, Puesto, IDJefe, FechaContratacion, Salario, Comision, IDDepartamento) VALUES ('JAMES', 'CLERK', 4, '1981-12-03', 950, NULL, 3);
INSERT INTO Empleado (NombreEmpleado, Puesto, IDJefe, FechaContratacion, Salario, Comision, IDDepartamento) VALUES ('MILLER', 'CLERK', 6, '1982-01-23', 1300, NULL, 1);
```
**Insertar registros en la tabla Proyecto**
```sql
INSERT INTO Proyecto (NombreProyecto, Ubicacion, IDDepartamento) VALUES ('P1', 'BOSTON', 2);
INSERT INTO Proyecto (NombreProyecto, Ubicacion, IDDepartamento) VALUES ('P4', 'CHICAGO', 3);
INSERT INTO Proyecto (NombreProyecto, Ubicacion, IDDepartamento) VALUES ('P5', 'CHICAGO', 3);
INSERT INTO Proyecto (NombreProyecto, Ubicacion, IDDepartamento) VALUES ('P6', 'LOS ANGELES', 3);
INSERT INTO Proyecto (NombreProyecto, Ubicacion, IDDepartamento) VALUES ('P8', 'NEW YORK', 3);
```
**Insertar registros en la tabla EmpleadoProyecto**
```sql
INSERT INTO EmpleadoProyecto (IDEmpleado, IDProyecto, HorasTrabajadas) VALUES (8, 2, 15);
INSERT INTO EmpleadoProyecto (IDEmpleado, IDProyecto, HorasTrabajadas) VALUES (8, 3, 12);
INSERT INTO EmpleadoProyecto (IDEmpleado, IDProyecto, HorasTrabajadas) VALUES (9, 2, 10);
INSERT INTO EmpleadoProyecto (IDEmpleado, IDProyecto, HorasTrabajadas) VALUES (9, 5, 8);
INSERT INTO EmpleadoProyecto (IDEmpleado, IDProyecto, HorasTrabajadas) VALUES (10, 1, 16);
INSERT INTO EmpleadoProyecto (IDEmpleado, IDProyecto, HorasTrabajadas) VALUES (10, 4, 15);
INSERT INTO EmpleadoProyecto (IDEmpleado, IDProyecto, HorasTrabajadas) VALUES (10, 5, 5);
INSERT INTO EmpleadoProyecto (IDEmpleado, IDProyecto, HorasTrabajadas) VALUES (11, 3, 6);
INSERT INTO EmpleadoProyecto (IDEmpleado, IDProyecto, HorasTrabajadas) VALUES (12, 1, 4);
```
---
## Consultas

### Consultas simples
**1)Consultar todos los empleados:**
```sql
SELECT * FROM Empleado;
```
**2)Consultar todos los departamentos:**
```sql
SELECT * FROM Departamento;
```
**3)Consultar todos los proyectos:**
```sql
SELECT * FROM Proyecto;
```
**4)Empleados que trabajan en un proyecto específico**
```sql
SELECT e.NombreEmpleado, p.NombreProyecto, ep.HorasTrabajadas
FROM Empleado e
JOIN EmpleadoProyecto ep ON e.IDEmpleado = ep.IDEmpleado
JOIN Proyecto p ON ep.IDProyecto = p.IDProyecto
WHERE ep.IDProyecto = 2;
```
**5)Consultar todos los empleados junto con el nombre de su departamento:**
```sql
SELECT e.NombreEmpleado, d.NombreDepartamento
FROM Empleado e
JOIN Departamento d ON e.IDDepartamento = d.IDDepartamento;
```
### Consultas avanzadas
**1) Consultar los empleados y sus respectivos jefes:**
```sql
SELECT e.NombreEmpleado AS Empleado, j.NombreEmpleado AS Jefe
FROM Empleado e
LEFT JOIN Empleado j ON e.IDJefe = j.IDEmpleado;
```
**2)Consultar el salario total y la comisión total de los empleados por departamento:**
```sql
SELECT d.NombreDepartamento, SUM(e.Salario) AS SalarioTotal, SUM(e.Comision) AS ComisionTotal
FROM Empleado e
JOIN Departamento d ON e.IDDepartamento = d.IDDepartamento
GROUP BY d.NombreDepartamento;
```
**3)Encontrar el proyecto en el que más horas se han trabajado:**
```sql
SELECT p.NombreProyecto, SUM(ep.HorasTrabajadas) AS TotalHoras
FROM Proyecto p
JOIN EmpleadoProyecto ep ON p.IDProyecto = ep.IDProyecto
GROUP BY p.NombreProyecto
ORDER BY TotalHoras DESC
```
**4)Consultar los empleados que no están asignados a ningún proyecto:**
```sql
SELECT e.NombreEmpleado
FROM Empleado e
LEFT JOIN EmpleadoProyecto ep ON e.IDEmpleado = ep.IDEmpleado
WHERE ep.IDEmpleado IS NULL;
```
**5)Consultar los empleados que ganan más que el promedio de salarios de su departamento:**
```sql
SELECT e.NombreEmpleado, e.Salario, d.NombreDepartamento
FROM Empleado e
JOIN Departamento d ON e.IDDepartamento = d.IDDepartamento
WHERE e.Salario > (
    SELECT AVG(Salario)
    FROM Empleado
    WHERE IDDepartamento = e.IDDepartamento
);
```
### Insertar
**1)Insertar un nuevo empleado:**
```sql
INSERT INTO Empleado (NombreEmpleado, Puesto, IDJefe, FechaContratacion, Salario, Comision, IDDepartamento)
VALUES ('GARCIA', 'ENGINEER', 3, '2024-06-13', 3200, 500, 2);
```
**2) Insertar un nuevo proyecto:**
```sql
INSERT INTO Proyecto (NombreProyecto, Ubicacion, IDDepartamento)
VALUES ('P9', 'MIAMI', 2);
```
**3) Asignar empleados a ese proyecto:**
```sql
INSERT INTO Proyecto (NombreProyecto, Ubicacion, IDDepartamento)
VALUES ('P9', 'MIAMI', 2);

INSERT INTO EmpleadoProyecto (IDEmpleado, IDProyecto, HorasTrabajadas)
VALUES (8, (SELECT MAX(IDProyecto) FROM Proyecto), 20);
INSERT INTO EmpleadoProyecto (IDEmpleado, IDProyecto, HorasTrabajadas)
VALUES (9, (SELECT MAX(IDProyecto) FROM Proyecto), 15);
```
### Actualizar
**1) Actualizar el salario de un empleado específico:**
```sql
UPDATE Empleado
SET Salario = 3500
WHERE NombreEmpleado = 'SMITH';
```
**2) Actualizar la ubicación de un departamento:**
```sql
UPDATE Departamento
SET Ubicacion = 'SAN FRANCISCO'
WHERE NombreDepartamento = 'RESEARCH';
```
### Eliminar
**1) Eliminar un empleado específico:**
```sql
DELETE FROM Empleado
WHERE NombreEmpleado = 'JAMES';
```
**2) Eliminar un proyecto y todas las asignaciones de empleados a ese proyecto:**
```sql
DELETE FROM EmpleadoProyecto
WHERE IDProyecto = (SELECT IDProyecto FROM Proyecto WHERE NombreProyecto = 'P5');

DELETE FROM Proyecto
WHERE NombreProyecto = 'P5';
```
### Procedimiento
**1) Procedimiento para insertar un nuevo empleado:**
```sql
CREATE PROCEDURE InsertarEmpleado
    @NombreEmpleado VARCHAR(50),
    @Puesto VARCHAR(50),
    @IDJefe INT,
    @FechaContratacion DATE,
    @Salario DECIMAL(10, 2),
    @Comision DECIMAL(10, 2),
    @IDDepartamento INT
AS
BEGIN
    INSERT INTO Empleado (NombreEmpleado, Puesto, IDJefe, FechaContratacion, Salario, Comision, IDDepartamento)
    VALUES (@NombreEmpleado, @Puesto, @IDJefe, @FechaContratacion, @Salario, @Comision, @IDDepartamento);
END;

EXEC InsertarEmpleado 
    @NombreEmpleado = 'LOPEZ', 
    @Puesto = 'ENGINEER', 
    @IDJefe = 3, 
    @FechaContratacion = '2024-06-13', 
    @Salario = 3200, 
    @Comision = 500, 
    @IDDepartamento = 2;
	```
**2)Procedimiento para actualizar la ubicación de un departamento:**
```SQL
CREATE PROCEDURE ActualizarUbicacionDepartamento
    @IDDepartamento INT,
    @NuevaUbicacion VARCHAR(50)
AS
BEGIN
    UPDATE Departamento
    SET Ubicacion = @NuevaUbicacion
    WHERE IDDepartamento = @IDDepartamento;
END;
EXEC ActualizarUbicacionDepartamento 
    @IDDepartamento = 2, 
    @NuevaUbicacion = 'SAN FRANCISCO';
```

# ENTREGABLE 2 CLINICA
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
