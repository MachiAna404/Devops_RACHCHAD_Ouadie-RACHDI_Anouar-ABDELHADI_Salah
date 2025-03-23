# 🌌 **Conception et Déploiement d’un Système de Gestion des Âges Étudiants avec Docker et Flask API**

---

## 🌟 **Introduction**

### 1.1 **L’Essence du Projet**  
Un système élégant pour gérer et afficher les âges des étudiants, construit avec **Flask API**, **PHP**, et conteneurisé avec **Docker**.

---

## 🏛️ **Architecture du Système**

### 2.1 **Composants Clés**

#### **API Flask (`student_age.py`)**  
Voici un extrait du code Flask pour gérer les requêtes :

```python
from flask import Flask, jsonify, request

app = Flask(__name__)

# Données des étudiants (exemple)
students = [
    {"id": 1, "name": "Alice", "age": 20},
    {"id": 2, "name": "Bob", "age": 22}
]

@app.route('/students', methods=['GET'])
def get_students():
    return jsonify(students)

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
