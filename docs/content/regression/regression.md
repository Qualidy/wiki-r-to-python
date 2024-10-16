Hier ist ein neuer Abschnitt, der das Thema **Lineare Regression mit `scikit-learn`** behandelt. 

Die Bibliothek `scikit-learn` ist eine der bekanntesten Bibliotheken für maschinelles Lernen in Python. Sie bietet eine Vielzahl von Algorithmen, darunter auch die **lineare Regression**, die wir in diesem Abschnitt verwenden werden. Der große Vorteil von `scikit-learn` liegt darin, dass sie viele nützliche Funktionen für die Datenvorverarbeitung, Modelltraining und Modellbewertung enthält.

In diesem Abschnitt führen wir Schritt für Schritt eine einfache lineare Regression durch und nutzen dabei die Funktionen von `scikit-learn`.

### Datensatz vorbereiten

Zuerst erstellen wir einen einfachen Datensatz, der die Beziehung zwischen einer unabhängigen Variable \(x\) und einer abhängigen Variable \(y\) darstellt. Unser Ziel ist es, die lineare Beziehung zwischen diesen Variablen zu modellieren.

```python
import numpy as np
import matplotlib.pyplot as plt

# Beispiel-Datensatz
x = np.array([1, 2, 3, 4, 5, 6, 7, 8, 9]).reshape(-1, 1)
y = np.array([2, 4, 5, 4, 6, 7, 8, 9, 10])

# Daten visualisieren
plt.scatter(x, y)
plt.xlabel("Unabhängige Variable (x)")
plt.ylabel("Abhängige Variable (y)")
plt.title("Datenpunkte")
plt.show()
```

In diesem Beispiel besteht unser Datensatz aus \(x\)- und \(y\)-Werten, die eine lineare Beziehung aufweisen, aber auch einige Variationen und Abweichungen enthalten.

### Modelltraining mit `scikit-learn`

Als Nächstes trainieren wir ein Modell der **linearen Regression** mit `scikit-learn`. Dazu verwenden wir die Klasse `LinearRegression`, die das Training und die Vorhersage sehr einfach macht.

```python
from sklearn.linear_model import LinearRegression

# Lineares Regressionsmodell erstellen
model = LinearRegression()

# Modell mit unseren Daten trainieren
model.fit(x, y)

# Steigung und Achsenabschnitt ausgeben
m = model.coef_[0]  # Steigung
b = model.intercept_  # Achsenabschnitt
print(f"Steigung (m): {m}")
print(f"Achsenabschnitt (b): {b}")
```

Nach dem Training gibt uns das Modell die Werte für die Steigung \(m\) und den Achsenabschnitt \(b\) zurück. Das sind die Parameter der linearen Gleichung \( y = m \cdot x + b \), die die Beziehung zwischen \(x\) und \(y\) beschreibt.

### Vorhersagen treffen

Nachdem wir das Modell trainiert haben, können wir nun Vorhersagen treffen. Dazu nutzen wir die Methode `predict` des Modells, um basierend auf neuen \(x\)-Werten die entsprechenden \(y\)-Werte zu berechnen.

```python
# Vorhersagen mit dem trainierten Modell treffen
y_pred = model.predict(x)

# Originale Datenpunkte und Regressionsgerade plotten
plt.scatter(x, y, label="Datenpunkte")
plt.plot(x, y_pred, color='red', label="Regressionsgerade")
plt.xlabel("Unabhängige Variable (x)")
plt.ylabel("Abhängige Variable (y)")
plt.title("Lineare Regression")
plt.legend()
plt.show()
```

Hier plotten wir die Originaldatenpunkte und die vorhergesagte Regressionsgerade, die unser Modell gelernt hat.

### Modellbewertung

Um die Güte unseres Modells zu bewerten, verwenden wir den sogenannten **Bestimmtheitsmaß** \(R^2\), der beschreibt, wie gut das Modell die Daten erklärt. Ein Wert von \(R^2 = 1\) bedeutet eine perfekte Anpassung, während ein Wert von \(R^2 = 0\) bedeutet, dass das Modell die Daten überhaupt nicht erklärt.

```python
# Modellbewertung
r_squared = model.score(x, y)
print(f"Bestimmtheitsmaß (R^2): {r_squared}")
```

Das `score`-Method von `scikit-learn` gibt uns direkt den \(R^2\)-Wert, mit dem wir die Qualität unseres Modells bewerten können.

### Komplexere Szenarien

In realen Anwendungen arbeitet man oft nicht nur mit einer unabhängigen Variable, sondern mit mehreren. `scikit-learn` unterstützt auch die **multiple lineare Regression**, bei der mehrere Prädiktoren (unabhängige Variablen) verwendet werden, um die Zielvariable vorherzusagen. Der Workflow für eine multiple lineare Regression ist identisch, mit dem Unterschied, dass \(x\) jetzt eine Matrix mit mehreren Spalten darstellt.

```python
# Beispiel mit zwei unabhängigen Variablen (x1 und x2)
x_multi = np.array([[1, 2], [2, 3], [3, 4], [4, 5], [5, 6], [6, 7], [7, 8], [8, 9], [9, 10]])

# Modell für multiple lineare Regression erstellen
model_multi = LinearRegression()

# Modell trainieren
model_multi.fit(x_multi, y)

# Steigung und Achsenabschnitt ausgeben
print(f"Steigung (m): {model_multi.coef_}")
print(f"Achsenabschnitt (b): {model_multi.intercept_}")
```