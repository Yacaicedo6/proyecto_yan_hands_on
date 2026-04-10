# Predict Insurance Bill

Aplicación web de predicción de costos de seguro médico anual usando Machine Learning con PyCaret y Flask, desplegada en Azure mediante un pipeline CI/CD con GitHub Actions.

---

## Tecnologías

- **Python 3.11**
- **Flask** — servidor web
- **PyCaret 3.3.1** — modelo de regresión
- **Docker** — contenedorización
- **Azure Container Registry** — registro de imágenes Docker
- **Azure App Service** — despliegue en la nube
- **GitHub Actions** — CI/CD automatizado

---

## Endpoints

| Método | Ruta | Descripción |
|---|---|---|
| GET | `/` | Interfaz web para predicción |
| GET | `/health` | Estado del servidor |
| POST | `/predict` | Predicción desde formulario web |
| POST | `/predict_api` | Predicción via API REST (JSON) |

---

## Uso de la API

```bash
POST /predict_api
Content-Type: application/json

{
  "age": 30,
  "sex": "male",
  "bmi": 25.0,
  "children": 1,
  "smoker": "no",
  "region": "southwest"
}
```

**Respuesta:** `4405` (valor en USD anuales)

**URL de producción:**
```
https://pycaret-insurance-yan-d4bte2g8a6f8drfa.canadacentral-01.azurewebsites.net
```

---

## Pipeline CI/CD

El workflow `.github/workflows/Deploy_Yan.yml` se ejecuta automáticamente en cada push a `main`:

```
Lint (flake8)  →  Build & Push imagen al ACR  →  Deploy en Azure App Service
```

### Secretos requeridos en GitHub

| Secreto | Descripción |
|---|---|
| `ACR_USERNAME` | Usuario del Azure Container Registry |
| `ACR_PASSWORD` | Password del Azure Container Registry |
| `AZURE_CREDENTIALS` | JSON del Service Principal de Azure |

---

## Correr localmente

```bash
# Clonar el repositorio
git clone https://github.com/Yacaicedo6/proyecto_yan_hands_on.git
cd proyecto_yan_hands_on

# Crear entorno virtual e instalar dependencias
python -m venv venv
venv\Scripts\activate
pip install -r requirements.txt

# Correr la app
python app.py
```

App disponible en `http://localhost:5000`

---

## Variables del modelo

| Variable | Tipo | Ejemplo |
|---|---|---|
| `age` | número | `30` |
| `sex` | `male` / `female` | `male` |
| `bmi` | decimal | `25.0` |
| `children` | número | `1` |
| `smoker` | `yes` / `no` | `no` |
| `region` | `southwest` / `southeast` / `northwest` / `northeast` | `southwest` |
