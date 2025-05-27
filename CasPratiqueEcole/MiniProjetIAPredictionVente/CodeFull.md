Parfait ! Je vais te générer un **projet Flask complet** (5 fichiers max) avec :

* Un script Python Flask (app.py) qui fait tout : upload CSV, analyse, prévision ARIMA, affichage résultats
* Un exemple simple de jeu de données CSV (à mettre dans /data/ventes.csv ou à uploader)
* Pages HTML stylées avec Bootstrap, effets sympa JS
* CSS et JS intégrés dans les templates pour éviter trop de fichiers
* Graphiques générés avec matplotlib et affichés en base64 dans la page (pas besoin de fichiers image)
* Export rapport CSV possible via un bouton

---

# Arborescence proposée

```
/project-flask-sales
│
├── app.py
├── requirements.txt
├── templates/
│   ├── base.html
│   ├── index.html
│   └── resultats.html
└── static/
    └── style.css   (optionnel, sinon CSS inline)
```

---

# 1. requirements.txt

```txt
Flask==2.2.2
pandas==2.0.3
matplotlib==3.7.1
statsmodels==0.14.0
numpy==1.24.3
```

---

# 2. `app.py` (serveur Flask)

```python
import io
import base64
from flask import Flask, request, render_template, send_file, redirect, url_for, flash
import pandas as pd
import matplotlib.pyplot as plt
from statsmodels.tsa.arima.model import ARIMA
from matplotlib.ticker import FuncFormatter

app = Flask(__name__)
app.secret_key = "secret_key_flask_sales"

def create_ca_mensuel(df):
    df['date_commande'] = pd.to_datetime(df['date_commande'], errors='coerce')
    df = df.dropna(subset=['date_commande', 'prix_unitaire', 'quantite'])
    df['ca'] = df['prix_unitaire'] * df['quantite']
    ca_mensuel = df.groupby(pd.Grouper(key='date_commande', freq='M'))['ca'].sum()
    return ca_mensuel

def create_ca_produit(df):
    df['ca'] = df['prix_unitaire'] * df['quantite']
    ca_produit = df.groupby('produit')['ca'].sum().sort_values(ascending=False)
    return ca_produit

def plot_to_img(plt):
    buf = io.BytesIO()
    plt.savefig(buf, format='png', bbox_inches='tight')
    buf.seek(0)
    img_b64 = base64.b64encode(buf.getvalue()).decode('utf8')
    plt.close()
    return img_b64

def prevoir_ventes(ca_mensuel, mois_a_prevoir=3):
    ts = ca_mensuel.copy()
    ts.index = pd.DatetimeIndex(ts.index)
    ts = ts.asfreq('M').fillna(0)
    model = ARIMA(ts, order=(1,1,1))
    model_fit = model.fit()
    forecast = model_fit.forecast(steps=mois_a_prevoir)
    return forecast

@app.route("/", methods=["GET", "POST"])
def index():
    if request.method == "POST":
        if "file" not in request.files:
            flash("Aucun fichier uploadé")
            return redirect(request.url)
        file = request.files["file"]
        if file.filename == "":
            flash("Aucun fichier sélectionné")
            return redirect(request.url)
        try:
            df = pd.read_csv(file)
        except Exception as e:
            flash(f"Erreur lecture CSV: {e}")
            return redirect(request.url)

        # Analyse CA mensuel
        ca_mensuel = create_ca_mensuel(df)
        # Analyse CA produit
        ca_produit = create_ca_produit(df)
        # Prévision
        forecast = prevoir_ventes(ca_mensuel)

        # Plot CA mensuel
        plt.figure(figsize=(8,4))
        ca_mensuel.plot(kind='bar', color='skyblue')
        plt.title("Chiffre d'affaires mensuel")
        plt.ylabel("CA (€)")
        plt.xticks(rotation=45)
        ca_mensuel_img = plot_to_img(plt)

        # Plot CA produit
        plt.figure(figsize=(8,4))
        ca_produit.plot(kind='bar', color='orange')
        plt.title("Chiffre d'affaires par produit")
        plt.ylabel("CA (€)")
        plt.xticks(rotation=45)
        ca_produit_img = plot_to_img(plt)

        # Plot prévision
        plt.figure(figsize=(8,4))
        ca_mensuel.plot(label="CA réel", color='blue')
        forecast.plot(label="Prévision 3 mois", color='red', linestyle='--')
        plt.title("Prévision chiffre d'affaires")
        plt.ylabel("CA (€)")
        plt.xticks(rotation=45)
        plt.legend()
        forecast_img = plot_to_img(plt)

        # Génération rapport CSV en mémoire
        rapport_df = ca_produit.reset_index()
        rapport_df.columns = ['Produit', 'CA (€)']
        csv_io = io.StringIO()
        rapport_df.to_csv(csv_io, index=False)
        csv_io.seek(0)

        # Sauvegarder données dans session (optionnel), ici on passe tout via POST/GET c’est limité, donc on va rendre tout dans la page.
        return render_template("resultats.html",
                               ca_mensuel_img=ca_mensuel_img,
                               ca_produit_img=ca_produit_img,
                               forecast_img=forecast_img,
                               rapport_csv=csv_io.getvalue())
    return render_template("index.html")

@app.route("/download_csv", methods=["POST"])
def download_csv():
    csv_data = request.form["csv_data"]
    return send_file(io.BytesIO(csv_data.encode('utf-8')),
                     mimetype="text/csv",
                     as_attachment=True,
                     download_name="rapport_ventes.csv")

if __name__ == "__main__":
    app.run(debug=True)
```

