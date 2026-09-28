# Orders & Deliveries Management: JavaFX + Oracle

Desktop application (JavaFX) for managing **customer orders, deliveries and staff**, backed by an **Oracle** database. It is a database course project (SGBD): the app connects with real Oracle accounts, and each user's access depends on their job position (poste) in the database.

## Features

- **Login with Oracle credentials**: the user's login and password open the JDBC connection directly
- **Role-based screens**: the user's position code (read from the `V_Mon_Profil` view) decides which screen opens
- **Order management**: list orders, create an order with several articles in a single transaction (commit / rollback), change order status, cancel an order
- **Delivery management**: add, edit and delete deliveries, assign a delivery person; only orders without a delivery can be selected
- **User management**: add, edit, delete and search staff, and create the matching Oracle user
- FXML views with CSS styling

## Tech stack

- Java, JavaFX (FXML, CSS)
- Oracle Database Express Edition, JDBC (`ojdbc17`)
- DAO pattern (`CommandeDAO`, `LivraisonDAO`, `UtilisateurDAO`)
- NetBeans (Ant) project

## Project structure

```
src/projetsgbd/
├── PROJETSGBD.java        # application entry point
├── ConnexionBD.java       # Oracle JDBC connection
├── DAO/                   # database access (orders, deliveries, users)
├── Model/                 # Commande, Livraison, Utilisateur, SessionManager
├── controllers/           # JavaFX controllers
└── View/                  # FXML screens and style.css
```

## Getting started

### Prerequisites

- JDK 17 or higher with JavaFX
- Oracle Database XE running on `localhost:1521` (SID `xE`)
- The Oracle JDBC driver jar (`ojdbc17`)
- NetBeans IDE (recommended, project files included)

### Run

1. Clone the repository:
   ```bash
   git clone https://github.com/Malekkk25/oracle-javafx-orders-delivery.git
   ```
2. Open the project in NetBeans.
3. Add the Oracle JDBC jar to the project libraries. The path saved in `nbproject/project.properties` points to a local Downloads folder, so update it.
4. Create the database schema (see below).
5. Run `PROJETSGBD` and log in with an Oracle account that exists in your database.

The connection URL is in `ConnexionBD.java`:

```java
private static final String URL = "jdbc:oracle:thin:@localhost:1521:xE";
```

## Database

The application expects these objects in the Oracle schema:

| Object | Purpose |
|--------|---------|
| `CLIENTS`, `ARTICLES` | customers and products |
| orders and order-line tables | customer orders |
| `LIVRAISONCOM` | deliveries linked to orders |
| `PERSONNEL`, `POSTES` | staff and job positions |
| `V_Mon_Profil` (view) | position of the connected user |

Add your SQL script (tables, view, users and privileges) to a `database/` folder in the repository so others can set up the schema.

## Author

**Malek** ([@Malekkk25](https://github.com/Malekkk25))
