----------------INSERTAR------------------
ALTER PROCEDURE [InsertarCliente]
	@name varchar(20),
	@address varchar (20),
	@phone varchar(24),
	@active bit
AS
BEGIN
INSERT INTO Customers (name, address, phone, active)
VALUES (
	@name,
	@address,
	@phone,
	@active
);
END

EXEC [InsertarCliente] 'Rafael', '123 Lima', '555-9876', 1;

---------------LISTAR-------------------------
ALTER PROCEDURE [ListarClientes]
	@customer_id int
AS
BEGIN
SELECT
	customer_id,
    name,
    address, 
    phone, 
    active
FROM Customers;
END

exec [ListarClientes] 1

---------------ACTUALIZAR----------------
ALTER PROCEDURE [ActualizarClientes]
	@customer_id int,
	@name varchar(20)=NULL,
	@address varchar(20)=NULL,
	@phone varchar(24)=NULL,
	@active bit=NULL
AS
BEGIN
	UPDATE Customers
	SET 
		name = ISNULL(@name, name),
        address = ISNULL(@address, address),
        phone = ISNULL(@phone, phone),
        active = ISNULL(@active, active)
	WHERE customer_id = @customer_id;
END

exec [ActualizarClientes] 3, 'Bob Stones', '789 Oak St', '555-9012', 1

---------------ELIMINAR---------------------
ALTER PROCEDURE [EliminarClientes]
	@customer_id int
AS
BEGIN
	-- Eliminar el cliente por su ID
	DELETE FROM Customers
	WHERE customer_id = @customer_id;
END

EXEC [EliminarClientes] 4

---------ELIMINACIONLOGICA----------------
ALTER PROCEDURE EliminarClienteLogicamente
    @customer_id INT
AS
BEGIN
    UPDATE customers
    SET 
        active = 0
    WHERE customer_id = @customer_id;
END
