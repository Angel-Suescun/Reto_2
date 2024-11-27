# Reto #02 - Sistema de Gestión de Reservas de Hotel

**- Diagrama de Clases: Gestión de Reservas Hoteleras**

```mermaid
classDiagram
    %% Clases principales
    class Hotel {
        +String nombre
        +String direccion
        +List~Habitacion~ habitaciones
        +List~Empleado~ empleados
        +List~Huesped~ huespedes
        +buscarHabitacionDisponible(String tipo, Date fechaInicio, Date fechaFin): Habitacion
    }

    class Habitacion {
        +int numero
        +String tipo
        +boolean estado
        +double precioPorNoche
        +List~Caracteristica~ caracteristicas
        +checkIn()
        +checkOut()
        +calcularCostoReserva(int dias): double
    }

    class Persona {
        +int id
        +String nombre
        +String correo
        +String telefono
    }

    class Cliente {
        +List~Reserva~ reservas
        +hacerReserva(Reserva reserva)
        +cancelarReserva(int idReserva)
    }

    class Empleado {
        +String turno
    }

    class Reserva {
        +int idReserva
        +Date fechaInicio
        +Date fechaFin
        +double costoTotal
        +calcularDuracion(): int
        +calcularCostoTotal(double precioHabitacion): double
    }

    %% Relaciones
    Hotel *-- Habitacion : "posee"
    Hotel *-- Empleado : "emplea"
    Hotel *-- Cliente : "recibe"
    Cliente "1" --> "0..*" Reserva : "realiza"
    Reserva "1" --> "1" Habitacion : "incluye"
    Persona <|-- Cliente
    Persona <|-- Empleado


```
#
**- Diagrama de Clases: Tipos de Habitaciones**


```mermaid
classDiagram
    %% Clases principales
    class Habitacion {
        +int numero
        +String tipo
        +boolean estado
        +double precioPorNoche
        +List~Caracteristica~ caracteristicas
        +List~Servicio~ servicios
        +checkIn()
        +checkOut()
        +calcularCostoReserva(int dias): double
    }

    class HabitacionSimple {
        +String tamaño
    }

    class HabitacionDoble {
        +int numeroDeCamas
    }

    class Suite {
        +boolean jacuzzi
        +boolean terraza
    }

    %% Clases de Composición y Asociación
    class Caracteristica {
        +String nombre
        +String descripcion
    }

    class Servicio {
        +String nombre
        +String descripcion
        +double costoAdicional
    }

    %% Relaciones
    Habitacion "1" *-- "0..*" Caracteristica : "tiene"
    Habitacion "1" *-- "0..*" Servicio : "ofrece"
    
    Habitacion <|-- HabitacionSimple
    Habitacion <|-- HabitacionDoble
    Habitacion <|-- Suite



```

# 

**- Diagrama de Clases: Tipos De Cliente**


```mermaid
classDiagram
    %% Clases principales

    class Cliente {
        +List~Reserva~ reservas
        +hacerReserva(Reserva reserva)
        +cancelarReserva(int idReserva)
    }

    class ClienteVIP {
        +double descuento
        +accederBeneficios()
    }
    class ClienteRegular {
        +int puntosFidelidad
    }



    %% Relaciones
   
    Cliente <|-- ClienteVIP
    Cliente <|-- ClienteRegular


```

**- Diagrama de Clases: Roles de los Empleados**


```mermaid
classDiagram
    %% Clases principales

    class Empleado {
        +String turno
        +String departamento
        +trabajar(): void
    }

    class Recepcionista {
        +atenderCheckIn(): void
        +atenderCheckOut(): void
    }

    class Camarero {
        +tomarPedido(): void
        +servirComida(): void
    }

    class Limpiador {
        +limpiarHabitaciones(): void
        +reponerArticulos(): void
    }

    class Cocinero {
        +prepararComida(): void
        +crearMenu(): void
    }

    %% Relaciones

    Empleado <|-- Recepcionista
    Empleado <|-- Camarero
    Empleado <|-- Limpiador
    Empleado <|-- Cocinero


```
#
**- Diagrama Completo**

```mermaid
classDiagram
    %% Clases principales
    class Hotel {
        +String nombre
        +String direccion
        +List~Habitacion~ habitaciones
        +List~Empleado~ empleados
        +List~Cliente~ huespedes
        +buscarHabitacionDisponible(String tipo, Date fechaInicio, Date fechaFin): Habitacion
    }

    class Habitacion {
        +int numero
        +String tipo
        +boolean estado
        +double precioPorNoche
        +List~Caracteristica~ caracteristicas
        +List~Servicio~ servicios
        +checkIn()
        +checkOut()
        +calcularCostoReserva(int dias): double
    }

    class HabitacionSimple {
        +String tamaño
    }

    class HabitacionDoble {
        +int numeroDeCamas
    }

    class Suite {
        +boolean jacuzzi
        +boolean terraza
    }

    %% Clases de Composición y Asociación
    class Caracteristica {
        +String nombre
        +String descripcion
    }

    class Servicio {
        +String nombre
        +String descripcion
        +double costoAdicional
    }

    class Persona {
        +int id
        +String nombre
        +String correo
        +String telefono
    }

    class Cliente {
        +List~Reserva~ reservas
        +hacerReserva(Reserva reserva)
        +cancelarReserva(int idReserva)
    }

    class ClienteVIP {
        +double descuento
        +accederBeneficios()
    }

    class ClienteRegular {
        +int puntosFidelidad
    }

    class Empleado {
        +String turno
        +String departamento
        +trabajar(): void
    }

    class Recepcionista {
        +atenderCheckIn(): void
        +atenderCheckOut(): void
    }

    class Camarero {
        +tomarPedido(): void
        +servirComida(): void
    }

    class Limpiador {
        +limpiarHabitaciones(): void
        +reponerArticulos(): void
    }

    class Cocinero {
        +prepararComida(): void
        +crearMenu(): void
    }

    class Reserva {
        +int idReserva
        +Date fechaInicio
        +Date fechaFin
        +double costoTotal
        +calcularDuracion(): int
        +calcularCostoTotal(double precioHabitacion): double
    }

    %% Relaciones

    Hotel *-- Habitacion : "posee"
    Hotel *-- Empleado : "emplea"
    Hotel *-- Cliente : "recibe"
    Cliente "1" --> "0..*" Reserva : "realiza"
    Reserva "1" --> "1" Habitacion : "incluye"
    Persona <|-- Cliente
    Persona <|-- Empleado
    Cliente <|-- ClienteVIP
    Cliente <|-- ClienteRegular
    Empleado <|-- Recepcionista
    Empleado <|-- Camarero
    Empleado <|-- Limpiador
    Empleado <|-- Cocinero
    Habitacion "1" *-- "0..*" Caracteristica : "tiene"
    Habitacion "1" *-- "0..*" Servicio : "ofrece"
    Habitacion <|-- HabitacionSimple
    Habitacion <|-- HabitacionDoble
    Habitacion <|-- Suite


```



