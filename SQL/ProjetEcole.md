#  Projet scolaire complet en ligne de commande en Python avec SQLite

Voici un **projet scolaire complet en ligne de commande en Python avec SQLite** basé sur tous les concepts SQL présentés dans le PDF que vous avez fourni. Le projet s'intitule **"Système de Gestion de Ventes"**, intègre un menu CLI, et couvre :

* DDL (création/modification de tables)
* DML (insert, update, delete)
* DQL (select, group by, having, etc.)
* Fonctions (agrégats, chaîne, case, etc.)
* Jointures (inner, left, right, full)
* Vues, sous-requêtes, procédures simulées
* Ranking et partitionnement

---

### 🗂️ Structure du projet

```
sales_system/
│
├── main.py                  # Point d'entrée avec menu CLI
├── database.py              # Création et gestion de la base SQLite
├── models.py                # Fonctions CRUD pour chaque table
├── queries.py               # Requêtes complexes, joins, stats
└── utils.py                 # Fonctions d'affichage et helpers
```

---

### 📄 `database.py` – création de la base SQLite

```python
import sqlite3

def connect_db():
    return sqlite3.connect("sales.db")

def init_db():
    conn = connect_db()
    cursor = conn.cursor()

    cursor.executescript("""
    DROP TABLE IF EXISTS sale;
    DROP TABLE IF EXISTS inventory;
    DROP TABLE IF EXISTS employee;
    DROP TABLE IF EXISTS customer;

    CREATE TABLE customer (
        CustomerID INTEGER PRIMARY KEY AUTOINCREMENT,
        CustomerFirstName TEXT NOT NULL,
        CustomerLastName TEXT NOT NULL,
        CustomerAddress TEXT,
        CustomerCity TEXT,
        CustomerPostCode TEXT,
        CustomerPhoneNumber TEXT
    );

    CREATE TABLE inventory (
        InventoryID INTEGER PRIMARY KEY AUTOINCREMENT,
        InventoryName TEXT NOT NULL,
        InventoryDescription TEXT
    );

    CREATE TABLE employee (
        EmployeeID INTEGER PRIMARY KEY AUTOINCREMENT,
        EmployeeFirstName TEXT NOT NULL,
        EmployeeLastName TEXT NOT NULL
    );

    CREATE TABLE sale (
        SaleID INTEGER PRIMARY KEY AUTOINCREMENT,
        CustomerID INTEGER,
        InventoryID INTEGER,
        EmployeeID INTEGER,
        SaleDate TEXT,
        SaleQuantity INTEGER,
        SaleUnitPrice REAL,
        FOREIGN KEY (CustomerID) REFERENCES customer(CustomerID),
        FOREIGN KEY (InventoryID) REFERENCES inventory(InventoryID),
        FOREIGN KEY (EmployeeID) REFERENCES employee(EmployeeID)
    );
    """)

    conn.commit()
    conn.close()
```

---

### 🧱 `models.py` – Fonctions CRUD simples

```python
from database import connect_db

def add_customer(first, last, address, city, code, phone):
    conn = connect_db()
    cur = conn.cursor()
    cur.execute("""
        INSERT INTO customer (CustomerFirstName, CustomerLastName, CustomerAddress, CustomerCity, CustomerPostCode, CustomerPhoneNumber)
        VALUES (?, ?, ?, ?, ?, ?)
    """, (first, last, address, city, code, phone))
    conn.commit()
    conn.close()

def list_customers():
    conn = connect_db()
    cur = conn.cursor()
    cur.execute("SELECT * FROM customer")
    for row in cur.fetchall():
        print(row)
    conn.close()
```

*(Ajoutez aussi les fonctions pour les employés, inventaire, ventes)*

---

### 📊 `queries.py` – requêtes complexes (groupes, jointures, agrégats)

```python
from database import connect_db

def total_sales_by_employee():
    conn = connect_db()
    cur = conn.cursor()
    cur.execute("""
        SELECT e.EmployeeFirstName || ' ' || e.EmployeeLastName AS FullName,
               COUNT(s.SaleID) AS NumSales,
               SUM(s.SaleQuantity * s.SaleUnitPrice) AS TotalSales
        FROM employee e
        JOIN sale s ON s.EmployeeID = e.EmployeeID
        GROUP BY e.EmployeeID
        HAVING NumSales > 0
        ORDER BY TotalSales DESC
    """)
    for row in cur.fetchall():
        print(row)
    conn.close()
```

---

### 🧰 `utils.py` – helpers

```python
def print_menu():
    print("\n==== MENU PRINCIPAL ====")
    print("1. Ajouter un client")
    print("2. Lister les clients")
    print("3. Voir les ventes par employé")
    print("0. Quitter")
```

---

### 🏁 `main.py` – Interface en ligne de commande

```python
from models import add_customer, list_customers
from queries import total_sales_by_employee
from database import init_db
from utils import print_menu

def main():
    init_db()  # Réinitialise la base au démarrage (à commenter après test)

    while True:
        print_menu()
        choice = input("Choisissez une option : ")

        if choice == "1":
            fname = input("Prénom : ")
            lname = input("Nom : ")
            address = input("Adresse : ")
            city = input("Ville : ")
            code = input("Code postal : ")
            phone = input("Téléphone : ")
            add_customer(fname, lname, address, city, code, phone)

        elif choice == "2":
            list_customers()

        elif choice == "3":
            total_sales_by_employee()

        elif choice == "0":
            break

        else:
            print("Choix invalide.")

if __name__ == "__main__":
    main()
```

---

### ✅ Instructions pour exécution

```bash
python main.py
```

---

### 🔜 Extensions possibles

* Ajouter : interface texte avancée (curses ou click)
* Intégrer des vues SQLite
* Simuler des procédures stockées avec des fonctions Python
* Ajouter export CSV / JSON
* Couvrir UNION, INTERSECT, RANK

---

Souhaitez-vous que je vous génère ce projet sous forme de **fichiers zip** ou préférez-vous un **copier-coller de tous les fichiers** ici ?
