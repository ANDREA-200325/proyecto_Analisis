Base de Datos (MySQL) 
CREATE DATABASE pos_retail;

USE pos_retail;

CREATE TABLE usuarios (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(50),
    correo VARCHAR(100) UNIQUE,
    password VARCHAR(255),
    intentos INT DEFAULT 0,
    estado VARCHAR(20) DEFAULT 'ACTIVO'
);

CREATE TABLE productos (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(100),
    precio DECIMAL(10,2),
    stock INT
);

CREATE TABLE compras (
    id INT AUTO_INCREMENT PRIMARY KEY,
    proveedor VARCHAR(100),
    fecha DATE,
    tipo_pago VARCHAR(20),
    total DECIMAL(10,2)
);

CREATE TABLE devoluciones (
    id INT AUTO_INCREMENT PRIMARY KEY,
    compra_id INT,
    producto_id INT,
    cantidad INT,
    fecha DATE,
    FOREIGN KEY (compra_id) REFERENCES compras(id),
    FOREIGN KEY (producto_id) REFERENCES productos(id)
);

CREATE TABLE ventas (
    id INT AUTO_INCREMENT PRIMARY KEY,
    cliente VARCHAR(100),
    fecha DATE,
    total DECIMAL(10,2)
);

CREATE TABLE pagos (
    id INT AUTO_INCREMENT PRIMARY KEY,
    venta_id INT,
    tipo_pago VARCHAR(20),
    fecha DATE,
    monto DECIMAL(10,2),
    FOREIGN KEY (venta_id) REFERENCES ventas(id)
);

CREATE TABLE kardex (
    id INT AUTO_INCREMENT PRIMARY KEY,
    producto_id INT,
    movimiento VARCHAR(50),
    cantidad INT,
    fecha DATE,
    FOREIGN KEY (producto_id) REFERENCES productos(id)
);
