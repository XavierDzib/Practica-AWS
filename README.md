# Práctica AWS
Repositorio donde se alojará una página web hecha para una práctica del curso AWS
```mermaid
graph TD
    %% Definición de Estilos
    classDef cliente fill:#e1f5fe,stroke:#0288d1,stroke-width:2px;
    classDef servidor fill:#efebe9,stroke:#5d4037,stroke-width:2px;
    classDef bd fill:#e8f5e9,stroke:#388e3c,stroke-width:2px;

    %% Capa del Cliente (Frontend)
    subgraph Frontend [Lado del Cliente - Navegador Web]
        A[index.html] -->|Vincula Estilos| B[styles.css]
        A -->|Vincula Comportamiento| C[update.js]
        C -->|Manipula / Escucha Eventos| A
    end
    class A,B,C cliente;

    %% Capa del Servidor (Backend)
    subgraph Backend [Lado del Servidor - PHP Engine]
        D[rss.php <br> Controlador Central]
        E[conexion.php <br> Instancia PDO]
        D -->|Requiere / Incluye| E
    end
    class D,E servidor;

    %% Capa de Almacenamiento e Infraestructura Externa
    subgraph Almacenamiento [Persistencia y Red]
        F[(Base de Datos <br> MySQL / MariaDB)]
        G[Servers Web Externos <br> Canales RSS remotos]
    end
    class F bd;
    class G servidor;

    %% Interconexiones y Flujos de Datos
    C -->|1. POST: feedUrl <br> 2. GET: buscar, categoria, ordenar, dir| D
    D -->|Respuesta: JSON Estructurado| C
    
    D -.->|Consumo asíncrono XML <br> simplexml_load_string| G
    E -->|Consultas Preparadas <br> INSERT IGNORE / SELECT LIKE| F