---

# 3. templates/base.html

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <title>{% block title %}Analyse Ventes{% endblock %}</title>
    <!-- Bootstrap CDN -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet" />
    <style>
        body { padding-top: 60px; background: #f8f9fa; }
        .footer { text-align:center; padding:15px; color:#777; margin-top:30px; }
        .navbar-brand { font-weight: bold; }
    </style>
    {% block head %}{% endblock %}
</head>
<body>
<nav class="navbar navbar-expand-lg navbar-dark bg-primary fixed-top">
  <div class="container">
    <a class="navbar-brand" href="{{ url_for('index') }}">Analyse Ventes</a>
  </div>
</nav>

<div class="container">
    {% with messages = get_flashed_messages() %}
      {% if messages %}
        <div class="alert alert-warning mt-3">
          {% for msg in messages %}
            <div>{{ msg }}</div>
          {% endfor %}
        </div>
      {% endif %}
    {% endwith %}
    {% block content %}{% endblock %}
</div>

<footer class="footer">
    &copy; 2025 Boutique en ligne - Analyse des ventes
</footer>

<!-- Bootstrap JS + Popper -->
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
{% block scripts %}{% endblock %}
</body>
</html>
```

---

# 4. templates/index.html

```html
{% extends "base.html" %}
{% block title %}Accueil - Analyse des ventes{% endblock %}

{% block content %}
<div class="card shadow-sm p-4 mt-5">
    <h2 class="mb-4">Importer fichier CSV des ventes</h2>
    <form method="POST" enctype="multipart/form-data">
        <div class="mb-3">
            <input class="form-control" type="file" name="file" accept=".csv" required />
        </div>
        <button type="submit" class="btn btn-primary">Analyser</button>
    </form>
    <hr />
    <h5>Exemple de fichier CSV :</h5>
    <pre class="bg-light p-3 rounded">
commande_id,produit,prix_unitaire,quantite,date_commande
1,Stylo,1.20,10,2025-01-05
2,Cahier,2.50,5,2025-01-06
3,Stylo,1.20,3,2025-02-10
4,Crayon,0.80,15,2025-02-15
5,Cahier,2.50,7,2025-03-01
6,Stylo,1.20,20,2025-03-10
7,Agenda,5.00,2,2025-03-15
8,Stylo,1.20,8,2025-04-05
9,Cahier,2.50,10,2025-04-10
10,Crayon,0.80,10,2025-04-15
    </pre>
</div>
{% endblock %}
```

---

# 5. templates/resultats.html

```html
{% extends "base.html" %}
{% block title %}Résultats Analyse{% endblock %}

{% block content %}
<div class="mb-4 text-center">
    <h2>Résultats de l’analyse et prévision des ventes</h2>
    <a href="{{ url_for('index') }}" class="btn btn-secondary mt-3">Nouvelle analyse</a>
</div>

<div class="row row-cols-1 row-cols-md-3 g-4">
    <div class="col">
        <div class="card shadow-sm">
            <div class="card-body text-center">
                <h5 class="card-title">Chiffre d'affaires mensuel</h5>
                <img src="data:image/png;base64,{{ ca_mensuel_img }}" alt="CA mensuel" class="img-fluid" />
            </div>
        </div>
    </div>
    <div class="col">
        <div class="card shadow-sm">
            <div class="card-body text-center">
                <h5 class="card-title">Chiffre d'affaires par produit</h5>
                <img src="data:image/png;base64,{{ ca_produit_img }}" alt="CA produit" class="img-fluid" />
            </div>
        </div>
    </div>
    <div class="col">
        <div class="card shadow-sm">
            <div class="card-body text-center">
                <h5 class="card-title">Prévision CA 3 mois</h5>
                <img src="data:image/png;base64,{{ forecast_img }}" alt="Prévision" class="img-fluid" />
            </div>
        </div>
    </div>
</div>

<div class="mt-4 text-center">
    <h5>Exporter le rapport CA par produit (CSV)</h5>
    <form method="POST" action="{{ url_for('download_csv') }}">
        <input type="hidden" name="csv_data" value="{{ rapport_csv|tojson|safe }}" />
        <button class="btn btn-success" type="submit">Télécharger CSV</button>
    </form>
</div>

{% endblock %}
```

---

# Instructions pour lancer

1. Créer un dossier projet, copier ces fichiers dans l’arborescence indiquée
2. Installer Python 3.8+ et faire :

```bash
pip install -r requirements.txt
```

3. Lancer l’app :

```bash
python app.py
```

4. Ouvrir dans navigateur [http://127.0.0.1:5000](http://127.0.0.1:5000)
5. Uploader un fichier CSV de ventes (exemple donné)
6. Voir résultats, graphiques, prévisions, et télécharger rapport

---

Veux-tu que je te fournisse aussi un script indépendant Python de prévision avec données et tests ?
Ou on continue à améliorer l’app Flask ?
